# Using a Different Computer to run the Patch My PC Publisher Settings console

_Applies to: Patch My PC Publisher V3.x_

<blockquote class="wp-block-quote">
<p>**PRE-RELEASE DOCUMENTATION**</p>
<p>This documentation is for a pre-release feature still under development and, therefore, incomplete. As a result, both functionality and documentation are subject to change.</p>
<p>Once this feature is released, it will be announced, and this banner will be removed.</p>
</blockquote>

When the Patch My PC (PMPC) Publisher Settings console and **PatchMyPCService** run on the same computer, they communicate over a local-only connection that never touches the network, so no certificate is involved.

However, when the Settings console runs on a different computer from the **PatchMyPCService**, the connection is protected with HTTPS, which requires a certificate on the server as detailed below.

## Why a certificate is needed, even inside a domain

A common question is: _Why is a certificate required if both machines are in the same Active Directory domain?_

* **For signing in - no.** Your identity is always proven with Integrated Windows Authentication (Kerberos or NTLM). That never uses a certificate.
* **For protecting the traffic - yes.** Windows authentication proves who you are, but it does not encrypt the configuration data that travels between the Settings console and the **PatchMyPCService**. On any connection that leaves the server, it is a certificate (HTTPS) that keeps that data private and confirms you reached the real server and not an impostor.

The only exception is the same-machine (local) case, which stays on a local connection because that traffic never reaches the network.

## Certificate requirements

Use the following checklist when requesting or generating the server certificate. The same requirements apply whether the certificate comes from a Certificate Authority (CA) or is self-signed - the only difference is how client workstations trust it.

<table><thead><tr><th width="211.22222900390625" valign="top">Requirement</th><th valign="top">Value</th><th valign="top">Why it matters</th></tr></thead><tbody><tr><td valign="top">Location on the server</td><td valign="top">Local Machine/Personal store, with its private key</td><td valign="top">The server needs the private key to establish the secure connection.</td></tr><tr><td valign="top">Purpose (EKU)</td><td valign="top">Server Authentication</td><td valign="top">Required for any TLS server certificate. Publisher checks for this before binding.</td></tr><tr><td valign="top">Subject Alternative Name (SAN)</td><td valign="top">A DNS entry matching the <strong>exact FQDN</strong> administrators connect to (add every name or alias used).</td><td valign="top">Modern clients match the connection name against the SAN. A missing or mismatched name fails validation, even if the certificate is otherwise trusted.</td></tr><tr><td valign="top">Key strength</td><td valign="top">RSA 2048-bit or larger, or ECDSA P-256 or stronger, signed with SHA-256 or better.</td><td valign="top">Meets current security standards. Older or weaker keys are rejected.</td></tr><tr><td valign="top">Validity</td><td valign="top">Current - not expired and not future-dated.</td><td valign="top">Expired certificates fail validation.</td></tr></tbody></table>

## Choosing your Certificate Type

We support the following types of certificate:

* [CA-issued (recommended)](using-different-computer.md#ca-issued-recommended)
* [Self-signed (test or non-domain)](using-different-computer.md#self-signed-test-or-non-domain)

### CA-issued (recommended)

Issue the certificate from your domain or enterprise certificate authority (for example, Active Directory Certificate Services), meeting the requirements above.

* Every domain-joined workstation already trusts your internal CA, so no per-workstation trust step is needed.
* Renewals handled by the CA do not require touching each console.
* On the workstation, a successful **Test Connection** simply confirms the certificate is already trusted; nothing is installed.

This is the cleanest option for a domain. Issue one Server Authentication certificate to the Publisher server with a SAN matching the FQDN, install it into the server's Local Machine/Personal store with its private key, and bind it (see [Binding the Certificate on the Server](using-different-computer.md#binding-the-certificate-on-the-server)).

### Self-signed (test or non-domain)

A self-signed certificate must still meet **all** of the requirements detailed above - the Server Authentication purpose and a matching DNS SAN are the two most commonly missed.

As no CA vouches for it, each workstation has to trust it individually. When an administrator clicks **Apply** in the **Remote Service Connection** wizard, the console adds the certificate to that user's Trusted Root store so future connections are trusted. We prefer a CA-issued certificate wherever a domain CA is available.

## Binding the Certificate on the Server

To bind the certificate on the server:

1. In the Settings console on the server, navigate to **Settings | Advanced | Config API External Access**.
2. Select the certificate from the Local Machine store.
3. Click **Apply**. As binding needs elevation, you may see a User Account Control prompt.

If you pick a self-signed certificate, the Settings console warns you that a CA-issued certificate is preferred (because a self-signed certificate must be trusted on every workstation). You can still choose to proceed.

## Trusting the Certificate on a Workstation

When an administrator runs **Test Connection** and then clicks **Apply** in **Settings | Advanced | Remote Service Connection**, the following happens for each certificate type:

* **CA-issued and already trusted:** the connection validates normally. Nothing is installed on the workstation.
* **Self-signed:** the certificate's public part is added to the current user's Trusted Root store, and the confirmation says so.

Only the **public** part of the certificate is ever stored on a workstation. The private key never leaves the server.

## If a hostname is set without a Certificate

If external access is configured with a hostname but no certificate is bound, the **PatchMyPCService** will still accept remote connections, but over plain, unencrypted HTTP. This is not recommended outside an isolated test network, as configuration data will travel in clear text. You should always bind a certificate for real deployments.