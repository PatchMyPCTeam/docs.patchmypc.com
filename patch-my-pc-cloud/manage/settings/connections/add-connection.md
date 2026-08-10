# Add a Connection in Patch My PC Cloud

_Applies to: Patch My PC Cloud and Publisher_

From the **Connections** page of the Patch My PC (PMPC) Cloud Portal, you can add the following connections:

* [Connection to Intune](add-connection.md#add-an-intune-connection)
* [Connection to Publisher](add-connection.md#add-a-publisher-connection)

## Add an Intune Connection

To add an Intune connection:

1. Navigate to **Settings | Connections**

![Navigating to 'Settings | Connections'](/_images/image-(301).png)

The **Connections** page is displayed showing any existing connections

!['Connections' page showing any existing connections](/_images/image-(302).png)

2. Click **Connect Intune**

![Clicking 'Connect Intune'](/_images/image-(303).png)

3. Enter the Entra ID you used to onboard to PMPC Cloud or click to select the relevant account from the list of already signed-in accounts. Then click **Next**.

!['Sign in' prompt](/_images/image-(304).png)

4. Enter the password and click **Sign in**.

![Entering the password](/_images/image-(305).png)

5. On the **Permissions requested** screen, click **Accept**.

> \*\*Note\*\*
>
> To connect with Intune, the signed-in user must have the \*\*Cloud Application Administrator\*\* or the \*\*Application Administrator\*\* role to allow creation of the Enterprise app, and the \*\*Privileged Role Administrator\*\* role to approve the Graph API permissions we require. A \*\*Global Administrator\*\* can also perform both steps.
>
> See [Permissions required for the Intune Apps](https://docs.patchmypc.com/patch-my-pc-cloud/cloud-reference/cloud-permissions-reference/permissions-required-for-intune-apps) for more details.

![Clicking 'Accept' on the 'Permissions requested' screen](/_images/image-(306).png)

> \*\*Tip\*\*
>
> You can click the down arrow beside each permission to get more information.

The **Connections** page is redisplayed, showing the newly added Intune connection.

![New Intune connection](/_images/image-(307).png)

## Add a Publisher Connection

Adding a connection between our on-premises Publisher and PMPC Cloud is done from Publisher.

If you click **Connect Publisher** on the **Connections** page of the Cloud Portal, you will see the **Publisher connection** screen, which outlines the process explained in detail below.

!['Publisher connection' screen](/_images/image-(308).png)

To connect our on-premises Publisher to PMPC Cloud, you need to:

1. Load the **Patch My PC Publishing Service** (Publisher) and verify you are running at least version 2.1.20.0. If you are not, upgrade to the latest version.
2. Click the **Cloud** tab.

![Clicking the 'Cloud' tab](/_images/image-(4849).png)

3. On the **Cloud** tab, check the **Enable cloud connection** checkbox.

![Checking the 'Enable cloud connection' checkbox](/_images/image-(4850).png)

4. In the **Connection Name** field, enter a unique name for the connection. For example, **Patch My PC Publisher Intune Connector**, then click **Connect**.

> \*\*Note\*\*
>
> The name you enter here determines how this connection shows on the \*\*Connections\*\* page of the Cloud Portal.

![Entering a 'Connection name' and clicking 'Connect'](/_images/image-(4851).png)

4. In your browser, enter the Entra ID you used to onboard to PMPC Cloud or click to select the relevant account from the list of already signed-in accounts. Then click **Next**.

!['Microsoft Sign in' screen](/_images/image-(2122).png)

5. Enter the password and click **Sign in**.

!['Enter password' screen](/_images/image-(2123).png)

If the connection is successful, a new browser tab opens with the following message:

**Authentication complete. You can return to the application. Feel free to close this browser tab.**

You can close this tab at this point.

6. If the **Select a customer for cloud connection** screen is not displayed, proceed to Step 8.
7. If the **Select a customer for cloud connection** screen is displayed, click to select the customer you want to connect to, then click **OK**.

!['Select a customer for cloud connection' dialog](/_images/image-(4853).png)

8. In Publisher, verify the **Connection Status** shows as **Connected**

> \*\*Note\*\*
>
> You don't need to click \*\*Apply\*\* or \*\*Save and Close\*\* in Publisher at this point, as the connection process automatically saves the details in Publisher.

![Verifying the 'Connection Status' shows as 'Connected'](/_images/image-(4852).png)

The new Publisher connection will be shown on the **Connections** page of the Cloud Portal.

![New Publisher connection](/_images/image-(4854).png)

> \*\*Note\*\*
>
> You can also use the \[View Connections]\(view-connections.md) process to verify that your Publisher is connected to the portal.