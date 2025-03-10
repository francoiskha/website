---
title: 访问集群
weight: 20
content_type: concept
---

<!--
title: Accessing Clusters
weight: 20
content_type: concept
-->

<!-- overview -->

<!--
This topic discusses multiple ways to interact with clusters.
-->
本文阐述多种与集群交互的方法。

{{< toc >}}

<!-- body -->

<!--
## Accessing for the first time with kubectl

When accessing the Kubernetes API for the first time, we suggest using the
Kubernetes CLI, `kubectl`.

To access a cluster, you need to know the location of the cluster and have credentials
to access it.  Typically, this is automatically set-up when you work through
a [Getting started guide](/docs/setup/),
or someone else setup the cluster and provided you with credentials and a location.

Check the location and credentials that kubectl knows about with this command:
-->
## 使用 kubectl 完成集群的第一次访问

当你第一次访问 Kubernetes API 的时候，我们建议你使用 Kubernetes CLI，`kubectl`。

访问集群时，你需要知道集群的地址并且拥有访问的凭证。通常，这些在你通过
[启动安装](/zh/docs/setup/)安装集群时都是自动安装好的，或者其他人安装时
也应该提供了凭证和集群地址。

通过以下命令检查 kubectl 是否知道集群地址及凭证：

```shell
kubectl config view
```

<!--
Many of the [examples](/docs/user-guide/kubectl-cheatsheet) provide an introduction to using
`kubectl` and complete documentation is found in the [kubectl reference](/docs/reference/kubectl/).
-->
有许多 [例子](/zh/docs/reference/kubectl/cheatsheet/) 介绍了如何使用 kubectl，
可以在 [kubectl 参考](/zh/docs/reference/kubectl/overview/) 中找到更完整的文档。

<!--
## Directly accessing the REST API

Kubectl handles locating and authenticating to the apiserver.
If you want to directly access the REST API with an http client like
curl or wget, or a browser, there are several ways to locate and authenticate:

  - Run kubectl in proxy mode.
    - Recommended approach.
    - Uses stored apiserver location.
    - Verifies identity of apiserver using self-signed cert.  No MITM possible.
    - Authenticates to apiserver.
    - In future, may do intelligent client-side load-balancing and failover.
  - Provide the location and credentials directly to the http client.
    - Alternate approach.
    - Works with some types of client code that are confused by using a proxy.
    - Need to import a root cert into your browser to protect against MITM.
-->
## 直接访问 REST API

Kubectl 处理 apiserver 的定位和身份验证。
如果要使用 curl 或 wget 等 http 客户端或浏览器直接访问 REST API，可以通过
多种方式查找和验证：

- 以代理模式运行 kubectl。
  - 推荐此方式。
  - 使用已存储的 apiserver 地址。
  - 使用自签名的证书来验证 apiserver 的身份。杜绝 MITM 攻击。
  - 对 apiserver 进行身份验证。
  - 未来可能会实现智能化的客户端负载均衡和故障恢复。
- 直接向 http 客户端提供位置和凭据。
  - 可选的方案。
  - 适用于代理可能引起混淆的某些客户端类型。
  - 需要引入根证书到你的浏览器以防止 MITM 攻击。

<!--
### Using kubectl proxy

The following command runs kubectl in a mode where it acts as a reverse proxy.  It handles
locating the apiserver and authenticating.
Run it like this:
-->
### 使用 kubectl proxy

以下命令以反向代理的模式运行 kubectl。它处理 apiserver 的定位和验证。
像这样运行：

```shell
kubectl proxy --port=8080 &
```

<!--
See [kubectl proxy](/docs/reference/generated/kubectl/kubectl-commands/#proxy) for more details.

Then you can explore the API with curl, wget, or a browser, replacing localhost
with [::1] for IPv6, like so:
-->
参阅 [kubectl proxy](/docs/reference/generated/kubectl/kubectl-commands/#proxy)
获取更多详细信息。

然后，你可以使用 curl、wget 或浏览器访问 API，如果是 IPv6 则用 [::1] 替换 localhost，
如下所示：

```shell
curl http://localhost:8080/api/
```
```json
{
  "kind": "APIVersions",
  "versions": [
    "v1"
  ],
  "serverAddressByClientCIDRs": [
    {
      "clientCIDR": "0.0.0.0/0",
      "serverAddress": "10.0.1.149:443"
    }
  ]
}
```

<!--
### Without kubectl proxy

In Kubernetes version 1.3 or later, `kubectl config view` no longer displays the token. Use `kubectl apply` and `kubectl describe secret...` to create a token for the default service account with grep/cut:

First, create the Secret, requesting a token for the default ServiceAccount:

-->

### 不使用 kubectl proxy

在 Kubernetes 1.3 或更高版本中，`kubectl config view` 不再显示 token。
使用 `kubectl apply` 和 `kubectl describe secret ...` 及 grep 和剪切操作来为 default 服务帐户创建令牌，如下所示：
`grep/cut` 方法实现：
首先，创建 Secret，请求默认 ServiceAccount 的令牌：
```shell
kubectl apply -f - <<EOF
apiVersion: v1
kind: Secret
metadata:
  name: default-token
  annotations:
    kubernetes.io/service-account.name: default
type: kubernetes.io/service-account-token
EOF
```

<!--
Next, wait for the token controller to populate the Secret with a token:

Capture and use the generated token:
-->
接下来，等待令牌控制器使用令牌填充 Secret：
```shell
while ! kubectl describe secret default-token | grep -E '^token' >/dev/null; do
  echo "waiting for token..." >&2
  sleep 1
done
```

捕获并使用生成的令牌：
```shell
APISERVER=$(kubectl config view | grep server | cut -f 2- -d ":" | tr -d " ")
TOKEN=$(kubectl describe secret default-token | grep -E '^token' | cut -f2 -d':' | tr -d ' ')
curl $APISERVER/api --header "Authorization: Bearer $TOKEN" --insecure
```
```json
{
  "kind": "APIVersions",
  "versions": [
    "v1"
  ],
  "serverAddressByClientCIDRs": [
    {
      "clientCIDR": "0.0.0.0/0",
      "serverAddress": "10.0.1.149:443"
    }
  ]
}
```

`jsonpath` 方法实现：

```shell
APISERVER=$(kubectl config view --minify -o jsonpath='{.clusters[0].cluster.server}')
TOKEN=$(kubectl get secret default-token -o jsonpath='{.data.token}' | base64 --decode )
curl $APISERVER/api --header "Authorization: Bearer $TOKEN" --insecure
```

```json
{
  "kind": "APIVersions",
  "versions": [
    "v1"
  ],
  "serverAddressByClientCIDRs": [
    {
      "clientCIDR": "0.0.0.0/0",
      "serverAddress": "10.0.1.149:443"
    }
  ]
}
```

<!--
The above examples use the `--insecure` flag.  This leaves it subject to MITM
attacks.  When kubectl accesses the cluster it uses a stored root certificate
and client certificates to access the server.  (These are installed in the
`~/.kube` directory).  Since cluster certificates are typically self-signed, it
may take special configuration to get your http client to use root
certificate.

On some clusters, the apiserver does not require authentication; it may serve
on localhost, or be protected by a firewall.  There is not a standard
for this.  [Configuring Access to the API](/docs/admin/accessing-the-api)
describes how a cluster admin can configure this.  Such approaches may conflict
with future high-availability support.
-->
上面的例子使用了 `--insecure` 参数，这使得它很容易受到 MITM 攻击。
当 kubectl 访问集群时，它使用存储的根证书和客户端证书来访问服务器
（它们安装在 `~/.kube` 目录中）。
由于集群证书通常是自签名的，因此可能需要特殊配置才能让你的 http 客户端使用根证书。

在一些集群中，apiserver 不需要身份验证；它可能只服务于 localhost，或者被防火墙保护，
这个没有一定的标准。
[配置对 API 的访问](/zh/docs/concepts/security/controlling-access/)
描述了集群管理员如何进行配置。此类方法可能与未来的高可用性支持相冲突。

<!--
## Programmatic access to the API

Kubernetes officially supports [Go](#go-client) and [Python](#python-client)
client libraries.

### Go client

* To get the library, run the following command: `go get k8s.io/client-go/<version number>/kubernetes`. See [https://github.com/kubernetes/client-go](https://github.com/kubernetes/client-go) to see which versions are supported.
* Write an application atop of the client-go clients. Note that client-go defines its own API objects, so if needed, please import API definitions from client-go rather than from the main repository, e.g., `import "k8s.io/client-go/1.4/pkg/api/v1"` is correct.

The Go client can use the same [kubeconfig file](/docs/concepts/configuration/organize-cluster-access-kubeconfig/)
as the kubectl CLI does to locate and authenticate to the apiserver. See this [example](https://git.k8s.io/client-go/examples/out-of-cluster-client-configuration/main.go).

If the application is deployed as a Pod in the cluster, please refer to the [next section](#accessing-the-api-from-a-pod).
-->
## 以编程方式访问 API

Kubernetes 官方提供对 [Go](#go-client) 和 [Python](#python-client) 的客户端库支持。

### Go 客户端

* 想要获得这个库，请运行命令：`go get k8s.io/client-go/<version number>/kubernetes`。
  参阅 [https://github.com/kubernetes/client-go](https://github.com/kubernetes/client-go)
  来查看目前支持哪些版本。
* 基于这个 client-go 客户端库编写应用程序。
  请注意，client-go 定义了自己的 API 对象，因此如果需要，请从 client-go 而不是从主存储库
  导入 API 定义，例如，`import "k8s.io/client-go/1.4/pkg/api/v1"` 才是对的。

Go 客户端可以像 kubectl CLI 一样使用相同的
[kubeconfig 文件](/zh/docs/concepts/configuration/organize-cluster-access-kubeconfig/)
来定位和验证 apiserver。可参阅
[示例](https://git.k8s.io/client-go/examples/out-of-cluster-client-configuration/main.go)。

如果应用程序以 Pod 的形式部署在集群中，那么请参阅
[下一章](#accessing-the-api-from-a-pod)。

<!--
### Python client

To use [Python client](https://github.com/kubernetes-client/python), run the following command: `pip install kubernetes`. See [Python Client Library page](https://github.com/kubernetes-client/python) for more installation options.

The Python client can use the same [kubeconfig file](/docs/concepts/cluster-administration/authenticate-across-clusters-kubeconfig/)
as the kubectl CLI does to locate and authenticate to the apiserver. See this [example](https://github.com/kubernetes-client/python/tree/master/examples).

### Other languages

There are [client libraries](/docs/reference/using-api/client-libraries/) for accessing the API from other languages.
See documentation for other libraries for how they authenticate.
-->
### Python 客户端

如果想要使用 [Python 客户端](https://github.com/kubernetes-client/python)，
请运行命令：`pip install kubernetes`。参阅
[Python Client Library page](https://github.com/kubernetes-client/python)
以获得更详细的安装参数。

Python 客户端可以像 kubectl CLI 一样使用相同的
[kubeconfig 文件](/zh/docs/concepts/configuration/organize-cluster-access-kubeconfig/)
来定位和验证 apiserver，可参阅
[示例](https://github.com/kubernetes-client/python/tree/master/examples)。

### 其它语言

目前有多个[客户端库](/zh/docs/reference/using-api/client-libraries/)
为其它语言提供访问 API 的方法。
参阅其它库的相关文档以获取他们是如何验证的。

<!--
## Accessing the API from a Pod

When accessing the API from a pod, locating and authenticating
to the apiserver are somewhat different.

The recommended way to locate the apiserver within the pod is with
the `kubernetes.default.svc` DNS name, which resolves to a Service IP which in turn
will be routed to an apiserver.

The recommended way to authenticate to the apiserver is with a
[service account](/docs/tasks/configure-pod-container/configure-service-account/) credential. By kube-system, a pod
is associated with a service account, and a credential (token) for that
service account is placed into the filesystem tree of each container in that pod,
at `/var/run/secrets/kubernetes.io/serviceaccount/token`.
-->
### 从 Pod 中访问 API   {#accessing-the-api-from-a-pod}

当你从 Pod 中访问 API 时，定位和验证 apiserver 会有些许不同。

在 Pod 中定位 apiserver 的推荐方式是通过 `kubernetes.default.svc`
这个 DNS 名称，该名称将会解析为服务 IP，然后服务 IP 将会路由到 apiserver。

向 apiserver 进行身份验证的推荐方法是使用
[服务帐户](/zh/docs/tasks/configure-pod-container/configure-service-account/) 凭据。
通过 kube-system，Pod 与服务帐户相关联，并且该服务帐户的凭证（token）
被放置在该 Pod 中每个容器的文件系统中，位于
`/var/run/secrets/kubernetes.io/serviceaccount/token`。

<!--
If available, a certificate bundle is placed into the filesystem tree of each
container at `/var/run/secrets/kubernetes.io/serviceaccount/ca.crt`, and should be
used to verify the serving certificate of the apiserver.

Finally, the default namespace to be used for namespaced API operations is placed in a file
at `/var/run/secrets/kubernetes.io/serviceaccount/namespace` in each container.
-->
如果可用，则将证书放入每个容器的文件系统中的
`/var/run/secrets/kubernetes.io/serviceaccount/ca.crt`，
并且应该用于验证 apiserver 的服务证书。

最后，名字空间作用域的 API 操作所使用的 default 名字空间将被放置在
每个容器的 `/var/run/secrets/kubernetes.io/serviceaccount/namespace`
文件中。

<!--
From within a pod the recommended ways to connect to API are:

  - run `kubectl proxy` in a sidecar container in the pod, or as a background
    process within the container. This proxies the
    Kubernetes API to the localhost interface of the pod, so that other processes
    in any container of the pod can access it.
  - use the Go client library, and create a client using the `rest.InClusterConfig()` and `kubernetes.NewForConfig()` functions.
    They handle locating and authenticating to the apiserver. [example](https://git.k8s.io/client-go/examples/in-cluster-client-configuration/main.go)

In each case, the credentials of the pod are used to communicate securely with the apiserver.
-->
在 Pod 中，建议连接 API 的方法是：

- 在 Pod 的边车容器中运行 `kubectl proxy`，或者以后台进程的形式运行。
  这将把 Kubernetes API 代理到当前 Pod 的 localhost 接口，
  所以 Pod 中的所有容器中的进程都能访问它。
- 使用 Go 客户端库，并使用 `rest.InClusterConfig()` 和
  `kubernetes.NewForConfig()` 函数创建一个客户端。
  他们处理 apiserver 的定位和身份验证。
  [示例](https://git.k8s.io/client-go/examples/in-cluster-client-configuration/main.go)

在每种情况下，Pod 的凭证都是为了与 apiserver 安全地通信。

<!--
## Accessing services running on the cluster

The previous section describes how to connect to the Kubernetes API server. For information about connecting to other services running on a Kubernetes cluster, see [Access Cluster Services.](/docs/tasks/administer-cluster/access-cluster-services/)
-->

## 访问集群上运行的服务  {#accessing-services-running-on-the-cluster}

上一节介绍了如何连接到 Kubernetes API 服务器。
有关连接到 Kubernetes 集群上运行的其他服务的信息，请参阅[访问集群服务](/zh/docs/tasks/administer-cluster/access-cluster-services/)。


<!--
## Requesting redirects

The redirect capabilities have been deprecated and removed.  Please use a proxy (see below) instead.
-->
## 请求重定向

重定向功能已弃用并被删除。请改用代理（见下文）。

<!--
## So Many Proxies

There are several different proxies you may encounter when using Kubernetes:

1.  The [kubectl proxy](#directly-accessing-the-rest-api):

    - runs on a user's desktop or in a pod
    - proxies from a localhost address to the Kubernetes apiserver
    - client to proxy uses HTTP
    - proxy to apiserver uses HTTPS
    - locates apiserver
    - adds authentication headers

-->
## 多种代理

使用 Kubernetes 时可能会遇到几种不同的代理：

1. [kubectl 代理](#directly-accessing-the-rest-api)：

   - 在用户的桌面或 Pod 中运行
   - 代理从本地主机地址到 Kubernetes apiserver
   - 客户端到代理将使用 HTTP
   - 代理到 apiserver 使用 HTTPS
   - 定位 apiserver
   - 添加身份验证头部

<!--
1.  The [apiserver proxy](#discovering-builtin-services):

    - is a bastion built into the apiserver
    - connects a user outside of the cluster to cluster IPs which otherwise might not be reachable
    - runs in the apiserver processes
    - client to proxy uses HTTPS (or http if apiserver so configured)
    - proxy to target may use HTTP or HTTPS as chosen by proxy using available information
    - can be used to reach a Node, Pod, or Service
    - does load balancing when used to reach a Service
-->
2. [apiserver 代理](#discovering-builtin-services)：

   - 内置于 apiserver 中
   - 将集群外部的用户连接到集群 IP，否则这些 IP 可能无法访问
   - 运行在 apiserver 进程中
   - 客户端代理使用 HTTPS（也可配置为 http）
   - 代理将根据可用的信息决定使用 HTTP 或者 HTTPS 代理到目标
   - 可用于访问节点、Pod 或服务
   - 在访问服务时进行负载平衡

<!--
1.  The [kube proxy](/docs/concepts/services-networking/service/#ips-and-vips):

    - runs on each node
    - proxies UDP and TCP
    - does not understand HTTP
    - provides load balancing
    - is only used to reach services
-->
3. [kube proxy](/zh/docs/concepts/services-networking/service/#ips-and-vips)：

   - 运行在每个节点上
   - 代理 UDP 和 TCP
   - 不能代理 HTTP
   - 提供负载均衡
   - 只能用来访问服务

<!--
1.  A Proxy/Load-balancer in front of apiserver(s):

    - existence and implementation varies from cluster to cluster (e.g. nginx)
    - sits between all clients and one or more apiservers
    - acts as load balancer if there are several apiservers.
-->
4. 位于 apiserver 之前的 Proxy/Load-balancer：

   - 存在和实现因集群而异（例如 nginx）
   - 位于所有客户和一个或多个 apiserver 之间
   - 如果有多个 apiserver，则充当负载均衡器

<!--
1.  Cloud Load Balancers on external services:

    - are provided by some cloud providers (e.g. AWS ELB, Google Cloud Load Balancer)
    - are created automatically when the Kubernetes service has type `LoadBalancer`
    - use UDP/TCP only
    - implementation varies by cloud provider.

Kubernetes users will typically not need to worry about anything other than the first two types.  The cluster admin
will typically ensure that the latter types are setup correctly.
-->
5. 外部服务上的云负载均衡器：

   - 由一些云提供商提供（例如 AWS ELB，Google Cloud Load Balancer）
   - 当 Kubernetes 服务类型为 `LoadBalancer` 时自动创建
   - 只使用 UDP/TCP
   - 具体实现因云提供商而异。

除了前两种类型之外，Kubernetes 用户通常不需要担心任何其他问题。
集群管理员通常会确保后者的正确配置。
