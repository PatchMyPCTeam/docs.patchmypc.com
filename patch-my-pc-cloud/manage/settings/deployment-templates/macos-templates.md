# Deployment Templates for macOS in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

When creating a new macOS deployment template in Patch My PC (PMPC) Cloud, as we do not know which **Installer Type** the deployment this template will be applied to, the **Install App as Managed** setting on the **Configurations** tab is enabled by default and can be configured.

Obviously, the same rules for creating [macOS deployments](../../../macos-support/deploy-macos-app.md) apply to macOS templates; i.e., templates don’t have different logic rules than creating a deployment without a template.

{% hint style="danger" %}
**Important**

If you try applying a template to a deployment that is configured with incompatible settings for the selected **Installer Type**, the following **Warning** notification is shown:

**Warning – Template ‘<**_**template\_name**_**>’ only partially applied as some template settings are incompatible with the selected Installer Type.**

Any incompatible settings are not applied. This could be because you applied the wrong template for the **Installer Type** in which case either:

* Apply the correct template.
* Switch the **Installer Type** and reapply the same template.
{% endhint %}

{% hint style="success" %}
**Tip**

To avoid issues applying incompatible templates when creating deployments, consider creating one template for LOB apps with the appropriate settings and another for non-LOB apps, with clear names. Then, when you create a deployment, you can easily determine which template to apply based on the **Installer Type** of the deployment.
{% endhint %}
