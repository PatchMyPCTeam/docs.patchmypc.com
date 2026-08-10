# Predefined Scripts option in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_&#x41;vailable at level: Product_\
_&#x41;vailable on tab: WSUS Updates, ConfigMgr Apps, Intune Apps, Intune Updates_

Patch My PC (PMPC) defined pre- and post-scripts are provided for specific products that cannot fully manage certain scenarios on their own. A common example is software that is unable to remove older versions during an upgrade, such as Oracle Java.

The **Predefined Scripts** right-click option automatically downloads and bundles the PMPC pre- and post-scripts with the application or updates them whenever the application is published using Publisher.

## Required Scripts

**Required Scripts** are enforced and cannot be modified or disabled. They are always executed as part of the installation or update to ensure the application installs correctly.

## Recommended Scripts

**Recommended Scripts** are optional. Although they are included with the application or update, they can be disabled if you prefer not to use them.

![Recommended Scripts](/_images/image-(4418).png)

### Review the Recommended Script

To view the PMPC recommended script:

1. Click the **Predefined Scripts** right-click customization option for the product in the Product Tree.
2. Click **View** to open the script in a browser and review its contents.
3. Review the **Description** field to understand what the script does and when it runs.

> \*\*Note\*\*
>
> Recommended scripts are hosted by PMPC and are referenced by URL. They are not editable from the Publisher UI.

### Configure Script Behavior

The following options control how the recommended script behaves:

* **Don’t attempt software update if the pre-script returns an exit code other than 0 or 3010**\
  When enabled, the installation or update stops if the recommended script fails. This option is enabled by default and prevents the deployment from continuing if required cleanup actions cannot be completed.
* **Disable the Patch My PC recommended pre-update script for this product**\
  When enabled, the recommended script is skipped for this product. This option is available only for recommended scripts and does not apply to required scripts.