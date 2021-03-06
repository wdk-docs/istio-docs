observability-issues
=========================================


No traces appearing in Zipkin when running Istio locally on Mac
---------------------------------------------------------------

Istio is installed and everything seems to be working except there are
no traces showing up in Zipkin when there should be.

This may be caused by a known `Docker
issue <https://github.com/docker/for-mac/issues/1260>`_ where the time
inside containers may skew significantly from the time on the host
machine. If this is the case, when you select a very long date range in
Zipkin you will see the traces appearing as much as several days too
early.

You can also confirm this problem by comparing the date inside a Docker
container to outside:

.. code:: sh

      $ docker run –entrypoint date
gcr.io/istio-testing/ubuntu-16-04-slave:latest Sun Jun 11 11:44:18 UTC
2017

.. code:: sh

      $ date -u Thu Jun 15 02:25:42 UTC 2017

To fix the problem, you’ll need to shutdown and then restart Docker
before reinstalling Istio.

Missing Grafana output
----------------------

If you’re unable to get Grafana output when connecting from a local web
client to Istio remotely hosted, you should validate the client and
server date and time match.

The time of the web client (e.g. Chrome) affects the output from
Grafana. A simple solution to this problem is to verify a time
synchronization service is running correctly within the Kubernetes
cluster and the web client machine also is correctly using a time
synchronization service. Some common time synchronization systems are
NTP and Chrony. This is especially problematic in engineering labs with
firewalls. In these scenarios, NTP may not be configured properly to
point at the lab-based NTP services.

Mixer Telemetry Issues
----------------------

.. warning::

   Mixer is deprecated. The functionality provided by Mixer
is being moved into the Envoy proxies. Use of Mixer with Istio will only
be supported through the 1.7 release of Istio. {{</ warning>}}

Expected metrics are not being collected
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following procedure helps you diagnose problems where metrics you
are expecting to see reported are not being collected.

The expected flow for metrics is:

1. Envoy reports attributes from requests asynchronously to Mixer in a
   batch.

2. Mixer translates the attributes into instances based on the
   operator-provided configuration.

3. Mixer hands the instances to Mixer adapters for processing and
   backend storage.

4. The backend storage systems record the metrics data.

The Mixer default installations include a Prometheus adapter and the
configuration to generate a `default set of metric
values </docs/reference/config/policy-and-telemetry/metrics/>`_ and
send them to the Prometheus adapter. The Prometheus adapter
configuration enables a Prometheus instance to scrape Mixer for metrics.

If the Istio Dashboard or the Prometheus queries don’t show the expected
metrics, any step of the flow above may present an issue. The following
sections provide instructions to troubleshoot each step.

Verify Istio CNI pods are running (if used)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Istio CNI plugin performs the Istio mesh pod traffic redirection in
the Kubernetes pod lifecycle’s network setup phase, thereby removing the
`requirement for the ``NET_ADMIN`` and ``NET_RAW``
capabilities </docs/ops/deployment/requirements/>`_ for users deploying
pods into the Istio mesh. The Istio CNI plugin replaces the
functionality provided by the ``istio-init`` container.

1. Verify that the ``istio-cni-node`` pods are running:

   .. code:: sh

      $ kubectl -n kube-system get pod -l
   k8s-app=istio-cni-node

2. If ``PodSecurityPolicy`` is being enforced in your cluster, ensure
   the ``istio-cni`` service account can use a ``PodSecurityPolicy``
   which `allows the ``NET_ADMIN`` and ``NET_RAW``
   capabilities </docs/ops/deployment/requirements/>`_ #### Verify
   Mixer is receiving report calls

Mixer generates metrics to monitor its own behavior. The first step is
to check these metrics:

1. Establish a connection to the Mixer self-monitoring endpoint for the
   ``istio-telemetry`` deployment. In Kubernetes environments, execute
   the following command:

   .. code:: sh

      $ kubectl -n istio-system port-forward 15014 &

2. Verify successful report calls. On the Mixer self-monitoring endpoint
   (``http://localhost:15014/metrics``), search for
   ``grpc_io_server_completed_rpcs``. You should see something like:

   {{< text plain >}}
   grpc_io_server_completed_rpcs{grpc_server_method=“istio.mixer.v1.Mixer/Report”,grpc_server_status=“OK”}
   2532

   If you do not see any data for ``grpc_io_server_completed_rpcs`` with
   a ``grpc_server_method="istio.mixer.v1.Mixer/Report"``, then Envoy is
   not calling Mixer to report telemetry.

3. In this case, ensure you integrated the services properly into the
   mesh. You can achieve this task with either `automatic or manual
   sidecar
   injection </docs/setup/additional-setup/sidecar-injection/>`_.

Verify the Mixer rules exist
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In Kubernetes environments, issue the following command:

.. code:: sh

      $ kubectl get rules –all-namespaces NAMESPACE NAME AGE
istio-system kubeattrgenrulerule 4h istio-system promhttp 4h
istio-system promtcp 4h istio-system promtcpconnectionclosed 4h
istio-system promtcpconnectionopen 4h istio-system
tcpkubeattrgenrulerule 4h

If the output shows no rules named ``promhttp`` or ``promtcp``, then the
Mixer configuration for sending metric instances to the Prometheus
adapter is missing. You must supply the configuration for rules
connecting the Mixer metric instances to a Prometheus handler.

For reference, please consult the `default rules for
Prometheus <%7B%7B%3C%20github_file%20%3E%7D%7D/install/kubernetes/helm/istio/charts/mixer/templates/config.yaml>`_.

Verify the Prometheus handler configuration exists
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. In Kubernetes environments, issue the following command:

   .. code:: sh

      $ kubectl get handlers.config.istio.io
   –all-namespaces NAMESPACE NAME AGE istio-system kubernetesenv 4h
   istio-system prometheus 4h

   If you’re upgrading from Istio 1.1 or earlier, issue the following
   command instead:

   .. code:: sh

      $ kubectl get prometheuses.config.istio.io
   –all-namespaces NAMESPACE NAME AGE istio-system handler 13d {{< /text
   >}}

2. If the output shows no configured Prometheus handlers, you must
   reconfigure Mixer with the appropriate handler configuration.

   For reference, please consult the `default handler configuration for
   Prometheus <%7B%7B%3C%20github_file%20%3E%7D%7D/install/kubernetes/helm/istio/charts/mixer/templates/config.yaml>`_.

Verify Mixer metric instances configuration exists
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. In Kubernetes environments, issue the following command:

   .. code:: sh

      $ kubectl get instances -o
   custom-columns=NAME:.metadata.name,TEMPLATE:.spec.compiledTemplate
   –all-namespaces

   If you’re upgrading from Istio 1.1 or earlier, issue the following
   command instead:

   .. code:: sh

      $ kubectl get metrics.config.istio.io
   –all-namespaces

2. If the output shows no configured metric instances, you must
   reconfigure Mixer with the appropriate instance configuration.

   For reference, please consult the `default instances configuration
   for
   metrics <%7B%7B%3C%20github_file%20%3E%7D%7D/install/kubernetes/helm/istio/charts/mixer/templates/config.yaml>`_.

Verify there are no known configuration errors
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. To establish a connection to the Istio-telemetry self-monitoring
   endpoint, setup a port-forward to the Istio-telemetry self-monitoring
   port as described in `Verify Mixer is receiving Report
   calls <#verify-mixer-is-receiving-report-calls>`_.

2. For each of the following metrics, verify that the most up-to-date
   value is 0:

   -  ``mixer_config_adapter_info_config_errors_total``

   -  ``mixer_config_template_config_errors_total``

   -  ``mixer_config_instance_config_errors_total``

   -  ``mixer_config_rule_config_errors_total``

   -  ``mixer_config_rule_config_match_error_total``

   -  ``mixer_config_unsatisfied_action_handler_total``

   -  ``mixer_config_handler_validation_error_total``

   -  ``mixer_handler_handler_build_failures_total``

On the page showing Mixer self-monitoring port, search for each of the
metrics listed above. You should not find any values for those metrics
if everything is configured correctly.

If any of those metrics have a value, confirm that the metric value with
the largest configuration ID is 0. This will verify that Mixer has
generated no errors in processing the most recent configuration as
supplied.

Verify Mixer is sending metric instances to the Prometheus adapter
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Establish a connection to the ``istio-telemetry`` self-monitoring
   endpoint. Setup a port-forward to the ``istio-telemetry``
   self-monitoring port as described in `Verify Mixer is receiving
   Report calls <#verify-mixer-is-receiving-report-calls>`_.

2. On the Mixer self-monitoring port, search for
   ``mixer_runtime_dispatches_total``. The output should be similar to:

   {{< text plain >}}
   mixer_runtime_dispatches_total{adapter=“prometheus”,error=“false”,handler=“prometheus.istio-system”,meshFunction=“metric”}
   2532

3. Confirm that ``mixer_runtime_dispatches_total`` is present with the
   values:

   {{< text plain >}} adapter=“prometheus” error=“false”

   If you can’t find recorded dispatches to the Prometheus adapter,
   there is likely a configuration issue. Please follow the steps above
   to ensure everything is configured properly.

   If the dispatches to the Prometheus adapter report errors, check the
   Mixer logs to determine the source of the error. The most likely
   cause is a configuration issue for the handler listed in
   ``mixer_runtime_dispatches_total``.

4. Check the Mixer logs in a Kubernetes environment with:

   .. code:: sh

      $ kubectl -n istio-system logs -c mixer {{< /text
   >}}

Verify Prometheus configuration
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Connect to the Prometheus UI

2. Verify you can successfully scrape Mixer through the UI.

3. In Kubernetes environments, setup port-forwarding with:

   .. code:: sh

      $ istioctl dashboard prometheus

4. In the Prometheus browser window, select **Status** then **Targets**.

5. Confirm the target ``istio-mesh`` has a status of UP.

6. In the Prometheus browser window, select **Status** then
   **Configuration**.

7. Confirm an entry exists similar to:

   {{< text plain >}}

   -  job_name: ‘istio-mesh’ # Override the global default and scrape
      targets from this job every 5 seconds. scrape_interval: 5s #
      metrics_path defaults to ‘/metrics’ # scheme defaults to ‘http’.
      static_configs:
   -  targets: [‘istio-mixer.istio-system:42422’]

      .. raw:: html

         </td>


