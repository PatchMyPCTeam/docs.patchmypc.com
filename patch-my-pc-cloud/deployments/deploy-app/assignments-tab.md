# About the "Assignments" tab of a Patch My PC Cloud Deployment

_Applies to: Patch My PC Cloud_

The **Assignments** tab of the Patch My PC (PMPC) Cloud deployment wizard allows you to configure various assignments (explained below) for how you want the app to be deployed.

{% hint style="info" %}
**Note**

See [Understand Patch My PC Cloud Assignments](../technical-references/understand-assignments.md) for more details about assignments and how they work in PMPC Cloud.

You can deploy an app without assignments as detailed in [Create a Deployment Without Assignments](../technical-references/deployment-without-assignments.md).
{% endhint %}

From the **Assignments** page you can also:

* Apply a [Template](../use-template.md) of pre-configured settings to this deployment.
* [Enable Update Rings](../update-rings/create.md) for this deployment.

To add an Assignment to a deployment:

1. Click **Add Assignment** and then choose the assignment type you want to add for this deployment:
   1. **Add Required –** A mandatory application that will be installed automatically for all users or devices it is assigned to.
   2. **Add Available –** An optional application that will be available to install via the Company Portal for the primary user of the device.
   3. **Add Update Only –** Creates a separate Win32 package in Intune that exclusively updates existing installations. It will not install the software on devices where it isn't already present, and only applies if the installed variant matches the one configured in the deployment.

{% hint style="info" %}
**Note**

Assignments configured in the portal are the _source of truth_ for deployments with assignments. If you manually add any assignments outside the portal, these will not be retained when a new version is created. To ensure your assignments persist, configure them directly in the portal.

Also:

* If your deployment uses a [Retention Policy](configurations-tab/additional-tools/retention-policy.md), using the **Update Only** assignment type will also retain the relevant number of versions of the app in addition to the regular deployment types in Intune.
* Intune does not support using the **Update Only** assignment type with a deployment that is also configured to use [ESP Profiles](configurations-tab/additional-tools/esp-profiles.md). If you try to use this configuration, the **Deploy** button will be greyed out and the **Configurations** tab will show a red "**X**".\
  \
  In this scenario, you either need to:
  * Remove the **Update Only** assignment type
  * Or remove all ESP Profiles.
{% endhint %}

d. **Add Uninstall –** A mandatory uninstall that will remove the application from any users or devices it is assigned to, using the apps uninstaller.

{% hint style="info" %}
**Note**

We do not support the **Uninstall** assignment type for pkg installers.

See [Uninstall a Custom App](../../custom-apps/uninstall-a-custom-app.md) for more details on how the Custom Apps uninstall feature works and its limitations.
{% endhint %}

e. **Install App -** Allows the Intune admin to add **Required**, **Available**, or **Uninstall** assignments from within the Intune admin center.

f. **Update Only App -** Allows the Intune admin to add an **Update Only** assignment from within the Intune admin center.

{% hint style="info" %}
**Note**

See [Create a Deployment Without Assignments](../technical-references/deployment-without-assignments.md) for more details on deploying apps without assignments.

Also, if the **Installed Apps Name** field on the **Configuration** tab of a Custom App is not completed, then the **Add Update Only** and **Update Only App** assignment types are unavailable, as per the tooltip you will see if you hover your mouse over either of these assignment types.
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (3088).png" alt="Choosing the desired assignment type"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

Adding an **Available** assignment allows you to add an **Update Only** application. This ensures that any applications assigned as **Available** are updated automatically when installed via Microsoft’s Company Portal.
{% endhint %}

2. On the **Add <**_**assignment\_type**_**> Assignment** screen, choose the relevant Entra ID security groups to target for this assignment, then click **Save**.

| Option  | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Include | If checked, all of the items in this group will receive the assigned app.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| Exclude | <p>If checked, all of the items in this group will not receive the assigned app.<br><br>Can be used in conjunction with <strong>Include</strong> to exclude a subset of devices when you have an <strong>Include</strong> of a superset of devices.<br><br>For example, you want to target all of your computers except for your test devices. To achieve this, you'd configure your Entra ID groups as follows:<br><br>o Check <strong>Include</strong> for your <strong>All Company Devices</strong> Entra ID group.<br>o Check <strong>Exclude</strong> for your <strong>Test Devices</strong> Entra ID group.</p> |

<figure><img src="../../../.gitbook/assets/image (3089).png" alt="Choosing the relevant Entra ID security groups to target for this assignment" width="449"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

You will be unable to select any options under the **Add update only app for** section for an Available Assignment until you select at least option.

Also, as our portal uses application permissions to read Entra ID groups, all groups will be visible whenever you manage assignments.
{% endhint %}

The **Assignments** page updates to show the newly added assignments, including their configuration.

<figure><img src="../../../.gitbook/assets/image (3090).png" alt="“Assignments” page updates to show the newly added assignments"><figcaption></figcaption></figure>

3. Make any of the following optional modifications to the assignment(s).

| Option           | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Add Filter       | <p>The ability to add Assignment Filters you have already created in Intune to target specific managed devices for the deployment.</p><p><mark style="color:$primary;"><strong>Note</strong></mark><br>We currently do not support using managed app filters. See <a href="https://learn.microsoft.com/en-us/intune/intune-service/fundamentals/filters">Use assignment filters to assign your apps, policies, and profiles in Microsoft Intune</a> for more details.<br><br><mark style="color:green;"><strong>TIP:</strong></mark><br>You can click the red <strong>X</strong> beside a filter to remove it.</p> |
| Notifications    | When to display notifications related to this deployment.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Content Download | <p>How to download the content for the deployment:<br><br>o Foreground - The default for initial installs.<br>o Background - The default for updates.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                          |

{% hint style="info" %}
**Note**

We automatically configure these settings based on our experience and best practices, but you can modify certain settings if necessary.
{% endhint %}

{% hint style="success" %}
**Tip**

You can click **Deploy** on this page if you don’t want to add additional assignments or see the **Summary** page, which allows you to double-check the settings you’ve configured for this deployment.
{% endhint %}

4. Add any additional assignments for this deployment by clicking **Add Assignment** and repeating the steps in this section.
5.  If you are happy you have entered all of the details for the deployment correctly, click **Deploy** to deploy the app. However, we recommend you click **Next** to move to the [**Summary** ](summary-tab.md)tab, where you can verify the settings for this deployment before you deploy this app.<br>

    <figure><img src="../../../.gitbook/assets/image (3091).png" alt="Clicking &#x22;Deploy&#x22; to deploy the app"><figcaption></figcaption></figure>
