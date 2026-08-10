# Modify/Recreate Branding in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

Once you have created a branding app in Patch My PC (PMPC) Cloud, you can modify it.

<blockquote class="wp-block-quote">
<p>**Note**&#x20;</p>
<p>The process for modifying a branding app is the same, regardless of the type (Classic or Modern (PSADT)).&#x20;</p>
</blockquote>

To modify a branding app:

1. Navigate to **Settings | Branding**

![Navigating to ‘Settings | Branding'](/_images/image-(536).png "Navigating to ‘Settings | Branding’")

2. Click the ellipsis (`⋮`) button beside the relevant branding app and select the action you want to perform:
   1. [Edit](modify-recreate-branding.md#edit-branding)
   2. [Recreate](modify-recreate-branding.md#recreate-branding)

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>See [Delete Branding](delete-branding.md) for details on how to delete a branding app.</p>
<p>You won’t be able to manage a branding app until it has been deployed successfully.</p>
<p>Also, see [Managing Localizations](localizations.md) for details on how to modify the localization used by a branding app.</p>
</blockquote>

### Edit Branding

Editing a branding app allows you to make any changes as though you were [Adding a Branding App](add-branding.md).

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>The process for editing a branding app is the same, regardless of the type (Classic or Modern (PSADT).</p>
</blockquote>

If you want to reset the logo used by a branding app:

1. Click **Edit** on the ellipsis (`⋮`) menu.

![Clicking the ellipsis (⋮) button beside the relevant branding app and selecting the action you want to perform:](/_images/image-(3743).png "Clicking the ellipsis (⋮) button beside the relevant branding app and selecting the action you want to perform:")

2. In the **Company Logo** area, click **Use Default**.

![Clicking 'Use Default' in the 'Company Logo' area](/_images/image-(538).png "Clicking &#x27;Use Default&#x27; in the &#x27;Company Logo&#x27; area")

The **Branding** page resets just the logo to the default for this branding app.

![Branding logo reset](/_images/image-(539).png "Branding logo reset")

3. If you want to switch branding types, select the relevant option under **Branding Types**

![Select the relevant option under 'Branding Types' if you want to change the type](/_images/image-(540).png "Select the relevant option under &#x27;Branding Types&#x27; if you want to change the type")

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>If you switch branding types, you will see the **Are you sure** prompt, asking you to confirm the switch.&#x20;</p>
<p>!['Are you sure' prompt](/_images/image-(541 "'Are you sure' prompt").png>)</p>
<p>Click **Confirm** to continue, but please note that by switching branding types, you will lose any configured localizations and settings configured for this branding app. Once you switch types, you should verify your localizations are configured as detailed in [Manage Localizations in Cloud](localizations.md).</p>
</blockquote>

4. Make any other required changes.
5. Click **Save** to save your changes to Intune, which will deploy the modified version to all of the resources this branding app is assigned to.

![Clicking 'Save' to save your changes](/_images/image-(542).png "Clicking &#x27;Save&#x27; to save your changes")

The **Success - Branding updated** notification is shown.

!['Success - Branding updated' notification](/_images/image-(3744).png "&#x27;Success - Branding updated&#x27; notification")

Once your branding app has been updated with the default PMPC logo, the **Status** and **Last Updated** fields will be updated to show when this branding app was last updated.

!['Status' and 'Last Updated' fields updated to show when this branding app was last updated](/_images/image-(3745).png "&#x27;Status&#x27; and &#x27;Last Updated&#x27; fields updated to show when this branding app was last updated")

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>If you look in the **Events** section, you see a message stating the branding app was updated.</p>
</blockquote>

5. The branding app will be automatically updated on all of the assigned resources. There is no need for you to [Recreate Branding](modify-recreate-branding.md#recreate-branding) as in previous versions.

### Recreate Branding

The **Recreate** function allows you to delete and recreate a branding app in Intune if you detect an issue with it.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>You can only recreate branding apps that have either been deployed successfully or failed.</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>The process for recreating a branding app is the same, regardless of the type (Classic or Modern (PSADT)).</p>
</blockquote>

To recreate branding:

1. Click **Recreate** on the ellipsis (`⋮`) menu.

![Clicking 'Recreate' on the ellipsis (⋮) menu](/_images/image-(3746).png "Clicking &#x27;Recreate&#x27; on the ellipsis (⋮) menu")

2. On the **Are you sure you want to recreate <**_**branding\_app\_name**_**>** dialog box click **Yes**.

![Clicking "Yes"](/_images/image-(3205).png "Clicking &#x22;Yes&#x22;")

The **Success - Recreating the branding <**_**branding\_app\_name**_**>** notification is shown.

![](/_images/image-(3747).png)

Once the branding app has been recreated, the **Status** and **Last Updated** fields update to show when this branding app was last modified.

!['Status' and 'Last updated' fields updated to show when this branding app was last modified](/_images/image-(3748).png "&#x27;Status&#x27; and &#x27;Last updated&#x27; fields updated to show when this branding app was last modified")

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>If you look in the **Events** node, you see a message stating the branding app was recreated</p>
</blockquote>