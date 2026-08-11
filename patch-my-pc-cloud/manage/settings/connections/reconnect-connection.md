# Reconnect a Connection in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

If your Patch My PC (PMPC) Cloud Portal loses its connection to your Intune tenant (for example, if a Global Admin revokes the [Permissions required for Intune Apps](https://docs.patchmypc.com/patch-my-pc-cloud/cloud-reference/cloud-permissions-reference/permissions-required-for-intune-apps) from within Intune), you can use this process to re-establish the connection to your previously connected Intune tenant, which will re-grant the required permissions.

{% hint style="info" %}
**Note**

The reconnect button is only available once an Intune connection has been established.

You will only be able to reconnect to an Intune tenant you’ve previously connected to, based on the tenant ID we have stored in the Cloud Portal’s database.
{% endhint %}

To reconnect your Cloud Portal to an Intune tenant you’ve previously connected to:

1. Navigate to **Settings | Connections**

<figure><img src="../../../../.gitbook/assets/image (310).png" alt="Navigating to &#x27;Settings | Connections&#x27;" width="563"><figcaption></figcaption></figure>

2. Click the reconnect icon beside your Intune connection.

<figure><img src="../../../../.gitbook/assets/image (311).png" alt="Clicking the reconnect icon beside your Intune connection" width="563"><figcaption></figcaption></figure>

3. Enter the Entra ID you used to onboard to PMPC Cloud or click to select the relevant account from the list of already signed-in accounts. Then click **Next**.

<figure><img src="../../../../.gitbook/assets/image (304).png" alt="&#x27;Sign in&#x27; prompt" width="329"><figcaption></figcaption></figure>

4. Enter the password and click **Sign in**.

<figure><img src="../../../../.gitbook/assets/image (305).png" alt="Entering the password" width="329"><figcaption></figcaption></figure>

5. On the **Permissions requested** screen, click **Accept**.

<figure><img src="../../../../.gitbook/assets/image (306).png" alt="Clicking &#x27;Accept&#x27; on the &#x27;Permissions requested&#x27; screen" width="330"><figcaption></figcaption></figure>

If the reconnection is successful, the **Connections** page is redisplayed, showing **Connected** if your Cloud Portal is now reconnected to your Intune tenant.

<figure><img src="../../../../.gitbook/assets/image (307).png" alt="New Intune connection" width="563"><figcaption></figcaption></figure>
