pilot-agent
=====================

---
WARNING: THIS IS AN AUTO-GENERATED FILE, DO NOT EDIT. PLEASE MODIFY THE ORIGINAL SOURCE IN THE 'https://github.com/istio/istio' REPO
source_repo: https://github.com/istio/istio
title: pilot-agent
description: Istio Pilot agent.
generator: pkg-collateral-docs
number_of_entries: 5
max_toc_level: 2
remove_toc_prefix: 'pilot-agent '
---
<p>Istio Pilot agent runs in the sidecar or gateway container and bootstraps Envoy.</p>
<table class="command-flags">
<thead>
<tr>
<th>Flags</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>--log_as_json</code></td>
<td>Whether to format output as JSON or in plain console-friendly format </td>
</tr>
<tr>
<td><code>--log_caller &lt;string&gt;</code></td>
<td>Comma-separated list of scopes for which to include caller information, scopes can be any of [all, authn, cache, citadelclient, configmapcontroller, default, googleca, model, rbac, sds, secretfetcher, stsclient, stsserver, token, validation, vault]  (default ``)</td>
</tr>
<tr>
<td><code>--log_output_level &lt;string&gt;</code></td>
<td>Comma-separated minimum per-scope logging level of messages to output, in the form of &lt;scope&gt;:&lt;level&gt;,&lt;scope&gt;:&lt;level&gt;,... where scope can be one of [all, authn, cache, citadelclient, configmapcontroller, default, googleca, model, rbac, sds, secretfetcher, stsclient, stsserver, token, validation, vault] and level can be one of [debug, info, warn, error, fatal, none]  (default `default:info`)</td>
</tr>
<tr>
<td><code>--log_rotate &lt;string&gt;</code></td>
<td>The path for the optional rotating log file  (default ``)</td>
</tr>
<tr>
<td><code>--log_rotate_max_age &lt;int&gt;</code></td>
<td>The maximum age in days of a log file beyond which the file is rotated (0 indicates no limit)  (default `30`)</td>
</tr>
<tr>
<td><code>--log_rotate_max_backups &lt;int&gt;</code></td>
<td>The maximum number of log file backups to keep before older files are deleted (0 indicates no limit)  (default `1000`)</td>
</tr>
<tr>
<td><code>--log_rotate_max_size &lt;int&gt;</code></td>
<td>The maximum size in megabytes of a log file beyond which the file is rotated  (default `104857600`)</td>
</tr>
<tr>
<td><code>--log_stacktrace_level &lt;string&gt;</code></td>
<td>Comma-separated minimum per-scope logging level at which stack traces are captured, in the form of &lt;scope&gt;:&lt;level&gt;,&lt;scope:level&gt;,... where scope can be one of [all, authn, cache, citadelclient, configmapcontroller, default, googleca, model, rbac, sds, secretfetcher, stsclient, stsserver, token, validation, vault] and level can be one of [debug, info, warn, error, fatal, none]  (default `default:none`)</td>
</tr>
<tr>
<td><code>--log_target &lt;stringArray&gt;</code></td>
<td>The set of paths where to output the log. This can be any path as well as the special values stdout and stderr  (default `[stdout]`)</td>
</tr>
</tbody>
</table>
<h2 id="pilot-agent-proxy">pilot-agent proxy</h2>
<p>Envoy proxy agent</p>
<pre class="language-bash"><code>pilot-agent proxy [flags]
</code></pre>
<table class="command-flags">
<thead>
<tr>
<th>Flags</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>--binaryPath &lt;string&gt;</code></td>
<td>Path to the proxy binary  (default `/usr/local/bin/envoy`)</td>
</tr>
<tr>
<td><code>--concurrency &lt;int&gt;</code></td>
<td>number of worker threads to run  (default `0`)</td>
</tr>
<tr>
<td><code>--configPath &lt;string&gt;</code></td>
<td>Path to the generated configuration file directory  (default `/etc/istio/proxy`)</td>
</tr>
<tr>
<td><code>--connectTimeout &lt;duration&gt;</code></td>
<td>Connection timeout used by Envoy for supporting services  (default `10s`)</td>
</tr>
<tr>
<td><code>--controlPlaneAuthPolicy &lt;string&gt;</code></td>
<td>Control Plane Authentication Policy  (default `NONE`)</td>
</tr>
<tr>
<td><code>--controlPlaneBootstrap</code></td>
<td>Process bootstrap provided via templateFile to be used by control plane components. </td>
</tr>
<tr>
<td><code>--customConfigFile &lt;string&gt;</code></td>
<td>Path to the custom configuration file  (default ``)</td>
</tr>
<tr>
<td><code>--datadogAgentAddress &lt;string&gt;</code></td>
<td>Address of the Datadog Agent  (default ``)</td>
</tr>
<tr>
<td><code>--disableInternalTelemetry</code></td>
<td>Disable internal telemetry </td>
</tr>
<tr>
<td><code>--discoveryAddress &lt;string&gt;</code></td>
<td>Address of the discovery service exposing xDS (e.g. istio-pilot:8080)  (default `istio-pilot:15010`)</td>
</tr>
<tr>
<td><code>--dnsRefreshRate &lt;string&gt;</code></td>
<td>The dns_refresh_rate for bootstrap STRICT_DNS clusters  (default `300s`)</td>
</tr>
<tr>
<td><code>--domain &lt;string&gt;</code></td>
<td>DNS domain suffix. If not provided uses ${POD_NAMESPACE}.svc.cluster.local  (default ``)</td>
</tr>
<tr>
<td><code>--drainDuration &lt;duration&gt;</code></td>
<td>The time in seconds that Envoy will drain connections during a hot restart  (default `45s`)</td>
</tr>
<tr>
<td><code>--envoyAccessLogService &lt;string&gt;</code></td>
<td>Settings of an Envoy gRPC Access Log Service API implementation  (default ``)</td>
</tr>
<tr>
<td><code>--envoyMetricsService &lt;string&gt;</code></td>
<td>Settings of an Envoy gRPC Metrics Service API implementation  (default ``)</td>
</tr>
<tr>
<td><code>--id &lt;string&gt;</code></td>
<td>Proxy unique ID. If not provided uses ${POD_NAME}.${POD_NAMESPACE} from environment variables  (default ``)</td>
</tr>
<tr>
<td><code>--ip &lt;string&gt;</code></td>
<td>Proxy IP address. If not provided uses ${INSTANCE_IP} environment variable.  (default ``)</td>
</tr>
<tr>
<td><code>--lightstepAccessToken &lt;string&gt;</code></td>
<td>Access Token for LightStep Satellite pool  (default ``)</td>
</tr>
<tr>
<td><code>--lightstepAddress &lt;string&gt;</code></td>
<td>Address of the LightStep Satellite pool  (default ``)</td>
</tr>
<tr>
<td><code>--lightstepCacertPath &lt;string&gt;</code></td>
<td>Path to the trusted cacert used to authenticate the pool  (default ``)</td>
</tr>
<tr>
<td><code>--lightstepSecure</code></td>
<td>Should connection to the LightStep Satellite pool be secure </td>
</tr>
<tr>
<td><code>--log_as_json</code></td>
<td>Whether to format output as JSON or in plain console-friendly format </td>
</tr>
<tr>
<td><code>--log_caller &lt;string&gt;</code></td>
<td>Comma-separated list of scopes for which to include caller information, scopes can be any of [all, authn, cache, citadelclient, configmapcontroller, default, googleca, model, rbac, sds, secretfetcher, stsclient, stsserver, token, validation, vault]  (default ``)</td>
</tr>
<tr>
<td><code>--log_output_level &lt;string&gt;</code></td>
<td>Comma-separated minimum per-scope logging level of messages to output, in the form of &lt;scope&gt;:&lt;level&gt;,&lt;scope&gt;:&lt;level&gt;,... where scope can be one of [all, authn, cache, citadelclient, configmapcontroller, default, googleca, model, rbac, sds, secretfetcher, stsclient, stsserver, token, validation, vault] and level can be one of [debug, info, warn, error, fatal, none]  (default `default:info`)</td>
</tr>
<tr>
<td><code>--log_rotate &lt;string&gt;</code></td>
<td>The path for the optional rotating log file  (default ``)</td>
</tr>
<tr>
<td><code>--log_rotate_max_age &lt;int&gt;</code></td>
<td>The maximum age in days of a log file beyond which the file is rotated (0 indicates no limit)  (default `30`)</td>
</tr>
<tr>
<td><code>--log_rotate_max_backups &lt;int&gt;</code></td>
<td>The maximum number of log file backups to keep before older files are deleted (0 indicates no limit)  (default `1000`)</td>
</tr>
<tr>
<td><code>--log_rotate_max_size &lt;int&gt;</code></td>
<td>The maximum size in megabytes of a log file beyond which the file is rotated  (default `104857600`)</td>
</tr>
<tr>
<td><code>--log_stacktrace_level &lt;string&gt;</code></td>
<td>Comma-separated minimum per-scope logging level at which stack traces are captured, in the form of &lt;scope&gt;:&lt;level&gt;,&lt;scope:level&gt;,... where scope can be one of [all, authn, cache, citadelclient, configmapcontroller, default, googleca, model, rbac, sds, secretfetcher, stsclient, stsserver, token, validation, vault] and level can be one of [debug, info, warn, error, fatal, none]  (default `default:none`)</td>
</tr>
<tr>
<td><code>--log_target &lt;stringArray&gt;</code></td>
<td>The set of paths where to output the log. This can be any path as well as the special values stdout and stderr  (default `[stdout]`)</td>
</tr>
<tr>
<td><code>--mixerIdentity &lt;string&gt;</code></td>
<td>The identity used as the suffix for mixer&#39;s spiffe SAN. This would only be used by pilot all other proxy would get this value from pilot  (default ``)</td>
</tr>
<tr>
<td><code>--outlierLogPath &lt;string&gt;</code></td>
<td>The log path for outlier detection  (default ``)</td>
</tr>
<tr>
<td><code>--parentShutdownDuration &lt;duration&gt;</code></td>
<td>The time in seconds that Envoy will wait before shutting down the parent process during a hot restart  (default `1m0s`)</td>
</tr>
<tr>
<td><code>--pilotIdentity &lt;string&gt;</code></td>
<td>The identity used as the suffix for pilot&#39;s spiffe SAN   (default ``)</td>
</tr>
<tr>
<td><code>--proxyAdminPort &lt;uint16&gt;</code></td>
<td>Port on which Envoy should listen for administrative commands  (default `15000`)</td>
</tr>
<tr>
<td><code>--proxyComponentLogLevel &lt;string&gt;</code></td>
<td>The component log level used to start the Envoy proxy  (default `misc:error`)</td>
</tr>
<tr>
<td><code>--proxyLogLevel &lt;string&gt;</code></td>
<td>The log level used to start the Envoy proxy (choose from {trace, debug, info, warning, error, critical, off})  (default `warning`)</td>
</tr>
<tr>
<td><code>--serviceCluster &lt;string&gt;</code></td>
<td>Service cluster  (default `istio-proxy`)</td>
</tr>
<tr>
<td><code>--serviceregistry &lt;string&gt;</code></td>
<td>Select the platform for service registry, options are {Kubernetes, Consul, Mock}  (default `Kubernetes`)</td>
</tr>
<tr>
<td><code>--statsdUdpAddress &lt;string&gt;</code></td>
<td>IP Address and Port of a statsd UDP listener (e.g. 10.75.241.127:9125)  (default ``)</td>
</tr>
<tr>
<td><code>--statusPort &lt;uint16&gt;</code></td>
<td>HTTP Port on which to serve pilot agent status. If zero, agent status will not be provided.  (default `0`)</td>
</tr>
<tr>
<td><code>--stsPort &lt;int&gt;</code></td>
<td>HTTP Port on which to serve Security Token Service (STS). If zero, STS service will not be provided.  (default `0`)</td>
</tr>
<tr>
<td><code>--templateFile &lt;string&gt;</code></td>
<td>Go template bootstrap config  (default ``)</td>
</tr>
<tr>
<td><code>--tokenManagerPlugin &lt;string&gt;</code></td>
<td>Token provider specific plugin name.  (default `GoogleTokenExchange`)</td>
</tr>
<tr>
<td><code>--trust-domain &lt;string&gt;</code></td>
<td>The domain to use for identities  (default ``)</td>
</tr>
<tr>
<td><code>--zipkinAddress &lt;string&gt;</code></td>
<td>Address of the Zipkin service (e.g. zipkin:9411)  (default ``)</td>
</tr>
</tbody>
</table>
<h2 id="pilot-agent-request">pilot-agent request</h2>
<p>Makes an HTTP request to the Envoy admin API</p>
<pre class="language-bash"><code>pilot-agent request &lt;method&gt; &lt;path&gt; [&lt;body&gt;] [flags]
</code></pre>
<table class="command-flags">
<thead>
<tr>
<th>Flags</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>--log_as_json</code></td>
<td>Whether to format output as JSON or in plain console-friendly format </td>
</tr>
<tr>
<td><code>--log_caller &lt;string&gt;</code></td>
<td>Comma-separated list of scopes for which to include caller information, scopes can be any of [all, authn, cache, citadelclient, configmapcontroller, default, googleca, model, rbac, sds, secretfetcher, stsclient, stsserver, token, validation, vault]  (default ``)</td>
</tr>
<tr>
<td><code>--log_output_level &lt;string&gt;</code></td>
<td>Comma-separated minimum per-scope logging level of messages to output, in the form of &lt;scope&gt;:&lt;level&gt;,&lt;scope&gt;:&lt;level&gt;,... where scope can be one of [all, authn, cache, citadelclient, configmapcontroller, default, googleca, model, rbac, sds, secretfetcher, stsclient, stsserver, token, validation, vault] and level can be one of [debug, info, warn, error, fatal, none]  (default `default:info`)</td>
</tr>
<tr>
<td><code>--log_rotate &lt;string&gt;</code></td>
<td>The path for the optional rotating log file  (default ``)</td>
</tr>
<tr>
<td><code>--log_rotate_max_age &lt;int&gt;</code></td>
<td>The maximum age in days of a log file beyond which the file is rotated (0 indicates no limit)  (default `30`)</td>
</tr>
<tr>
<td><code>--log_rotate_max_backups &lt;int&gt;</code></td>
<td>The maximum number of log file backups to keep before older files are deleted (0 indicates no limit)  (default `1000`)</td>
</tr>
<tr>
<td><code>--log_rotate_max_size &lt;int&gt;</code></td>
<td>The maximum size in megabytes of a log file beyond which the file is rotated  (default `104857600`)</td>
</tr>
<tr>
<td><code>--log_stacktrace_level &lt;string&gt;</code></td>
<td>Comma-separated minimum per-scope logging level at which stack traces are captured, in the form of &lt;scope&gt;:&lt;level&gt;,&lt;scope:level&gt;,... where scope can be one of [all, authn, cache, citadelclient, configmapcontroller, default, googleca, model, rbac, sds, secretfetcher, stsclient, stsserver, token, validation, vault] and level can be one of [debug, info, warn, error, fatal, none]  (default `default:none`)</td>
</tr>
<tr>
<td><code>--log_target &lt;stringArray&gt;</code></td>
<td>The set of paths where to output the log. This can be any path as well as the special values stdout and stderr  (default `[stdout]`)</td>
</tr>
</tbody>
</table>
<h2 id="pilot-agent-version">pilot-agent version</h2>
<p>Prints out build version information</p>
<pre class="language-bash"><code>pilot-agent version [flags]
</code></pre>
<table class="command-flags">
<thead>
<tr>
<th>Flags</th>
<th>Shorthand</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>--log_as_json</code></td>
<td></td>
<td>Whether to format output as JSON or in plain console-friendly format </td>
</tr>
<tr>
<td><code>--log_caller &lt;string&gt;</code></td>
<td></td>
<td>Comma-separated list of scopes for which to include caller information, scopes can be any of [all, authn, cache, citadelclient, configmapcontroller, default, googleca, model, rbac, sds, secretfetcher, stsclient, stsserver, token, validation, vault]  (default ``)</td>
</tr>
<tr>
<td><code>--log_output_level &lt;string&gt;</code></td>
<td></td>
<td>Comma-separated minimum per-scope logging level of messages to output, in the form of &lt;scope&gt;:&lt;level&gt;,&lt;scope&gt;:&lt;level&gt;,... where scope can be one of [all, authn, cache, citadelclient, configmapcontroller, default, googleca, model, rbac, sds, secretfetcher, stsclient, stsserver, token, validation, vault] and level can be one of [debug, info, warn, error, fatal, none]  (default `default:info`)</td>
</tr>
<tr>
<td><code>--log_rotate &lt;string&gt;</code></td>
<td></td>
<td>The path for the optional rotating log file  (default ``)</td>
</tr>
<tr>
<td><code>--log_rotate_max_age &lt;int&gt;</code></td>
<td></td>
<td>The maximum age in days of a log file beyond which the file is rotated (0 indicates no limit)  (default `30`)</td>
</tr>
<tr>
<td><code>--log_rotate_max_backups &lt;int&gt;</code></td>
<td></td>
<td>The maximum number of log file backups to keep before older files are deleted (0 indicates no limit)  (default `1000`)</td>
</tr>
<tr>
<td><code>--log_rotate_max_size &lt;int&gt;</code></td>
<td></td>
<td>The maximum size in megabytes of a log file beyond which the file is rotated  (default `104857600`)</td>
</tr>
<tr>
<td><code>--log_stacktrace_level &lt;string&gt;</code></td>
<td></td>
<td>Comma-separated minimum per-scope logging level at which stack traces are captured, in the form of &lt;scope&gt;:&lt;level&gt;,&lt;scope:level&gt;,... where scope can be one of [all, authn, cache, citadelclient, configmapcontroller, default, googleca, model, rbac, sds, secretfetcher, stsclient, stsserver, token, validation, vault] and level can be one of [debug, info, warn, error, fatal, none]  (default `default:none`)</td>
</tr>
<tr>
<td><code>--log_target &lt;stringArray&gt;</code></td>
<td></td>
<td>The set of paths where to output the log. This can be any path as well as the special values stdout and stderr  (default `[stdout]`)</td>
</tr>
<tr>
<td><code>--output &lt;string&gt;</code></td>
<td><code>-o</code></td>
<td>One of &#39;yaml&#39; or &#39;json&#39;.  (default ``)</td>
</tr>
<tr>
<td><code>--short</code></td>
<td><code>-s</code></td>
<td>Use --short=false to generate full version information </td>
</tr>
</tbody>
</table>
<h2 id="envvars">Environment variables</h2>
These environment variables affect the behavior of the <code>pilot-agent</code> command.
<table class="envvars">
<thead>
<tr>
<th>Variable Name</th>
<th>Type</th>
<th>Default Value</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>CA_ADDR</code></td>
<td>String</td>
<td><code></code></td>
<td></td>
</tr>
<tr>
<td><code>CA_PROVIDER</code></td>
<td>String</td>
<td><code>Citadel</code></td>
<td></td>
</tr>
<tr>
<td><code>ENABLE_INGRESS_GATEWAY_SDS</code></td>
<td>Boolean</td>
<td><code>false</code></td>
<td></td>
</tr>
<tr>
<td><code>GKE_CLUSTER_URL</code></td>
<td>String</td>
<td><code></code></td>
<td>The url of GKE cluster</td>
</tr>
<tr>
<td><code>INGRESS_GATEWAY_FALLBACK_SECRET</code></td>
<td>String</td>
<td><code>gateway-fallback</code></td>
<td></td>
</tr>
<tr>
<td><code>INGRESS_GATEWAY_NAMESPACE</code></td>
<td>String</td>
<td><code></code></td>
<td></td>
</tr>
<tr>
<td><code>INITIAL_BACKOFF_MSEC</code></td>
<td>Integer</td>
<td><code>0</code></td>
<td></td>
</tr>
<tr>
<td><code>INSTANCE_IP</code></td>
<td>String</td>
<td><code></code></td>
<td></td>
</tr>
<tr>
<td><code>ISTIOD_ADDR</code></td>
<td>String</td>
<td><code></code></td>
<td>Service name of istiod. If empty the istiod listener, certs will be disabled.</td>
</tr>
<tr>
<td><code>ISTIO_AUTO_MTLS_ENABLED</code></td>
<td>Boolean</td>
<td><code>false</code></td>
<td>If true, auto mTLS is enabled, sidecar checks key/cert if SDS is not enabled.</td>
</tr>
<tr>
<td><code>ISTIO_BOOTSTRAP</code></td>
<td>String</td>
<td><code></code></td>
<td></td>
</tr>
<tr>
<td><code>ISTIO_BOOTSTRAP_OVERRIDE</code></td>
<td>String</td>
<td><code></code></td>
<td></td>
</tr>
<tr>
<td><code>ISTIO_GPRC_MAXRECVMSGSIZE</code></td>
<td>Integer</td>
<td><code>4194304</code></td>
<td>Sets the max receive buffer size of gRPC stream in bytes.</td>
</tr>
<tr>
<td><code>ISTIO_GPRC_MAXSTREAMS</code></td>
<td>Integer</td>
<td><code>100000</code></td>
<td>Sets the maximum number of concurrent grpc streams.</td>
</tr>
<tr>
<td><code>ISTIO_KUBE_APP_PROBERS</code></td>
<td>String</td>
<td><code></code></td>
<td></td>
</tr>
<tr>
<td><code>ISTIO_META_TLS_CLIENT_CERT_CHAIN</code></td>
<td>String</td>
<td><code>/etc/certs/cert-chain.pem</code></td>
<td></td>
</tr>
<tr>
<td><code>ISTIO_META_TLS_CLIENT_KEY</code></td>
<td>String</td>
<td><code>/etc/certs/key.pem</code></td>
<td></td>
</tr>
<tr>
<td><code>ISTIO_META_TLS_CLIENT_ROOT_CERT</code></td>
<td>String</td>
<td><code>/etc/certs/root-cert.pem</code></td>
<td></td>
</tr>
<tr>
<td><code>ISTIO_META_TLS_SERVER_CERT_CHAIN</code></td>
<td>String</td>
<td><code>/etc/certs/cert-chain.pem</code></td>
<td></td>
</tr>
<tr>
<td><code>ISTIO_META_TLS_SERVER_KEY</code></td>
<td>String</td>
<td><code>/etc/certs/key.pem</code></td>
<td></td>
</tr>
<tr>
<td><code>ISTIO_META_TLS_SERVER_ROOT_CERT</code></td>
<td>String</td>
<td><code>/etc/certs/root-cert.pem</code></td>
<td></td>
</tr>
<tr>
<td><code>ISTIO_NAMESPACE</code></td>
<td>String</td>
<td><code></code></td>
<td></td>
</tr>
<tr>
<td><code>JWT_POLICY</code></td>
<td>String</td>
<td><code>third-party-jwt</code></td>
<td>The JWT validation policy.</td>
</tr>
<tr>
<td><code>MESH_CONFIG</code></td>
<td>String</td>
<td><code></code></td>
<td>The mesh configuration</td>
</tr>
<tr>
<td><code>NAMESPACE</code></td>
<td>String</td>
<td><code>istio-system</code></td>
<td>namespace that nodeagent/citadel run in</td>
</tr>
<tr>
<td><code>OUTPUT_KEY_CERT_TO_DIRECTORY</code></td>
<td>String</td>
<td><code></code></td>
<td>The output directory for the key and certificate. If empty, no output of key and certificate.</td>
</tr>
<tr>
<td><code>PILOT_BLOCK_HTTP_ON_443</code></td>
<td>Boolean</td>
<td><code>true</code></td>
<td>If enabled, any HTTP services will be blocked on HTTPS port (443). If this is disabled, any HTTP service on port 443 could block all external traffic</td>
</tr>
<tr>
<td><code>PILOT_CERT_DIR</code></td>
<td>String</td>
<td><code></code></td>
<td></td>
</tr>
<tr>
<td><code>PILOT_CERT_PROVIDER</code></td>
<td>String</td>
<td><code>citadel</code></td>
<td>the provider of Pilot DNS certificate.</td>
</tr>
<tr>
<td><code>PILOT_DEBOUNCE_AFTER</code></td>
<td>Time Duration</td>
<td><code>100ms</code></td>
<td>The delay added to config/registry events for debouncing. This will delay the push by at least this internal. If no change is detected within this period, the push will happen,  otherwise we&#39;ll keep delaying until things settle, up to a max of PILOT_DEBOUNCE_MAX.</td>
</tr>
<tr>
<td><code>PILOT_DEBOUNCE_MAX</code></td>
<td>Time Duration</td>
<td><code>10s</code></td>
<td>The maximum amount of time to wait for events while debouncing. If events keep showing up with no breaks for this time, we&#39;ll trigger a push.</td>
</tr>
<tr>
<td><code>PILOT_DEBUG_ADSZ_CONFIG</code></td>
<td>Boolean</td>
<td><code>false</code></td>
<td></td>
</tr>
<tr>
<td><code>PILOT_DISTRIBUTION_HISTORY_RETENTION</code></td>
<td>Time Duration</td>
<td><code>1m0s</code></td>
<td>If enabled, Pilot will keep track of old versions of distributed config for this duration.</td>
</tr>
<tr>
<td><code>PILOT_ENABLE_CONFIG_DISTRIBUTION_TRACKING</code></td>
<td>Boolean</td>
<td><code>true</code></td>
<td>If enabled, Pilot will assign meaningful nonces to each Envoy configuration message, and allow users to interrogate which envoy has which config from the debug interface.</td>
</tr>
<tr>
<td><code>PILOT_ENABLE_CRD_VALIDATION</code></td>
<td>Boolean</td>
<td><code>false</code></td>
<td>If enabled, pilot will validate CRDs while retrieving CRDs from kubernetes cache.Use this flag to enable validation of CRDs in Pilot, especially in deployments that do not have galley installed.</td>
</tr>
<tr>
<td><code>PILOT_ENABLE_EDS_DEBOUNCE</code></td>
<td>Boolean</td>
<td><code>true</code></td>
<td>If enabled, Pilot will include EDS pushes in the push debouncing, configured by PILOT_DEBOUNCE_AFTER and PILOT_DEBOUNCE_MAX. EDS pushes may be delayed, but there will be fewer pushes. By default this is enabled</td>
</tr>
<tr>
<td><code>PILOT_ENABLE_EDS_FOR_HEADLESS_SERVICES</code></td>
<td>Boolean</td>
<td><code>false</code></td>
<td>If enabled, for headless service in Kubernetes, pilot will send endpoints over EDS, allowing the sidecar to load balance among pods in the headless service. This feature should be enabled if applications access all services explicitly via a HTTP proxy port in the sidecar.</td>
</tr>
<tr>
<td><code>PILOT_ENABLE_FALLTHROUGH_ROUTE</code></td>
<td>Boolean</td>
<td><code>true</code></td>
<td>EnableFallthroughRoute provides an option to add a final wildcard match for routes. When ALLOW_ANY traffic policy is used, a Passthrough cluster is used. When REGISTRY_ONLY traffic policy is used, a 502 error is returned.</td>
</tr>
<tr>
<td><code>PILOT_ENABLE_HEADLESS_SERVICE_POD_LISTENERS</code></td>
<td>Boolean</td>
<td><code>true</code></td>
<td>If enabled, for a headless service/stateful set in Kubernetes, pilot will generate an outbound listener for each pod in a headless service. This feature should be disabled if headless services have a large number of pods.</td>
</tr>
<tr>
<td><code>PILOT_ENABLE_MYSQL_FILTER</code></td>
<td>Boolean</td>
<td><code>false</code></td>
<td>EnableMysqlFilter enables injection of `envoy.filters.network.mysql_proxy` in the filter chain.</td>
</tr>
<tr>
<td><code>PILOT_ENABLE_PROTOCOL_SNIFFING_FOR_INBOUND</code></td>
<td>Boolean</td>
<td><code>true</code></td>
<td>If enabled, protocol sniffing will be used for inbound listeners whose port protocol is not specified or unsupported</td>
</tr>
<tr>
<td><code>PILOT_ENABLE_PROTOCOL_SNIFFING_FOR_OUTBOUND</code></td>
<td>Boolean</td>
<td><code>true</code></td>
<td>If enabled, protocol sniffing will be used for outbound listeners whose port protocol is not specified or unsupported</td>
</tr>
<tr>
<td><code>PILOT_ENABLE_REDIS_FILTER</code></td>
<td>Boolean</td>
<td><code>false</code></td>
<td>EnableRedisFilter enables injection of `envoy.filters.network.redis_proxy` in the filter chain.</td>
</tr>
<tr>
<td><code>PILOT_ENABLE_TCP_METADATA_EXCHANGE</code></td>
<td>Boolean</td>
<td><code>true</code></td>
<td>If enabled, metadata exchange will be enabled for TCP using ALPN and Network Metadata Exchange filters in Envoy</td>
</tr>
<tr>
<td><code>PILOT_ENABLE_THRIFT_FILTER</code></td>
<td>Boolean</td>
<td><code>false</code></td>
<td>EnableThriftFilter enables injection of `envoy.filters.network.thrift_proxy` in the filter chain.</td>
</tr>
<tr>
<td><code>PILOT_FILTER_GATEWAY_CLUSTER_CONFIG</code></td>
<td>Boolean</td>
<td><code>false</code></td>
<td></td>
</tr>
<tr>
<td><code>PILOT_HTTP10</code></td>
<td>Boolean</td>
<td><code>false</code></td>
<td>Enables the use of HTTP 1.0 in the outbound HTTP listeners, to support legacy applications.</td>
</tr>
<tr>
<td><code>PILOT_INBOUND_PROTOCOL_DETECTION_TIMEOUT</code></td>
<td>Time Duration</td>
<td><code>1s</code></td>
<td>Protocol detection timeout for inbound listener</td>
</tr>
<tr>
<td><code>PILOT_INITIAL_FETCH_TIMEOUT</code></td>
<td>Time Duration</td>
<td><code>0s</code></td>
<td>Specifies the initial_fetch_timeout for config. If this time is reached without a response to the config requested by Envoy, the Envoy will move on with the init phase. This prevents envoy from getting stuck waiting on config during startup.</td>
</tr>
<tr>
<td><code>PILOT_PUSH_THROTTLE</code></td>
<td>Integer</td>
<td><code>100</code></td>
<td>Limits the number of concurrent pushes allowed. On larger machines this can be increased for faster pushes</td>
</tr>
<tr>
<td><code>PILOT_RESPECT_DNS_TTL</code></td>
<td>Boolean</td>
<td><code>true</code></td>
<td>If enabled, DNS based clusters will respect the TTL of the DNS, rather than polling at a fixed rate. This option is only provided for backward compatibility purposes and will be removed in the near future.</td>
</tr>
<tr>
<td><code>PILOT_RESTRICT_POD_UP_TRAFFIC_LOOP</code></td>
<td>Boolean</td>
<td><code>true</code></td>
<td>If enabled, this will block inbound traffic from matching outbound listeners, which could result in an infinite loop of traffic. This option is only provided for backward compatibility purposes and will be removed in the near future.</td>
</tr>
<tr>
<td><code>PILOT_SCOPE_GATEWAY_TO_NAMESPACE</code></td>
<td>Boolean</td>
<td><code>false</code></td>
<td>If enabled, a gateway workload can only select gateway resources in the same namespace. Gateways with same selectors in different namespaces will not be applicable.</td>
</tr>
<tr>
<td><code>PILOT_SCOPE_PUSHES</code></td>
<td>Boolean</td>
<td><code>true</code></td>
<td>If enabled, pilot will attempt to limit unnecessary pushes by determining what proxies a config or endpoint update will impact.</td>
</tr>
<tr>
<td><code>PILOT_SIDECAR_USE_REMOTE_ADDRESS</code></td>
<td>Boolean</td>
<td><code>false</code></td>
<td>UseRemoteAddress sets useRemoteAddress to true for side car outbound listeners.</td>
</tr>
<tr>
<td><code>PILOT_SKIP_VALIDATE_TRUST_DOMAIN</code></td>
<td>Boolean</td>
<td><code>false</code></td>
<td>Skip validating the peer is from the same trust domain when mTLS is enabled in authentication policy</td>
</tr>
<tr>
<td><code>PILOT_TRACE_SAMPLING</code></td>
<td>Floating-Point</td>
<td><code>100</code></td>
<td>Sets the mesh-wide trace sampling percentage. Should be 0.0 - 100.0. Precision to 0.01. Default is 100, not recommended for production use.</td>
</tr>
<tr>
<td><code>PILOT_USE_ENDPOINT_SLICE</code></td>
<td>Boolean</td>
<td><code>false</code></td>
<td>If enabled, Pilot will use EndpointSlices as the source of endpoints for Kubernetes services. By default, this is false, and Endpoints will be used. This requires the Kubernetes EndpointSlice controller to be enabled. Currently this is mutual exclusive - either Endpoints or EndpointSlices will be used</td>
</tr>
<tr>
<td><code>PKCS8_KEY</code></td>
<td>Boolean</td>
<td><code>false</code></td>
<td>Whether to generate PKCS#8 private keys</td>
</tr>
<tr>
<td><code>PLUGINS</code></td>
<td>String</td>
<td><code></code></td>
<td></td>
</tr>
<tr>
<td><code>POD_NAME</code></td>
<td>String</td>
<td><code></code></td>
<td></td>
</tr>
<tr>
<td><code>POD_NAMESPACE</code></td>
<td>String</td>
<td><code></code></td>
<td></td>
</tr>
<tr>
<td><code>SDS_ENABLED</code></td>
<td>Boolean</td>
<td><code>false</code></td>
<td></td>
</tr>
<tr>
<td><code>SDS_UDS_PATH</code></td>
<td>String</td>
<td><code>unix:/var/run/sds/uds_path</code></td>
<td>SDS address</td>
</tr>
<tr>
<td><code>SECRET_GRACE_DURATION</code></td>
<td>Time Duration</td>
<td><code>12h0m0s</code></td>
<td></td>
</tr>
<tr>
<td><code>SECRET_JOB_RUN_INTERVAL</code></td>
<td>Time Duration</td>
<td><code>10m0s</code></td>
<td></td>
</tr>
<tr>
<td><code>SECRET_TTL</code></td>
<td>Time Duration</td>
<td><code>24h0m0s</code></td>
<td></td>
</tr>
<tr>
<td><code>SECRET_WATCHER_RESYNC_PERIOD</code></td>
<td>String</td>
<td><code></code></td>
<td></td>
</tr>
<tr>
<td><code>STACKDRIVER_TRACING_DEBUG</code></td>
<td>Boolean</td>
<td><code>false</code></td>
<td>If set to true, enables trace output to stdout</td>
</tr>
<tr>
<td><code>STACKDRIVER_TRACING_ENABLED</code></td>
<td>Boolean</td>
<td><code>false</code></td>
<td>If enabled, stackdriver will get configured as the tracer.</td>
</tr>
<tr>
<td><code>STACKDRIVER_TRACING_MAX_NUMBER_OF_ANNOTATIONS</code></td>
<td>Integer</td>
<td><code>200</code></td>
<td>Sets the max number of annotations for stackdriver</td>
</tr>
<tr>
<td><code>STACKDRIVER_TRACING_MAX_NUMBER_OF_ATTRIBUTES</code></td>
<td>Integer</td>
<td><code>200</code></td>
<td>Sets the max number of attributes for stackdriver</td>
</tr>
<tr>
<td><code>STACKDRIVER_TRACING_MAX_NUMBER_OF_MESSAGE_EVENTS</code></td>
<td>Integer</td>
<td><code>200</code></td>
<td>Sets the max number of message events for stackdriver</td>
</tr>
<tr>
<td><code>STALED_CONNECTION_RECYCLE_RUN_INTERVAL</code></td>
<td>Time Duration</td>
<td><code>5m0s</code></td>
<td></td>
</tr>
<tr>
<td><code>TERMINATION_DRAIN_DURATION_SECONDS</code></td>
<td>Integer</td>
<td><code>5</code></td>
<td>The amount of time allowed for connections to complete on pilot-agent shutdown. On receiving SIGTERM or SIGINT, pilot-agent tells the active Envoy to start draining, preventing any new connections and allowing existing connections to complete. It then sleeps for the TerminationDrainDuration and then kills any remaining active Envoy processes.</td>
</tr>
<tr>
<td><code>TRUST_DOMAIN</code></td>
<td>String</td>
<td><code></code></td>
<td></td>
</tr>
<tr>
<td><code>USE_ISTIO_JWT_FILTER</code></td>
<td>Boolean</td>
<td><code>false</code></td>
<td>Use the Istio JWT filter for JWT token verification.</td>
</tr>
</tbody>
</table>
<h2 id="metrics">Exported metrics</h2>
<table class="metrics">
<thead>
<tr><th>Metric Name</th><th>Type</th><th>Description</th></tr>
</thead>
<tbody>
<tr><td><code>endpoint_no_pod</code></td><td><code>LastValue</code></td><td>Endpoints without an associated pod.</td></tr>
<tr><td><code>istio_build</code></td><td><code>LastValue</code></td><td>Istio component build info</td></tr>
<tr><td><code>num_failed_outgoing_requests</code></td><td><code>Sum</code></td><td>Number of failed outgoing requests (e.g. to a token exchange server, CA, etc.)</td></tr>
<tr><td><code>num_outgoing_requests</code></td><td><code>Sum</code></td><td>Number of total outgoing requests (e.g. to a token exchange server, CA, etc.)</td></tr>
<tr><td><code>num_outgoing_retries</code></td><td><code>Sum</code></td><td>Number of outgoing retry requests (e.g. to a token exchange server, CA, etc.)</td></tr>
<tr><td><code>outgoing_latency</code></td><td><code>Sum</code></td><td>The latency of outgoing requests (e.g. to a token exchange server, CA, etc.) in milliseconds.</td></tr>
<tr><td><code>pilot_conflict_inbound_listener</code></td><td><code>LastValue</code></td><td>Number of conflicting inbound listeners.</td></tr>
<tr><td><code>pilot_conflict_outbound_listener_http_over_current_tcp</code></td><td><code>LastValue</code></td><td>Number of conflicting wildcard http listeners with current wildcard tcp listener.</td></tr>
<tr><td><code>pilot_conflict_outbound_listener_http_over_https</code></td><td><code>LastValue</code></td><td>Number of conflicting HTTP listeners with well known HTTPS ports</td></tr>
<tr><td><code>pilot_conflict_outbound_listener_tcp_over_current_http</code></td><td><code>LastValue</code></td><td>Number of conflicting wildcard tcp listeners with current wildcard http listener.</td></tr>
<tr><td><code>pilot_conflict_outbound_listener_tcp_over_current_tcp</code></td><td><code>LastValue</code></td><td>Number of conflicting tcp listeners with current tcp listener.</td></tr>
<tr><td><code>pilot_destrule_subsets</code></td><td><code>LastValue</code></td><td>Duplicate subsets across destination rules for same host</td></tr>
<tr><td><code>pilot_duplicate_envoy_clusters</code></td><td><code>LastValue</code></td><td>Duplicate envoy clusters caused by service entries with same hostname</td></tr>
<tr><td><code>pilot_eds_no_instances</code></td><td><code>LastValue</code></td><td>Number of clusters without instances.</td></tr>
<tr><td><code>pilot_endpoint_not_ready</code></td><td><code>LastValue</code></td><td>Endpoint found in unready state.</td></tr>
<tr><td><code>pilot_jwks_resolver_network_fetch_fail_total</code></td><td><code>Sum</code></td><td>Total number of failed network fetch by pilot jwks resolver</td></tr>
<tr><td><code>pilot_jwks_resolver_network_fetch_success_total</code></td><td><code>Sum</code></td><td>Total number of successfully network fetch by pilot jwks resolver</td></tr>
<tr><td><code>pilot_no_ip</code></td><td><code>LastValue</code></td><td>Pods not found in the endpoint table, possibly invalid.</td></tr>
<tr><td><code>pilot_total_rejected_configs</code></td><td><code>Sum</code></td><td>Total number of configs that Pilot had to reject or ignore.</td></tr>
<tr><td><code>pilot_virt_services</code></td><td><code>LastValue</code></td><td>Total virtual services known to pilot.</td></tr>
<tr><td><code>pilot_vservice_dup_domain</code></td><td><code>LastValue</code></td><td>Virtual services with dup domains.</td></tr>
<tr><td><code>total_active_connections</code></td><td><code>Sum</code></td><td>The total number of active SDS connections.</td></tr>
<tr><td><code>total_push_errors</code></td><td><code>Sum</code></td><td>The total number of failed SDS pushes.</td></tr>
<tr><td><code>total_pushes</code></td><td><code>Sum</code></td><td>The total number of SDS pushes.</td></tr>
<tr><td><code>total_secret_update_failures</code></td><td><code>Sum</code></td><td>The total number of dynamic secret update failures reported by proxy.</td></tr>
<tr><td><code>total_stale_connections</code></td><td><code>Sum</code></td><td>The total number of stale SDS connections.</td></tr>
</tbody>
</table>
