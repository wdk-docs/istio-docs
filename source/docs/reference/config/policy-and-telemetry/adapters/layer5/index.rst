
Layer5
============================

---
WARNING: THIS IS AN AUTO-GENERATED FILE, DO NOT EDIT. PLEASE MODIFY THE ORIGINAL SOURCE IN THE 'https://github.com/layer5io/layer5-istio-adapter' REPO
source_repo: https://github.com/layer5io/layer5-istio-adapter
title: Layer5
description: Adapter to deliver metrics to Layer5.
location: https://istio.io/docs/reference/config/policy-and-telemetry/adapters/layer5.html
layout: partner-component
generator: protoc-gen-docs
provider: Layer5, Inc.
contact_email: community@layer5.io
support_link:
source_link: https://github.com/layer5io/layer5-istio-adapter
latest_release_link: https://github.com/layer5io/layer5-istio-adapter/releases
helm_chart_link:
istio_versions: "1.1+"
supported_templates: metric
logo_link: https://github.com/layer5io/layer5-istio-adapter/blob/master/layer5.svg
number_of_entries: 1
---
<p>The <code>layer5</code> adapter collects metrics</p>

<p>This adapter supports the <a href="/docs/reference/config/policy-and-telemetry/templates/metric/">metric template</a>.</p>

<h2 id="Params">Params</h2>
<section>
<p>config for layer5 adapter</p>

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
<tr id="Params-file_path">
<td><code>filePath</code></td>
<td><code>string</code></td>
<td>
<p>Path of the file to save the information about runtime requests.</p>

</td>
<td>
No
</td>
</tr>
</tbody>
</table>
</section>
