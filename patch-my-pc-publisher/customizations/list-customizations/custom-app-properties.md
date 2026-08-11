# Custom App Properties option in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_&#x41;vailable at level: Product_\
_&#x41;vailable on tab: ConfigMgr Apps_

> \*\*Important\*\*
>
> This article has not been updated for Version 3.x. Once it has, this banner will be removed.

The **Custom App Properties** right-click option in Patch My PC (PMPC) Publisher allows you to override the default name, description, and icon used for applications created by the Publisher.

This option is used when you want application metadata to remain consistent across ConfigMgr and Intune apps, rather than changing automatically with each new version. The Publisher applies the configured properties when the application is first created and reapplies them whenever the application is updated.

You can configure a custom application name, description, and icon. For ConfigMgr applications, you can also define a localized application name. These settings ensure a consistent end user experience in the Intune Company Portal or ConfigMgr Software Center.

If no custom values are specified, the Publisher uses the default Patch My PC generated values.

> \*\*Note\*\*
>
> This option is especially useful for task sequence scenarios or long running deployments where a static application name or icon is required and changes between versions could cause confusion or unexpected behavior.

### Token Values

Naming conventions are built using token values. At least one token must be included.\
The available tokens are shown at the top of the dialog and can be clicked to insert them at the cursor position.

* **%VendorName%**\
  Resolves to the software vendor name.
* **%ProductName%**\
  Resolves to the product name and architecture.
* **%Version%**\
  Resolves to the application version.
* **%OriginalName%**\
  Resolves to the default Patch My PC application name.

**Example**\
Custom ConfigMgr App name configured as:

```
DEV - %OriginalName%
```

Resulting ConfigMgr application name:

```
DEV - Brave 144.1.86.148 (EXE-x64)
```

> \*\*Note\*\*
>
> Token values are populated from the Publisher catalog definition. These values are stored in English and are not automatically translated to another language.

> \*\*Important\*\*
>
> If the ConfigMgr apps global option to \[Do not include the version in the application name]\(../../../patch-my-pc-publisherv2/administration/configmgr-apps/options/application-creation-options.md#do-not-include-the-version-in-the-application-name) is enabled, the \*\*%OriginalName%\*\* token will also omit the version number. In this scenario, the original name resolves to the product name and variant/architecture only, without the version suffix.

## **Configure** Custom Application Properties

![Configure Custom Application Properties](../../../.gitbook/assets/image-\(111\).png)

To configure Custom Application Properties:

1. Right-click the Product you want to customize.
2. Select **Set custom application icon and properties**.
3. Enter a custom Application name if required. For ConfigMgr, optionally configure a Localized application name.
4. Enter a Custom Description\*.
5. Select **Browse** to upload a custom icon if required.
6. Click **OK** to save the configuration.

\*Click **Show default description** to display the original catalog description. Copy the text to the clipboard, paste it into the **Custom Description** field, and edit it to create your custom description.

![Show default description](<../../../.gitbook/assets/image-(77) (1).png>)

The custom properties are applied during the next Publisher [synchronization](../../../patch-my-pc-publisherv2/administration/sync-schedule.md) and affect newly created and updated applications for that product.
