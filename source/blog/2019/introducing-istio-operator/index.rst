introducing-istio-operator
================================================

Kubernetes
`operators <https://kubernetes.io/docs/concepts/extend-kubernetes/operator/>`_
provide a pattern for encoding human operational knowledge in software
and are a popular way to simplify the administration of software
infrastructure components. Istio is a natural candidate for an automated
operator as it is challenging to administer.

Up until now, `Helm <https://github.com/helm/helm>`_ has been the
primary tool to install and upgrade Istio. Istio 1.4 introduces a new
method of `installation using {{< istioctl
>}} </docs/setup/install/istioctl/>`_. This new installation method
builds on the strengths of Helm with the addition of the following:

-  Users only need to install one tool: ``istioctl``
-  All API fields are validated
-  Small customizations not in the API don’t require chart or API
   changes
-  Version specific upgrade hooks can be easily and robustly implemented

The `Helm installation </docs/setup/install/helm/>`_ method is in the
process of deprecation. Upgrading from Istio 1.4 with a version not
initially installed with Helm will also be replaced by a new `{{<
istioctl >}} upgrade feature </docs/setup/upgrade/istioctl-upgrade/>`_.

The new ``istioctl`` installation commands use a `custom
resource <https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/>`_
to configure the installation. The custom resource is part of a new
Istio operator implementation intended to simplify the common
administrative tasks of installation, upgrade, and complex configuration
changes for Istio. Validation and checking for installation and upgrade
is tightly integrated with the tools to prevent common errors and
simplify troubleshooting.

The Operator API
----------------

Every operator implementation requires a `custom resource definition
(CRD) <https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/#customresourcedefinitions>`_
to define its custom resource, that is, its API. Istio’s operator API is
defined by the `IstioControlPlane
CRD <https://archive.istio.io/v1.4/docs/reference/config/istio.operator.v1alpha12.pb/>`_,
which is generated from an `IstioControlPlane
proto <https://github.com/istio/operator/blob/release-1.4/pkg/apis/istio/v1alpha2/istiocontrolplane_types.proto>`_.
The API supports all of Istio’s current `configuration
profiles </docs/setup/additional-setup/config-profiles/>`_ using a
single field to select the profile. For example, the following
``IstioControlPlane`` resource configures Istio using the ``demo``
profile:

.. code:: yaml

    apiVersion: install.istio.io/v1alpha2 kind:
IstioControlPlane metadata: namespace: istio-operator name:
example-istiocontrolplane spec: profile: demo

You can then customize the configuration with additional settings. For
example, to disable telemetry:

.. code:: yaml

    apiVersion: install.istio.io/v1alpha2 kind:
IstioControlPlane metadata: namespace: istio-operator name:
example-istiocontrolplane spec: profile: demo telemetry: enabled: false


Installing with {{< istioctl >}}
--------------------------------

The recommended way to use the Istio operator API is through a new set
of ``istioctl`` commands. For example, to install Istio into a cluster:

.. code:: sh

      $ istioctl manifest apply -f

Make changes to the installation configuration by editing the
configuration file and executing ``istioctl manifest apply`` again.

To upgrade to a new version of Istio:

.. code:: sh

      $ istioctl x upgrade -f

In addition to specifying the complete configuration in an
``IstioControlPlane`` resource, the ``istioctl`` commands can also be
passed individual settings using a ``--set`` flag:

.. code:: sh

      $ istioctl manifest apply –set telemetry.enabled=false


There are also a number of other ``istioctl`` commands that, for
example, help you list, display, and compare configuration profiles and
manifests.

Refer to the Istio `install
instructions </docs/setup/install/istioctl>`_ for more details.

Istio Controller (alpha)
------------------------

Operator implementations use a Kubernetes controller to continuously
monitor their custom resource and apply the corresponding configuration
changes. The Istio controller monitors an ``IstioControlPlane`` resource
and reacts to changes by updating the Istio installation configuration
in the corresponding cluster.

In the 1.4 release, the Istio controller is in the alpha phase of
development and not fully integrated with ``istioctl``. It is, however,
`available for
experimentation </docs/setup/install/standalone-operator/>`_ using
``kubectl`` commands. For example, to install the controller and a
default version of Istio into your cluster, run the following command:

.. code:: sh

      $ kubectl apply -f https:///operator.yaml $ kubectl
apply -f https:///default-cr.yaml

You can then make changes to the Istio installation configuration:

.. code:: sh

      $ kubectl edit istiocontrolplane
example-istiocontrolplane -n istio-system

As soon as the resource is updated, the controller will detect the
changes and respond by updating the Istio installation correspondingly.

Both the operator controller and ``istioctl`` commands share the same
implementation. The significant difference is the execution context. In
the ``istioctl`` case, the operation runs in the admin user’s command
execution and security context. In the controller case, a pod in the
cluster runs the code in its security context. In both cases,
configuration is validated against a schema and the same correctness
checks are performed.

Migration from Helm
-------------------

To help ease the transition from previous configurations using Helm,
``istioctl`` and the controller support pass-through access for the full
Helm installation API.

You can pass Helm configuration options using ``istioctl --set`` by
prepending the string ``values.`` to the option name. For example,
instead of this Helm command:

.. code:: sh

      $ helm template … –set global.mtls.enabled=true

You can use this ``istioctl`` command:

.. code:: sh

      $ istioctl manifest generate … –set
values.global.mtls.enabled=true

You can also set Helm configuration values in an ``IstioControlPlane``
custom resource. See `Customize Istio settings using
Helm </docs/setup/install/istioctl/#customize-istio-settings-using-the-helm-api>`_
for details.

Another feature to help with the transition from Helm is the alpha `{{<
istioctl >}} manifest
migrate </docs/reference/commands/istioctl/#istioctl-manifest-migrate>`_
command. This command can be used to automatically convert a Helm
``values.yaml`` file to a corresponding ``IstioControlPlane``
configuration.

Implementation
--------------

Several frameworks have been created to help implement operators by
generating stubs for some or all of the components. The Istio operator
was created with the help of a combination of
`kubebuilder <https://github.com/kubernetes-sigs/kubebuilder>`_ and
`operator framework <https://github.com/operator-framework>`_. Istio’s
installation now uses a proto to describe the API such that runtime
validation can be executed against a schema.

More information about the implementation can be found in the README and
ARCHITECTURE documents in the `Istio operator
repository <https://github.com/istio/operator>`_.

Summary
-------

Starting in Istio 1.4, Helm installation is being replaced by new
``istioctl`` commands using a new operator custom resource definition,
``IstioControlPlane``, for the configuration API. An alpha controller is
also available for early experimentation with the operator.

The new ``istioctl`` commands and operator controller both validate
configuration schemas and perform a range of checks for installation
change or upgrade. These checks are tightly integrated with the tools to
prevent common errors and simplify troubleshooting.

The Istio maintainers expect that this new approach will improve the
user experience during Istio installation and upgrade, better stabilize
the installation API, and help users better manage and monitor their
Istio installations.

We welcome your feedback about the new installation approach at
`discuss.istio.io <https://discuss.istio.io/>`_.
