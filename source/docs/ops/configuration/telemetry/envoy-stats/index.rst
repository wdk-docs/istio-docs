envoy-stats
==============================================

The Envoy proxy keeps detailed statistics about network traffic.

Envoy’s statistics only cover the traffic for a particular Envoy
instance. See `Observability </docs/tasks/observability/>`_ for
persistent per-service Istio telemetry. The statistics the Envoy proxies
record can provide more information about specific pod instances.

To see the statistics for a pod:

.. code:: sh

      $ kubectl exec $POD -c istio-proxy – pilot-agent
request GET stats

See `the Envoy
documentation <https://www.envoyproxy.io/docs/envoy/latest/configuration/upstream/cluster_manager/cluster_stats>`_
for an explanation of the data recorded.

By default, Istio configures Envoy to record minimal statistics. The
default collection keys are:

-  ``cluster_manager``
-  ``listener_manager``
-  ``http_mixer_filter``
-  ``tcp_mixer_filter``
-  ``server``
-  ``cluster.xds-grpc``

To see the Envoy settings for statistics data collection use
```istioctl proxy-config bootstrap`` </docs/reference/commands/istioctl/#istioctl-proxy-config-bootstrap>`_
and follow the `deep dive into Envoy
configuration </docs/ops/diagnostic-tools/proxy-cmd/#deep-dive-into-envoy-configuration>`_.
Envoy only collects statistical data on items matching the
``inclusion_list`` within the ``stats_matcher`` JSON element.

To Configure Envoy to record statistics for inbound or outbound traffic,
add the ``sidecar.istio.io/statsInclusionPrefixes`` annotation to the
pod template in the Kubernetes ``Deployment``. Add the
``cluster.outbound`` prefix to gather data about outbound traffic
activity and circuit breaking. To gather data on inbound traffic, add
the ``listener`` prefix. The sample
`fortio-deploy.yaml <%7B%7B%3C%20github_file%3E%7D%7D/samples/httpbin/sample-client/fortio-deploy.yaml>`_
shows use of ``sidecar.istio.io/statsInclusionPrefixes`` with the
``cluster.outbound`` prefix.

You can override the Envoy defaults to gather less data than usual. Use
``sidecar.istio.io/statsInclusionPrefixes: cluster_manager,listener_manager``
to collect the least statistics possible.
