# Configure the Default Deployment Template in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

The _Templates_ feature of Patch My PC (PMPC) Cloud allows you to optionally set one template per operating system (OS) platform as the default template to use whenever you create a deployment for that specific platform.

Once a default template has been configured, when you create a new deployment for that OS platform, the configuration settings defined in the template are automatically applied. You can still modify the settings if required.

You also apply a template to deployment as detailed in [Using Templates in Deployments](../../../deployments/use-template.md).

> \*\*Note\*\*
>
> If you previously set a default template but do not want to use it, see the \[Unconfigure a Default Template]\(configure-default-template.md#unconfigure-a-default-template) section.
>
> Also, configuring a default template for an OS platform does not affect any existing deployments to that platform. The default template will only apply to new deployments created after the default has been configured.

To configure the default template for all deployments to a specific OS platform:

1. Navigate to **Settings | Templates**

![Navigating to "Settings | Templates"](../../../../.gitbook/assets/image-\(963\).png)

2. On the **Templates** page, click the relevant slider under the **Default** column beside the template you want to configure as the default for all deployments created for that OS platform going forward.

![Clicking the 'default' slider beside the relevant template](../../../../.gitbook/assets/image-\(3697\).png)

3. On the **Are you sure you want to set ‘<**_**template\_name**_**>’ template as the default** popup, click **Yes**.

![](../../../../.gitbook/assets/image-\(3701\).png)

The **Templates** page is redisplayed, showing that the selected template is now the default template for all new deployments created for the relevant OS platform, along with the **Success - Template “<**_**template\_name**_**>" successfully set as the default for <**_**platform**_**>** notification.

![](../../../../.gitbook/assets/image-\(3698\).png)

> \*\*Note\*\*
>
> You can only configure one template as the default per OS platform. If you want to choose a different template as the default, click the \*\*Default\*\* slider beside the relevant template and confirm you want to set that one as the default instead.

## Unconfigure a Default Template

If you have previously configured a default template but now do not want a default template to be applied to any new deployments:

1. Click the slider under the **Default** column beside the template you currently have configured as the default.

![Clicking the slider under the 'Default' column beside the template currently configured as the default.](../../../../.gitbook/assets/image-\(3699\).png)

2. On the A**re you sure you want to unset ‘<**_**template\_name**_**>’ template as the default** popup, click **Yes**.

![](../../../../.gitbook/assets/image-\(968\).png)

The **Templates** page is redisplayed, showing that the selected template is no longer the default template for all new deployments created for the relevant OS platform, along with the **Success - Template “<**_**template\_name**_**>" successfully unset as the default for <**_**platform**_**>** notification.

![](../../../../.gitbook/assets/image-\(3700\).png)
