header-rules
==================================

Mixer rules must be valid to be applied at runtime. That means the match
conditions are well-defined expressions in the
`language </docs/reference/config/policy-and-telemetry/expression-language/>`_,
the attributes are declared in an `attribute
manifest </docs/reference/config/policy-and-telemetry/attribute-vocabulary/>`_,
and rules have no dangling references to handlers and instances.

The attribute values are typically normalized before evaluating rules on
them. For example, HTTP headers have lowercase keys in
``request.headers`` and ``response.headers`` attributes. An expression
``request.headers["X-Forwarded-Proto"] == "http"`` does not match any
request even though HTTP headers are case-insensitive. Instead, use an
expression ``request.headers["x-forwarded-proto"] == "http"``.
