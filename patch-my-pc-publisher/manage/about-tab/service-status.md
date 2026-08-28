# Service Status tab of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Service Status** tab of the **About** tab of Patch My PC (PMPC) Publisher consists of the following sections:

* [Sync Status](service-status.md#sync-status)
* [Publisher Statistics](service-status.md#publisher-statistics)

## Sync Status

The **Sync Status** section displays the current state of Publisher during a publishing synchronization. This status updates in real time as products are evaluated and processed.

<figure><img src="../../../.gitbook/assets/image (4836).png" alt="&#x27;Sync Status&#x27; section" width="563"><figcaption></figcaption></figure>

When the **Status** shows as **Idle**, no publishing synchronization is running, and Publisher is not actively evaluating or publishing content.

Other statuses are **Syncing**, **Completed**, and **Error**.

{% hint style="info" %}
**Note**

See the [Status](../sync-schedule-tab/sync-status.md#status) section of [Sync Status](../sync-schedule-tab/sync-status.md) for more details on the values of the **Status** field.
{% endhint %}

## Publisher Statistics

The **Publisher Statistics** section provides a real-time summary of publishing activity within Publisher.

<figure><img src="../../../.gitbook/assets/image (4837).png" alt="&#x27;Publisher Statistics&#x27; section" width="563"><figcaption></figcaption></figure>

These statistics help you understand how many applications, updates, and CVEs have been published, as well as the overall synchronization activity. This information is useful for validating that publishing is working as expected and for gaining insight into ongoing usage over time.

<table><thead><tr><th width="203.22222900390625" valign="top">Field</th><th valign="top">Shows the...</th></tr></thead><tbody><tr><td valign="top">Last sync</td><td valign="top">Date and time of the last successful sync.</td></tr><tr><td valign="top">Next sync</td><td valign="top">Scheduled date and time of the next synchronization, based on your configured sync schedule.</td></tr><tr><td valign="top">Last save</td><td valign="top">Date/time Publisher settings were last saved.</td></tr><tr><td valign="top">Published CVEs</td><td valign="top">Total number of Common Vulnerabilities and Exposures (CVEs) addressed by the applications and updates published through Publisher.</td></tr><tr><td valign="top">Published updates</td><td valign="top">Total number of third-party updates that have been published.</td></tr><tr><td valign="top">Published applications</td><td valign="top">Total number of third-party applications that have been published.</td></tr><tr><td valign="top">Selected products</td><td valign="top">Number of products selected to be managed by Publisher.</td></tr><tr><td valign="top">Total syncs</td><td valign="top">Total number of synchronization operations performed by Publisher.</td></tr><tr><td valign="top">Cloud connection</td><td valign="top"><p>Status of the connection to a PMPC Cloud Company (<strong>Not Configured</strong> or <strong>Connected</strong>).</p><p>Clicking <a href="https://portal.patchmypc.com/">Open Patch My PC Cloud</a> opens the link to sign in to the PMPC Cloud Portal.</p></td></tr></tbody></table>
