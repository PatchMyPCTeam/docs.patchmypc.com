# Configure App Info in a Patch My PC Cloud Deployment

_Applies to: Patch My PC Cloud_

The **App Info** tool of the Patch My PC (PMPC) Cloud deployment wizard allows you to define default values for items that will be included in the app’s metadata when it is packaged to Intune.&#x20;

Any values set for the following items will appear in the app’s properties when viewed in the Intune admin center:

* **Vendor**<mark style="color:red;">**\***</mark>**&#x20;-** The vendor of the app.
* **Owner –** The name of the owner of this app.
* **Description**<mark style="color:red;">**\***</mark>**&#x20;-** A description of the app.
* **Notes –** Notes about the app that we send to Intune when we create a deployment.
* **Information URL -** Link to a website or documentation that has more information about the app.
* **Privacy URL -** A link for people who want to learn more about the app's privacy settings and terms
* **Developer –** The name/contact details of the developer as this is a plain text field.
* **Set App as Featured -** If checked, allows this app to appear as a featured app in the Company Portal. Once the app has been deployed, the **Show this as a featured app in the Company Portal** setting on the app’s properties should be set to **Yes** in the Intune admin center.

<mark style="color:red;">**\***</mark> denotes a required field

{% hint style="success" %}
**Tip**

If you make a mistake and want to reset the information in this section, click **Reset to Default** followed by **OK** on the **Are you sure you want to reset to the default values?** dialog box.

Also, if the **App Info** section has been configured, you can view it as part of the app’s properties in the Microsoft Intune admin center.
{% endhint %}

To manage the App Info for a Deployment:

1. Click the **App Info** tool.

<figure><img src="../../../../../.gitbook/assets/image (660).png" alt="Clicking the &#x27;App Info&#x27; tool" width="563"><figcaption></figcaption></figure>

2. Configure the settings as required.

{% hint style="info" %}
**Note**

We pre-populate this screen with the information received from the vendor/added by us.
{% endhint %}

<figure><img src="../../../../../.gitbook/assets/image (661).png" alt="&#x27;App Info&#x27; tool" width="563"><figcaption></figcaption></figure>

## Next Steps

If you do not want to configure any additional settings, click **Next** to move to the [Assignments](../../assignments-tab.md) tab.

Otherwise, navigate to the relevant tool to configure the required settings, which are explained in the relevant section.

<figure><img src="../../../../../.gitbook/assets/image (662).png" alt="Clicking &#x27;Next&#x27;" width="563"><figcaption></figcaption></figure>
