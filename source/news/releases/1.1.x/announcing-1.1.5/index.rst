announcing-1.1.5
=========================

We’re pleased to announce the availability of Istio 1.1.5. Please see
below for what’s changed.

{{< relnote >}}

Bug fixes
---------

-  Add additional validation to Pilot to reject gateway configuration
   with overlapping hosts matches (`Issue
   13717 <https://github.com/istio/istio/issues/13717>`_).
-  Build against the latest stable version of ``istio-cni`` instead of
   the latest daily build (`Issue
   13171 <https://github.com/istio/istio/issues/13171>`_).

Small enhancements
------------------

-  Add additional logging to help diagnose hostname resolution failures
   (`Issue 13581 <https://github.com/istio/istio/issues/13581>`_).
-  Improve ease of installing ``prometheus`` by removing unnecessary use
   of ``busybox`` image (`Issue
   13501 <https://github.com/istio/istio/issues/13501>`_).
-  Make Pilot Agent’s certificate paths configurable (`Issue
   11984 <https://github.com/istio/istio/issues/11984>`_).
