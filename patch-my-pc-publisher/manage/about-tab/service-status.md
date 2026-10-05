# Service Status tab of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Service Status** tab of the **About** tab of Patch My PC (PMPC) Publisher consists of the following sections:

* [Service Status](service-status.md#service-status)
* [Publisher Statistics](service-status.md#publisher-statistics)
* [Publisher Details](service-status.md#publisher-details)

## Service Status

The **SERVICE STATUS** section displays the current state of Publisher during a publishing synchronization. This status updates in real time as products are evaluated and processed.

<figure><img src="../../../.gitbook/assets/image (1310).png" alt="&#x27;SERVICE STATUS&#x27; section" width="563"><figcaption></figcaption></figure>

When the Status shows as **Idle**, no publishing synchronization is running, and Publisher is not actively evaluating or publishing content.

Other statuses are **Syncing**, **Completed**, and **Error**.

{% hint style="info" %}
**Note**

See the [Status](../sync-tab/schedule/sync-status.md#status) section of [Sync Status](../sync-tab/schedule/sync-status.md) for more details on the values of the **Status** field.
{% endhint %}

## Publisher Statistics

The **PUBLISHER STATISTICS** section provides a real-time summary of statistics about Publisher.

<figure><img src="../../../.gitbook/assets/image (1315).png" alt="&#x27;PUBLISHER STATISTICS&#x27; section" width="563"><figcaption></figcaption></figure>

These statistics help you understand how many applications, updates, and CVEs have been published. This information is useful for validating that publishing is working as expected and for gaining insight into ongoing usage over time.

<table><thead><tr><th width="203.22222900390625" valign="top">Field</th><th valign="top">Shows the...</th></tr></thead><tbody><tr><td valign="top">Total syncs</td><td valign="top">Total number of synchronization operations performed by Publisher.</td></tr><tr><td valign="top">Published apps</td><td valign="top">Total number of third-party applications that have been published.</td></tr><tr><td valign="top">Published updates</td><td valign="top">Total number of third-party updates that have been published.</td></tr><tr><td valign="top">Published CVEs</td><td valign="top">Total number of Common Vulnerabilities and Exposures (CVEs) addressed by the applications and updates published through Publisher.</td></tr><tr><td valign="top">Selected products</td><td valign="top">Number of products selected to be managed by Publisher.</td></tr></tbody></table>

## Publisher Details

The **PUBLISHER DETAILS** section provides a real-time summary of publishing activity within Publisher.

<figure><img src="../../../.gitbook/assets/image (1317).png" alt="&#x27;PUBLISHER DETAILS&#x27; section" width="563"><figcaption></figcaption></figure>

These details help you understand how the overall synchronization activity as well as providing other useful information.

<table><thead><tr><th width="203.22222900390625" valign="top">Field</th><th valign="top">Shows the...</th></tr></thead><tbody><tr><td valign="top">Last sync</td><td valign="top">Date and time of the last successful sync.</td></tr><tr><td valign="top">Next sync</td><td valign="top">Scheduled date and time of the next synchronization, based on your configured sync schedule.</td></tr><tr><td valign="top">Last settings save</td><td valign="top">Date/time Publisher settings were last saved.</td></tr><tr><td valign="top">Installed version </td><td valign="top">The version of Publisher currently installed.</td></tr><tr><td valign="top">Published applications</td><td valign="top">Total number of third-party applications that have been published.</td></tr><tr><td valign="top">Cloud connection</td><td valign="top"><p>Status of the connection to a PMPC Cloud Company (<strong>Not Configured</strong> or <strong>Connected</strong>).</p><p>Clicking <a href="https://portal.patchmypc.com/">Open Patch My PC Cloud</a> opens the link to sign in to the PMPC Cloud Portal.</p></td></tr></tbody></table>
