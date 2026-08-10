# Create an App Registration in Entra ID

_Applies to: Patch My PC Cloud_

There may be some scenarios (such as [Recover Your Company](../../manage/settings/company-settings/recover-company.md) ) where you need to create an App Registration in Entra ID for use with Patch My PC (PMPC) Cloud.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>Once you create an App Registration, it must be used within 72 hours; otherwise, it will be considered expired, and you will need to create a new one.</p>
</blockquote>

We use this process to verify you are an Application Administrator or a higher privilege user (such as a Global Admin), in the same Entra ID tenant as the PMPC Company being managed.

To create an App Registration:

1. Sign in to the Microsoft Azure portal using an account with the Global Admin role and navigate to the [App Registrations](https://portal.azure.com/#view/Microsoft_AAD_RegisteredApps/ApplicationsListBlade) blade.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>You must use an account in the same Microsoft 365 subscription (tenant) as your PMPC Company.</p>
</blockquote>

![Navigating to the 'App registrations' blade](/_images/image-(1244).png "Navigating to the &#x27;App registrations&#x27; blade")

2. Click **New registration**.

![Clicking 'New registration'](/_images/image-(1245).png "Clicking &#x27;New registration&#x27;")

3. In the **Name** field, enter **PMPC Recovery**, then click **Register**.

![Entering 'PMPC Recovery' then clicking 'Register'](/_images/image-(1246).png "Entering &#x27;PMPC Recovery&#x27; then clicking &#x27;Register&#x27;")

4. Make a note of the following values:
   1. **Application (client) ID**
   2. **Object ID**
   3. **Directory (tenant) ID**

![Noting the required values](/_images/image-(1247).png "Noting the required values")

5. Navigate to **Manage | API Permissions**.

![Navigating to 'Manage | API Permissions'](/_images/image-(1248).png "Navigating to &#x27;Manage | API Permissions&#x27;")

6. Under the **Configured permissions** section, click **Add a permission**.

![Clicking 'Add a permission'](/_images/image-(1249).png "Clicking &#x27;Add a permission&#x27;")

7. In the **Request API permissions** blade, click **Microsoft Graph**.

![Clicking 'Microsoft Graph'](/_images/image-(1250).png "Clicking &#x27;Microsoft Graph&#x27;")

8. In the **Request API permissions** blade, click **Application permissions**.

![Clicking "Application permissions"](/_images/image-(1251).png "Clicking “Application permissions”")



9. In the **Select permissions** field, type **AuditLog**, then expand this section and check the **AuditLog.Read.All** permission checkbox.

![Checking the 'AuditLog.Read.All' permission checkbox](/_images/image-(1252).png "Checking the &#x27;AuditLog.Read.All&#x27; permission checkbox")

10. Click **Add permissions**.

![Clicking 'Add permissions'](/_images/image-(1253).png "Clicking &#x27;Add permissions&#x27;")

11. On the **API permissions** screen, under the **Configured permissions** section, click **Grant admin consent for <**_**your\_tenant\_name**_**>**.

![](/_images/image-(1254).png)

12. On the **Grant admin consent confirmation** popup, click **Yes**.

![Clicking 'Yes' on the 'Grant admin consent confirmation' popup](/_images/image-(1255).png "Clicking &#x27;Yes&#x27; on the &#x27;Grant admin consent confirmation&#x27; popup")

The **Grant consent - Grant consent successful** notification is shown and the **Status** for the **AuditLog.Read.All** permission changes to a green tick.

!['Grant consent - Grant consent successful notification' shown and the 'Status' for the 'AuditLog.Read.All' permission changes to a green tick.](/_images/image-(1256).png "&#x27;Grant consent - Grant consent successful notification&#x27; shown and the &#x27;Status&#x27; for the &#x27;AuditLog.Read.All&#x27; permission changes to a green tick.")

13. Navigate to **Certificates and secrets**.

![Navigating to 'Certificates and secrets'](/_images/image-(1257).png "Navigating to &#x27;Certificates and secrets&#x27;")

14. Under the **Client secrets** section, click **New client secret**.

![Clicking 'New client secret' under the 'Client secrets' section](/_images/image-(1258).png "Clicking &#x27;New client secret&#x27; under the &#x27;Client secrets&#x27; section")

15. In the **Add a client secret** panel, type **PMPC Recovery**, then click **Add**.

![Typing 'PMPC Recovery' in the 'Description' field, then clicking 'Add'](/_images/image-(1259).png "Typing &#x27;PMPC Recovery&#x27; in the &#x27;Description&#x27; field, then clicking &#x27;Add&#x27;")

The new Client Secret appears along with the **Update application credentials - Successfully updated application PMPC Recovery credentials** notification.

![New Client Secret and the 'Update application credentials - Successfully updated application PMPC Recovery credentials' notification](/_images/image-(1260).png "New Client Secret and the &#x27;Update application credentials - Successfully updated application PMPC Recovery credentials&#x27; notification")

16. Make a note of the **Value** of the **PMPC Recovery** client secret.