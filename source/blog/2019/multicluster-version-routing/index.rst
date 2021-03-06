multicluster-version-routing
================================================

If you’ve spent any time looking at Istio, you’ve probably noticed that
it includes a lot of features that can be demonstrated with simple
`tasks </docs/tasks/>`_ and `examples </docs/examples/>`_ running on a
single Kubernetes cluster. Because most, if not all, real-world cloud
and microservices-based applications are not that simple and will need
to have the services distributed and running in more than one location,
you may be wondering if all these things will be just as simple in your
real production environment.

Fortunately, Istio provides several ways to configure a service mesh so
that applications can, more-or-less transparently, be part of a mesh
where the services are running in more than one cluster, i.e., in a
`multicluster
deployment </docs/ops/deployment/deployment-models/#multiple-clusters>`_.
The simplest way to set up a multicluster mesh, because it has no
special networking requirements, is using a replicated `control plane
model </docs/ops/deployment/deployment-models/#control-plane-models>`_.
In this configuration, each Kubernetes cluster contributing to the mesh
has its own control plane, but each control plane is synchronized and
running under a single administrative control.

In this article we’ll look at how one of the features of Istio, `traffic
management </docs/concepts/traffic-management/>`_, works in a
multicluster mesh with a dedicated control plane topology. We’ll show
how to configure Istio route rules to call remote services in a
multicluster service mesh by deploying the `Bookinfo
sample <%7B%7B%3C%20github_tree%20%3E%7D%7D/samples/bookinfo>`_ with
version ``v1`` of the ``reviews`` service running in one cluster,
versions ``v2`` and ``v3`` running in a second cluster.

Set up clusters
---------------

To start, you’ll need two Kubernetes clusters, both running a slightly
customized configuration of Istio.

-  Set up a multicluster environment with two Istio clusters by
   following the `replicated control
   planes </docs/setup/install/multicluster/gateways/>`_ instructions.

-  The ``kubectl`` command is used to access both clusters with the
   ``--context`` flag. Use the following command to list your contexts:

   .. code:: sh

      $ kubectl config get-contexts CURRENT NAME CLUSTER
   AUTHINFO NAMESPACE

   -  ::

             cluster1   cluster1   user@foo.com   default
             cluster2   cluster2   user@foo.com   default



-  Export the following environment variables with the context names of
   your configuration:

   .. code:: sh

      $ export CTX_CLUSTER1= $ export CTX_CLUSTER2=

Deploy version v1 of the ``bookinfo`` application in ``cluster1``
-----------------------------------------------------------------

Run the ``productpage`` and ``details`` services and version ``v1`` of
the ``reviews`` service in ``cluster1``:

.. code:: sh

      $ kubectl label –context=$CTX_CLUSTER1 namespace
default istio-injection=enabled $ kubectl apply –context=$CTX_CLUSTER1
-f - <<EOF apiVersion: v1 kind: Service metadata: name: productpage
labels: app: productpage spec: ports: - port: 9080 name: http selector:
app: productpage — apiVersion: extensions/v1beta1 kind: Deployment
metadata: name: productpage-v1 spec: replicas: 1 template: metadata:
labels: app: productpage version: v1 spec: containers: - name:
productpage image: istio/examples-bookinfo-productpage-v1:1.10.0
imagePullPolicy: IfNotPresent ports: - containerPort: 9080 — apiVersion:
v1 kind: Service metadata: name: details labels: app: details spec:
ports: - port: 9080 name: http selector: app: details — apiVersion:
extensions/v1beta1 kind: Deployment metadata: name: details-v1 spec:
replicas: 1 template: metadata: labels: app: details version: v1 spec:
containers: - name: details image:
istio/examples-bookinfo-details-v1:1.10.0 imagePullPolicy: IfNotPresent
ports: - containerPort: 9080 — apiVersion: v1 kind: Service metadata:
name: reviews labels: app: reviews spec: ports: - port: 9080 name: http
selector: app: reviews — apiVersion: extensions/v1beta1 kind: Deployment
metadata: name: reviews-v1 spec: replicas: 1 template: metadata: labels:
app: reviews version: v1 spec: containers: - name: reviews image:
istio/examples-bookinfo-reviews-v1:1.10.0 imagePullPolicy: IfNotPresent
ports: - containerPort: 9080 EOF

Deploy ``bookinfo`` v2 and v3 services in ``cluster2``
------------------------------------------------------

Run the ``ratings`` service and version ``v2`` and ``v3`` of the
``reviews`` service in ``cluster2``:

.. code:: sh

      $ kubectl label –context=$CTX_CLUSTER2 namespace
default istio-injection=enabled $ kubectl apply –context=$CTX_CLUSTER2
-f - <<EOF apiVersion: v1 kind: Service metadata: name: ratings labels:
app: ratings spec: ports: - port: 9080 name: http selector: app: ratings
— apiVersion: extensions/v1beta1 kind: Deployment metadata: name:
ratings-v1 spec: replicas: 1 template: metadata: labels: app: ratings
version: v1 spec: containers: - name: ratings image:
istio/examples-bookinfo-ratings-v1:1.10.0 imagePullPolicy: IfNotPresent
ports: - containerPort: 9080 — apiVersion: v1 kind: Service metadata:
name: reviews labels: app: reviews spec: ports: - port: 9080 name: http
selector: app: reviews — apiVersion: extensions/v1beta1 kind: Deployment
metadata: name: reviews-v2 spec: replicas: 1 template: metadata: labels:
app: reviews version: v2 spec: containers: - name: reviews image:
istio/examples-bookinfo-reviews-v2:1.10.0 imagePullPolicy: IfNotPresent
ports: - containerPort: 9080 — apiVersion: extensions/v1beta1 kind:
Deployment metadata: name: reviews-v3 spec: replicas: 1 template:
metadata: labels: app: reviews version: v3 spec: containers: - name:
reviews image: istio/examples-bookinfo-reviews-v3:1.10.0
imagePullPolicy: IfNotPresent ports: - containerPort: 9080 EOF {{< /text
>}}

Access the ``bookinfo`` application
-----------------------------------

Just like any application, we’ll use an Istio gateway to access the
``bookinfo`` application.

-  Create the ``bookinfo`` gateway in ``cluster1``:

   .. code:: sh

      $ kubectl apply –context=$CTX_CLUSTER1 -f
   @samples/bookinfo/networking/bookinfo-gateway.yaml@

-  Follow the `Bookinfo sample
   instructions </docs/examples/bookinfo/#determine-the-ingress-ip-and-port>`_
   to determine the ingress IP and port and then point your browser to
   ``http://$GATEWAY_URL/productpage``.

You should see the ``productpage`` with reviews, but without ratings,
because only ``v1`` of the ``reviews`` service is running on
``cluster1`` and we have not yet configured access to ``cluster2``.

Create a service entry and destination rule on ``cluster1`` for the remote reviews service
------------------------------------------------------------------------------------------

As described in the `setup
instructions </docs/setup/install/multicluster/gateways/#setup-dns>`_,
remote services are accessed with a ``.global`` DNS name. In our case,
it’s ``reviews.default.global``, so we need to create a service entry
and destination rule for that host. The service entry will use the
``cluster2`` gateway as the endpoint address to access the service. You
can use the gateway’s DNS name, if it has one, or its public IP, like
this:

| .. code:: sh

      $ export
  CLUSTER2_GW_ADDR=\ :math:`(kubectl get --context=`\ CTX_CLUSTER2 svc
  –selector=app=istio-ingressgateway
| -n istio-system -o
  jsonpath=“{.items[0].status.loadBalancer.ingress[0].ip}”) {{< /text
  >}}

Now create the service entry and destination rule using the following
command:

.. code:: sh

      $ kubectl apply –context=$CTX_CLUSTER1 -f - <<EOF
apiVersion: networking.istio.io/v1alpha3 kind: ServiceEntry metadata:
name: reviews-default spec: hosts: - reviews.default.global location:
MESH_INTERNAL ports: - name: http1 number: 9080 protocol: http
resolution: DNS addresses: - 240.0.0.3 endpoints: - address:
${CLUSTER2_GW_ADDR} labels: cluster: cluster2 ports: http1: 15443 # Do
not change this port value — apiVersion: networking.istio.io/v1alpha3
kind: DestinationRule metadata: name: reviews-global spec: host:
reviews.default.global trafficPolicy: tls: mode: ISTIO_MUTUAL subsets: -
name: v2 labels: cluster: cluster2 - name: v3 labels: cluster: cluster2
EOF

The address ``240.0.0.3`` of the service entry can be any arbitrary
unallocated IP. Using an IP from the class E addresses range 240.0.0.0/4
is a good choice. Check out the `gateway-connected multicluster
example </docs/setup/install/multicluster/gateways/#configure-the-example-services>`_
for more details.

Note that the labels of the subsets in the destination rule map to the
service entry endpoint label (``cluster: cluster2``) corresponding to
the ``cluster2`` gateway. Once the request reaches the destination
cluster, a local destination rule will be used to identify the actual
pod labels (``version: v1`` or ``version: v2``) corresponding to the
requested subset.

Create a destination rule on both clusters for the local reviews service
------------------------------------------------------------------------

Technically, we only need to define the subsets of the local service
that are being used in each cluster (i.e., ``v1`` in ``cluster1``,
``v2`` and ``v3`` in ``cluster2``), but for simplicity we’ll just define
all three subsets in both clusters, since there’s nothing wrong with
defining subsets for versions that are not actually deployed.

.. code:: sh

      $ kubectl apply –context=$CTX_CLUSTER1 -f - <<EOF
apiVersion: networking.istio.io/v1alpha3 kind: DestinationRule metadata:
name: reviews spec: host: reviews.default.svc.cluster.local
trafficPolicy: tls: mode: ISTIO_MUTUAL subsets: - name: v1 labels:
version: v1 - name: v2 labels: version: v2 - name: v3 labels: version:
v3 EOF

.. code:: sh

      $ kubectl apply –context=$CTX_CLUSTER2 -f - <<EOF
apiVersion: networking.istio.io/v1alpha3 kind: DestinationRule metadata:
name: reviews spec: host: reviews.default.svc.cluster.local
trafficPolicy: tls: mode: ISTIO_MUTUAL subsets: - name: v1 labels:
version: v1 - name: v2 labels: version: v2 - name: v3 labels: version:
v3 EOF

Create a virtual service to route reviews service traffic
---------------------------------------------------------

At this point, all calls to the ``reviews`` service will go to the local
``reviews`` pods (``v1``) because if you look at the source code you
will see that the ``productpage`` implementation is simply making
requests to ``http://reviews:9080`` (which expands to host
``reviews.default.svc.cluster.local``), the local version of the
service. The corresponding remote service is named
``reviews.default.global``, so route rules are needed to redirect
requests to the global host.

.. note::

   Note that if all of the versions of the ``reviews`` service
were remote, so there is no local ``reviews`` service defined, the DNS
would resolve ``reviews`` directly to ``reviews.default.global``. In
that case we could call the remote ``reviews`` service without any route
rules.

Apply the following virtual service to direct traffic for user ``jason``
to ``reviews`` versions ``v2`` and ``v3`` (50/50) which are running on
``cluster2``. Traffic for any other user will go to ``reviews`` version
``v1``.

.. code:: sh

      $ kubectl apply –context=$CTX_CLUSTER1 -f - <<EOF
apiVersion: networking.istio.io/v1alpha3 kind: VirtualService metadata:
name: reviews spec: hosts: - reviews.default.svc.cluster.local http: -
match: - headers: end-user: exact: jason route: - destination: host:
reviews.default.global subset: v2 weight: 50 - destination: host:
reviews.default.global subset: v3 weight: 50 - route: - destination:
host: reviews.default.svc.cluster.local subset: v1 EOF

.. note::

   This 50/50 rule isn’t a particularly realistic example. It’s
just a convenient way to demonstrate accessing multiple subsets of a
remote service.

Return to your browser and login as user ``jason``. If you refresh the
page several times, you should see the display alternating between black
and red ratings stars (``v2`` and ``v3``). If you logout, you will only
see reviews without ratings (``v1``).

Summary
-------

In this article, we’ve seen how to use Istio route rules to distribute
the versions of a service across clusters in a multicluster service mesh
with a replicated control plane model. In this example, we manually
configured the ``.global`` service entry and destination rules needed to
provide connectivity to one remote service, ``reviews``. In general,
however, if we wanted to enable any service to run either locally or
remotely, we would need to create ``.global`` resources for every
service. Fortunately, this process could be automated and likely will be
in a future Istio release.
