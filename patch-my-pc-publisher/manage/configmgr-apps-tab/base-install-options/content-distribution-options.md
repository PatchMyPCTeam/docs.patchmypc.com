# Content Distribution Options section in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Content Distribution Options** section on the **Base Install Options** tab of Patch My PC (PMPC) Publisher controls how Publisher distributes application content to ConfigMgr Distribution Points (DPs) when apps are published.

<figure><img src="../../../../.gitbook/assets/image (1081).png" alt="&#x27;Content Distribution Options&#x27; section" width="563"><figcaption></figcaption></figure>

By default, Publisher automatically distributes application content as soon as you create a new application. This ensures content is available on DPs as soon as possible, preventing deployment failures caused by missing or undistributed content.

## **Automatically distribute content for any newly created applications**

If the **Automatically distribute content for any newly created applications** checkbox is checked (by default) and no DP Groups are configured, Publisher distributes content to all DPs in the site. This is the most common configuration and ensures applications are broadly available without additional administrative effort.

## Manage Distribution Point Group(s)

When Publisher is configured to use DP Groups (by clicking **Manage Distribution Point Group(s)**), Publisher distributes content only to the DPs in those groups. This allows administrators to control distribution scope and reduce unnecessary replication.

In the following example, the environment includes a DP Group containing a Cloud Management Gateway (CMG). The administrator does **not** want Publisher to automatically distribute application content to the CMG.

To achieve this, only the on-premises DP Group (**BBCM1**) is selected in the **Manage Edit DP groups** dialog, while the group containing the CMG (**BBCMG1**) is left unchecked.

<figure><img src="../../../../.gitbook/assets/image (4013).png" alt="Manage Distribution Point Group(s)" width="563"><figcaption></figcaption></figure>

## Do Not Distribute Content

If Automatically distribute content for any newly created applications is unchecked, the Publisher does not distribute content at all. In this scenario, administrators must manually distribute content using the ConfigMgr console after applications are created or updated. This approach is generally not recommended, as it increases operational overhead and can lead to deployment failures if content distribution is missed or delayed.
