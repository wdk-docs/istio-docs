metrics
==================

The following are the standard service level metrics exported by Istio.
Istio standard metrics are directly exported by the Envoy proxy since
Istio 1.5. In prior Istio releases Mixer produced these metrics.

Metrics
-------

For HTTP, HTTP/2, and GRPC traffic, Istio generates the following
metrics:

-  **Request Count** (``istio_requests_total``): This is a ``COUNTER``
   incremented for every request handled by an Istio proxy.

-  **Request Duration** (``istio_request_duration_seconds``): This is a
   ``DISTRIBUTION`` which measures the duration of requests.

-  **Request Size** (``istio_request_bytes``): This is a
   ``DISTRIBUTION`` which measures HTTP request body sizes.

-  **Response Size** (``istio_response_bytes``): This is a
   ``DISTRIBUTION`` which measures HTTP response body sizes.

For TCP traffic, Istio generates the following metrics:

-  **Tcp Byte Sent** (``istio_tcp_sent_bytes_total``): This is a
   ``COUNTER`` which measures the size of total bytes sent during
   response in case of a TCP connection.

-  **Tcp Byte Received** (``istio_tcp_received_bytes_total``): This is a
   ``COUNTER`` which measures the size of total bytes received during
   request in case of a TCP connection.

-  **Tcp Connections Opened** (``istio_tcp_connections_opened_total``):
   This is a ``COUNTER`` incremented for every opened connection.

-  **Tcp Connections Closed** (``istio_tcp_connections_closed_total``):
   This is a ``COUNTER`` incremented for every closed connection.

Labels
------

-  **Reporter**: This identifies the reporter of the request. It is set
   to ``destination`` if report is from a server Istio proxy and
   ``source`` if report is from a client Istio proxy.

   .. code:: yaml

    reporter: conditional((context.reporter.kind \|
   “inbound”) == “outbound”, “source”, “destination”)

-  **Source Workload**: This identifies the name of source workload
   which controls the source.

   .. code:: yaml

    source_workload: source.workload.name \| “unknown”


-  **Source Workload Namespace**: This identifies the namespace of the
   source workload.

   .. code:: yaml

    source_workload_namespace:
   source.workload.namespace \| “unknown”

-  **Source Principal**: This identifies the peer principal of the
   traffic source. It is set when peer authentication is used.

   .. code:: yaml

    source_principal: source.principal \| “unknown”

-  **Source App**: This identifies the source app based on ``app`` label
   of the source workload.

   .. code:: yaml

    source_app: source.labels[“app”] \| “unknown”

-  **Source Version**: This identifies the version of the source
   workload.

   .. code:: yaml

    source_version: source.labels[“version”] \|
   “unknown”

-  **Destination Workload**: This identifies the name of destination
   workload.

   .. code:: yaml

    destination_workload: destination.workload.name \|
   “unknown”

-  **Destination Workload Namespace**: This identifies the namespace of
   the destination workload.

   .. code:: yaml

    destination_workload_namespace:
   destination.workload.namespace \| “unknown”

-  **Destination Principal**: This identifies the peer principal of the
   traffic destination. It is set when peer authentication is used.

   .. code:: yaml

    destination_principal: destination.principal \|
   “unknown”

-  **Destination App**: This identifies the destination app based on
   ``app`` label of the destination workload.

   .. code:: yaml

    destination_app: destination.labels[“app”] \|
   “unknown”

-  **Destination Version**: This identifies the version of the
   destination workload.

   .. code:: yaml

    destination_version: destination.labels[“version”]
   \| “unknown”

-  **Destination Service**: This identifies destination service host
   responsible for an incoming request. Ex:
   ``details.default.svc.cluster.local``.

   .. code:: yaml

    destination_service: destination.service.host \|
   “unknown”

-  **Destination Service Name**: This identifies the destination service
   name. Ex: “details”.

   .. code:: yaml

    destination_service_name: destination.service.name
   \| “unknown”

-  **Destination Service Namespace**: This identifies the namespace of
   destination service.

   .. code:: yaml

    destination_service_namespace:
   destination.service.namespace \| “unknown”

-  **Request Protocol**: This identifies the protocol of the request. It
   is set to API protocol if provided, otherwise request or connection
   protocol.

   .. code:: yaml

    request_protocol: api.protocol \| context.protocol
   \| “unknown”

-  **Response Code**: This identifies the response code of the request.
   This label is present only on HTTP metrics.

   .. code:: yaml

    response_code: response.code \| 200

-  **Connection Security Policy**: This identifies the service
   authentication policy of the request. It is set to ``mutual_tls``
   when Istio is used to make communication secure and report is from
   destination. It is set to ``unknown`` when report is from source
   since security policy cannot be properly populated.

   .. code:: yaml

    connection_security_policy:
   conditional((context.reporter.kind \| “inbound”) == “outbound”,
   “unknown”, conditional(connection.mtls \| false, “mutual_tls”,
   “none”))

-  **Response Flags**: Additional details about the response or
   connection from proxy. In case of Envoy, see ``%RESPONSE_FLAGS%`` in
   `Envoy Access
   Log <https://www.envoyproxy.io/docs/envoy/latest/configuration/observability/access_log#configuration>`_
   for more detail.

   .. code:: yaml

    response_flags: context.proxy_error_code \| “-”

-  **Canonical Service**: A workload belongs to exactly one canonical
   service, whereas it can belong to multiple services. A canonical
   service has a name and a revision so it results in the following
   labels.

   .. code:: yaml

    source_canonical_service source_canonical_revision
   destination_canonical_service destination_canonical_revision
