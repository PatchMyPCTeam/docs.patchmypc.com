# Manage Application Updates and Retention

_Applies to: Patch My PC Publisher V2.x_\
_&#x41;vailable at level: Vendor, Product_\
_&#x41;vailable on tab: ConfigMgr Apps_

## Overview

Manage Application Updates and Retention allows you to override the global ConfigMgr application behavior for a specific vendor or individual product.

![Manage Application Updates and Retention](/_images/image-(4055).png)

Global behavior for application updates and retention is configured on the [ConfigMgr Apps](../administration/configmgr-apps/) tab by clicking [Options](../administration/configmgr-apps/options/). These settings define how new application versions are handled, whether applications are updated in place or created as new applications, and how many previous versions are retained.

![ConfigMgr Apps Options](/_images/image-(4056).png)

In some cases, a one size fits all approach is not ideal. This option allows you to customize update and retention behavior at the vendor or product level without changing your global defaults.

## When Overrides Are Useful

Overrides are commonly used for applications that update frequently, such as web browsers.

Products like Google Chrome, Microsoft Edge, and Mozilla Firefox release updates often. Issues introduced by these updates may not be identified immediately. If a global retention setting keeps only a small number of previous versions, for example 2, the version you want to roll back to may no longer be available by the time a problem is discovered.

By configuring a product level override, you can retain more versions for specific applications. For example, you might retain 5 previous versions of Chrome while keeping a global default of 2 for all other applications. This provides additional time for testing and a safer rollback path for frequently updated software.

## Configuring Overrides

Overrides configured here take precedence over the global options defined on the ConfigMgr Apps tab and are applied only to the selected vendor or product during publishing.

![ConfigMgr Application Retention Options Override](/_images/image-(4057).png)

To Configure Application Update Mode:

1. Right click the Vendor or Product you want to configure.
2. Select **Manage Application Updates and Retention**.
3. Under **Application Update Mode**, choose one of the following.
   1. **Create a new application** to publish each new version as a separate ConfigMgr application.
   2. **Update existing application in-place** to replace the current application with the new version.
   3. **As defined in ConfigMgr application options** to inherit the global behavior (default selection).

To confiure Application Retention Settings:

1. To customize retention behavior, enable **Override global application retention settings**.
2. Enable **Enable ConfigMgr Application Retention**.
3. Configure Retain up to n previously created applications to control how many older versions are kept.
4. Optionally enable **Remove administrative categories from retained applications** if older versions should not remain visible for deployment.
5. Optionally enable **Delete applications even if they have a deployment** if retained applications should be removed regardless of active deployments.
6. Click **OK** to save the configuration.

The override is evaluated and applied during the next Publisher [synchronization](../administration/sync-schedule.md) and affects only the selected vendor or product.

> Note
>
> For more details about Application and Retention Settings, use the \[ConfigMgr Apps Global Options page]\(../administration/configmgr-apps/options/application-creation-options.md) for reference.