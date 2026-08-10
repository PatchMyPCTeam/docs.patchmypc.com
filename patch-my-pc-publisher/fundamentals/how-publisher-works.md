# How Patch My PC Publisher Works

_Applies to: Patch My PC Publisher V3.x_

At a high level, the workflow for Patch My PC (PMPC) Publisher is:

1. Publisher downloads a [curated catalog](../security/overview.md) from Patch My PC.
2. Administrators select which products to enable.
3. During synchronization, Publisher:
   * Validates catalog integrity
   * Downloads vendor binaries
   * Verifies file hashes
   * Packages content according to customizations and platform requirements
   * Publishes to Microsoft WSUS, ConfigMgr, and/or Intune.
4. The management platform then distributes the update or application to client devices using its native mechanisms.

![How the Publisher Works](/_images/image-(4187).png "How the Publisher Works")

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>The Publisher is installed on a Windows device and operates within your existing infrastructure and security boundaries.</p>
<p>If you are solely publishing to Intune, we recommend our SaaS based solution [Patch My PC Cloud](../../patch-my-pc-cloud/).</p>
</blockquote>