Authentication Policy
============================
---
WARNING: THIS IS AN AUTO-GENERATED FILE, DO NOT EDIT. PLEASE MODIFY THE ORIGINAL SOURCE IN THE 'https://github.com/istio/api' REPO
source_repo: https://github.com/istio/api
title: Authentication Policy
description: Authentication policy for Istio services.
location: https://istio.io/docs/reference/config/security/istio.authentication.v1alpha1.html
layout: protoc-gen-docs
generator: protoc-gen-docs
schema: istio.authentication.v1alpha1.Policy
weight: 10
aliases: [/docs/reference/config/istio.authentication.v1alpha1]
number_of_entries: 4
---
<p>This package defines user-facing authentication policy.</p>

<h2 id="MutualTls">MutualTls</h2>
<section>
<p>TLS authentication params.</p>

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
<tr id="MutualTls-mode">
<td><code>mode</code></td>
<td><code><a href="#MutualTls-Mode">Mode</a></code></td>
<td>
<p>Defines the mode of mTLS authentication.</p>

</td>
<td>
No
</td>
</tr>
<tr id="MutualTls-allow_tls" class="deprecated ">
<td><code>allowTls</code></td>
<td><code>bool</code></td>
<td>
<p>Deprecated. Please use mode = PERMISSIVE instead.
If set, will translate to <code>TLS_PERMISSIVE</code> mode.
Set this flag to true to allow regular TLS (i.e without client x509
certificate). If request carries client certificate, identity will be
extracted and used (set to peer identity). Otherwise, peer identity will
be left unset.
When the flag is false (default), request must have client certificate.</p>

</td>
<td>
No
</td>
</tr>
</tbody>
</table>
</section>
<h2 id="MutualTls-Mode">MutualTls.Mode</h2>
<section>
<p>Defines the acceptable connection TLS mode.</p>

<table class="enum-values">
<thead>
<tr>
<th>Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr id="MutualTls-Mode-STRICT">
<td><code>STRICT</code></td>
<td>
<p>Client cert must be presented, connection is in TLS.</p>

</td>
</tr>
<tr id="MutualTls-Mode-PERMISSIVE">
<td><code>PERMISSIVE</code></td>
<td>
<p>Connection can be either plaintext or TLS with Client cert.</p>

</td>
</tr>
</tbody>
</table>
</section>
<h2 id="PeerAuthenticationMethod">PeerAuthenticationMethod</h2>
<section>
<p>PeerAuthenticationMethod defines one particular type of authentication. Only mTLS is supported
at the moment.
The type can be progammatically determine by checking the type of the
&ldquo;params&rdquo; field.</p>

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
<tr id="PeerAuthenticationMethod-mtls" class="oneof oneof-start">
<td><code>mtls</code></td>
<td><code><a href="#MutualTls">MutualTls (oneof)</a></code></td>
<td>
<p>Set if mTLS is used.</p>

</td>
<td>
Yes
</td>
</tr>
</tbody>
</table>
</section>
<h2 id="Policy">Policy</h2>
<section>
<p>Policy defines what authentication methods can be accepted on workload(s),
and if authenticated, which method/certificate will set the request principal
(i.e request.auth.principal attribute).</p>

<p>Authentication policy is composed of 2-part authentication:
- peer: verify caller service credentials. This part will set source.user
(peer identity).
- origin: verify the origin credentials. This part will set request.auth.user
(origin identity), as well as other attributes like request.auth.presenter,
request.auth.audiences and raw claims. Note that the identity could be
end-user, service account, device etc.</p>

<p>Last but not least, the principal binding rule defines which identity (peer
or origin) should be used as principal. By default, it uses peer.</p>

<p>Examples:</p>

<p>Policy to enable mTLS for all services in namespace frod. The policy name must be
<code>default</code>, and it contains no rule for <code>targets</code>.</p>

<pre><code class="language-yaml">apiVersion: authentication.istio.io/v1alpha1
kind: Policy
metadata:
  name: default
  namespace: frod
spec:
  peers:
  - mtls:
</code></pre>

<p>Policy to disable mTLS for &ldquo;productpage&rdquo; service</p>

<pre><code class="language-yaml">apiVersion: authentication.istio.io/v1alpha1
kind: Policy
metadata:
  name: productpage-mTLS-disable
  namespace: frod
spec:
  targets:
  - name: productpage
</code></pre>

<p>Policy to require mTLS for peer authentication, and JWT for origin authentication
for productpage:9000 except the path &lsquo;/health_check&rsquo; . Principal is set from origin identity.</p>

<pre><code class="language-yaml">apiVersion: authentication.istio.io/v1alpha1
kind: Policy
metadata:
  name: productpage-mTLS-with-JWT
  namespace: frod
spec:
  targets:
  - name: productpage
    ports:
    - number: 9000
  peers:
  - mtls:
  origins:
  - jwt:
      issuer: &quot;https://securetoken.google.com&quot;
      audiences:
      - &quot;productpage&quot;
      jwksUri: &quot;https://www.googleapis.com/oauth2/v1/certs&quot;
      jwtHeaders:
      - &quot;x-goog-iap-jwt-assertion&quot;
      triggerRules:
      - excludedPaths:
        - exact: /health_check
  principalBinding: USE_ORIGIN
</code></pre>

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
<tr id="Policy-peers">
<td><code>peers</code></td>
<td><code><a href="#PeerAuthenticationMethod">PeerAuthenticationMethod[]</a></code></td>
<td>
<p>List of authentication methods that can be used for peer authentication.
They will be evaluated in order; the first validate one will be used to
set peer identity (source.user) and other peer attributes. If none of
these methods pass, request will be rejected with authentication failed error (401).
Leave the list empty if peer authentication is not required</p>

</td>
<td>
No
</td>
</tr>
<tr id="Policy-targets" class="deprecated ">
<td><code>targets</code></td>
<td><code><a href="#TargetSelector">TargetSelector[]</a></code></td>
<td>
<p>Deprecated. Only mesh-level and namespace-level policies are supported.
List rules to select workloads that the policy should be applied on.
If empty, policy will be used on all workloads in the same namespace.</p>

</td>
<td>
No
</td>
</tr>
<tr id="Policy-peer_is_optional" class="deprecated ">
<td><code>peerIsOptional</code></td>
<td><code>bool</code></td>
<td>
<p>Deprecated. Should set mTLS to PERMISSIVE instead.
Set this flag to true to accept request (for peer authentication perspective),
even when none of the peer authentication methods defined above satisfied.
Typically, this is used to delay the rejection decision to next layer (e.g
authorization).
This flag is ignored if no authentication defined for peer (peers field is empty).</p>

</td>
<td>
No
</td>
</tr>
<tr id="Policy-origins" class="deprecated ">
<td><code>origins</code></td>
<td><code><a href="#OriginAuthenticationMethod">OriginAuthenticationMethod[]</a></code></td>
<td>
<p>Deprecated. Please use security/v1beta1/RequestAuthentication instead.
List of authentication methods that can be used for origin authentication.
Similar to peers, these will be evaluated in order; the first validate one
will be used to set origin identity and attributes (i.e request.auth.user,
request.auth.issuer etc). If none of these methods pass, request will be
rejected with authentication failed error (401).
A method may be skipped, depends on its trigger rule. If all of these methods
are skipped, origin authentication will be ignored, as if it is not defined.
Leave the list empty if origin authentication is not required.</p>

</td>
<td>
No
</td>
</tr>
<tr id="Policy-origin_is_optional" class="deprecated ">
<td><code>originIsOptional</code></td>
<td><code>bool</code></td>
<td>
<p>Deprecated. Please use security/v1beta1/RequestAuthentication instead.
Set this flag to true to accept request (for origin authentication perspective),
even when none of the origin authentication methods defined above satisfied.
Typically, this is used to delay the rejection decision to next layer (e.g
authorization).
This flag is ignored if no authentication defined for origin (origins field is empty).</p>

</td>
<td>
No
</td>
</tr>
<tr id="Policy-principal_binding" class="deprecated ">
<td><code>principalBinding</code></td>
<td><code><a href="#PrincipalBinding">PrincipalBinding</a></code></td>
<td>
<p>Deprecated. Source principal is always from peer, and request principal is always from
RequestAuthentication.
Define whether peer or origin identity should be use for principal. Default
value is USE_PEER.
If peer (or origin) identity is not available, either because of peer/origin
authentication is not defined, or failed, principal will be left unset.
In other words, binding rule does not affect the decision to accept or
reject request.</p>

</td>
<td>
No
</td>
</tr>
</tbody>
</table>
</section>
