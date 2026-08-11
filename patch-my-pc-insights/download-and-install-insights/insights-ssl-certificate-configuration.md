---
description: Advanced Insights SSL Certificate configuration.
---

# Insights SSL Certificate Configuration

_Applies to: Patch My PC Advanced and Patch Insights_

Advanced Insights requires a valid SSL certificate to bind to the application websites and supports the following types:

* Server host (FQDN) standard certificate.
* Wildcard certificate.
* Custom CNAME / Alias certificate.
* Self-signed certificate.

{% hint style="warning" %}
Ensure the SSL certificate requirements are reviewed here: [insights-certificate-requirements.md](../advanced-and-patch-insights-requirements-and-prerequisites/insights-certificate-requirements.md "mention")
{% endhint %}

### Certificate configuration scenarios

* **Scenario 1 - Server Host name certificate.**
  * For Advanced Insights URL deployment using **server host name** (e.g. _https://server01.contoso.local_) follow steps described in section:[#standard-server-host-name-certificate](insights-ssl-certificate-configuration.md#standard-server-host-name-certificate "mention")
* **Scenario 2 - Wildcard certificate.**
  * For custom Advanced Insights URL deployment using a **wildcard certificate** (e.g. \*.contoso.local) follow steps described in section: [#wildcard-certificate](insights-ssl-certificate-configuration.md#wildcard-certificate "mention")
* **Scenario 3 - CNAME / Alias certificate.**
  * For custom Advanced Insights URL deployment using a **CNAME / Alias,** (e.g. _https://AdvancedInsights.contoso.local_) follow steps described in section: [#cname-alias-certificate](insights-ssl-certificate-configuration.md#cname-alias-certificate "mention")
* **Scenario 4 - Self-signed certificate.**
  * For Advanced Insights URL deployment using a **Self-signed** certificate follow steps described in section: [#self-signed-certificate](insights-ssl-certificate-configuration.md#self-signed-certificate "mention")



## Standard Server host name certificate

Select the certificate which represents the server host name (FQDN).

<figure><img src="../../.gitbook/assets/image (4326).png" alt="Select a certificate" width="563"><figcaption></figcaption></figure>

Once selected, no further certificate configuration is required.

Click Next to proceed to the [insights-sqlite-database.md](insights-sqlite-database.md "mention") page.

## Wildcard certificate

Select the certificate which represents the wildcard certificate.

<figure><img src="../../.gitbook/assets/image (4328).png" alt="Wildcard certificate" width="563"><figcaption></figcaption></figure>

Click the **'Set CNAME / Alias'** button.

In the CNAME / Alias configuration page, the installer will automatically pre-populate the domain wildcard property from the selected certificate.

<figure><img src="../../.gitbook/assets/image (4329).png" alt="Clicking the &#x27;Set CNAME / Alias&#x27; button." width="563"><figcaption></figcaption></figure>

The CNAME / Alias property value box will need to be updated with a chosen CNAME / Alias prefix. For example:

_**'AdvancedInsights.corp.contoso.local'**_

Then click **'Set CNAME - Alias'**.

<figure><img src="../../.gitbook/assets/image (4330).png" alt="Clicking &#x27;Set CNAME - Alias&#x27;." width="563"><figcaption></figcaption></figure>

Click Next to proceed to the [insights-sqlite-database.md](insights-sqlite-database.md "mention") page.

<figure><img src="../../.gitbook/assets/image (4331).png" alt="Click Next" width="563"><figcaption></figcaption></figure>

{% hint style="warning" %}
When using a wildcard certificate, if no CNAME / Alias is set using the CNAME / Alias configuration page, the installer will automatically default to setting the Advanced Insights URL to the server host name FQDN.\
\
Example:&#x20;

_https://server01.corp.contoso.local_
{% endhint %}

## CNAME / Alias certificate

Select the certificate that represents the CNAME / Alias certificate.

<figure><img src="../../.gitbook/assets/image (4332).png" alt="Selecting the certificate that represents the CNAME / Alias certificate" width="563"><figcaption></figcaption></figure>

Click the **'Set CNAME / Alias'** button.

In the CNAME / Alias configuration page, the installer will automatically pre-populate the CNAME / Alias property based on the available SAN entries from the selected certificate.

In this example, the selected certificate has one SAN entry which has been automatically pre-populated:

<figure><img src="../../.gitbook/assets/image (4333).png" alt="Clicking the &#x27;Set CNAME / Alias&#x27; button." width="563"><figcaption></figcaption></figure>

Confirm the CNAME / Alias configuration by clicking the **'Set CNAME / Alias'** button.

<figure><img src="../../.gitbook/assets/image (4334).png" alt="Confirming the CNAME / Alias configuration" width="563"><figcaption></figcaption></figure>

Click Next to proceed to the [insights-sqlite-database.md](insights-sqlite-database.md "mention") page.

## Self-signed certificate

To deploy Advanced Insights using a self-signed certificate, on the certificate selection page, click the **'Create Self -Signed Cert'** button:

<figure><img src="../../.gitbook/assets/image (4335).png" alt="Clicking the &#x27;Create Self -Signed Cert&#x27; button" width="563"><figcaption></figcaption></figure>

The installer will then automatically proceed to the [insights-sqlite-database.md](insights-sqlite-database.md "mention") dialog page.
