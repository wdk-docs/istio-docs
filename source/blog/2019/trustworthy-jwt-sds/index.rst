trustworthy-jwt-sds
================================================

In Istio 1.3, we are taking advantage of improvements in Kubernetes to
issue certificates for workload instances more securely.

When a Citadel Agent sends a certificate signing request to Citadel to
get a certificate for a workload instance, it includes the JWT that the
Kubernetes API server issued representing the service account of the
workload instance. If Citadel can authenticate the JWT, it extracts the
service account name needed to issue the certificate for the workload
instance.

Before Kubernetes 1.12, the Kubernetes API server issues JWTs with the
following issues:

1. The tokens don’t have important fields to limit their scope of usage,
   such as ``aud`` or ``exp``. See `Bound Service
   Tokens <https://github.com/kubernetes/community/blob/master/contributors/design-proposals/auth/bound-service-account-tokens.md>`_
   for more info.
2. The tokens are mounted onto all the pods without a way to opt-out.
   See `Service Account Token
   Volumes <https://github.com/kubernetes/community/blob/master/contributors/design-proposals/storage/svcacct-token-volume-source.md>`_
   for motivation.

Kubernetes 1.12 introduces ``trustworthy`` JWTs to solve these issues.
However, support for the ``aud`` field to have a different value than
the API server audience didn’t become available until `Kubernetes
1.13 <https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.13.md>`_.
To better secure the mesh, Istio 1.3 only supports ``trustworthy`` JWTs
and requires the value of the ``aud`` field to be ``istio-ca`` when you
enable SDS. Before upgrading your Istio deployment to 1.3 with SDS
enabled, verify that you use Kubernetes 1.13 or later.

Make the following considerations based on your platform of choice:

-  **GKE:** Upgrade your cluster version to at least 1.13.
-  **On-prem Kubernetes** and **GKE on-prem:** Add `extra
   configurations <https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/#service-account-token-volume-projection>`_
   to your Kubernetes. You may also want to refer to the `api-server
   page <https://kubernetes.io/docs/reference/command-line-tools-reference/kube-apiserver/>`_
   for the most up-to-date flag names.
-  For other platforms, check with your provider. If your vendor does
   not support trustworthy JWTs, you will need to fall back to the
   file-mount approach to propagate the workload keys and certificates
   in Istio 1.3.
