---
title: Kubelet Configuration (v1beta1)
content_type: tool-reference
package: kubelet.config.k8s.io/v1beta1
auto_generated: true
---


## Resource Types 


- [KubeletConfiguration](#kubelet-config-k8s-io-v1beta1-KubeletConfiguration)
- [SerializedNodeConfigSource](#kubelet-config-k8s-io-v1beta1-SerializedNodeConfigSource)
  
    

## `KubeletConfiguration`     {#kubelet-config-k8s-io-v1beta1-KubeletConfiguration}
    


<p>KubeletConfiguration contains the configuration for the Kubelet</p>


<table class="table">
<thead><tr><th width="30%">Field</th><th>Description</th></tr></thead>
<tbody>
    
<tr><td><code>apiVersion</code><br/>string</td><td><code>kubelet.config.k8s.io/v1beta1</code></td></tr>
<tr><td><code>kind</code><br/>string</td><td><code>KubeletConfiguration</code></td></tr>
    
  
<tr><td><code>enableServer</code> <B>[Required]</B><br/>
<code>bool</code>
</td>
<td>
   <p>enableServer enables Kubelet's secured server.
Note: Kubelet's insecure port is controlled by the readOnlyPort option.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may disrupt components that interact with the Kubelet server.
Default: true</p>
</td>
</tr>
<tr><td><code>staticPodPath</code><br/>
<code>string</code>
</td>
<td>
   <p>staticPodPath is the path to the directory containing local (static) pods to
run, or the path to a single static pod file.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
the set of static pods specified at the new path may be different than the
ones the Kubelet initially started with, and this may disrupt your node.
Default: &quot;&quot;</p>
</td>
</tr>
<tr><td><code>syncFrequency</code><br/>
<a href="https://pkg.go.dev/k8s.io/apimachinery/pkg/apis/meta/v1#Duration"><code>meta/v1.Duration</code></a>
</td>
<td>
   <p>syncFrequency is the max period between synchronizing running
containers and config.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
shortening this duration may have a negative performance impact, especially
as the number of Pods on the node increases. Alternatively, increasing this
duration will result in longer refresh times for ConfigMaps and Secrets.
Default: &quot;1m&quot;</p>
</td>
</tr>
<tr><td><code>fileCheckFrequency</code><br/>
<a href="https://pkg.go.dev/k8s.io/apimachinery/pkg/apis/meta/v1#Duration"><code>meta/v1.Duration</code></a>
</td>
<td>
   <p>fileCheckFrequency is the duration between checking config files for
new data.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
shortening the duration will cause the Kubelet to reload local Static Pod
configurations more frequently, which may have a negative performance impact.
Default: &quot;20s&quot;</p>
</td>
</tr>
<tr><td><code>httpCheckFrequency</code><br/>
<a href="https://pkg.go.dev/k8s.io/apimachinery/pkg/apis/meta/v1#Duration"><code>meta/v1.Duration</code></a>
</td>
<td>
   <p>httpCheckFrequency is the duration between checking http for new data.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
shortening the duration will cause the Kubelet to poll staticPodURL more
frequently, which may have a negative performance impact.
Default: &quot;20s&quot;</p>
</td>
</tr>
<tr><td><code>staticPodURL</code><br/>
<code>string</code>
</td>
<td>
   <p>staticPodURL is the URL for accessing static pods to run.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
the set of static pods specified at the new URL may be different than the
ones the Kubelet initially started with, and this may disrupt your node.
Default: &quot;&quot;</p>
</td>
</tr>
<tr><td><code>staticPodURLHeader</code><br/>
<code>map[string][]string</code>
</td>
<td>
   <p>staticPodURLHeader is a map of slices with HTTP headers to use when accessing the podURL.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may disrupt the ability to read the latest set of static pods from StaticPodURL.
Default: nil</p>
</td>
</tr>
<tr><td><code>address</code><br/>
<code>string</code>
</td>
<td>
   <p>address is the IP address for the Kubelet to serve on (set to 0.0.0.0
for all interfaces).
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may disrupt components that interact with the Kubelet server.
Default: &quot;0.0.0.0&quot;</p>
</td>
</tr>
<tr><td><code>port</code><br/>
<code>int32</code>
</td>
<td>
   <p>port is the port for the Kubelet to serve on.
The port number must be between 1 and 65535, inclusive.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may disrupt components that interact with the Kubelet server.
Default: 10250</p>
</td>
</tr>
<tr><td><code>readOnlyPort</code><br/>
<code>int32</code>
</td>
<td>
   <p>readOnlyPort is the read-only port for the Kubelet to serve on with
no authentication/authorization.
The port number must be between 1 and 65535, inclusive.
Setting this field to 0 disables the read-only service.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may disrupt components that interact with the Kubelet server.
Default: 0 (disabled)</p>
</td>
</tr>
<tr><td><code>tlsCertFile</code><br/>
<code>string</code>
</td>
<td>
   <p>tlsCertFile is the file containing x509 Certificate for HTTPS. (CA cert,
if any, concatenated after server cert). If tlsCertFile and
tlsPrivateKeyFile are not provided, a self-signed certificate
and key are generated for the public address and saved to the directory
passed to the Kubelet's --cert-dir flag.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may disrupt components that interact with the Kubelet server.
Default: &quot;&quot;</p>
</td>
</tr>
<tr><td><code>tlsPrivateKeyFile</code><br/>
<code>string</code>
</td>
<td>
   <p>tlsPrivateKeyFile is the file containing x509 private key matching tlsCertFile.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may disrupt components that interact with the Kubelet server.
Default: &quot;&quot;</p>
</td>
</tr>
<tr><td><code>tlsCipherSuites</code><br/>
<code>[]string</code>
</td>
<td>
   <p>tlsCipherSuites is the list of allowed cipher suites for the server.
Values are from tls package constants (https://golang.org/pkg/crypto/tls/#pkg-constants).
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may disrupt components that interact with the Kubelet server.
Default: nil</p>
</td>
</tr>
<tr><td><code>tlsMinVersion</code><br/>
<code>string</code>
</td>
<td>
   <p>tlsMinVersion is the minimum TLS version supported.
Values are from tls package constants (https://golang.org/pkg/crypto/tls/#pkg-constants).
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may disrupt components that interact with the Kubelet server.
Default: &quot;&quot;</p>
</td>
</tr>
<tr><td><code>rotateCertificates</code><br/>
<code>bool</code>
</td>
<td>
   <p>rotateCertificates enables client certificate rotation. The Kubelet will request a
new certificate from the certificates.k8s.io API. This requires an approver to approve the
certificate signing requests.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
disabling it may disrupt the Kubelet's ability to authenticate with the API server
after the current certificate expires.
Default: false</p>
</td>
</tr>
<tr><td><code>serverTLSBootstrap</code><br/>
<code>bool</code>
</td>
<td>
   <p>serverTLSBootstrap enables server certificate bootstrap. Instead of self
signing a serving certificate, the Kubelet will request a certificate from
the 'certificates.k8s.io' API. This requires an approver to approve the
certificate signing requests (CSR). The RotateKubeletServerCertificate feature
must be enabled when setting this field.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
disabling it will stop the renewal of Kubelet server certificates, which can
disrupt components that interact with the Kubelet server in the long term,
due to certificate expiration.
Default: false</p>
</td>
</tr>
<tr><td><code>authentication</code><br/>
<a href="#kubelet-config-k8s-io-v1beta1-KubeletAuthentication"><code>KubeletAuthentication</code></a>
</td>
<td>
   <p>authentication specifies how requests to the Kubelet's server are authenticated.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may disrupt components that interact with the Kubelet server.
Defaults:
anonymous:
enabled: false
webhook:
enabled: true
cacheTTL: &quot;2m&quot;</p>
</td>
</tr>
<tr><td><code>authorization</code><br/>
<a href="#kubelet-config-k8s-io-v1beta1-KubeletAuthorization"><code>KubeletAuthorization</code></a>
</td>
<td>
   <p>authorization specifies how requests to the Kubelet's server are authorized.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may disrupt components that interact with the Kubelet server.
Defaults:
mode: Webhook
webhook:
cacheAuthorizedTTL: &quot;5m&quot;
cacheUnauthorizedTTL: &quot;30s&quot;</p>
</td>
</tr>
<tr><td><code>registryPullQPS</code><br/>
<code>int32</code>
</td>
<td>
   <p>registryPullQPS is the limit of registry pulls per second.
The value must not be a negative number.
Setting it to 0 means no limit.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may impact scalability by changing the amount of traffic produced
by image pulls.
Default: 5</p>
</td>
</tr>
<tr><td><code>registryBurst</code><br/>
<code>int32</code>
</td>
<td>
   <p>registryBurst is the maximum size of bursty pulls, temporarily allows
pulls to burst to this number, while still not exceeding registryPullQPS.
The value must not be a negative number.
Only used if registryPullQPS is greater than 0.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may impact scalability by changing the amount of traffic produced
by image pulls.
Default: 10</p>
</td>
</tr>
<tr><td><code>eventRecordQPS</code><br/>
<code>int32</code>
</td>
<td>
   <p>eventRecordQPS is the maximum event creations per second. If 0, there
is no limit enforced. The value cannot be a negative number.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may impact scalability by changing the amount of traffic produced by
event creations.
Default: 5</p>
</td>
</tr>
<tr><td><code>eventBurst</code><br/>
<code>int32</code>
</td>
<td>
   <p>eventBurst is the maximum size of a burst of event creations, temporarily
allows event creations to burst to this number, while still not exceeding
eventRecordQPS. This field canot be a negative number and it is only used
when eventRecordQPS &gt; 0.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may impact scalability by changing the amount of traffic produced by
event creations.
Default: 10</p>
</td>
</tr>
<tr><td><code>enableDebuggingHandlers</code><br/>
<code>bool</code>
</td>
<td>
   <p>enableDebuggingHandlers enables server endpoints for log access
and local running of containers and commands, including the exec,
attach, logs, and portforward features.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
disabling it may disrupt components that interact with the Kubelet server.
Default: true</p>
</td>
</tr>
<tr><td><code>enableContentionProfiling</code><br/>
<code>bool</code>
</td>
<td>
   <p>enableContentionProfiling enables lock contention profiling, if enableDebuggingHandlers is true.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
enabling it may carry a performance impact.
Default: false</p>
</td>
</tr>
<tr><td><code>healthzPort</code><br/>
<code>int32</code>
</td>
<td>
   <p>healthzPort is the port of the localhost healthz endpoint (set to 0 to disable).
A valid number is between 1 and 65535.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may disrupt components that monitor Kubelet health.
Default: 10248</p>
</td>
</tr>
<tr><td><code>healthzBindAddress</code><br/>
<code>string</code>
</td>
<td>
   <p>healthzBindAddress is the IP address for the healthz server to serve on.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may disrupt components that monitor Kubelet health.
Default: &quot;127.0.0.1&quot;</p>
</td>
</tr>
<tr><td><code>oomScoreAdj</code><br/>
<code>int32</code>
</td>
<td>
   <p>oomScoreAdj is The oom-score-adj value for kubelet process. Values
must be within the range [-1000, 1000].
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may impact the stability of nodes under memory pressure.
Default: -999</p>
</td>
</tr>
<tr><td><code>clusterDomain</code><br/>
<code>string</code>
</td>
<td>
   <p>clusterDomain is the DNS domain for this cluster. If set, kubelet will
configure all containers to search this domain in addition to the
host's search domains.
Dynamic Kubelet Config (deprecated): Dynamically updating this field is not recommended,
as it should be kept in sync with the rest of the cluster.
Default: &quot;&quot;</p>
</td>
</tr>
<tr><td><code>clusterDNS</code><br/>
<code>[]string</code>
</td>
<td>
   <p>clusterDNS is a list of IP addresses for the cluster DNS server. If set,
kubelet will configure all containers to use this for DNS resolution
instead of the host's DNS servers.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
changes will only take effect on Pods created after the update. Draining
the node is recommended before changing this field.
Default: nil</p>
</td>
</tr>
<tr><td><code>streamingConnectionIdleTimeout</code><br/>
<a href="https://pkg.go.dev/k8s.io/apimachinery/pkg/apis/meta/v1#Duration"><code>meta/v1.Duration</code></a>
</td>
<td>
   <p>streamingConnectionIdleTimeout is the maximum time a streaming connection
can be idle before the connection is automatically closed.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may impact components that rely on infrequent updates over streaming
connections to the Kubelet server.
Default: &quot;4h&quot;</p>
</td>
</tr>
<tr><td><code>nodeStatusUpdateFrequency</code><br/>
<a href="https://pkg.go.dev/k8s.io/apimachinery/pkg/apis/meta/v1#Duration"><code>meta/v1.Duration</code></a>
</td>
<td>
   <p>nodeStatusUpdateFrequency is the frequency that kubelet computes node
status. If node lease feature is not enabled, it is also the frequency that
kubelet posts node status to master.
Note: When node lease feature is not enabled, be cautious when changing the
constant, it must work with nodeMonitorGracePeriod in nodecontroller.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may impact node scalability, and also that the node controller's
nodeMonitorGracePeriod must be set to N*NodeStatusUpdateFrequency,
where N is the number of retries before the node controller marks
the node unhealthy.
Default: &quot;10s&quot;</p>
</td>
</tr>
<tr><td><code>nodeStatusReportFrequency</code><br/>
<a href="https://pkg.go.dev/k8s.io/apimachinery/pkg/apis/meta/v1#Duration"><code>meta/v1.Duration</code></a>
</td>
<td>
   <p>nodeStatusReportFrequency is the frequency that kubelet posts node
status to master if node status does not change. Kubelet will ignore this
frequency and post node status immediately if any change is detected. It is
only used when node lease feature is enabled. nodeStatusReportFrequency's
default value is 5m. But if nodeStatusUpdateFrequency is set explicitly,
nodeStatusReportFrequency's default value will be set to
nodeStatusUpdateFrequency for backward compatibility.
Default: &quot;5m&quot;</p>
</td>
</tr>
<tr><td><code>nodeLeaseDurationSeconds</code><br/>
<code>int32</code>
</td>
<td>
   <p>nodeLeaseDurationSeconds is the duration the Kubelet will set on its corresponding Lease.
NodeLease provides an indicator of node health by having the Kubelet create and
periodically renew a lease, named after the node, in the kube-node-lease namespace.
If the lease expires, the node can be considered unhealthy.
The lease is currently renewed every 10s, per KEP-0009. In the future, the lease renewal
interval may be set based on the lease duration.
The field value must be greater than 0.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
decreasing the duration may reduce tolerance for issues that temporarily prevent
the Kubelet from renewing the lease (e.g. a short-lived network issue).
Default: 40</p>
</td>
</tr>
<tr><td><code>imageMinimumGCAge</code><br/>
<a href="https://pkg.go.dev/k8s.io/apimachinery/pkg/apis/meta/v1#Duration"><code>meta/v1.Duration</code></a>
</td>
<td>
   <p>imageMinimumGCAge is the minimum age for an unused image before it is
garbage collected. If DynamicKubeletConfig (deprecated; default off)
is on, when dynamically updating this field, consider that  it may trigger or
delay garbage collection, and may change the image overhead on the node.
Default: &quot;2m&quot;</p>
</td>
</tr>
<tr><td><code>imageGCHighThresholdPercent</code><br/>
<code>int32</code>
</td>
<td>
   <p>imageGCHighThresholdPercent is the percent of disk usage after which
image garbage collection is always run. The percent is calculated by
dividing this field value by 100, so this field must be between 0 and
100, inclusive. When specified, the value must be greater than
imageGCLowThresholdPercent.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may trigger or delay garbage collection, and may change the image overhead
on the node.
Default: 85</p>
</td>
</tr>
<tr><td><code>imageGCLowThresholdPercent</code><br/>
<code>int32</code>
</td>
<td>
   <p>imageGCLowThresholdPercent is the percent of disk usage before which
image garbage collection is never run. Lowest disk usage to garbage
collect to. The percent is calculated by dividing this field value by 100,
so the field value must be between 0 and 100, inclusive. When specified, the
value must be less than imageGCHighThresholdPercent.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may trigger or delay garbage collection, and may change the image overhead
on the node.
Default: 80</p>
</td>
</tr>
<tr><td><code>volumeStatsAggPeriod</code><br/>
<a href="https://pkg.go.dev/k8s.io/apimachinery/pkg/apis/meta/v1#Duration"><code>meta/v1.Duration</code></a>
</td>
<td>
   <p>volumeStatsAggPeriod is the frequency for calculating and caching volume
disk usage for all pods.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
shortening the period may carry a performance impact.
Default: &quot;1m&quot;</p>
</td>
</tr>
<tr><td><code>kubeletCgroups</code><br/>
<code>string</code>
</td>
<td>
   <p>kubeletCgroups is the absolute name of cgroups to isolate the kubelet in
Dynamic Kubelet Config (deprecated): This field should not be updated without a full node
reboot. It is safest to keep this value the same as the local config.
Default: &quot;&quot;</p>
</td>
</tr>
<tr><td><code>systemCgroups</code><br/>
<code>string</code>
</td>
<td>
   <p>systemCgroups is absolute name of cgroups in which to place
all non-kernel processes that are not already in a container. Empty
for no container. Rolling back the flag requires a reboot.
The cgroupRoot must be specified if this field is not empty.
Dynamic Kubelet Config (deprecated): This field should not be updated without a full node
reboot. It is safest to keep this value the same as the local config.
Default: &quot;&quot;</p>
</td>
</tr>
<tr><td><code>cgroupRoot</code><br/>
<code>string</code>
</td>
<td>
   <p>cgroupRoot is the root cgroup to use for pods. This is handled by the
container runtime on a best effort basis.
Dynamic Kubelet Config (deprecated): This field should not be updated without a full node
reboot. It is safest to keep this value the same as the local config.
Default: &quot;&quot;</p>
</td>
</tr>
<tr><td><code>cgroupsPerQOS</code><br/>
<code>bool</code>
</td>
<td>
   <p>cgroupsPerQOS enable QoS based CGroup hierarchy: top level CGroups for QoS classes
and all Burstable and BestEffort Pods are brought up under their specific top level
QoS CGroup.
Dynamic Kubelet Config (deprecated): This field should not be updated without a full node
reboot. It is safest to keep this value the same as the local config.
Default: true</p>
</td>
</tr>
<tr><td><code>cgroupDriver</code><br/>
<code>string</code>
</td>
<td>
   <p>cgroupDriver is the driver kubelet uses to manipulate CGroups on the host (cgroupfs
or systemd).
Dynamic Kubelet Config (deprecated): This field should not be updated without a full node
reboot. It is safest to keep this value the same as the local config.
Default: &quot;cgroupfs&quot;</p>
</td>
</tr>
<tr><td><code>cpuManagerPolicy</code><br/>
<code>string</code>
</td>
<td>
   <p>cpuManagerPolicy is the name of the policy to use.
Requires the CPUManager feature gate to be enabled.
Dynamic Kubelet Config (deprecated): This field should not be updated without a full node
reboot. It is safest to keep this value the same as the local config.
Default: &quot;None&quot;</p>
</td>
</tr>
<tr><td><code>cpuManagerPolicyOptions</code><br/>
<code>map[string]string</code>
</td>
<td>
   <p>cpuManagerPolicyOptions is a set of key=value which 	allows to set extra options
to fine tune the behaviour of the cpu manager policies.
Requires  both the &quot;CPUManager&quot; and &quot;CPUManagerPolicyOptions&quot; feature gates to be enabled.
Dynamic Kubelet Config (beta): This field should not be updated without a full node
reboot. It is safest to keep this value the same as the local config.
Default: nil</p>
</td>
</tr>
<tr><td><code>cpuManagerReconcilePeriod</code><br/>
<a href="https://pkg.go.dev/k8s.io/apimachinery/pkg/apis/meta/v1#Duration"><code>meta/v1.Duration</code></a>
</td>
<td>
   <p>cpuManagerReconcilePeriod is the reconciliation period for the CPU Manager.
Requires the CPUManager feature gate to be enabled.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
shortening the period may carry a performance impact.
Default: &quot;10s&quot;</p>
</td>
</tr>
<tr><td><code>memoryManagerPolicy</code><br/>
<code>string</code>
</td>
<td>
   <p>memoryManagerPolicy is the name of the policy to use by memory manager.
Requires the MemoryManager feature gate to be enabled.
Dynamic Kubelet Config (deprecated): This field should not be updated without a full node
reboot. It is safest to keep this value the same as the local config.
Default: &quot;none&quot;</p>
</td>
</tr>
<tr><td><code>topologyManagerPolicy</code><br/>
<code>string</code>
</td>
<td>
   <p>topologyManagerPolicy is the name of the topology manager policy to use.
Valid values include:</p>
<ul>
<li><code>restricted</code>: kubelet only allows pods with optimal NUMA node alignment for
requested resources;</li>
<li><code>best-effort</code>: kubelet will favor pods with NUMA alignment of CPU and device
resources;</li>
<li><code>none</code>: kubelet has no knowledge of NUMA alignment of a pod's CPU and device resources.</li>
<li><code>single-numa-node</code>: kubelet only allows pods with a single NUMA alignment
of CPU and device resources.</li>
</ul>
<p>Policies other than &quot;none&quot; require the TopologyManager feature gate to be enabled.
Dynamic Kubelet Config (deprecated): This field should not be updated without a full node
reboot. It is safest to keep this value the same as the local config.
Default: &quot;none&quot;</p>
</td>
</tr>
<tr><td><code>topologyManagerScope</code><br/>
<code>string</code>
</td>
<td>
   <p>topologyManagerScope represents the scope of topology hint generation
that topology manager requests and hint providers generate. Valid values include:</p>
<ul>
<li><code>container</code>: topology policy is applied on a per-container basis.</li>
<li><code>pod</code>: topology policy is applied on a per-pod basis.</li>
</ul>
<p>&quot;pod&quot; scope requires the TopologyManager feature gate to be enabled.
Default: &quot;container&quot;</p>
</td>
</tr>
<tr><td><code>qosReserved</code><br/>
<code>map[string]string</code>
</td>
<td>
   <p>qosReserved is a set of resource name to percentage pairs that specify
the minimum percentage of a resource reserved for exclusive use by the
guaranteed QoS tier.
Currently supported resources: &quot;memory&quot;
Requires the QOSReserved feature gate to be enabled.
Dynamic Kubelet Config (deprecated): This field should not be updated without a full node
reboot. It is safest to keep this value the same as the local config.
Default: nil</p>
</td>
</tr>
<tr><td><code>runtimeRequestTimeout</code><br/>
<a href="https://pkg.go.dev/k8s.io/apimachinery/pkg/apis/meta/v1#Duration"><code>meta/v1.Duration</code></a>
</td>
<td>
   <p>runtimeRequestTimeout is the timeout for all runtime requests except long running
requests - pull, logs, exec and attach.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may disrupt components that interact with the Kubelet server.
Default: &quot;2m&quot;</p>
</td>
</tr>
<tr><td><code>hairpinMode</code><br/>
<code>string</code>
</td>
<td>
   <p>hairpinMode specifies how the Kubelet should configure the container
bridge for hairpin packets.
Setting this flag allows endpoints in a Service to loadbalance back to
themselves if they should try to access their own Service. Values:</p>
<ul>
<li>&quot;promiscuous-bridge&quot;: make the container bridge promiscuous.</li>
<li>&quot;hairpin-veth&quot;:       set the hairpin flag on container veth interfaces.</li>
<li>&quot;none&quot;:               do nothing.</li>
</ul>
<p>Generally, one must set <code>--hairpin-mode=hairpin-veth to</code> achieve hairpin NAT,
because promiscuous-bridge assumes the existence of a container bridge named cbr0.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may require a node reboot, depending on the network plugin.
Default: &quot;promiscuous-bridge&quot;</p>
</td>
</tr>
<tr><td><code>maxPods</code><br/>
<code>int32</code>
</td>
<td>
   <p>maxPods is the maximum number of Pods that can run on this Kubelet.
The value must be a non-negative integer.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
changes may cause Pods to fail admission on Kubelet restart, and may change
the value reported in Node.Status.Capacity[v1.ResourcePods], thus affecting
future scheduling decisions. Increasing this value may also decrease performance,
as more Pods can be packed into a single node.
Default: 110</p>
</td>
</tr>
<tr><td><code>podCIDR</code><br/>
<code>string</code>
</td>
<td>
   <p>podCIDR is the CIDR to use for pod IP addresses, only used in standalone mode.
In cluster mode, this is obtained from the control plane.
Dynamic Kubelet Config (deprecated): This field should always be set to the empty default.
It should only set for standalone Kubelets, which cannot use Dynamic Kubelet Config.
Default: &quot;&quot;</p>
</td>
</tr>
<tr><td><code>podPidsLimit</code><br/>
<code>int64</code>
</td>
<td>
   <p>podPidsLimit is the maximum number of PIDs in any pod.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
lowering it may prevent container processes from forking after the change.
Default: -1</p>
</td>
</tr>
<tr><td><code>resolvConf</code><br/>
<code>string</code>
</td>
<td>
   <p>resolvConf is the resolver configuration file used as the basis
for the container DNS resolution configuration.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
changes will only take effect on Pods created after the update. Draining
the node is recommended before changing this field.
If set to the empty string, will override the default and effectively disable DNS lookups.
Default: &quot;/etc/resolv.conf&quot;</p>
</td>
</tr>
<tr><td><code>runOnce</code><br/>
<code>bool</code>
</td>
<td>
   <p>runOnce causes the Kubelet to check the API server once for pods,
run those in addition to the pods specified by static pod files, and exit.
Default: false</p>
</td>
</tr>
<tr><td><code>cpuCFSQuota</code><br/>
<code>bool</code>
</td>
<td>
   <p>cpuCFSQuota enables CPU CFS quota enforcement for containers that
specify CPU limits.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
disabling it may reduce node stability.
Default: true</p>
</td>
</tr>
<tr><td><code>cpuCFSQuotaPeriod</code><br/>
<a href="https://pkg.go.dev/k8s.io/apimachinery/pkg/apis/meta/v1#Duration"><code>meta/v1.Duration</code></a>
</td>
<td>
   <p>cpuCFSQuotaPeriod is the CPU CFS quota period value, <code>cpu.cfs_period_us</code>.
The value must be between 1 us and 1 second, inclusive.
Requires the CustomCPUCFSQuotaPeriod feature gate to be enabled.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
limits set for containers will result in different cpu.cfs_quota settings. This
will trigger container restarts on the node being reconfigured.
Default: &quot;100ms&quot;</p>
</td>
</tr>
<tr><td><code>nodeStatusMaxImages</code><br/>
<code>int32</code>
</td>
<td>
   <p>nodeStatusMaxImages caps the number of images reported in Node.status.images.
The value must be greater than -2.
Note: If -1 is specified, no cap will be applied. If 0 is specified, no image is returned.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
different values can be reported on node status.
Default: 50</p>
</td>
</tr>
<tr><td><code>maxOpenFiles</code><br/>
<code>int64</code>
</td>
<td>
   <p>maxOpenFiles is Number of files that can be opened by Kubelet process.
The value must be a non-negative number.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may impact the ability of the Kubelet to interact with the node's filesystem.
Default: 1000000</p>
</td>
</tr>
<tr><td><code>contentType</code><br/>
<code>string</code>
</td>
<td>
   <p>contentType is contentType of requests sent to apiserver.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may impact the ability for the Kubelet to communicate with the API server.
If the Kubelet loses contact with the API server due to a change to this field,
the change cannot be reverted via dynamic Kubelet config.
Default: &quot;application/vnd.kubernetes.protobuf&quot;</p>
</td>
</tr>
<tr><td><code>kubeAPIQPS</code><br/>
<code>int32</code>
</td>
<td>
   <p>kubeAPIQPS is the QPS to use while talking with kubernetes apiserver.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may impact scalability by changing the amount of traffic the Kubelet
sends to the API server.
Default: 5</p>
</td>
</tr>
<tr><td><code>kubeAPIBurst</code><br/>
<code>int32</code>
</td>
<td>
   <p>kubeAPIBurst is the burst to allow while talking with kubernetes API server.
This field cannot be a negative number.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may impact scalability by changing the amount of traffic the Kubelet
sends to the API server.
Default: 10</p>
</td>
</tr>
<tr><td><code>serializeImagePulls</code><br/>
<code>bool</code>
</td>
<td>
   <p>serializeImagePulls when enabled, tells the Kubelet to pull images one
at a time. We recommend <em>not</em> changing the default value on nodes that
run docker daemon with version  &lt; 1.9 or an Aufs storage backend.
Issue #10959 has more details.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may impact the performance of image pulls.
Default: true</p>
</td>
</tr>
<tr><td><code>evictionHard</code><br/>
<code>map[string]string</code>
</td>
<td>
   <p>evictionHard is a map of signal names to quantities that defines hard eviction
thresholds. For example: <code>{&quot;memory.available&quot;: &quot;300Mi&quot;}</code>.
To explicitly disable, pass a 0% or 100% threshold on an arbitrary resource.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may trigger or delay Pod evictions.
Default:
memory.available:  &quot;100Mi&quot;
nodefs.available:  &quot;10%&quot;
nodefs.inodesFree: &quot;5%&quot;
imagefs.available: &quot;15%&quot;</p>
</td>
</tr>
<tr><td><code>evictionSoft</code><br/>
<code>map[string]string</code>
</td>
<td>
   <p>evictionSoft is a map of signal names to quantities that defines soft eviction thresholds.
For example: <code>{&quot;memory.available&quot;: &quot;300Mi&quot;}</code>.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may trigger or delay Pod evictions, and may change the allocatable reported
by the node.
Default: nil</p>
</td>
</tr>
<tr><td><code>evictionSoftGracePeriod</code><br/>
<code>map[string]string</code>
</td>
<td>
   <p>evictionSoftGracePeriod is a map of signal names to quantities that defines grace
periods for each soft eviction signal. For example: <code>{&quot;memory.available&quot;: &quot;30s&quot;}</code>.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may trigger or delay Pod evictions.
Default: nil</p>
</td>
</tr>
<tr><td><code>evictionPressureTransitionPeriod</code><br/>
<a href="https://pkg.go.dev/k8s.io/apimachinery/pkg/apis/meta/v1#Duration"><code>meta/v1.Duration</code></a>
</td>
<td>
   <p>evictionPressureTransitionPeriod is the duration for which the kubelet has to wait
before transitioning out of an eviction pressure condition.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
lowering it may decrease the stability of the node when the node is overcommitted.
Default: &quot;5m&quot;</p>
</td>
</tr>
<tr><td><code>evictionMaxPodGracePeriod</code><br/>
<code>int32</code>
</td>
<td>
   <p>evictionMaxPodGracePeriod is the maximum allowed grace period (in seconds) to use
when terminating pods in response to a soft eviction threshold being met. This value
effectively caps the Pod's terminationGracePeriodSeconds value during soft evictions.
Note: Due to issue #64530, the behavior has a bug where this value currently just
overrides the grace period during soft eviction, which can increase the grace
period from what is set on the Pod. This bug will be fixed in a future release.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
lowering it decreases the amount of time Pods will have to gracefully clean
up before being killed during a soft eviction.
Default: 0</p>
</td>
</tr>
<tr><td><code>evictionMinimumReclaim</code><br/>
<code>map[string]string</code>
</td>
<td>
   <p>evictionMinimumReclaim is a map of signal names to quantities that defines minimum reclaims,
which describe the minimum amount of a given resource the kubelet will reclaim when
performing a pod eviction while that resource is under pressure.
For example: <code>{&quot;imagefs.available&quot;: &quot;2Gi&quot;}</code>.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may change how well eviction can manage resource pressure.
Default: nil</p>
</td>
</tr>
<tr><td><code>podsPerCore</code><br/>
<code>int32</code>
</td>
<td>
   <p>podsPerCore is the maximum number of pods per core. Cannot exceed maxPods.
The value must be a non-negative integer.
If 0, there is no limit on the number of Pods.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
changes may cause Pods to fail admission on Kubelet restart, and may change
the value reported in <code>Node.status.capacity.pods</code>, thus affecting
future scheduling decisions. Increasing this value may also decrease performance,
as more Pods can be packed into a single node.
Default: 0</p>
</td>
</tr>
<tr><td><code>enableControllerAttachDetach</code><br/>
<code>bool</code>
</td>
<td>
   <p>enableControllerAttachDetach enables the Attach/Detach controller to
manage attachment/detachment of volumes scheduled to this node, and
disables kubelet from executing any attach/detach operations.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
changing which component is responsible for volume management on a live node
may result in volumes refusing to detach if the node is not drained prior to
the update, and if Pods are scheduled to the node before the
volumes.kubernetes.io/controller-managed-attach-detach annotation is updated by the
Kubelet. In general, it is safest to leave this value set the same as local config.
Default: true</p>
</td>
</tr>
<tr><td><code>protectKernelDefaults</code><br/>
<code>bool</code>
</td>
<td>
   <p>protectKernelDefaults, if true, causes the Kubelet to error if kernel
flags are not as it expects. Otherwise the Kubelet will attempt to modify
kernel flags to match its expectation.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
enabling it may cause the Kubelet to crash-loop if the Kernel is not configured as
Kubelet expects.
Default: false</p>
</td>
</tr>
<tr><td><code>makeIPTablesUtilChains</code><br/>
<code>bool</code>
</td>
<td>
   <p>makeIPTablesUtilChains, if true, causes the Kubelet ensures a set of iptables rules
are present on host.
These rules will serve as utility rules for various components, e.g. kube-proxy.
The rules will be created based on iptablesMasqueradeBit and iptablesDropBit.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
disabling it will prevent the Kubelet from healing locally misconfigured iptables rules.
Default: true</p>
</td>
</tr>
<tr><td><code>iptablesMasqueradeBit</code><br/>
<code>int32</code>
</td>
<td>
   <p>iptablesMasqueradeBit is the bit of the iptables fwmark space to mark for SNAT.
Values must be within the range [0, 31]. Must be different from other mark bits.
Warning: Please match the value of the corresponding parameter in kube-proxy.
TODO: clean up IPTablesMasqueradeBit in kube-proxy.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it needs to be coordinated with other components, like kube-proxy, and the update
will only be effective if MakeIPTablesUtilChains is enabled.
Default: 14</p>
</td>
</tr>
<tr><td><code>iptablesDropBit</code><br/>
<code>int32</code>
</td>
<td>
   <p>iptablesDropBit is the bit of the iptables fwmark space to mark for dropping packets.
Values must be within the range [0, 31]. Must be different from other mark bits.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it needs to be coordinated with other components, like kube-proxy, and the update
will only be effective if MakeIPTablesUtilChains is enabled.
Default: 15</p>
</td>
</tr>
<tr><td><code>featureGates</code><br/>
<code>map[string]bool</code>
</td>
<td>
   <p>featureGates is a map of feature names to bools that enable or disable experimental
features. This field modifies piecemeal the built-in default values from
&quot;k8s.io/kubernetes/pkg/features/kube_features.go&quot;.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider the
documentation for the features you are enabling or disabling. While we
encourage feature developers to make it possible to dynamically enable
and disable features, some changes may require node reboots, and some
features may require careful coordination to retroactively disable.
Default: nil</p>
</td>
</tr>
<tr><td><code>failSwapOn</code><br/>
<code>bool</code>
</td>
<td>
   <p>failSwapOn tells the Kubelet to fail to start if swap is enabled on the node.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
setting it to true will cause the Kubelet to crash-loop if swap is enabled.
Default: true</p>
</td>
</tr>
<tr><td><code>memorySwap</code><br/>
<a href="#kubelet-config-k8s-io-v1beta1-MemorySwapConfiguration"><code>MemorySwapConfiguration</code></a>
</td>
<td>
   <p>memorySwap configures swap memory available to container workloads.</p>
</td>
</tr>
<tr><td><code>containerLogMaxSize</code><br/>
<code>string</code>
</td>
<td>
   <p>containerLogMaxSize is a quantity defining the maximum size of the container log
file before it is rotated. For example: &quot;5Mi&quot; or &quot;256Ki&quot;.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may trigger log rotation.
Default: &quot;10Mi&quot;</p>
</td>
</tr>
<tr><td><code>containerLogMaxFiles</code><br/>
<code>int32</code>
</td>
<td>
   <p>containerLogMaxFiles specifies the maximum number of container log files that can
be present for a container.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
lowering it may cause log files to be deleted.
Default: 5</p>
</td>
</tr>
<tr><td><code>configMapAndSecretChangeDetectionStrategy</code><br/>
<a href="#kubelet-config-k8s-io-v1beta1-ResourceChangeDetectionStrategy"><code>ResourceChangeDetectionStrategy</code></a>
</td>
<td>
   <p>configMapAndSecretChangeDetectionStrategy is a mode in which ConfigMap and Secret
managers are running. Valid values include:</p>
<ul>
<li><code>Get</code>: kubelet fetches necessary objects directly from the API server;</li>
<li><code>Cache</code>: kubelet uses TTL cache for object fetched from the API server;</li>
<li><code>Watch</code>: kubelet uses watches to observe changes to objects that are in its interest.</li>
</ul>
<p>Default: &quot;Watch&quot;</p>
</td>
</tr>
<tr><td><code>systemReserved</code><br/>
<code>map[string]string</code>
</td>
<td>
   <p>systemReserved is a set of ResourceName=ResourceQuantity (e.g. cpu=200m,memory=150G)
pairs that describe resources reserved for non-kubernetes components.
Currently only cpu and memory are supported.
See http://kubernetes.io/docs/user-guide/compute-resources for more detail.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may not be possible to increase the reserved resources, because this
requires resizing cgroups. Always look for a NodeAllocatableEnforced event
after updating this field to ensure that the update was successful.
Default: nil</p>
</td>
</tr>
<tr><td><code>kubeReserved</code><br/>
<code>map[string]string</code>
</td>
<td>
   <p>kubeReserved is a set of ResourceName=ResourceQuantity (e.g. cpu=200m,memory=150G) pairs
that describe resources reserved for kubernetes system components.
Currently cpu, memory and local storage for root file system are supported.
See https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/
for more details.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may not be possible to increase the reserved resources, because this
requires resizing cgroups. Always look for a NodeAllocatableEnforced event
after updating this field to ensure that the update was successful.
Default: nil</p>
</td>
</tr>
<tr><td><code>reservedSystemCPUs</code> <B>[Required]</B><br/>
<code>string</code>
</td>
<td>
   <p>The reservedSystemCPUs option specifies the CPU list reserved for the host
level system threads and kubernetes related threads. This provide a &quot;static&quot;
CPU list rather than the &quot;dynamic&quot; list by systemReserved and kubeReserved.
This option does not support systemReservedCgroup or kubeReservedCgroup.</p>
</td>
</tr>
<tr><td><code>showHiddenMetricsForVersion</code><br/>
<code>string</code>
</td>
<td>
   <p>showHiddenMetricsForVersion is the previous version for which you want to show
hidden metrics.
Only the previous minor version is meaningful, other values will not be allowed.
The format is <code>&lt;major&gt;.&lt;minor&gt;</code>, e.g.: <code>1.16</code>.
The purpose of this format is make sure you have the opportunity to notice
if the next release hides additional metrics, rather than being surprised
when they are permanently removed in the release after that.
Default: &quot;&quot;</p>
</td>
</tr>
<tr><td><code>systemReservedCgroup</code><br/>
<code>string</code>
</td>
<td>
   <p>systemReservedCgroup helps the kubelet identify absolute name of top level CGroup used
to enforce <code>systemReserved</code> compute resource reservation for OS system daemons.
Refer to <a href="https://git.k8s.io/community/contributors/design-proposals/node/node-allocatable.md">Node Allocatable</a>
doc for more information.
Dynamic Kubelet Config (deprecated): This field should not be updated without a full node
reboot. It is safest to keep this value the same as the local config.
Default: &quot;&quot;</p>
</td>
</tr>
<tr><td><code>kubeReservedCgroup</code><br/>
<code>string</code>
</td>
<td>
   <p>kubeReservedCgroup helps the kubelet identify absolute name of top level CGroup used
to enforce <code>KubeReserved</code> compute resource reservation for Kubernetes node system daemons.
Refer to <a href="https://git.k8s.io/community/contributors/design-proposals/node/node-allocatable.md">Node Allocatable</a>
doc for more information.
Dynamic Kubelet Config (deprecated): This field should not be updated without a full node
reboot. It is safest to keep this value the same as the local config.
Default: &quot;&quot;</p>
</td>
</tr>
<tr><td><code>enforceNodeAllocatable</code><br/>
<code>[]string</code>
</td>
<td>
   <p>This flag specifies the various Node Allocatable enforcements that Kubelet needs to perform.
This flag accepts a list of options. Acceptable options are <code>none</code>, <code>pods</code>,
<code>system-reserved</code> and <code>kube-reserved</code>.
If <code>none</code> is specified, no other options may be specified.
When <code>system-reserved</code> is in the list, systemReservedCgroup must be specified.
When <code>kube-reserved</code> is in the list, kubeReservedCgroup must be specified.
This field is supported only when <code>cgroupsPerQOS</code> is set to true.
Refer to <a href="https://git.k8s.io/community/contributors/design-proposals/node/node-allocatable.md">Node Allocatable</a>
for more information.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
removing enforcements may reduce the stability of the node. Alternatively, adding
enforcements may reduce the stability of components which were using more than
the reserved amount of resources; for example, enforcing kube-reserved may cause
Kubelets to OOM if it uses more than the reserved resources, and enforcing system-reserved
may cause system daemons to OOM if they use more than the reserved resources.
Default: [&quot;pods&quot;]</p>
</td>
</tr>
<tr><td><code>allowedUnsafeSysctls</code><br/>
<code>[]string</code>
</td>
<td>
   <p>A comma separated whitelist of unsafe sysctls or sysctl patterns (ending in <code>*</code>).
Unsafe sysctl groups are <code>kernel.shm*</code>, <code>kernel.msg*</code>, <code>kernel.sem</code>, <code>fs.mqueue.*</code>,
and <code>net.*</code>. For example: &quot;<code>kernel.msg*,net.ipv4.route.min_pmtu</code>&quot;
Default: []</p>
</td>
</tr>
<tr><td><code>volumePluginDir</code><br/>
<code>string</code>
</td>
<td>
   <p>volumePluginDir is the full path of the directory in which to search
for additional third party volume plugins.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that changing
the volumePluginDir may disrupt workloads relying on third party volume plugins.
Default: &quot;/usr/libexec/kubernetes/kubelet-plugins/volume/exec/&quot;</p>
</td>
</tr>
<tr><td><code>providerID</code><br/>
<code>string</code>
</td>
<td>
   <p>providerID, if set, sets the unique ID of the instance that an external
provider (i.e. cloudprovider) can use to identify a specific node.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may impact the ability of the Kubelet to interact with cloud providers.
Default: &quot;&quot;</p>
</td>
</tr>
<tr><td><code>kernelMemcgNotification</code><br/>
<code>bool</code>
</td>
<td>
   <p>kernelMemcgNotification, if set, instructs the the kubelet to integrate with the
kernel memcg notification for determining if memory eviction thresholds are
exceeded rather than polling.
If DynamicKubeletConfig (deprecated; default off) is on, when
dynamically updating this field, consider that
it may impact the way Kubelet interacts with the kernel.
Default: false</p>
</td>
</tr>
<tr><td><code>logging</code> <B>[Required]</B><br/>
<a href="#LoggingConfiguration"><code>LoggingConfiguration</code></a>
</td>
<td>
   <p>logging specifies the options of logging.
Refer to <a href="https://github.com/kubernetes/component-base/blob/master/logs/options.go">Logs Options</a>
for more information.
Default:
Format: text</p>
</td>
</tr>
<tr><td><code>enableSystemLogHandler</code><br/>
<code>bool</code>
</td>
<td>
   <p>enableSystemLogHandler enables system logs via web interface host:port/logs/
Default: true</p>
</td>
</tr>
<tr><td><code>shutdownGracePeriod</code><br/>
<a href="https://pkg.go.dev/k8s.io/apimachinery/pkg/apis/meta/v1#Duration"><code>meta/v1.Duration</code></a>
</td>
<td>
   <p>shutdownGracePeriod specifies the total duration that the node should delay the
shutdown and total grace period for pod termination during a node shutdown.
Default: &quot;0s&quot;</p>
</td>
</tr>
<tr><td><code>shutdownGracePeriodCriticalPods</code><br/>
<a href="https://pkg.go.dev/k8s.io/apimachinery/pkg/apis/meta/v1#Duration"><code>meta/v1.Duration</code></a>
</td>
<td>
   <p>shutdownGracePeriodCriticalPods specifies the duration used to terminate critical
pods during a node shutdown. This should be less than shutdownGracePeriod.
For example, if shutdownGracePeriod=30s, and shutdownGracePeriodCriticalPods=10s,
during a node shutdown the first 20 seconds would be reserved for gracefully
terminating normal pods, and the last 10 seconds would be reserved for terminating
critical pods.
Default: &quot;0s&quot;</p>
</td>
</tr>
<tr><td><code>shutdownGracePeriodByPodPriority</code><br/>
<a href="#kubelet-config-k8s-io-v1beta1-ShutdownGracePeriodByPodPriority"><code>[]ShutdownGracePeriodByPodPriority</code></a>
</td>
<td>
   <p>shutdownGracePeriodByPodPriority specifies the shutdown grace period for Pods based
on their associated priority class value.
When a shutdown request is received, the Kubelet will initiate shutdown on all pods
running on the node with a grace period that depends on the priority of the pod,
and then wait for all pods to exit.
Each entry in the array represents the graceful shutdown time a pod with a priority
class value that lies in the range of that value and the next higher entry in the
list when the node is shutting down.
For example, to allow critical pods 10s to shutdown, priority&gt;=10000 pods 20s to
shutdown, and all remaining pods 30s to shutdown.</p>
<p>shutdownGracePeriodByPodPriority:</p>
<ul>
<li>priority: 2000000000
shutdownGracePeriodSeconds: 10</li>
<li>priority: 10000
shutdownGracePeriodSeconds: 20</li>
<li>priority: 0
shutdownGracePeriodSeconds: 30</li>
</ul>
<p>The time the Kubelet will wait before exiting will at most be the maximum of all
shutdownGracePeriodSeconds for each priority class range represented on the node.
When all pods have exited or reached their grace periods, the Kubelet will release
the shutdown inhibit lock.
Requires the GracefulNodeShutdown feature gate to be enabled.
This configuration must be empty if either ShutdownGracePeriod or ShutdownGracePeriodCriticalPods is set.
Default: nil</p>
</td>
</tr>
<tr><td><code>reservedMemory</code><br/>
<a href="#kubelet-config-k8s-io-v1beta1-MemoryReservation"><code>[]MemoryReservation</code></a>
</td>
<td>
   <p>reservedMemory specifies a comma-separated list of memory reservations for NUMA nodes.
The parameter makes sense only in the context of the memory manager feature.
The memory manager will not allocate reserved memory for container workloads.
For example, if you have a NUMA0 with 10Gi of memory and the reservedMemory was
specified to reserve 1Gi of memory at NUMA0, the memory manager will assume that
only 9Gi is available for allocation.
You can specify a different amount of NUMA node and memory types.
You can omit this parameter at all, but you should be aware that the amount of
reserved memory from all NUMA nodes should be equal to the amount of memory specified
by the <a href="https://kubernetes.io/docs/tasks/administer-cluster/reserve-compute-resources/#node-allocatable">node allocatable</a>.
If at least one node allocatable parameter has a non-zero value, you will need
to specify at least one NUMA node.
Also, avoid specifying:</p>
<ol>
<li>Duplicates, the same NUMA node, and memory type, but with a different value.</li>
<li>zero limits for any memory type.</li>
<li>NUMAs nodes IDs that do not exist under the machine.</li>
<li>memory types except for memory and hugepages-<!-- raw HTML omitted --></li>
</ol>
<p>Default: nil</p>
</td>
</tr>
<tr><td><code>enableProfilingHandler</code><br/>
<code>bool</code>
</td>
<td>
   <p>enableProfilingHandler enables profiling via web interface host:port/debug/pprof/
Default: true</p>
</td>
</tr>
<tr><td><code>enableDebugFlagsHandler</code><br/>
<code>bool</code>
</td>
<td>
   <p>enableDebugFlagsHandler enables flags endpoint via web interface host:port/debug/flags/v
Default: true</p>
</td>
</tr>
<tr><td><code>seccompDefault</code><br/>
<code>bool</code>
</td>
<td>
   <p>SeccompDefault enables the use of <code>RuntimeDefault</code> as the default seccomp profile for all workloads.
This requires the corresponding SeccompDefault feature gate to be enabled as well.
Default: false</p>
</td>
</tr>
<tr><td><code>memoryThrottlingFactor</code><br/>
<code>float64</code>
</td>
<td>
   <p>MemoryThrottlingFactor specifies the factor multiplied by the memory limit or node allocatable memory
when setting the cgroupv2 memory.high value to enforce MemoryQoS.
Decreasing this factor will set lower high limit for container cgroups and put heavier reclaim pressure
while increasing will put less reclaim pressure.
See http://kep.k8s.io/2570 for more details.
Default: 0.8</p>
</td>
</tr>
<tr><td><code>registerWithTaints</code><br/>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.23/#taint-v1-core"><code>[]core/v1.Taint</code></a>
</td>
<td>
   <p>registerWithTaints are an array of taints to add to a node object when
the kubelet registers itself. This only takes effect when registerNode
is true and upon the initial registration of the node.
Default: nil</p>
</td>
</tr>
<tr><td><code>registerNode</code><br/>
<code>bool</code>
</td>
<td>
   <p>registerNode enables automatic registration with the apiserver.
Default: true</p>
</td>
</tr>
</tbody>
</table>

## `SerializedNodeConfigSource`     {#kubelet-config-k8s-io-v1beta1-SerializedNodeConfigSource}
    


<p>SerializedNodeConfigSource allows us to serialize v1.NodeConfigSource.
This type is used internally by the Kubelet for tracking checkpointed dynamic configs.
It exists in the kubeletconfig API group because it is classified as a versioned input to the Kubelet.</p>


<table class="table">
<thead><tr><th width="30%">Field</th><th>Description</th></tr></thead>
<tbody>
    
<tr><td><code>apiVersion</code><br/>string</td><td><code>kubelet.config.k8s.io/v1beta1</code></td></tr>
<tr><td><code>kind</code><br/>string</td><td><code>SerializedNodeConfigSource</code></td></tr>
    
  
<tr><td><code>source</code><br/>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.23/#nodeconfigsource-v1-core"><code>core/v1.NodeConfigSource</code></a>
</td>
<td>
   <p>source is the source that we are serializing.</p>
</td>
</tr>
</tbody>
</table>

## `KubeletAnonymousAuthentication`     {#kubelet-config-k8s-io-v1beta1-KubeletAnonymousAuthentication}
    

**Appears in:**

- [KubeletAuthentication](#kubelet-config-k8s-io-v1beta1-KubeletAuthentication)



<table class="table">
<thead><tr><th width="30%">Field</th><th>Description</th></tr></thead>
<tbody>
    
  
<tr><td><code>enabled</code><br/>
<code>bool</code>
</td>
<td>
   <p>enabled allows anonymous requests to the kubelet server.
Requests that are not rejected by another authentication method are treated as
anonymous requests.
Anonymous requests have a username of <code>system:anonymous</code>, and a group name of
<code>system:unauthenticated</code>.</p>
</td>
</tr>
</tbody>
</table>

## `KubeletAuthentication`     {#kubelet-config-k8s-io-v1beta1-KubeletAuthentication}
    

**Appears in:**

- [KubeletConfiguration](#kubelet-config-k8s-io-v1beta1-KubeletConfiguration)



<table class="table">
<thead><tr><th width="30%">Field</th><th>Description</th></tr></thead>
<tbody>
    
  
<tr><td><code>x509</code><br/>
<a href="#kubelet-config-k8s-io-v1beta1-KubeletX509Authentication"><code>KubeletX509Authentication</code></a>
</td>
<td>
   <p>x509 contains settings related to x509 client certificate authentication.</p>
</td>
</tr>
<tr><td><code>webhook</code><br/>
<a href="#kubelet-config-k8s-io-v1beta1-KubeletWebhookAuthentication"><code>KubeletWebhookAuthentication</code></a>
</td>
<td>
   <p>webhook contains settings related to webhook bearer token authentication.</p>
</td>
</tr>
<tr><td><code>anonymous</code><br/>
<a href="#kubelet-config-k8s-io-v1beta1-KubeletAnonymousAuthentication"><code>KubeletAnonymousAuthentication</code></a>
</td>
<td>
   <p>anonymous contains settings related to anonymous authentication.</p>
</td>
</tr>
</tbody>
</table>

## `KubeletAuthorization`     {#kubelet-config-k8s-io-v1beta1-KubeletAuthorization}
    

**Appears in:**

- [KubeletConfiguration](#kubelet-config-k8s-io-v1beta1-KubeletConfiguration)



<table class="table">
<thead><tr><th width="30%">Field</th><th>Description</th></tr></thead>
<tbody>
    
  
<tr><td><code>mode</code><br/>
<a href="#kubelet-config-k8s-io-v1beta1-KubeletAuthorizationMode"><code>KubeletAuthorizationMode</code></a>
</td>
<td>
   <p>mode is the authorization mode to apply to requests to the kubelet server.
Valid values are <code>AlwaysAllow</code> and <code>Webhook</code>.
Webhook mode uses the SubjectAccessReview API to determine authorization.</p>
</td>
</tr>
<tr><td><code>webhook</code><br/>
<a href="#kubelet-config-k8s-io-v1beta1-KubeletWebhookAuthorization"><code>KubeletWebhookAuthorization</code></a>
</td>
<td>
   <p>webhook contains settings related to Webhook authorization.</p>
</td>
</tr>
</tbody>
</table>

## `KubeletAuthorizationMode`     {#kubelet-config-k8s-io-v1beta1-KubeletAuthorizationMode}
    
(Alias of `string`)

**Appears in:**

- [KubeletAuthorization](#kubelet-config-k8s-io-v1beta1-KubeletAuthorization)





## `KubeletWebhookAuthentication`     {#kubelet-config-k8s-io-v1beta1-KubeletWebhookAuthentication}
    

**Appears in:**

- [KubeletAuthentication](#kubelet-config-k8s-io-v1beta1-KubeletAuthentication)



<table class="table">
<thead><tr><th width="30%">Field</th><th>Description</th></tr></thead>
<tbody>
    
  
<tr><td><code>enabled</code><br/>
<code>bool</code>
</td>
<td>
   <p>enabled allows bearer token authentication backed by the
tokenreviews.authentication.k8s.io API.</p>
</td>
</tr>
<tr><td><code>cacheTTL</code><br/>
<a href="https://pkg.go.dev/k8s.io/apimachinery/pkg/apis/meta/v1#Duration"><code>meta/v1.Duration</code></a>
</td>
<td>
   <p>cacheTTL enables caching of authentication results</p>
</td>
</tr>
</tbody>
</table>

## `KubeletWebhookAuthorization`     {#kubelet-config-k8s-io-v1beta1-KubeletWebhookAuthorization}
    

**Appears in:**

- [KubeletAuthorization](#kubelet-config-k8s-io-v1beta1-KubeletAuthorization)



<table class="table">
<thead><tr><th width="30%">Field</th><th>Description</th></tr></thead>
<tbody>
    
  
<tr><td><code>cacheAuthorizedTTL</code><br/>
<a href="https://pkg.go.dev/k8s.io/apimachinery/pkg/apis/meta/v1#Duration"><code>meta/v1.Duration</code></a>
</td>
<td>
   <p>cacheAuthorizedTTL is the duration to cache 'authorized' responses from the
webhook authorizer.</p>
</td>
</tr>
<tr><td><code>cacheUnauthorizedTTL</code><br/>
<a href="https://pkg.go.dev/k8s.io/apimachinery/pkg/apis/meta/v1#Duration"><code>meta/v1.Duration</code></a>
</td>
<td>
   <p>cacheUnauthorizedTTL is the duration to cache 'unauthorized' responses from
the webhook authorizer.</p>
</td>
</tr>
</tbody>
</table>

## `KubeletX509Authentication`     {#kubelet-config-k8s-io-v1beta1-KubeletX509Authentication}
    

**Appears in:**

- [KubeletAuthentication](#kubelet-config-k8s-io-v1beta1-KubeletAuthentication)



<table class="table">
<thead><tr><th width="30%">Field</th><th>Description</th></tr></thead>
<tbody>
    
  
<tr><td><code>clientCAFile</code><br/>
<code>string</code>
</td>
<td>
   <p>clientCAFile is the path to a PEM-encoded certificate bundle. If set, any request
presenting a client certificate signed by one of the authorities in the bundle
is authenticated with a username corresponding to the CommonName,
and groups corresponding to the Organization in the client certificate.</p>
</td>
</tr>
</tbody>
</table>

## `MemoryReservation`     {#kubelet-config-k8s-io-v1beta1-MemoryReservation}
    

**Appears in:**

- [KubeletConfiguration](#kubelet-config-k8s-io-v1beta1-KubeletConfiguration)


<p>MemoryReservation specifies the memory reservation of different types for each NUMA node</p>


<table class="table">
<thead><tr><th width="30%">Field</th><th>Description</th></tr></thead>
<tbody>
    
  
<tr><td><code>numaNode</code> <B>[Required]</B><br/>
<code>int32</code>
</td>
<td>
   <span class="text-muted">No description provided.</span></td>
</tr>
<tr><td><code>limits</code> <B>[Required]</B><br/>
<a href="https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.23/#resourcelist-v1-core"><code>core/v1.ResourceList</code></a>
</td>
<td>
   <span class="text-muted">No description provided.</span></td>
</tr>
</tbody>
</table>

## `MemorySwapConfiguration`     {#kubelet-config-k8s-io-v1beta1-MemorySwapConfiguration}
    

**Appears in:**

- [KubeletConfiguration](#kubelet-config-k8s-io-v1beta1-KubeletConfiguration)



<table class="table">
<thead><tr><th width="30%">Field</th><th>Description</th></tr></thead>
<tbody>
    
  
<tr><td><code>swapBehavior</code><br/>
<code>string</code>
</td>
<td>
   <p>swapBehavior configures swap memory available to container workloads. May be one of
&quot;&quot;, &quot;LimitedSwap&quot;: workload combined memory and swap usage cannot exceed pod memory limit
&quot;UnlimitedSwap&quot;: workloads can use unlimited swap, up to the allocatable limit.</p>
</td>
</tr>
</tbody>
</table>

## `ResourceChangeDetectionStrategy`     {#kubelet-config-k8s-io-v1beta1-ResourceChangeDetectionStrategy}
    
(Alias of `string`)

**Appears in:**

- [KubeletConfiguration](#kubelet-config-k8s-io-v1beta1-KubeletConfiguration)


<p>ResourceChangeDetectionStrategy denotes a mode in which internal
managers (secret, configmap) are discovering object changes.</p>




## `ShutdownGracePeriodByPodPriority`     {#kubelet-config-k8s-io-v1beta1-ShutdownGracePeriodByPodPriority}
    

**Appears in:**

- [KubeletConfiguration](#kubelet-config-k8s-io-v1beta1-KubeletConfiguration)


<p>ShutdownGracePeriodByPodPriority specifies the shutdown grace period for Pods based on their associated priority class value</p>


<table class="table">
<thead><tr><th width="30%">Field</th><th>Description</th></tr></thead>
<tbody>
    
  
<tr><td><code>priority</code> <B>[Required]</B><br/>
<code>int32</code>
</td>
<td>
   <p>priority is the priority value associated with the shutdown grace period</p>
</td>
</tr>
<tr><td><code>shutdownGracePeriodSeconds</code> <B>[Required]</B><br/>
<code>int64</code>
</td>
<td>
   <p>shutdownGracePeriodSeconds is the shutdown grace period in seconds</p>
</td>
</tr>
</tbody>
</table>
  
  
    

## `FormatOptions`     {#FormatOptions}
    

**Appears in:**

- [LoggingConfiguration](#LoggingConfiguration)


<p>FormatOptions contains options for the different logging formats.</p>


<table class="table">
<thead><tr><th width="30%">Field</th><th>Description</th></tr></thead>
<tbody>
    
  
<tr><td><code>json</code> <B>[Required]</B><br/>
<a href="#JSONOptions"><code>JSONOptions</code></a>
</td>
<td>
   <p>[Experimental] JSON contains options for logging format &quot;json&quot;.</p>
</td>
</tr>
</tbody>
</table>

## `JSONOptions`     {#JSONOptions}
    

**Appears in:**

- [FormatOptions](#FormatOptions)


<p>JSONOptions contains options for logging format &quot;json&quot;.</p>


<table class="table">
<thead><tr><th width="30%">Field</th><th>Description</th></tr></thead>
<tbody>
    
  
<tr><td><code>splitStream</code> <B>[Required]</B><br/>
<code>bool</code>
</td>
<td>
   <p>[Experimental] SplitStream redirects error messages to stderr while
info messages go to stdout, with buffering. The default is to write
both to stdout, without buffering.</p>
</td>
</tr>
<tr><td><code>infoBufferSize</code> <B>[Required]</B><br/>
<a href="https://pkg.go.dev/k8s.io/apimachinery/pkg/api/resource#QuantityValue"><code>k8s.io/apimachinery/pkg/api/resource.QuantityValue</code></a>
</td>
<td>
   <p>[Experimental] InfoBufferSize sets the size of the info stream when
using split streams. The default is zero, which disables buffering.</p>
</td>
</tr>
</tbody>
</table>

## `LoggingConfiguration`     {#LoggingConfiguration}
    

**Appears in:**

- [KubeletConfiguration](#kubelet-config-k8s-io-v1beta1-KubeletConfiguration)


<p>LoggingConfiguration contains logging options
Refer <a href="https://github.com/kubernetes/component-base/blob/master/logs/options.go">Logs Options</a> for more information.</p>


<table class="table">
<thead><tr><th width="30%">Field</th><th>Description</th></tr></thead>
<tbody>
    
  
<tr><td><code>format</code> <B>[Required]</B><br/>
<code>string</code>
</td>
<td>
   <p>Format Flag specifies the structure of log messages.
default value of format is <code>text</code></p>
</td>
</tr>
<tr><td><code>flushFrequency</code> <B>[Required]</B><br/>
<a href="https://pkg.go.dev/time#Duration"><code>time.Duration</code></a>
</td>
<td>
   <p>Maximum number of seconds between log flushes. Ignored if the
selected logging backend writes log messages without buffering.</p>
</td>
</tr>
<tr><td><code>verbosity</code> <B>[Required]</B><br/>
<code>uint32</code>
</td>
<td>
   <p>Verbosity is the threshold that determines which log messages are
logged. Default is zero which logs only the most important
messages. Higher values enable additional messages. Error messages
are always logged.</p>
</td>
</tr>
<tr><td><code>vmodule</code> <B>[Required]</B><br/>
<a href="#VModuleConfiguration"><code>VModuleConfiguration</code></a>
</td>
<td>
   <p>VModule overrides the verbosity threshold for individual files.
Only supported for &quot;text&quot; log format.</p>
</td>
</tr>
<tr><td><code>sanitization</code> <B>[Required]</B><br/>
<code>bool</code>
</td>
<td>
   <p>[Experimental] When enabled prevents logging of fields tagged as sensitive (passwords, keys, tokens).
Runtime log sanitization may introduce significant computation overhead and therefore should not be enabled in production.`)</p>
</td>
</tr>
<tr><td><code>options</code> <B>[Required]</B><br/>
<a href="#FormatOptions"><code>FormatOptions</code></a>
</td>
<td>
   <p>[Experimental] Options holds additional parameters that are specific
to the different logging formats. Only the options for the selected
format get used, but all of them get validated.</p>
</td>
</tr>
</tbody>
</table>

## `VModuleConfiguration`     {#VModuleConfiguration}
    
(Alias of `[]k8s.io/component-base/config/v1alpha1.VModuleItem`)

**Appears in:**

- [LoggingConfiguration](#LoggingConfiguration)


<p>VModuleConfiguration is a collection of individual file names or patterns
and the corresponding verbosity threshold.</p>



