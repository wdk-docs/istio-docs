galley
=====================

---
WARNING: THIS IS AN AUTO-GENERATED FILE, DO NOT EDIT. PLEASE MODIFY THE ORIGINAL SOURCE IN THE 'https://github.com/istio/istio' REPO
source_repo: https://github.com/istio/istio
title: galley
description: Galley provides configuration management services for Istio.
generator: pkg-collateral-docs
number_of_entries: 5
max_toc_level: 2
remove_toc_prefix: 'galley '
---
<p>Galley provides configuration management services for Istio.</p>
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
<td><code>--config &lt;string&gt;</code></td>
<td><code>-c</code></td>
<td>Config file containing args  (default ``)</td>
</tr>
<tr>
<td><code>--log_as_json</code></td>
<td></td>
<td>Whether to format output as JSON or in plain console-friendly format </td>
</tr>
<tr>
<td><code>--log_caller &lt;string&gt;</code></td>
<td></td>
<td>Comma-separated list of scopes for which to include caller information, scopes can be any of [all, analysis, attributes, default, grpcAdapter, mcp, model, processing, rbac, resource, server, source, validation, validationController, validationServer]  (default ``)</td>
</tr>
<tr>
<td><code>--log_output_level &lt;string&gt;</code></td>
<td></td>
<td>Comma-separated minimum per-scope logging level of messages to output, in the form of &lt;scope&gt;:&lt;level&gt;,&lt;scope&gt;:&lt;level&gt;,... where scope can be one of [all, analysis, attributes, default, grpcAdapter, mcp, model, processing, rbac, resource, server, source, validation, validationController, validationServer] and level can be one of [debug, info, warn, error, fatal, none]  (default `default:info`)</td>
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
<td>Comma-separated minimum per-scope logging level at which stack traces are captured, in the form of &lt;scope&gt;:&lt;level&gt;,&lt;scope:level&gt;,... where scope can be one of [all, analysis, attributes, default, grpcAdapter, mcp, model, processing, rbac, resource, server, source, validation, validationController, validationServer] and level can be one of [debug, info, warn, error, fatal, none]  (default `default:none`)</td>
</tr>
<tr>
<td><code>--log_target &lt;stringArray&gt;</code></td>
<td></td>
<td>The set of paths where to output the log. This can be any path as well as the special values stdout and stderr  (default `[stdout]`)</td>
</tr>
</tbody>
</table>
<h2 id="galley-probe">galley probe</h2>
<p>Check the liveness or readiness of a locally-running server</p>
<pre class="language-bash"><code>galley probe [flags]
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
<td><code>--config &lt;string&gt;</code></td>
<td><code>-c</code></td>
<td>Config file containing args  (default ``)</td>
</tr>
<tr>
<td><code>--interval &lt;duration&gt;</code></td>
<td></td>
<td>Duration used for checking the target file&#39;s last modified time.  (default `0s`)</td>
</tr>
<tr>
<td><code>--log_as_json</code></td>
<td></td>
<td>Whether to format output as JSON or in plain console-friendly format </td>
</tr>
<tr>
<td><code>--log_caller &lt;string&gt;</code></td>
<td></td>
<td>Comma-separated list of scopes for which to include caller information, scopes can be any of [all, analysis, attributes, default, grpcAdapter, mcp, model, processing, rbac, resource, server, source, validation, validationController, validationServer]  (default ``)</td>
</tr>
<tr>
<td><code>--log_output_level &lt;string&gt;</code></td>
<td></td>
<td>Comma-separated minimum per-scope logging level of messages to output, in the form of &lt;scope&gt;:&lt;level&gt;,&lt;scope&gt;:&lt;level&gt;,... where scope can be one of [all, analysis, attributes, default, grpcAdapter, mcp, model, processing, rbac, resource, server, source, validation, validationController, validationServer] and level can be one of [debug, info, warn, error, fatal, none]  (default `default:info`)</td>
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
<td>Comma-separated minimum per-scope logging level at which stack traces are captured, in the form of &lt;scope&gt;:&lt;level&gt;,&lt;scope:level&gt;,... where scope can be one of [all, analysis, attributes, default, grpcAdapter, mcp, model, processing, rbac, resource, server, source, validation, validationController, validationServer] and level can be one of [debug, info, warn, error, fatal, none]  (default `default:none`)</td>
</tr>
<tr>
<td><code>--log_target &lt;stringArray&gt;</code></td>
<td></td>
<td>The set of paths where to output the log. This can be any path as well as the special values stdout and stderr  (default `[stdout]`)</td>
</tr>
<tr>
<td><code>--probe-path &lt;string&gt;</code></td>
<td></td>
<td>Path of the file for checking the availability.  (default ``)</td>
</tr>
</tbody>
</table>
<h2 id="galley-server">galley server</h2>
<p>Starts Galley as a server</p>
<pre class="language-bash"><code>galley server [flags]
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
<td><code>--accessListFile &lt;string&gt;</code></td>
<td></td>
<td>The access list yaml file that contains the allowed mTLS peer ids.  (default `/etc/config/accesslist.yaml`)</td>
</tr>
<tr>
<td><code>--caCertFile &lt;string&gt;</code></td>
<td></td>
<td>File containing the caBundle that signed the cert/key specified by --tlsCertFile and --tlsKeyFile.  (default `/etc/certs/root-cert.pem`)</td>
</tr>
<tr>
<td><code>--config &lt;string&gt;</code></td>
<td><code>-c</code></td>
<td>Config file containing args  (default ``)</td>
</tr>
<tr>
<td><code>--configPath &lt;string&gt;</code></td>
<td></td>
<td>Istio config file path  (default ``)</td>
</tr>
<tr>
<td><code>--ctrlz_address &lt;string&gt;</code></td>
<td></td>
<td>The IP Address to listen on for the ControlZ introspection facility. Use &#39;*&#39; to indicate all addresses.  (default `localhost`)</td>
</tr>
<tr>
<td><code>--ctrlz_port &lt;uint16&gt;</code></td>
<td></td>
<td>The IP port to use for the ControlZ introspection facility  (default `9876`)</td>
</tr>
<tr>
<td><code>--deployment-name &lt;string&gt;</code></td>
<td></td>
<td>Name of the deployment for the validation pod  (default `istio-galley`)</td>
</tr>
<tr>
<td><code>--deployment-namespace &lt;string&gt;</code></td>
<td></td>
<td>Namespace of the deployment for the validation pod  (default `istio-system`)</td>
</tr>
<tr>
<td><code>--disableResourceReadyCheck</code></td>
<td></td>
<td>Disable resource readiness checks. This allows Galley to start if not all resource types are supported </td>
</tr>
<tr>
<td><code>--domain &lt;string&gt;</code></td>
<td></td>
<td>DNS domain suffix  (default `cluster.local`)</td>
</tr>
<tr>
<td><code>--enable-reconcileWebhookConfiguration</code></td>
<td></td>
<td>Enable reconciliation for webhook configuration. </td>
</tr>
<tr>
<td><code>--enable-server</code></td>
<td></td>
<td>Run galley server mode </td>
</tr>
<tr>
<td><code>--enable-validation</code></td>
<td></td>
<td>Run galley validation mode </td>
</tr>
<tr>
<td><code>--enableAnalysis</code></td>
<td></td>
<td>Enable config analysis service </td>
</tr>
<tr>
<td><code>--enableProfiling</code></td>
<td></td>
<td>Enable profiling for Galley </td>
</tr>
<tr>
<td><code>--enableServiceDiscovery</code></td>
<td></td>
<td>Enable service discovery processing in Galley </td>
</tr>
<tr>
<td><code>--excludedResourceKinds &lt;stringSlice&gt;</code></td>
<td></td>
<td>Comma-separated list of resource kinds that should not generate source events  (default `[Endpoints,Namespace,Node,Pod,Service]`)</td>
</tr>
<tr>
<td><code>--insecure</code></td>
<td></td>
<td>Use insecure gRPC communication </td>
</tr>
<tr>
<td><code>--kubeconfig &lt;string&gt;</code></td>
<td></td>
<td>Use a Kubernetes configuration file instead of in-cluster configuration  (default ``)</td>
</tr>
<tr>
<td><code>--livenessProbeInterval &lt;duration&gt;</code></td>
<td></td>
<td>Interval of updating file for the Galley liveness probe.  (default `2s`)</td>
</tr>
<tr>
<td><code>--livenessProbePath &lt;string&gt;</code></td>
<td></td>
<td>Path to the file for the Galley liveness probe.  (default `/healthLiveness`)</td>
</tr>
<tr>
<td><code>--log_as_json</code></td>
<td></td>
<td>Whether to format output as JSON or in plain console-friendly format </td>
</tr>
<tr>
<td><code>--log_caller &lt;string&gt;</code></td>
<td></td>
<td>Comma-separated list of scopes for which to include caller information, scopes can be any of [all, analysis, attributes, default, grpcAdapter, mcp, model, processing, rbac, resource, server, source, validation, validationController, validationServer]  (default ``)</td>
</tr>
<tr>
<td><code>--log_output_level &lt;string&gt;</code></td>
<td></td>
<td>Comma-separated minimum per-scope logging level of messages to output, in the form of &lt;scope&gt;:&lt;level&gt;,&lt;scope&gt;:&lt;level&gt;,... where scope can be one of [all, analysis, attributes, default, grpcAdapter, mcp, model, processing, rbac, resource, server, source, validation, validationController, validationServer] and level can be one of [debug, info, warn, error, fatal, none]  (default `default:info`)</td>
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
<td>Comma-separated minimum per-scope logging level at which stack traces are captured, in the form of &lt;scope&gt;:&lt;level&gt;,&lt;scope:level&gt;,... where scope can be one of [all, analysis, attributes, default, grpcAdapter, mcp, model, processing, rbac, resource, server, source, validation, validationController, validationServer] and level can be one of [debug, info, warn, error, fatal, none]  (default `default:none`)</td>
</tr>
<tr>
<td><code>--log_target &lt;stringArray&gt;</code></td>
<td></td>
<td>The set of paths where to output the log. This can be any path as well as the special values stdout and stderr  (default `[stdout]`)</td>
</tr>
<tr>
<td><code>--meshConfigFile &lt;string&gt;</code></td>
<td></td>
<td>Path to the mesh config file  (default `/etc/mesh-config/mesh`)</td>
</tr>
<tr>
<td><code>--monitoringPort &lt;uint&gt;</code></td>
<td></td>
<td>Port to use for exposing self-monitoring information  (default `15014`)</td>
</tr>
<tr>
<td><code>--pprofPort &lt;uint&gt;</code></td>
<td></td>
<td>Port to use for exposing profiling  (default `9094`)</td>
</tr>
<tr>
<td><code>--readinessProbeInterval &lt;duration&gt;</code></td>
<td></td>
<td>Interval of updating file for the Galley readiness probe.  (default `2s`)</td>
</tr>
<tr>
<td><code>--readinessProbePath &lt;string&gt;</code></td>
<td></td>
<td>Path to the file for the Galley readiness probe.  (default `/healthReadiness`)</td>
</tr>
<tr>
<td><code>--resyncPeriod &lt;duration&gt;</code></td>
<td></td>
<td>Resync period for rescanning Kubernetes resources  (default `0s`)</td>
</tr>
<tr>
<td><code>--server-address &lt;string&gt;</code></td>
<td></td>
<td>Address to use for Galley&#39;s gRPC API, e.g. tcp://localhost:9092 or unix:///path/to/file  (default `tcp://0.0.0.0:9901`)</td>
</tr>
<tr>
<td><code>--server-maxConcurrentStreams &lt;uint&gt;</code></td>
<td></td>
<td>Maximum number of outstanding RPCs per connection  (default `1024`)</td>
</tr>
<tr>
<td><code>--server-maxReceivedMessageSize &lt;uint&gt;</code></td>
<td></td>
<td>Maximum size of individual gRPC messages  (default `1048576`)</td>
</tr>
<tr>
<td><code>--service-name &lt;string&gt;</code></td>
<td></td>
<td>Name of the validation service running in the same namespace as the deployment  (default `istio-galley`)</td>
</tr>
<tr>
<td><code>--sinkAddress &lt;string&gt;</code></td>
<td></td>
<td>Address of MCP Resource Sink server for Galley to connect to. Ex: &#39;foo.com:1234&#39;  (default ``)</td>
</tr>
<tr>
<td><code>--sinkAuthMode &lt;string&gt;</code></td>
<td></td>
<td>Name of authentication plugin to use for connection to sink server.  (default ``)</td>
</tr>
<tr>
<td><code>--sinkMeta &lt;stringSlice&gt;</code></td>
<td></td>
<td>Comma-separated list of key=values to attach as metadata to outgoing sink connections. Ex: &#39;key=value,key2=value2&#39;  (default `[]`)</td>
</tr>
<tr>
<td><code>--tlsCertFile &lt;string&gt;</code></td>
<td></td>
<td>File containing the x509 Certificate for HTTPS.  (default `/etc/certs/cert-chain.pem`)</td>
</tr>
<tr>
<td><code>--tlsKeyFile &lt;string&gt;</code></td>
<td></td>
<td>File containing the x509 private key matching --tlsCertFile.  (default `/etc/certs/key.pem`)</td>
</tr>
<tr>
<td><code>--validation-port &lt;uint&gt;</code></td>
<td></td>
<td>HTTPS port of the validation service.  (default `9443`)</td>
</tr>
<tr>
<td><code>--validation.tls.caCertificates &lt;string&gt;</code></td>
<td></td>
<td>File containing the caBundle that signed the cert/key specified by --validation.tls.clientCertificate and --validation.tls.privateKey.  (default `/etc/certs/root-cert.pem`)</td>
</tr>
<tr>
<td><code>--validation.tls.clientCertificate &lt;string&gt;</code></td>
<td></td>
<td>File containing the x509 Certificate for HTTPS validation.  (default `/etc/certs/cert-chain.pem`)</td>
</tr>
<tr>
<td><code>--validation.tls.privateKey &lt;string&gt;</code></td>
<td></td>
<td>File containing the x509 private key matching --validation.tls.clientCertificate.  (default `/etc/certs/key.pem`)</td>
</tr>
<tr>
<td><code>--watchConfigFiles</code></td>
<td></td>
<td>Enable the Fsnotify for watching config source files on the disk and implicit signaling on a config change. Explicit signaling will still be enabled </td>
</tr>
<tr>
<td><code>--webhook-name &lt;string&gt;</code></td>
<td></td>
<td>Name of the k8s validatingwebhookconfiguration  (default `istio-galley`)</td>
</tr>
</tbody>
</table>
<p/>Accepts deep config files, like:
<pre class="language-yaml"><code>general:
  introspection:
    address: --ctrlz_address
    port: --ctrlz_port
  kubeconfig: --kubeconfig
processing:
  domainsuffix: --domain
  server:
    address: --server-address
    auth:
      insecure: --insecure
    enable: --enable-server
validation:
  deploymentname: --deployment-name
  deploymentnamespace: --deployment-namespace
  enable: --enable-validation
  servicename: --service-name
  tls:
    caCertificates: --validation.tls.caCertificates
    clientCertificate: --validation.tls.clientCertificate
    privateKey: --validation.tls.privateKey
  webhookconfigfile: --validation-webhook-config-file
  webhookname: --webhook-name
  webhookport: --validation-port

</code></pre>
<h2 id="galley-version">galley version</h2>
<p>Prints out build version information</p>
<pre class="language-bash"><code>galley version [flags]
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
<td><code>--config &lt;string&gt;</code></td>
<td><code>-c</code></td>
<td>Config file containing args  (default ``)</td>
</tr>
<tr>
<td><code>--log_as_json</code></td>
<td></td>
<td>Whether to format output as JSON or in plain console-friendly format </td>
</tr>
<tr>
<td><code>--log_caller &lt;string&gt;</code></td>
<td></td>
<td>Comma-separated list of scopes for which to include caller information, scopes can be any of [all, analysis, attributes, default, grpcAdapter, mcp, model, processing, rbac, resource, server, source, validation, validationController, validationServer]  (default ``)</td>
</tr>
<tr>
<td><code>--log_output_level &lt;string&gt;</code></td>
<td></td>
<td>Comma-separated minimum per-scope logging level of messages to output, in the form of &lt;scope&gt;:&lt;level&gt;,&lt;scope&gt;:&lt;level&gt;,... where scope can be one of [all, analysis, attributes, default, grpcAdapter, mcp, model, processing, rbac, resource, server, source, validation, validationController, validationServer] and level can be one of [debug, info, warn, error, fatal, none]  (default `default:info`)</td>
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
<td>Comma-separated minimum per-scope logging level at which stack traces are captured, in the form of &lt;scope&gt;:&lt;level&gt;,&lt;scope:level&gt;,... where scope can be one of [all, analysis, attributes, default, grpcAdapter, mcp, model, processing, rbac, resource, server, source, validation, validationController, validationServer] and level can be one of [debug, info, warn, error, fatal, none]  (default `default:none`)</td>
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
These environment variables affect the behavior of the <code>galley</code> command.
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
<td><code>AUTHZ_FAILURE_LOG_BURST_SIZE</code></td>
<td>Integer</td>
<td><code>1</code></td>
<td></td>
</tr>
<tr>
<td><code>AUTHZ_FAILURE_LOG_FREQ</code></td>
<td>Time Duration</td>
<td><code>1m0s</code></td>
<td></td>
</tr>
<tr>
<td><code>MCP_SOURCE_REQ_BURST_SIZE</code></td>
<td>Integer</td>
<td><code>100</code></td>
<td></td>
</tr>
<tr>
<td><code>MCP_SOURCE_REQ_FREQ</code></td>
<td>Time Duration</td>
<td><code>1s</code></td>
<td></td>
</tr>
<tr>
<td><code>SOURCE_SERVER_STREAM_BURST_SIZE</code></td>
<td>Integer</td>
<td><code>100</code></td>
<td></td>
</tr>
<tr>
<td><code>SOURCE_SERVER_STREAM_FREQ</code></td>
<td>Time Duration</td>
<td><code>1s</code></td>
<td></td>
</tr>
</tbody>
</table>
<h2 id="metrics">Exported metrics</h2>
<table class="metrics">
<thead>
<tr><th>Metric Name</th><th>Type</th><th>Description</th></tr>
</thead>
<tbody>
<tr><td><code>galley_runtime_processor_event_span_duration_milliseconds</code></td><td><code>Distribution</code></td><td>The duration between each incoming event</td></tr>
<tr><td><code>galley_runtime_processor_events_processed_total</code></td><td><code>Count</code></td><td>The number of events that have been processed</td></tr>
<tr><td><code>galley_runtime_processor_snapshot_events_total</code></td><td><code>Distribution</code></td><td>The number of events per snapshot</td></tr>
<tr><td><code>galley_runtime_processor_snapshot_lifetime_duration_milliseconds</code></td><td><code>Distribution</code></td><td>The duration of each snapshot</td></tr>
<tr><td><code>galley_runtime_processor_snapshots_published_total</code></td><td><code>Count</code></td><td>The number of snapshots that have been published</td></tr>
<tr><td><code>galley_runtime_state_type_instances_total</code></td><td><code>LastValue</code></td><td>The number of type instances per type URL</td></tr>
<tr><td><code>galley_runtime_strategy_on_change_total</code></td><td><code>Count</code></td><td>The number of times the strategy's onChange has been called</td></tr>
<tr><td><code>galley_runtime_strategy_timer_max_time_reached_total</code></td><td><code>Count</code></td><td>The number of times the max time has been reached</td></tr>
<tr><td><code>galley_runtime_strategy_timer_quiesce_reached_total</code></td><td><code>Count</code></td><td>The number of times a quiesce has been reached</td></tr>
<tr><td><code>galley_runtime_strategy_timer_resets_total</code></td><td><code>Count</code></td><td>The number of times the timer has been reset</td></tr>
<tr><td><code>galley_source_kube_dynamic_converter_failure_total</code></td><td><code>Count</code></td><td>The number of times a dynamnic kubernetes source failed converting a resources</td></tr>
<tr><td><code>galley_source_kube_dynamic_converter_success_total</code></td><td><code>Count</code></td><td>The number of times a dynamic kubernetes source successfully converted a resource</td></tr>
<tr><td><code>galley_source_kube_event_error_total</code></td><td><code>Count</code></td><td>The number of times a kubernetes source encountered errored while handling an event</td></tr>
<tr><td><code>galley_source_kube_event_success_total</code></td><td><code>Count</code></td><td>The number of times a kubernetes source successfully handled an event</td></tr>
<tr><td><code>galley_validation_cert_key_update_errors</code></td><td><code>Count</code></td><td>Galley validation webhook certificate updates errors</td></tr>
<tr><td><code>galley_validation_cert_key_updates</code></td><td><code>Count</code></td><td>Galley validation webhook certificate updates</td></tr>
<tr><td><code>galley_validation_config_delete_error</code></td><td><code>Count</code></td><td>k8s webhook configuration delete error</td></tr>
<tr><td><code>galley_validation_config_load</code></td><td><code>Count</code></td><td>k8s webhook configuration (re)loads</td></tr>
<tr><td><code>galley_validation_config_load_error</code></td><td><code>Count</code></td><td>k8s webhook configuration (re)load error</td></tr>
<tr><td><code>galley_validation_config_update_error</code></td><td><code>Count</code></td><td>k8s webhook configuration update error</td></tr>
<tr><td><code>galley_validation_config_updates</code></td><td><code>Count</code></td><td>k8s webhook configuration updates</td></tr>
<tr><td><code>galley_validation_failed</code></td><td><code>Count</code></td><td>Resource validation failed</td></tr>
<tr><td><code>galley_validation_http_error</code></td><td><code>Count</code></td><td>Resource validation http serve errors</td></tr>
<tr><td><code>galley_validation_passed</code></td><td><code>Count</code></td><td>Resource is valid</td></tr>
<tr><td><code>istio_build</code></td><td><code>LastValue</code></td><td>Istio component build info</td></tr>
<tr><td><code>istio_mcp_clients_total</code></td><td><code>LastValue</code></td><td>The number of streams currently connected.</td></tr>
<tr><td><code>istio_mcp_message_sizes_bytes</code></td><td><code>Distribution</code></td><td>Size of messages received from clients.</td></tr>
<tr><td><code>istio_mcp_reconnections</code></td><td><code>Sum</code></td><td>The number of times the sink has reconnected.</td></tr>
<tr><td><code>istio_mcp_recv_failures_total</code></td><td><code>Sum</code></td><td>The number of recv failures in the source.</td></tr>
<tr><td><code>istio_mcp_request_acks_total</code></td><td><code>Sum</code></td><td>The number of request acks received by the source.</td></tr>
<tr><td><code>istio_mcp_request_nacks_total</code></td><td><code>Sum</code></td><td>The number of request nacks received by the source.</td></tr>
<tr><td><code>istio_mcp_send_failures_total</code></td><td><code>Sum</code></td><td>The number of send failures in the source.</td></tr>
</tbody>
</table>
