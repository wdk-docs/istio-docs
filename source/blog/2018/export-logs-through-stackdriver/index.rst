export-logs-through-stackdriver
================================================

This post shows how to direct Istio logs to
`Stackdriver <https://cloud.google.com/stackdriver/>`_ and export those
logs to various configured sinks such as such as
`BigQuery <https://cloud.google.com/bigquery/>`_, `Google Cloud
Storage <https://cloud.google.com/storage/>`_ or `Cloud
Pub/Sub <https://cloud.google.com/pubsub/>`_. At the end of this post
you can perform analytics on Istio data from your favorite places such
as BigQuery, GCS or Cloud Pub/Sub.

The `Bookinfo </docs/examples/bookinfo/>`_ sample application is used
as the example application throughout this task.

Before you begin
----------------

`Install Istio </docs/setup/>`_ in your cluster and deploy an
application.

Configuring Istio to export logs
--------------------------------

Istio exports logs using the ``logentry``
`template </docs/reference/config/policy-and-telemetry/templates/logentry>`_.
This specifies all the variables that are available for analysis. It
contains information like source service, destination service, auth
metrics (coming..) among others. Following is a diagram of the pipeline:

.. image:: ./istio-analytics-using-stackdriver.png
   :alt: Exporting logs from Istio to Stackdriver for analysis
   :width: “75%

Istio supports exporting logs to Stackdriver which can in turn be
configured to export logs to your favorite sink like BigQuery, Pub/Sub
or GCS. Please follow the steps below to setup your favorite sink for
exporting logs first and then Stackdriver in Istio.

Setting up various log sinks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Common setup for all sinks:

1. Enable `Stackdriver Monitoring API <https://cloud.google.com/monitoring/api/enable-api>`_ for the project.
2. Make sure ``principalEmail`` that would be setting up the sink has write access to the project and Logging Admin role permissions.
3. Make sure the ``GOOGLE_APPLICATION_CREDENTIALS`` environment variable
   is set. Please follow instructions
   `here <https://cloud.google.com/docs/authentication/getting-started>`_
   to set it up.

BigQuery
^^^^^^^^

1. `Create a BigQuery
   dataset <https://cloud.google.com/bigquery/docs/datasets>`_ as a
   destination for the logs export.
2. Record the ID of the dataset. It will be needed to configure the
   Stackdriver handler. It would be of the form
   ``bigquery.googleapis.com/projects/[PROJECT_ID]/datasets/[DATASET_ID]``
3. Give `sink’s writer
   identity <https://cloud.google.com/logging/docs/api/tasks/exporting-logs#writing_to_the_destination>`_:
   ``cloud-logs@system.gserviceaccount.com`` BigQuery Data Editor role
   in IAM.
4. If using `Google Kubernetes
   Engine </docs/setup/platform-setup/gke/>`_, make sure ``bigquery``
   `Scope <https://cloud.google.com/sdk/gcloud/reference/container/clusters/create>`_
   is enabled on the cluster.

Google Cloud Storage (GCS)
^^^^^^^^^^^^^^^^^^^^^^^^^^

1. `Create a GCS
   bucket <https://cloud.google.com/storage/docs/creating-buckets>`_
   where you would like logs to get exported in GCS.
2. Recode the ID of the bucket. It will be needed to configure
   Stackdriver. It would be of the form
   ``storage.googleapis.com/[BUCKET_ID]``
3. Give `sink’s writer
   identity <https://cloud.google.com/logging/docs/api/tasks/exporting-logs#writing_to_the_destination>`_:
   ``cloud-logs@system.gserviceaccount.com`` Storage Object Creator role
   in IAM.

Google Cloud Pub/Sub
^^^^^^^^^^^^^^^^^^^^

1. `Create a topic <https://cloud.google.com/pubsub/docs/admin>`_ where
   you would like logs to get exported in Google Cloud Pub/Sub.
2. Recode the ID of the topic. It will be needed to configure
   Stackdriver. It would be of the form
   ``pubsub.googleapis.com/projects/[PROJECT_ID]/topics/[TOPIC_ID]``
3. Give `sink’s writer
   identity <https://cloud.google.com/logging/docs/api/tasks/exporting-logs#writing_to_the_destination>`_:
   ``cloud-logs@system.gserviceaccount.com`` Pub/Sub Publisher role in
   IAM.
4. If using `Google Kubernetes
   Engine </docs/setup/platform-setup/gke/>`_, make sure ``pubsub``
   `Scope <https://cloud.google.com/sdk/gcloud/reference/container/clusters/create>`_
   is enabled on the cluster.

Setting up Stackdriver
~~~~~~~~~~~~~~~~~~~~~~

A Stackdriver handler must be created to export data to Stackdriver. The
configuration for a Stackdriver handler is described
`here </docs/reference/config/policy-and-telemetry/adapters/stackdriver/>`_.

1. Save the following yaml file as ``stackdriver.yaml``. Replace
   ``<project_id>, <sink_id>, <sink_destination>, <log_filter>`` with
   their specific values.

   .. code:: yaml

    apiVersion: “config.istio.io/v1alpha2” kind:
   stackdriver metadata: name: handler namespace: istio-system spec: #
   We’ll use the default value from the adapter, once per minute, so we
   don’t need to supply a value. # pushInterval: 1m # Must be supplied
   for the Stackdriver adapter to work project_id: “” # One of the
   following must be set; the preferred method is ``appCredentials``,
   which corresponds to # Google Application Default Credentials. # If
   none is provided we default to app credentials. # appCredentials: #
   apiKey: # serviceAccountPath: # Describes how to map Istio logs into
   Stackdriver. logInfo: accesslog.logentry.istio-system:
   payloadTemplate: ‘{{or (.sourceIp) “-”}} - {{or (.sourceUser) “-”}}
   [{{or (.timestamp.Format “02/Jan/2006:15:04:05 -0700”) “-”}}] “{{or
   (.method)”-“}} {{or (.url)”-“}} {{or (.protocol)”-“}}” {{or
   (.responseCode) “-”}} {{or (.responseSize) “-”}}’ httpMapping: url:
   url status: responseCode requestSize: requestSize responseSize:
   responseSize latency: latency localIp: sourceIp remoteIp:
   destinationIp method: method userAgent: userAgent referer: referer
   labelNames: - sourceIp - destinationIp - sourceService - sourceUser -
   sourceNamespace - destinationIp - destinationService -
   destinationNamespace - apiClaims - apiKey - protocol - method - url -
   responseCode - responseSize - requestSize - latency - connectionMtls
   - userAgent - responseTimestamp - receivedBytes - sentBytes - referer
   sinkInfo: id: ‘’ destination: ‘’ filter: ‘’ — apiVersion:
   “config.istio.io/v1alpha2” kind: rule metadata: name: stackdriver
   namespace: istio-system spec: match: “true” # If omitted match is
   true. actions:

   -  handler: handler.stackdriver instances:

      -  .. rubric:: accesslog.logentry
            :name: accesslog.logentry



2. Push the configuration

   .. code:: sh

      $ kubectl apply -f stackdriver.yaml stackdriver
   “handler” created rule “stackdriver” created logentry
   “stackdriverglobalmr” created metric “stackdriverrequestcount”
   created metric “stackdriverrequestduration” created metric
   “stackdriverrequestsize” created metric “stackdriverresponsesize”
   created

3. Send traffic to the sample application.

   For the Bookinfo sample, visit ``http://$GATEWAY_URL/productpage`` in
   your web browser or issue the following command:

   .. code:: sh

      $ curl http://$GATEWAY_URL/productpage {{< /text
   >}}

4. Verify that logs are flowing through Stackdriver to the configured
   sink.

   -  Stackdriver: Navigate to the `Stackdriver Logs
      Viewer <https://pantheon.corp.google.com/logs/viewer>`_ for your
      project and look under “GKE Container” -> “Cluster Name” ->
      “Namespace Id” for Istio Access logs.
   -  BigQuery: Navigate to the `BigQuery
      Interface <https://bigquery.cloud.google.com/>`_ for your project
      and you should find a table with prefix
      ``accesslog_logentry_istio`` in your sink dataset.
   -  GCS: Navigate to the `Storage
      Browser <https://pantheon.corp.google.com/storage/browser/>`_ for
      your project and you should find a bucket named
      ``accesslog.logentry.istio-system`` in your sink bucket.
   -  Pub/Sub: Navigate to the `Pub/Sub Topic
      List <https://pantheon.corp.google.com/cloudpubsub/topicList>`_
      for your project and you should find a topic for ``accesslog`` in
      your sink topic.

Understanding what happened
---------------------------

``Stackdriver.yaml`` file above configured Istio to send access logs to
Stackdriver and then added a sink configuration where these logs could
be exported. In detail as follows:

1. Added a handler of kind ``stackdriver``

   .. code:: yaml

    apiVersion: “config.istio.io/v1alpha2” kind:
   stackdriver metadata: name: handler namespace:

2. Added ``logInfo`` in spec

   .. code:: yaml

    spec: logInfo: accesslog.logentry.istio-system:
   labelNames: - sourceIp - destinationIp … … sinkInfo: id: ‘’
   destination: ‘’ filter: ‘’

   In the above configuration sinkInfo contains information about the
   sink where you want the logs to get exported to. For more information
   on how this gets filled for different sinks please refer
   `here <https://cloud.google.com/logging/docs/export/#sink-terms>`_.

3. Added a rule for Stackdriver

   .. code:: yaml

    apiVersion: “config.istio.io/v1alpha2” kind: rule
   metadata: name: stackdriver namespace: istio-system spec: match:
   “true” # If omitted match is true actions:

   -  handler: handler.stackdriver instances:

      -  accesslog.logentry

Cleanup
-------

-  Remove the new Stackdriver configuration:

   .. code:: sh

      $ kubectl delete -f stackdriver.yaml

-  If you are not planning to explore any follow-on tasks, refer to the
   `Bookinfo cleanup </docs/examples/bookinfo/#cleanup>`_ instructions
   to shutdown the application.

Availability of logs in export sinks
------------------------------------

Export to BigQuery is within minutes (we see it to be almost instant),
GCS can have a delay of 2 to 12 hours and Pub/Sub is almost immediately.
