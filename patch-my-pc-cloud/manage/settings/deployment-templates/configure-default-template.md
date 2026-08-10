# Configure the Default Deployment Template in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

The _Templates_ feature of Patch My PC (PMPC) Cloud allows you to optionally set one template per operating system (OS) platform as the default template to use whenever you create a deployment for that specific platform.

Once a default template has been configured, when you create a new deployment for that OS platform, the configuration settings defined in the template are automatically applied. You can still modify the settings if required.

You also apply a template to deployment as detailed in [Using Templates in Deployments](../../../deployments/use-template.md).

{% hint style="info" %}
**Note**

If you previously set a default template but do not want to use it, see the [Unconfigure a Default Template](configure-default-template.md#unconfigure-a-default-template) section.

Also, configuring a default template for an OS platform does not affect any existing deployments to that platform. The default template will only apply to new deployments created after the default has been configured.
{% endhint %}

To configure the default template for all deployments to a specific OS platform:

1. Navigate to **Settings | Templates**

<figure><img src="../../../../.gitbook/assets/image (963).png" alt="Navigating to “Settings | Templates”" width="563"><figcaption></figcaption></figure>

2. On the **Templates** page, click the relevant slider under the **Default** column beside the template you want to configure as the default for all deployments created for that OS platform going forward.

<figure><img src="../../../../.gitbook/assets/image (3697).png" alt="Clicking the &#x27;default&#x27; slider beside the relevant template" width="563"><figcaption></figcaption></figure>

3. On the **Are you sure you want to set ‘<**_**template\_name**_**>’ template as the default** popup, click **Yes**.

<figure><img src="../../../../.gitbook/assets/image (3701).png" alt="Clicking &#x27;Yes&#x27; on the &#x27;Are you sure you want to set ‘<template_name>’ template as the default&#x27; popup" width="245"><figcaption></figcaption></figure>

The **Templates** page is redisplayed, showing that the selected template is now the default template for all new deployments created for the relevant OS platform, along with the **Success - Template “<**_**template\_name**_**>" successfully set as the default for <**_**platform**_**>** notification.

<figure><img src="../../../../.gitbook/assets/image (3698).png" alt="&#x27;Success - Template &#x27;<template_name>&#x27; successfully set as the default for <platform>&#x27; notification" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

You can only configure one template as the default per OS platform. If you want to choose a different template as the default, click the **Default** slider beside the relevant template and confirm you want to set that one as the default instead.
{% endhint %}

## Unconfigure a Default Template

If you have previously configured a default template but now do not want a default template to be applied to any new deployments:

1. Click the slider under the **Default** column beside the template you currently have configured as the default.

<figure><img src="../../../../.gitbook/assets/image (3699).png" alt="Clicking the slider under the &#x27;Default&#x27; column beside the template currently configured as the default." width="563"><figcaption></figcaption></figure>

2. On the A**re you sure you want to unset ‘<**_**template\_name**_**>’ template as the default** popup, click **Yes**.

<figure><img src="../../../../.gitbook/assets/image (968).png" alt="Clicking “Yes” on the “Are you sure you want to unset ‘<template_name>’ template as the default” popup" width="288"><figcaption></figcaption></figure>

The **Templates** page is redisplayed, showing that the selected template is no longer the default template for all new deployments created for the relevant OS platform, along with the **Success - Template “<**_**template\_name**_**>" successfully unset as the default for <**_**platform**_**>** notification.

<figure><img src="../../../../.gitbook/assets/image (3700).png" alt="&#x27;Success - Template &#x27;<template_name>&#x27; successfully unset as the default for <platform>&#x27; notification" width="563"><figcaption></figcaption></figure>
