# License Information section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The first time you load Patch My PC (PMPC) Publisher, the **General tab** is selected. The **License Information** section is empty and the **No license key entered, unable to show subscription information** message is shown.

![](/_images/image-(4839).png)

You have three options at this point:

* [Activate a License](license-information.md#activate-a-license)
* [Request a free 30-day trial](license-information.md#request-a-free-30-day-trial)
* [Enable limited trial mode](license-information.md#enable-limited-trial-mode)

Until you do one of these, you will be unable to continue using Publisher.

## Activate a License

If you purchased a license or requested a free 30-day trial, you will receive an email containing your 20-character license key.

To activate your license:

Enter your license key in the **License Key** field and click **Validate**

![](/_images/image-(4840).png)

If validation is successful, you will see the **License validated successfully** message.

![License validation successful dialog](/_images/image-(4841).png)

The **License Information** section updates to show the details of your license, and Publisher unlocks the corresponding features so you can proceed with configuration, customization, and publishing.

![Updated 'License Information' section](/_images/image-(4846).png)

> \*\*Note\*\*
>
> See the \[Subscription Information]\(license-information.md#subscription-information) section below for more details.

If validation fails, the dialog indicates that the key could not be verified and typically suggests checking either the license value or [network connectivity](../../requirements/core-requirements.md#network).

> \*\*Note\*\*
>
> If you started your trial through Patch My PC Cloud, your license key can also be retrieved directly from the Cloud portal by navigating to \*\*Settings | Subscription\*\* and clicking on the obfuscated license key.

![](/_images/image-(411) (1).png>)

## Request a free 30-day trial

You can [request a free 30-day trial](https://patchmypc.com/free-trial) of Publisher from our website to have your license key emailed to you. Once you have your license, you can then [activate it](license-information.md#activate-a-license).

## Enable limited trial mode

If you do not have a license or trial key, you can use Publisher in _Limited Trial Mode_. This allows you to evaluate Publisher functionality using a predefined set of products.

> \*\*Note\*\*
>
> See \[Products Available in Limited Trial Mode]\(../../technical-references/products-available-limited-trial-mode.md) for more information on the products available in this mode.

To enable **limited trial mode**:

1. Launch Publisher.
2. Click the **General** tab.
3. Under the **License Information** section, check the **Enable limited trial mode** checkbox.

!['Enable limited trial mode' checkbox](/_images/image-(4844).png)

4. On the **Switch To Trial Catalog Mode** dialog, click **Yes** to continue.

!['Switch To Trial Catalog Mode' dialog](/_images/image-(4845).png)

> \*\*Important\*\*
>
> Enabling Trial Mode overwrites any product selections previously made in non-trial mode.

Once enabled, Publisher automatically populates the product catalog with a limited set of applications that are available for evaluation.

> \*\*Note\*\*
>
> See \[Products Available in Limited Trial Mode]\(../../technical-references/products-available-limited-trial-mode.md) for more information on the products available in this mode.

## Subscription Information

This section displays details about your current Patch My PC license, including the subscription tier, license validity period, and the number of devices covered.

This information helps confirm Publisher is correctly licensed for your environment, and your device count aligns with your deployment scope.

<table><thead><tr><th width="125" valign="top">Field</th><th valign="top">Shows the...</th></tr></thead><tbody><tr><td valign="top">Subscription</td><td valign="top"><p>Patch My PC license tier currently applied (for example, <em>Enterprise Premium</em>), which determines the features, products, and capabilities available within Publisher.</p><p><mark style="color:$primary;"><strong>Note:</strong></mark></p><p>See <a href="https://patchmypc.com/pricing/">Patch My PC Pricing</a> for more details of the various subscriptions we offer.</p></td></tr><tr><td valign="top">Expires</td><td valign="top"><p>Expiration date of the current license/trial. Publisher will continue to function normally until this date.</p><p>Once the license expires, new applications and updates will no longer be published.</p><p>Any applications and updates that were published prior to expiration will remain available and unaffected.</p><p>To avoid interruptions, renewal or trial extension should be planned ahead of the expiration date.</p></td></tr><tr><td valign="top">Devices</td><td valign="top">Maximum number of devices the license covers. This should align with the number of managed devices that will <em>receive</em> applications or updates published by Publisher, which may differ from the total number of managed devices in your environment.</td></tr></tbody></table>