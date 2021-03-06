announcing-1.4.1
==========================

This release includes bug fixes to improve robustness. This release note
describes what’s different between Istio 1.4.0 and Istio 1.4.1.

{{< relnote >}}

Bug fixes
---------

-  **Fixed** ``istioctl`` installation on Windows (`Issue
   19020 <https://github.com/istio/istio/pull/19020>`_).
-  **Fixed** an issue with route matching order when using cert-manager
   with Kubernetes Ingress (`Issue
   19000 <https://github.com/istio/istio/pull/19000>`_).
-  **Fixed** Mixer source namespace attribute when the pod name contains
   a period (`Issue
   19015 <https://github.com/istio/istio/issues/19015>`_).
-  **Fixed** excessive metrics generated by Galley (`Issue
   19165 <https://github.com/istio/istio/issues/19165>`_).
-  **Fixed** tracing Service port to correctly listen on port 80 (`Issue
   19227 <https://github.com/istio/istio/issues/19227>`_).
-  **Fixed** missing ``istioctl`` auto-completion files (`Issue
   19297 <https://github.com/istio/istio/issues/19297>`_).
