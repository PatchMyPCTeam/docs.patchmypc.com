# Product Export settings section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Product Export** section on the **Advanced** tab of Patch My PC (PMPC) Publisher allows you to export a list of enabled products and their configuration from the Publisher into a CSV file. The export includes product-level settings and right-click options, which makes it useful for documentation, audits, change reviews, and comparing configurations.

<figure><img src="../../../.gitbook/assets/image (4).png" alt="&#x27;Product Export&#x27; section" width="563"><figcaption></figcaption></figure>

Some exported properties may appear populated even if they are not actively in use. This occurs when a property has a default value defined by the Publisher. For example, Intune apps and Intune updates may show a maximum run time value that is only applicable when the same product is published to ConfigMgr.

## Export a List of Products

To export a list of products:

1. Open the Publisher and select the Advanced tab.
2. Scroll down to the Product Export section.
3. Select the checkbox for each product type you want to export.
4. Select **Export**.
5. Choose a location to save the CSV file.

The available export options align with the main product categories in the Publisher. These include WSUS updates, ConfigMgr apps, Intune apps, and Intune updates. Only product types that are currently available and enabled in the Publisher can be selected

Below is an example of an exported CSV.

<figure><img src="../../../.gitbook/assets/image (3951).png" alt="Exported product CSV example" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

A product type checkbox is only selectable when two conditions are met. The product type must be enabled using the main checkbox at the top of its corresponding tab, and at least one product of that type must exist. If either condition is not met, the checkbox will appear disabled.
{% endhint %}

{% hint style="danger" %}
**Important**

The Product Export CSV is intended for reference and reporting purposes. It is not designed to be imported back into the Publisher.
{% endhint %}
