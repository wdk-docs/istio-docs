announcing-0.6
========================

In addition to the usual pile of bug fixes and performance improvements,
this release includes the new or updated features detailed below.

{{< relnote >}}

Networking
----------

-  **Custom Envoy Configuration**. Pilot now supports ferrying custom
   Envoy configuration to the proxy. `Learn
   more <https://github.com/mandarjog/istioluawebhook>`_

Mixer adapters
--------------

-  **SolarWinds**. Mixer can now interface to AppOptics and Papertrail.
   `Learn
   more </docs/reference/config/policy-and-telemetry/adapters/solarwinds/>`_

-  **Redis Quota**. Mixer now supports a Redis-based adapter for rate
   limit tracking. `Learn
   more </docs/reference/config/policy-and-telemetry/adapters/redisquota/>`_

-  **Datadog**. Mixer now provides an adapter to deliver metric data to
   a Datadog agent. `Learn
   more </docs/reference/config/policy-and-telemetry/adapters/datadog/>`_

Other
-----

-  **Separate Check & Report Clusters**. When configuring Envoy, it’s
   now possible to use different clusters for Mixer instances that are
   used for Mixer’s Check functionality from those used for Mixer’s
   Report functionality. This may be useful in large deployments for
   better scaling of Mixer instances.

-  **Monitoring Dashboards**. There are now preliminary Mixer & Pilot
   monitoring dashboard in Grafana.

-  **Liveness and Readiness Probes**. Istio components now provide
   canonical liveness and readiness probe support to help ensure mesh
   infrastructure health. `Learn
   more </docs/tasks/security/citadel-config/health-check/>`_

-  **Egress Policy and Telemetry**. Istio can monitor traffic to
   external services defined by ``EgressRule`` or External Service.
   Istio can also apply Mixer policies on this traffic.
