# Content Distribution Options

_Applies to: Patch My PC Publisher V2.x_

## Overview

The **Content Distribution Options** section controls how application content created by the Publisher is distributed to ConfigMgr Distribution Points (DPs) when apps are published.

<figure><img src="../../../../.gitbook/assets/image (4012).png" alt="Content Distribution Options" width="563"><figcaption></figcaption></figure>

By default, the Publisher automatically distributes application content as soon as a new application is created. This ensures content is available on Distribution Points as soon as possible, preventing deployment failures caused by missing or undistributed content.

## Distribute Content to All Distribution Points (Default)

When **Automatically distribute content for any newly created applications** is enabled and no Distribution Point Groups are specified, the Publisher distributes content to all Distribution Points in the site. This is the most common configuration and ensures applications are broadly available without additional administrative effort.

## Distribute Content to Selected Distribution Points

When one or more Distribution Point Groups are selected, by clicking **Manage Distribution Point Group(s)**, the Publisher distributes content only to the Distribution Points in those groups. This allows administrators to control distribution scope and reduce unnecessary replication.

In the example below, the environment includes a Distribution Point Group that contains a Cloud Management Gateway (CMG). The administrator does **not** want the Publisher to automatically distribute application content to the CMG.

To achieve this, only the on-premises Distribution Point Group (**BBCM1**) is selected in the **Manage Edit DP groups** dialog, while the group containing the CMG (**BBCMG1**) is left unchecked.

<figure><img src="../../../../.gitbook/assets/image (4013).png" alt="Manage Distribution Point Group(s)" width="563"><figcaption></figcaption></figure>

## Do Not Distribute Content

If Automatically distribute content for any newly created applications is unchecked, the Publisher does not distribute content at all. In this scenario, administrators must manually distribute content using the ConfigMgr console after applications are created or updated. This approach is generally not recommended, as it increases operational overhead and can lead to deployment failures if content distribution is missed or delayed.
