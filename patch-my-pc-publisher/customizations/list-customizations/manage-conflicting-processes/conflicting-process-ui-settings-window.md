# Conflicting Process UI Settings window in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_&#x41;vailable at level: All Custom Products, All Products, Vendor, Product_\
_&#x41;vailable on tab: WSUS Updates, ConfigMgr Apps, Intune Apps, Intune Updates_

The **Conflicting Process UI Settings** window in Patch My PC (PMPC) Publisher lets you customize the end-user notification shown when an application must close to complete an update.

<figure><img src="../../../../.gitbook/assets/image (3983).png" alt="Conflicting Process UI Settings" width="450"><figcaption></figcaption></figure>

These settings allow you to control branding, organization identity, language, and the notification text displayed to users during conflicting process scenarios.

{% hint style="info" %}
**Note**

The **Conflicting Process UI Settings** window is leveraged when the [Notify the user to close the application](policy-section.md#notify-the-user-to-close-the-application) policy is selected.
{% endhint %}

{% hint style="danger" %}
**Important**

Branding and localization settings are global. You cannot configure different branding or localization profiles for different applications or updates. The configured branding and language settings apply to every application or update where conflicting process management is enabled.

For customers using an MSP or MSP Plus license with multiple Intune tenants configured, branding and localization settings are global per tenant. Each configured tenant maintains its own branding configuration, but all applications and updates within that tenant share the same branding and localization settings.
{% endhint %}

## Is a separate Client or Agent required to show the Notification?

No. A separate client or agent is not required to display conflicting process notifications.

When conflicting process management is enabled, the notification configuration is packaged directly with the application or update. Notification text, localization, and behavior are stored in XML configuration files, while the company logo is included as a separate image file alongside the package content.

## How does Branding work?

During installation, Patch My PC ScriptRunner (which manages the installation on the device), reads this XML to determine how notifications should be displayed, including which branding image to use and what text is shown to the user. This ensures a consistent notification experience across all applicable deployments.

In the example below, the highlighted files show the components involved in displaying the end-user notification. These files are downloaded to the local cache folder alongside the application or update package and are used at runtime to render the notification experience.

<figure><img src="../../../../.gitbook/assets/image (133).png" alt="Manage Conflicting Processes Files" width="549"><figcaption></figcaption></figure>

{% hint style="danger" %}
**Important**

Any changes made to branding or notification content apply to newly published applications and updates. Existing deployments must be [republished](../republish-product.md) for updated branding settings to be included.
{% endhint %}

## Company Logo

The **Company Logo** setting allows you to display a custom banner image in conflicting process notifications shown to end users.

The configured logo appears at the top of the notification experience in the bottom right of the screen. This helps users clearly identify that the notification is coming from your organization.

Supported image formats include BMP, GIF, JPG, and PNG.

The recommended image size is 370 x 100 pixels to ensure proper scaling and alignment within the notification UI.

You can manage the company logo using the following options:

* **Set Custom** to upload a custom image.
* **Use Default** to revert to the default banner image.
* **Preview** to see how the logo will appear to end users before saving the configuration.

<figure><img src="../../../../.gitbook/assets/image (132).png" alt="Notification Preview" width="282"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

Clicking **Close All and Install** or **Snooze Install** in the preview window only closes the preview. These buttons do not trigger any installation or enforcement actions and are provided for visualization purposes only.
{% endhint %}

## Organization Name Configuration

The **Organization Name** field allows you to specify the organization name displayed in notification text.&#x20;

<figure><img src="../../../../.gitbook/assets/image (824).png" alt="&#x27;Organization Name&#x27; field" width="423"><figcaption></figcaption></figure>

You can reference this value dynamically within notification messages using the supported variables.

<figure><img src="../../../../.gitbook/assets/image (136).png" alt="The Organization Name replaces this text in the notification window" width="282"><figcaption></figcaption></figure>

## Localization

The **Localization** section controls the language and user-facing text displayed in conflicting process notifications.

<figure><img src="../../../../.gitbook/assets/image (878).png" alt="&#x27;Localization&#x27; section" width="420"><figcaption></figcaption></figure>

### Selected Language

**English** is the default language. The **Selected language** dropdown shows the language currently being edited, which may be English or another configured language.

To add or manage languages, click **Add/Remove**, which opens the **Select Language for Conflicting Processes UI Translation** window, where you can choose languages from the available list, add them to the selected languages list, and define which language is the default.

<figure><img src="../../../../.gitbook/assets/image (879).png" alt="&#x27;Select Language for Conflicting Processes UI Translation&#x27; window" width="488"><figcaption></figcaption></figure>

At runtime, Patch My PC ScriptRunner detects the device's locale and displays notifications in the matching language if it's configured. If the device locale does not match any configured language in the **Selected Languages** list, the default language is used to display the notification.

#### Add or Remove Languages

To add or remove languages from the **Selected Languages** list:

1. In the **Available Languages** list, select one or more languages and click **Add** to move them to the **Selected Languages** list. Languages in the selected list are available for notification localization.
2. To remove a language, select it from the **Selected Languages** list and click **Remove**.
3. Use the **Default language** dropdown to choose which language is used when a device locale does not match any of the selected languages.
4. Select **OK** to save changes.

### Intent

The **Intent** setting controls the notification context, such as **Install**, **Update**, or **Uninstall**. Each intent has its own set of localized text fields.

When you change the intent, the text fields update to reflect the messaging for that specific intent. This ensures the end user clearly understands whether an application is being installed, updated, or uninstalled.

### Custom Notification Text and Variables

You can customize all notification text fields, including the header, main message, deferral messaging, and default actions. These fields support variables that are replaced dynamically at runtime.

Available variables include organization name, product name, deferral count, and deferral date.

To insert a variable into any text field, select the field where you want the variable to appear, then select the variable from the list at the bottom of the form. The variable is inserted at the current cursor position and is expanded automatically at runtime.

{% hint style="info" %}
**Note**

The product name is populated automatically and cannot be customized.
{% endhint %}
