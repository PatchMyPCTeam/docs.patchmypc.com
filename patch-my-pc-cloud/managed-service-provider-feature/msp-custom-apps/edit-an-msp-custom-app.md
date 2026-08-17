# Edit an MSP Custom App

_Applies to: Patch My PC Cloud_

To edit a Custom App for a Managed Service Provider (MSP) you’ve created in Patch My PC (PMPC) Cloud, follow the [Modify a Custom App](../../custom-apps/modify-a-custom-app.md) process for the relevant app.

{% hint style="info" %}
**Note**

When you view the properties of a Custom App for an MSP, the **Source** field shows the name of the company that created the app.
{% endhint %}

You can also change:

* The visibility of the Custom App by selecting the new setting under the **Custom App Visibility** section of the **Configurations** page.
* Which child companies the app is visible on.

For example:

| Current setting         | New Setting        | Impact                                                                          |
| ----------------------- | ------------------ | ------------------------------------------------------------------------------- |
| No Customers            | All Customers      | Custom App will appear in the App Catalog of all child companies.               |
| No Customers            | Specific Customers | Custom App will only appear in the App Catalog of the selected child companies. |
| All /Specific Customers | No Customers       | Custom App will be removed from the App Catalog of all child companies.         |

{% hint style="warning" %}
**Important**

If an app has been shared with and deployed from that company, changing either of the above settings may generate the "**Are you sure?**" popup warning you of the impact and asking you to confirm the deletion of the deployment of this app at the child company.

<img src="../../../.gitbook/assets/image (1045).png" alt="“Are you sure” popup" data-size="original">
{% endhint %}

{% hint style="info" %}
**Note**

If a child company has been selected in the **Customers** field, you cannot remove it if the app has been deployed from there. You must delete the deployment first, after which you can remove that child company from the list.
{% endhint %}
