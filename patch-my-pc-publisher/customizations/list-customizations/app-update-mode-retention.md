# App Update Mode & Retention option in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_&#x41;vailable at level: Vendor, Product_\
_&#x41;vailable on tab: ConfigMgr Apps_

The **App Update Mode & Retention** right-click option in Patch My PC (PMPC) Publisher allows you to override the global Microsoft ConfigMgr application behavior for a specific vendor or individual product.

> \*\*Note\*\*
>
> Global behavior for application updates and retention is configured under the \[Application Creation Options]\(../../manage/configmgr-apps-tab/base-install-options/application-creation-options.md) section of the \[Base Install Options]\(../../manage/configmgr-apps-tab/base-install-options/) tab.

## When Overrides Are Useful

Overrides are commonly used for applications that update frequently, such as web browsers.

Products like Google Chrome, Microsoft Edge, and Mozilla Firefox release updates often. Issues introduced by these updates may not be identified immediately. If a global retention setting keeps only a small number of previous versions (for example, two), the version you want to roll back to may no longer be available by the time a problem is discovered.

By configuring a product-level override, you can retain more versions for specific applications. For example, you might retain five previous versions of Chrome, whilst keeping a global default of two for all other applications. This provides additional time for testing and a safer rollback path for frequently updated software.

## Configuring Overrides

Overrides configured using the **App Update Mode & Retention** right-click option take precedence over the global options (defined on the under the [Application Creation Options](../../manage/configmgr-apps-tab/base-install-options/application-creation-options.md) section of the [Base Install Options](../../manage/configmgr-apps-tab/base-install-options/) tab), and are applied only to the selected vendor or product during publishing.

To configure **Application Update Mode**:

1. Right-click the Vendor or Product you want to configure and select **App Update Mode & Retention**.\
   \
   The **ConfigMgr Application Retention Options** dialog appears.

!['ConfigMgr Application Retention Options' dialog appears.](/_images/image-(4794).png)

2. Under **Application Update Mode**, choose one of the following:
   1. **Create a new application** to publish each new version as a separate ConfigMgr application.
   2. **Update existing application in-place** to replace the current application with the new version.
   3. **As defined in ConfigMgr application options** to inherit the global behavior (default selection).
3. Click **OK** if you don't want to configure any additional settings.
4. If you want to configure **Application Retention Settings** check the **Override global application retention settings** checkbox.
5. If required, check the **Enable ConfigMgr Application Retention** checkbox and configure the value for the **Retain up to&#x20;**_**n**_**&#x20;previously created applications** where _**n**_ is the number of older versions you want to keep.
6. Optionally enable **Remove administrative categories from retained applications** if older versions should not remain visible for deployment.
7. Optionally enable **Delete applications even if they have a deployment** if retained applications should be removed regardless of active deployments.
8. Click **OK** to save the configuration.

The override is evaluated and applied during the next Publisher [synchronization](../../manage/sync-schedule-tab/) and affects only the selected vendor or product.

> \*\*Note\*\*
>
> See \[Application Creation Options]\(../../manage/configmgr-apps-tab/base-install-options/application-creation-options.md) for more details about Application and Retention Settings.