List Entry
========================================

---
WARNING: THIS IS AN AUTO-GENERATED FILE, DO NOT EDIT. PLEASE MODIFY THE ORIGINAL SOURCE IN THE 'https://github.com/istio/istio' REPO
source_repo: https://github.com/istio/istio
title: List Entry
description: A template designed to let you perform list checking operations.
location: https://istio.io/docs/reference/config/policy-and-telemetry/templates/listentry.html
layout: protoc-gen-docs
generator: protoc-gen-docs
aliases:
  - /docs/reference/config/template/listentry.html
number_of_entries: 1
---
<p>The <code>listentry</code> template is designed to let you perform list check operations
with the <a href="/docs/reference/config/policy-and-telemetry/adapters/list/">list</a> adapter.</p>

<p>Example config:</p>

<pre><code class="language-yaml">apiVersion: &quot;config.istio.io/v1alpha2&quot;
kind: instance
metadata:
  name: appversion
  namespace: istio-system
spec:
  compiledTemplate: listentry
  params:
    value: source.labels[&quot;version&quot;]
</code></pre>

<h2 id="Template">Template</h2>
<section>
<p>The <code>listentry</code> template is used to verify the presence/absence of a string
within a list.</p>

<p>When writing the configuration, the value for the fields associated with this template can either be a
literal or an <a href="/docs/reference//config/policy-and-telemetry/expression-language/">expression</a>. Please note that if the datatype of a field is not istio.policy.v1beta1.Value,
then the expression&rsquo;s <a href="/docs/reference//config/policy-and-telemetry/expression-language/#type-checking">inferred type</a> must match the datatype of the field.</p>

<table class="message-fields">
<thead>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
<th>Required</th>
</tr>
</thead>
<tbody>
<tr id="Template-value">
<td><code>value</code></td>
<td><code><a href="/docs/reference/config/policy-and-telemetry/istio.policy.v1beta1.html#Value">Value</a></code></td>
<td>
<p>Specifies the entry to verify in the list. This value can either be a string or an IP address.</p>

</td>
<td>
No
</td>
</tr>
</tbody>
</table>
</section>
