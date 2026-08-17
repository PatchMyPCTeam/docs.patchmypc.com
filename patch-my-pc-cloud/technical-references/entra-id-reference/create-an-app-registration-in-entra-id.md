# Create an App Registration in Entra ID

_Applies to: Patch My PC Cloud_

There may be some scenarios (such as [Recover Your Company](../../manage/settings/company-settings/recover-company.md) ) where you need to create an App Registration in Entra ID for use with Patch My PC (PMPC) Cloud.

{% hint style="danger" %}
**Important**

Once you create an App Registration, it must be used within 72 hours; otherwise, it will be considered expired, and you will need to create a new one.
{% endhint %}

We use this process to verify you are an Application Administrator or a higher privilege user (such as a Global Admin), in the same Entra ID tenant as the PMPC Company being managed.

To create an App Registration:

1. Sign in to the Microsoft Azure portal using an account with the Global Admin role and navigate to the [App Registrations](https://portal.azure.com/#view/Microsoft_AAD_RegisteredApps/ApplicationsListBlade) blade.

{% hint style="danger" %}
**Important**

You must use an account in the same Microsoft 365 subscription (tenant) as your PMPC Company.
{% endhint %}

<figure><img src="../../../.gitbook/assets/image-(542).png" alt="Navigating to the &#x27;App registrations&#x27; blade" width="563"><figcaption></figcaption></figure>

2. Click **New registration**.

<figure><img src="../../../.gitbook/assets/image (1245).png" alt="Clicking &#x27;New registration&#x27;" width="563"><figcaption></figcaption></figure>

3. In the **Name** field, enter **PMPC Recovery**, then click **Register**.

<figure><img src="../../../.gitbook/assets/image (1246).png" alt="Entering &#x27;PMPC Recovery&#x27; then clicking &#x27;Register&#x27;" width="563"><figcaption></figcaption></figure>

4. Make a note of the following values:
   1. **Application (client) ID**
   2. **Object ID**
   3. **Directory (tenant) ID**

<figure><img src="../../../.gitbook/assets/image-(545).png" alt="Noting the required values" width="563"><figcaption></figcaption></figure>

5. Navigate to **Manage | API Permissions**.

<figure><img src="../../../.gitbook/assets/image-(546).png" alt="Navigating to &#x27;Manage | API Permissions&#x27;" width="563"><figcaption></figcaption></figure>

6. Under the **Configured permissions** section, click **Add a permission**.

<figure><img src="../../../.gitbook/assets/image-(547).png" alt="Clicking &#x27;Add a permission&#x27;" width="563"><figcaption></figcaption></figure>

7. In the **Request API permissions** blade, click **Microsoft Graph**.

<figure><img src="../../../.gitbook/assets/image-(548).png" alt="Clicking &#x27;Microsoft Graph&#x27;" width="563"><figcaption></figcaption></figure>

8. In the **Request API permissions** blade, click **Application permissions**.

<figure><img src="../../../.gitbook/assets/image-(549).png" alt="Clicking “Application permissions”" width="563"><figcaption></figcaption></figure>

9. In the **Select permissions** field, type **AuditLog**, then expand this section and check the **AuditLog.Read.All** permission checkbox.

<figure><img src="../../../.gitbook/assets/image-(550).png" alt="Checking the &#x27;AuditLog.Read.All&#x27; permission checkbox" width="563"><figcaption></figcaption></figure>

10. Click **Add permissions**.

<figure><img src="../../../.gitbook/assets/image-(551).png" alt="Clicking &#x27;Add permissions&#x27;" width="563"><figcaption></figcaption></figure>

11. On the **API permissions** screen, under the **Configured permissions** section, click **Grant admin consent for <**_**your\_tenant\_name**_**>**.

<figure><img src="../../../.gitbook/assets/image-(552).png" alt="Clicking &#x27;Grant admin consent for <your_tenant_name>&#x27;" width="563"><figcaption></figcaption></figure>

12. On the **Grant admin consent confirmation** popup, click **Yes**.

<figure><img src="../../../.gitbook/assets/image-(553).png" alt="Clicking &#x27;Yes&#x27; on the &#x27;Grant admin consent confirmation&#x27; popup" width="563"><figcaption></figcaption></figure>

The **Grant consent - Grant consent successful** notification is shown and the **Status** for the **AuditLog.Read.All** permission changes to a green tick.

<figure><img src="../../../.gitbook/assets/image-(554).png" alt="&#x27;Grant consent - Grant consent successful notification&#x27; shown and the &#x27;Status&#x27; for the &#x27;AuditLog.Read.All&#x27; permission changes to a green tick." width="563"><figcaption></figcaption></figure>

13. Navigate to **Certificates and secrets**.

<figure><img src="../../../.gitbook/assets/image (1257).png" alt="Navigating to &#x27;Certificates and secrets&#x27;" width="563"><figcaption></figcaption></figure>

14. Under the **Client secrets** section, click **New client secret**.

<figure><img src="../../../.gitbook/assets/image (1258).png" alt="Clicking &#x27;New client secret&#x27; under the &#x27;Client secrets&#x27; section" width="563"><figcaption></figcaption></figure>

15. In the **Add a client secret** panel, type **PMPC Recovery**, then click **Add**.

<figure><img src="../../../.gitbook/assets/image (1259).png" alt="Typing &#x27;PMPC Recovery&#x27; in the &#x27;Description&#x27; field, then clicking &#x27;Add&#x27;" width="563"><figcaption></figcaption></figure>

The new Client Secret appears along with the **Update application credentials - Successfully updated application PMPC Recovery credentials** notification.

<figure><img src="../../../.gitbook/assets/image (1260).png" alt="New Client Secret and the &#x27;Update application credentials - Successfully updated application PMPC Recovery credentials&#x27; notification" width="563"><figcaption></figcaption></figure>

16. Make a note of the **Value** of the **PMPC Recovery** client secret.
