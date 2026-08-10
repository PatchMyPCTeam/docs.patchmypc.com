# Add a Connection in Patch My PC Cloud

_Applies to: Patch My PC Cloud and Publisher_

From the **Connections** page of the Patch My PC (PMPC) Cloud Portal, you can add the following connections:

* [Connection to Intune](add-connection.md#add-an-intune-connection)
* [Connection to Publisher](add-connection.md#add-a-publisher-connection)

## Add an Intune Connection

To add an Intune connection:

1. Navigate to **Settings | Connections**

<figure><img src="../../../../.gitbook/assets/image (301).png" alt="Navigating to &#x27;Settings | Connections&#x27;" width="563"><figcaption></figcaption></figure>

The **Connections** page is displayed showing any existing connections

<figure><img src="../../../../.gitbook/assets/image (302).png" alt="&#x27;Connections&#x27; page showing any existing connections" width="563"><figcaption></figcaption></figure>

2. Click **Connect Intune**

<figure><img src="../../../../.gitbook/assets/image (303).png" alt="Clicking &#x27;Connect Intune&#x27;" width="563"><figcaption></figcaption></figure>

3. Enter the Entra ID you used to onboard to PMPC Cloud or click to select the relevant account from the list of already signed-in accounts. Then click **Next**.

<figure><img src="../../../../.gitbook/assets/image (304).png" alt="&#x27;Sign in&#x27; prompt" width="329"><figcaption></figcaption></figure>

4. Enter the password and click **Sign in**.

<figure><img src="../../../../.gitbook/assets/image (305).png" alt="Entering the password" width="329"><figcaption></figcaption></figure>

5. On the **Permissions requested** screen, click **Accept**.

{% hint style="info" %}
**Note**

To connect with Intune, the signed-in user must have the **Cloud Application Administrator** or the **Application Administrator** role to allow creation of the Enterprise app, and the **Privileged Role Administrator** role to approve the Graph API permissions we require. A **Global Administrator** can also perform both steps.

See [Permissions required for the Intune Apps](https://docs.patchmypc.com/patch-my-pc-cloud/cloud-reference/cloud-permissions-reference/permissions-required-for-intune-apps) for more details.
{% endhint %}

<figure><img src="../../../../.gitbook/assets/image (306).png" alt="Clicking &#x27;Accept&#x27; on the &#x27;Permissions requested&#x27; screen" width="330"><figcaption></figcaption></figure>

{% hint style="success" %}
**Tip**

You can click the down arrow beside each permission to get more information.
{% endhint %}

The **Connections** page is redisplayed, showing the newly added Intune connection.

<figure><img src="../../../../.gitbook/assets/image (307).png" alt="New Intune connection" width="563"><figcaption></figcaption></figure>

## Add a Publisher Connection

Adding a connection between our on-premises Publisher and PMPC Cloud is done from Publisher.

If you click **Connect Publisher** on the **Connections** page of the Cloud Portal, you will see the **Publisher connection** screen, which outlines the process explained in detail below.

<figure><img src="../../../../.gitbook/assets/image (308).png" alt="&#x27;Publisher connection&#x27; screen" width="291"><figcaption></figcaption></figure>

To connect our on-premises Publisher to PMPC Cloud, you need to:

1. Load the **Patch My PC Publishing Service** (Publisher) and verify you are running at least version 2.1.20.0. If you are not, upgrade to the latest version.
2. Click the **Cloud** tab.

<figure><img src="../../../../.gitbook/assets/image (4849).png" alt="Clicking the &#x27;Cloud&#x27; tab" width="563"><figcaption></figcaption></figure>

3. On the **Cloud** tab, check the **Enable cloud connection** checkbox.

<figure><img src="../../../../.gitbook/assets/image (4850).png" alt="Checking the &#x27;Enable cloud connection&#x27; checkbox" width="563"><figcaption></figcaption></figure>

4. In the **Connection Name** field, enter a unique name for the connection. For example, **Patch My PC Publisher Intune Connector**, then click **Connect**.

{% hint style="info" %}
**Note**

The name you enter here determines how this connection shows on the **Connections** page of the Cloud Portal.
{% endhint %}

<figure><img src="../../../../.gitbook/assets/image (4851).png" alt="Entering a &#x27;Connection name&#x27; and clicking &#x27;Connect&#x27;" width="563"><figcaption></figcaption></figure>

4. In your browser, enter the Entra ID you used to onboard to PMPC Cloud or click to select the relevant account from the list of already signed-in accounts. Then click **Next**.

<figure><img src="../../../../.gitbook/assets/image (2122).png" alt="&#x27;Microsoft Sign in&#x27; screen" width="329"><figcaption></figcaption></figure>

5. Enter the password and click **Sign in**.

<figure><img src="../../../../.gitbook/assets/image (2123).png" alt="&#x27;Enter password&#x27; screen" width="329"><figcaption></figcaption></figure>

If the connection is successful, a new browser tab opens with the following message:

**Authentication complete. You can return to the application. Feel free to close this browser tab.**

You can close this tab at this point.

6. If the **Select a customer for cloud connection** screen is not displayed, proceed to Step 8.
7. If the **Select a customer for cloud connection** screen is displayed, click to select the customer you want to connect to, then click **OK**.

<figure><img src="../../../../.gitbook/assets/image (4853).png" alt="&#x27;Select a customer for cloud connection&#x27; dialog" width="375"><figcaption></figcaption></figure>

8. In Publisher, verify the **Connection Status** shows as **Connected**

{% hint style="info" %}
**Note**

You don't need to click **Apply** or **Save and Close** in Publisher at this point, as the connection process automatically saves the details in Publisher.
{% endhint %}

<figure><img src="../../../../.gitbook/assets/image (4852).png" alt="Verifying the &#x27;Connection Status&#x27; shows as &#x27;Connected&#x27;" width="563"><figcaption></figcaption></figure>

The new Publisher connection will be shown on the **Connections** page of the Cloud Portal.

<figure><img src="../../../../.gitbook/assets/image (4854).png" alt="New Publisher connection" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

You can also use the [View Connections](view-connections.md) process to verify that your Publisher is connected to the portal.
{% endhint %}
