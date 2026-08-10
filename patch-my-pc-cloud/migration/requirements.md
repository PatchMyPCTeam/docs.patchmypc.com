# ConfigMgr to Intune App Migration using Patch My PC Cloud Requirements&#x20;

_Applies to: Patch My PC Cloud_

To use the Patch My PC (PMPC) Cloud Migration tool, you need to have a:

* A supported version of Microsoft Configuration Manager (ConfigMgr).
* Patch My PC Publisher, version 2.1.99.0 or later.
* PMPC Cloud Company:
  * To which you have an account that has been granted the **Full Admin** user role (either by having this account created directly in the Cloud Company or by being a member of an Entra ID Group that has been granted this role).
* A valid Enterprise Premium or Enterprise Plus license:
  * **Enterprise Premium** allows you to:
    * Use Publisher to retrieve a list of applications from your ConfigMgr site and send it to your PMPC Cloud Company.
    * Use PMPC Cloud to review and evaluate if an application can be migrated to Intune.
    *   Click **Migrate** (when supported) to migrate the application to Intune, which creates either a:

        * Deployment for a PMPC catalog app (if we match to a catalog app).
        * Custom App and a Deployment (if we match to a Custom App).

        In both cases, you can specify the configuration and assignments in the same way as a regular Cloud deployment.
  * **Enterprise Plus** only allows you to:
    * Use Publisher to retrieve a list of applications from your ConfigMgr site and send it to your PMPC Cloud Company.
    * Use PMPC Cloud to review and evaluate if an application can be migrated to Intune.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>Because the Migration feature is part of our Enterprise Premium license SKU, if your PMPC Cloud company is using an Enterprise Plus license, the **Migrate** button will be locked, preventing you from migrating the app to PMPC Cloud.&#x20;</p>
<p>However, the [Migration Dashboard](about-migration-dashboard.md) is available and can be used to give you an overview of the detected ConfigMgr applications and to see a list of the ConfigMgr applications detected, along with their associated information.</p>
<p>To unlock the **Migrate** button so you can perform the migration, you either need to:</p>
<p>* [Request a quote for upgrading to Enterprise Premium](../manage/settings/subscription/license/request-quote.md).</p>
<p>* [Sign up for an Enterprise Premium Trial from Enterprise Plus](../manage/settings/company-settings/sign-up-enterprise-premium-trial.md), which allows you to migrate up to five applications.</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>The Migration feature is unsupported if your PMPC Cloud company is running an MSP license.</p>
</blockquote>