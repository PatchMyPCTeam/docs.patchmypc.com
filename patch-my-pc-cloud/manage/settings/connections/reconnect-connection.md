# Reconnect a Connection in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

If your Patch My PC (PMPC) Cloud Portal loses its connection to your Intune tenant (for example, if a Global Admin revokes the [Permissions required for Intune Apps](https://docs.patchmypc.com/patch-my-pc-cloud/cloud-reference/cloud-permissions-reference/permissions-required-for-intune-apps) from within Intune), you can use this process to re-establish the connection to your previously connected Intune tenant, which will re-grant the required permissions.

> \*\*Note\*\*
>
> The reconnect button is only available once an Intune connection has been established.
>
> You will only be able to reconnect to an Intune tenant you’ve previously connected to, based on the tenant ID we have stored in the Cloud Portal’s database.

To reconnect your Cloud Portal to an Intune tenant you’ve previously connected to:

1. Navigate to **Settings | Connections**

![Navigating to 'Settings | Connections'](<../../../../.gitbook/assets/image-(310) (1).png>)

2. Click the reconnect icon beside your Intune connection.

![Clicking the reconnect icon beside your Intune connection](<../../../../.gitbook/assets/image-(311) (1).png>)

3. Enter the Entra ID you used to onboard to PMPC Cloud or click to select the relevant account from the list of already signed-in accounts. Then click **Next**.

!['Sign in' prompt](<../../../../.gitbook/assets/image-(304) (1).png>)

4. Enter the password and click **Sign in**.

![Entering the password](<../../../../.gitbook/assets/image-(305) (1).png>)

5. On the **Permissions requested** screen, click **Accept**.

![Clicking 'Accept' on the 'Permissions requested' screen](<../../../../.gitbook/assets/image-(306) (1).png>)

If the reconnection is successful, the **Connections** page is redisplayed, showing **Connected** if your Cloud Portal is now reconnected to your Intune tenant.

![New Intune connection](<../../../../.gitbook/assets/image-(307) (1).png>)
