# Content Distribution Options section in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Content Distribution Options** section on the **Base Install Options** tab of Patch My PC (PMPC) Publisher controls how Publisher distributes application content to ConfigMgr Distribution Points (DPs) when apps are published.

<figure><img src="../../../../.gitbook/assets/image (1081).png" alt="&#x27;Content Distribution Options&#x27; section" width="563"><figcaption></figcaption></figure>

By default, Publisher automatically distributes application content as soon as you create a new application. This ensures content is available on DPs as soon as possible, preventing deployment failures caused by missing or undistributed content.

## **Automatically distribute content for any newly created applications**

If the **Automatically distribute content for any newly created applications** checkbox is checked (by default) and no DP Groups are configured, Publisher distributes content to all DPs in the site. This is the most common configuration and ensures applications are broadly available without additional administrative effort.

If the **Automatically distribute content for any newly created applications** checkbox is unchecked, Publisher does not distribute any content. In this scenario, administrators must manually distribute content using the ConfigMgr console after creating or updating applications. This approach is generally not recommended, as it increases operational overhead and can lead to deployment failures if content distribution is missed or delayed.

## Manage Distribution Point Group(s)

When Publisher is configured to use DP Groups (by clicking **Manage Distribution Point Group(s)**), Publisher distributes content only to the DPs in those groups. This allows administrators to control distribution scope and reduce unnecessary replication.

### To Manage Distribution Point Group(s)

1. Load Publisher.
2. Navigate to **ConfigMgr Apps | Base Install Options**.
3. Scroll down to the **Content Distribution Options** and click **Manage Distribution Point Group(s)**.

<figure><img src="../../../../.gitbook/assets/image (1082).png" alt="Clicking &#x27;Manage Distribution Point Group(s)&#x27;." width="563"><figcaption></figcaption></figure>

4. On the **Select DP Groups for Content Distribution** screen, check the relevant checkboxes then click **OK**.

<figure><img src="../../../../.gitbook/assets/image (1084).png" alt="&#x27;Select DP Groups for Content Distribution&#x27; screen" width="450"><figcaption></figcaption></figure>

In the following example, the environment includes a DP Group containing a Cloud Management Gateway (CMG). The administrator does **not** want Publisher to automatically distribute application content to the CMG.

To achieve this, only the on-premises DP Group (**BBCM1**) checkbox is checked on the **Select DP Groups for Content Distribution** screen, whilst the checkbox group containing the CMG (**BBCMG1**), is left unchecked.

<figure><img src="../../../../.gitbook/assets/image (1085).png" alt="&#x27;Select DP Groups for Content Distribution&#x27; example" width="450"><figcaption></figcaption></figure>
