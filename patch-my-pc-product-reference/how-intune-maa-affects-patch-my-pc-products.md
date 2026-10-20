# How Microsoft Intune Multi-Admin Approval affects Patch My PC products

_Applies to: Publisher and Patch My PC Cloud_

_Microsoft Intune Multi Admin Approval_ (MAA) lets administrators add a layer of governance to sensitive Intune changes, such as creating or modifying apps and scripts, by requiring a second administrator to approve a change before it takes effect. When an MAA access policy protects a resource, Intune holds the change until an approver signs off.

Historically, MAA applied only to delegated authentication flows: changes made interactively in the Intune admin center, or via Microsoft Graph using a signed-in administrator’s credentials. Because Patch My PC (PMPC) Cloud and PMPC Publisher authenticate using the application credential flow (a service principal or app registration rather than a signed-in user), MAA access policies did not affect them.

## What’s changed

In its Week of June 22, 2026 Intune service update, Microsoft confirmed that MAA now applies to API calls made by automation through the Microsoft Graph API, not just interactive admin actions.

If your tenant has MAA access policies configured and you use service principals, automation scripts, or third-party applications to modify protected Intune resources, those calls are now subject to the same approval workflow as interactive operations.

This directly affects PMPC Cloud (service principal) and PMPC Publisher (app registration). Under an app-scoped MAA access policy, calls that don’t include the required approval headers return an HTTP 403 error, causing Patch My PC Win32 app create and update operations to fail.

To resolve this, Microsoft recommends updating automation to follow the MAA approval workflow. When an immediate code change isn’t feasible for applications using app-authentication tokens (as is the case for PMPC’s automation), Microsoft has delivered the ability to exclude specific applications from enforcement using the new **Exclusions** tab in the access policy wizard.

Adding the relevant PMPC application as an exclusion is the supported way to keep your MAA policy in place while allowing PMPC automation to continue running uninterrupted.

## What do you need to do?

### Patch My PC Cloud customers

Add the Patch My PC Cloud enterprise application as an exclusion. This enterprise application has the same Application (client) ID for all PMPC Cloud customers (**d7708ecc-2a0f-4773-a38a-ff197163f5fe**), so it can be identified consistently across tenants.

If you enable MAA and do not add the Patch My PC Cloud enterprise application as an exclusion, you will see the following behavior in PMPC Cloud:

* The **Multi Admin Approval Enabled** dialog will be shown when you try to sign in to your Cloud Company.

<figure><img src="../.gitbook/assets/image (1499).png" alt="‘Multi Admin Approval Enabled’ dialog" width="455"><figcaption></figcaption></figure>

* Clicking **Close** will close the dialog and load the Cloud Portal, but you will see the same message as a banner at the top of the Cloud Portal.

<figure><img src="../.gitbook/assets/image (1500).png" alt="‘Multi Admin Approval Enabled’ banner" width="563"><figcaption></figcaption></figure>

Until you add the Patch My PC Cloud enterprise application as an exclusion, PMPC Cloud will be limited as follows:

* All background retry actions for deployments will stop and will not be executed. Any affected deployments will move to a **Failed** state.
* Deployment updates will not be run on the user sync schedule.
* You will be unable to create, edit, delete, or recreate deployments.
* App migrations will not be allowed.
* Discovery data will still be collected, but you will be unable to create deployments from discovered apps.
* For Managed Service Providers (MSPs):
  * If an MSP child tenant has MAA enabled, that company cannot be added to an App Set.
  * If an existing App Set already includes an MSP child tenant with MAA enabled, that company will be excluded from App Set update actions.
  * If an App Set includes a child tenant with MAA enabled, the MSP will be required to remove that customer from the App Set before any changes can be saved.

Once a company adds the Patch My PC Cloud Enterprise application as an MAA exclusion and it is approved, previously disabled functionality will be available again. However, users must manually recreate any failed deployments in the portal.

{% hint style="info" %}
**Note**

You may need to wait up to an hour after the PMPC Cloud enterprise application exclusion is approved before you can use your PMPC Cloud Company. This is an Intune limitation, not PMPC Cloud.
{% endhint %}

### Patch My PC Publisher customers

Add the app registration that Publisher uses as an exclusion. Unlike Cloud, this app registration’s name and ID are unique to each customer’s tenant. Retrieve your specific Application (Client) ID from Publisher as follows:

1. Load Publisher.
2. Navigate to the **Intune Apps\* | Intune Options** tab.
3. Make a note of the value of the **Application (Client) ID** field.

**\*** This can be either the Intune Apps or Intune Apps tab.

## To add an exclusion

1. In the **Microsoft Intune admin center**, navigate to the **Tenant administration| Multi Admin Approval | Access policies** tab.

<figure><img src="../.gitbook/assets/image (1501).png" alt="Navigating to ‘Tenant administration| Multi Admin Approval | Access policies’ tab." width="563"><figcaption></figcaption></figure>

2. Click the app-scoped access policy you want to edit.
3. Click **Edit** beside **Exclusions**.

<figure><img src="../.gitbook/assets/image (1503).png" alt="Clicking ‘Edit’ beside ‘Exclusions’." width="563"><figcaption></figcaption></figure>

4. On the **Exclusions** step, click the **+** (add) control under **Apps**.

<figure><img src="../.gitbook/assets/image (1504).png" alt="Clicking + (add) control under ‘Apps’ on the ‘Exclusions’ step" width="563"><figcaption></figcaption></figure>

5. In the **Select apps to exclude** pane, use the **Search** box to find the PMPC application you want to exclude :
   1. For PMPC Cloud, search for **Patch My PC Cloud** and confirm in the Details column that the enterprise application’s ID matches the known Patch My PC Cloud client ID of **d7708ecc-2a0f-4773-a38a-ff197163f5fe**.
   2. For PMPC Publisher, search for your Publisher app registration using the **Application (Client ID)** noted in the [Patch My PC Publisher customers](how-intune-maa-affects-patch-my-pc-products.md#patch-my-pc-publisher-customers) section of [What do you need to do?](how-intune-maa-affects-patch-my-pc-products.md#what-do-you-need-to-do)
6. Check the checkbox next to the result. It appears in the **Selected** list on the right.
7. Repeat the search to add both applications if you use both products, then click **Select** to confirm.

<figure><img src="../.gitbook/assets/image (1507).png" alt="Adding the apps to exclude" width="563"><figcaption></figcaption></figure>

The applications now appear in the **Display name** list on the **Exclusions** step.

<figure><img src="../.gitbook/assets/image (1508).png" alt="Applications appearing in the ‘Display name’ list on the ‘Exclusions’ step" width="563"><figcaption></figcaption></figure>

8. Click **Review + submit for approval**.
9. On the **Review + submit for approval** step, enter a **Business justification**, then click **Submit for approval**.

{% hint style="info" %}
**Note**

Editing an MAA access policy is itself a change governed by MAA. Your exclusion request will be placed in **Needs review** status and must be approved by a second administrator (a member of the policy’s approver group) before it takes effect.
{% endhint %}

Once approved, the excluded applications are listed under the **Apps** section of the policy, and Patch My PC operations using those applications will no longer be held by the MAA workflow.

<figure><img src="../.gitbook/assets/image (1509).png" alt="Approved Access Policy" width="563"><figcaption></figcaption></figure>
