announcing-1.0.5
=============================

We’re pleased to announce the availability of Istio 1.0.5. Please see
below for what’s changed.

{{< relnote >}}

General
-------

-  Disabled the precondition cache in the ``istio-policy`` service as it
   lead to invalid results. The cache will be reintroduced in a later
   release.

-  Mixer now only generates spans when there is an enabled ``tracespan``
   adapter, resulting in lower CPU overhead in normal cases.

-  Fixed a problem that could lead Pilot to hang.
