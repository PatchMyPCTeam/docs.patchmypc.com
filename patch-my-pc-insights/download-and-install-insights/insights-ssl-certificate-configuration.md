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

> Ensure the SSL certificate requirements are reviewed here: \[insights-certificate-requirements.md]\(../advanced-and-patch-insights-requirements-and-prerequisites/insights-certificate-requirements.md "mention")

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

![Select a certificate](../../.gitbook/assets/image-\(4326\).png)

Once selected, no further certificate configuration is required.

Click Next to proceed to the [insights-sqlite-database.md](insights-sqlite-database.md "mention") page.

## Wildcard certificate

Select the certificate which represents the wildcard certificate.

![Wildcard certificate](../../.gitbook/assets/image-\(4328\).png)

Click the **'Set CNAME / Alias'** button.

In the CNAME / Alias configuration page, the installer will automatically pre-populate the domain wildcard property from the selected certificate.

![Clicking the 'Set CNAME / Alias' button.](../../.gitbook/assets/image-\(4329\).png)

The CNAME / Alias property value box will need to be updated with a chosen CNAME / Alias prefix. For example:

_**'AdvancedInsights.corp.contoso.local'**_

Then click **'Set CNAME - Alias'**.

![Clicking 'Set CNAME - Alias'.](../../.gitbook/assets/image-\(4330\).png)

Click Next to proceed to the [insights-sqlite-database.md](insights-sqlite-database.md "mention") page.

![Click Next](../../.gitbook/assets/image-\(4331\).png)

> When using a wildcard certificate, if no CNAME / Alias is set using the CNAME / Alias configuration page, the installer will automatically default to setting the Advanced Insights URL to the server host name FQDN.\\
>
> \\
>
> Example:
>
> \_https://server01.corp.contoso.local\_

## CNAME / Alias certificate

Select the certificate that represents the CNAME / Alias certificate.

![Selecting the certificate that represents the CNAME / Alias certificate](../../.gitbook/assets/image-\(4332\).png)

Click the **'Set CNAME / Alias'** button.

In the CNAME / Alias configuration page, the installer will automatically pre-populate the CNAME / Alias property based on the available SAN entries from the selected certificate.

In this example, the selected certificate has one SAN entry which has been automatically pre-populated:

![Clicking the 'Set CNAME / Alias' button.](../../.gitbook/assets/image-\(4333\).png)

Confirm the CNAME / Alias configuration by clicking the **'Set CNAME / Alias'** button.

![Confirming the CNAME / Alias configuration](../../.gitbook/assets/image-\(4334\).png)

Click Next to proceed to the [insights-sqlite-database.md](insights-sqlite-database.md "mention") page.

## Self-signed certificate

To deploy Advanced Insights using a self-signed certificate, on the certificate selection page, click the **'Create Self -Signed Cert'** button:

![Clicking the 'Create Self -Signed Cert' button](../../.gitbook/assets/image-\(4335\).png)

The installer will then automatically proceed to the [insights-sqlite-database.md](insights-sqlite-database.md "mention") dialog page.
