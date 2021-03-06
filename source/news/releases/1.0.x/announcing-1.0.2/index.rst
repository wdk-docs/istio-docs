announcing-1.0.2
=============================

We’re pleased to announce the availability of Istio 1.0.2. Please see
below for what’s changed.

{{< relnote >}}

General
-------

-  Fixed bug in Envoy where the sidecar would crash if receiving normal
   traffic on the mutual TLS port.

-  Fixed bug with Pilot propagating incomplete updates to Envoy in a
   multicluster environment.

-  Added a few more Helm options for Grafana.

-  Improved Kubernetes service registry queue performance.

-  Fixed bug where ``istioctl proxy-status`` was not showing the patch
   version.

-  Add validation of virtual service SNI hosts.
