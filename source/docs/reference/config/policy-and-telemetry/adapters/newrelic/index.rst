New Relic
============================

---
WARNING: THIS IS AN AUTO-GENERATED FILE, DO NOT EDIT. PLEASE MODIFY THE ORIGINAL SOURCE IN THE 'https://github.com/newrelic/newrelic-istio-adapter' REPO
source_repo: https://github.com/newrelic/newrelic-istio-adapter
title: New Relic
description: An Istio Mixer adapter to send telemetry data to New Relic.
location: https://istio.io/docs/reference/config/policy-and-telemetry/adapters/newrelic.html
layout: partner-component
generator: protoc-gen-docs
provider: New Relic, Inc.
source_link: https://github.com/newrelic/newrelic-istio-adapter
latest_release_link: https://github.com/newrelic/newrelic-istio-adapter/releases
supported_templates: metric, tracespan
number_of_entries: 3
---
<p>An Istio Mixer adapter to send telemetry data to New Relic.</p>

<h2 id="Params">Params</h2>
<section>
<p>Configuration format for the <code>newrelic</code> adapter.</p>

<table class="message-fields">
<thead>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr id="Params-namespace">
<td><code>namespace</code></td>
<td><code>string</code></td>
<td>
<p>Optional. The namespace is used as a prefix for metric names in New Relic.
An example: for a metric named <code>requestSize</code> with a namespace of <code>istio</code>,
the full metric name in New Relic becomes <code>istio.requestSize</code>.</p>

</td>
</tr>
<tr id="Params-metrics">
<td><code>metrics</code></td>
<td><code>map&lt;string,&nbsp;<a href="#Params-MetricInfo">Params.MetricInfo</a>&gt;</code></td>
<td>
<p>Map of Istio metric instance names and the corresponding New Relic
MetricInfo specification. This identifies what to send New Relic and
in what form it should be sent.</p>

<p>Any metric instances Istio sends to the adapter but not specified here
will be dropped and not exported to New Relic.</p>

</td>
</tr>
</tbody>
</table>
</section>
<h2 id="Params-MetricInfo">Params.MetricInfo</h2>
<section>
<p>Describes how to represent an Istio metric instance in New Relic.</p>

<table class="message-fields">
<thead>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr id="Params-MetricInfo-name">
<td><code>name</code></td>
<td><code>string</code></td>
<td>
<p>Recommended. The name of the metric (scoped by namespaces) in New Relic.</p>

<p>The name must not be empty and the fully qualified name (prefixed
with the namespace) must contain 255 16-bit code units (UTF-16) or
less. Otherwise, an error will be logged and no metric will be sent
to New Relic.</p>

</td>
</tr>
<tr id="Params-MetricInfo-type">
<td><code>type</code></td>
<td><code><a href="#Params-MetricInfo-Type">Params.MetricInfo.Type</a></code></td>
<td>
<p>Required. New Relic metric type to interpret the Istio instance as.</p>

</td>
</tr>
</tbody>
</table>
</section>
<h2 id="Params-MetricInfo-Type">Params.MetricInfo.Type</h2>
<section>
<p>New Relic Metric types.</p>

<table class="enum-values">
<thead>
<tr>
<th>Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr id="Params-MetricInfo-Type-UNSPECIFIED">
<td><code>UNSPECIFIED</code></td>
<td>
<p>Default and invalid unspecified type.</p>

<p>An error will be logged and the metric dropped if unspecified.</p>

</td>
</tr>
<tr id="Params-MetricInfo-Type-GAUGE">
<td><code>GAUGE</code></td>
<td>
<p>A New Relic <code>Gauge</code> type.</p>

<p>This metric type represents the instantaneous state of something
or process that can both increase and decrease in value.</p>

<p>For example, this metric type would be used to record:</p>

<ul>
<li>the network throughput of a service</li>
<li>the storage capacity used on a server</li>
<li>the size of a queue</li>
</ul>

</td>
</tr>
<tr id="Params-MetricInfo-Type-COUNT">
<td><code>COUNT</code></td>
<td>
<p>A New Relic <code>Count</code> type.</p>

<p>This metric type represents the number of occurrences for an event
within a time window. It is important to note that this is not the
cumulative tally of occurrences since the beginning of
measurements. Rather, this metric type represents the change in the
cumulative tally of events within a time window.</p>

<p>For example, this metric type would be used to record:</p>

<ul>
<li>the number of requests to a service</li>
<li>the number of tasks submitted to a processor</li>
<li>the number of errors produced</li>
</ul>

</td>
</tr>
<tr id="Params-MetricInfo-Type-SUMMARY">
<td><code>SUMMARY</code></td>
<td>
<p>New Relic <code>Summary</code> type.</p>

<p>This metric type reports aggregated information about discrete
events. The information is recorded as a count of events, average
event values, sum of event values, and the minimum and maximum
event values observed within a time window.</p>

<p>For example, this metric type would be used to record:</p>

<ul>
<li>the duration and count of requests to service</li>
<li>the duration and count of database transactions</li>
<li>the time each message spent in a queue</li>
</ul>

</td>
</tr>
</tbody>
</table>
</section>
