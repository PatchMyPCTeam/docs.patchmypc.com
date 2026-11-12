# Timeline section of Patch My PC Publisher

The **Timeline** tab of the **Sync** tab of Patch My PC (PMPC) Publisher shows you when your Sync Schedules run. This helps you spot overlapping schedules before they cause a run to wait or be skipped.

## To open the Timeline

Navigate to **Sync** | **Timeline.**

<figure><img src="../../../../.gitbook/assets/image (1598).png" alt="Timeline" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

Dots mark planned start times. Run length is unknown until a sync finishes, so the timeline uses the typical run length from previous syncs.
{% endhint %}

## Change the view

The **Timeline** tab can be viewed using the following options:

* **By schedule (default)**\
  The **By schedule** view groups lanes by target, such as **Intune Updates**, **Intune Apps**, **ConfigMgr**, and **WSUS**. Schedules that publish to more than one target appear in a mixed group. Manual runs and catch-up runs appear under **Other runs**. A line marks the current time.\
  Hover over a run to see:
  * When the run starts.
  * The target.
  * How long the run typically takes.
  * When the schedule last ran.
* **List**\
  The **List** view shows each run with its start time, the time until it starts, the schedule name, and its targets. It also shows how long the run usually takes and its status, such as **Planned**. A warning appears when the run shares a target with another schedule.

<figure><img src="../../../../.gitbook/assets/image (1600).png" alt="&#x27;List&#x27; view" width="563"><figcaption></figcaption></figure>

* **Show**\
  Sets how far ahead the timeline shows (default is **7 days**). **Month** shows about 31 days.

## Refresh&#x20;

Clicking **Refresh** reloads the timeline from the Publishing Service.

## Legend

<table><thead><tr><th width="255.66668701171875" valign="top">Marker</th><th valign="top">Meaning</th></tr></thead><tbody><tr><td valign="top">Planned start</td><td valign="top">A run is scheduled to start.</td></tr><tr><td valign="top">Several runs close together</td><td valign="top">More than one run is planned in a short period. Zoom in with <strong>Show</strong> to see each run.</td></tr><tr><td valign="top">Waits for an earlier run</td><td valign="top">The run waits for an overlapping run to finish.</td></tr><tr><td valign="top">Skipped</td><td valign="top">The run is skipped because it overlaps with another run.</td></tr><tr><td valign="top">Queued</td><td valign="top">The run is waiting to start.</td></tr><tr><td valign="top">Running</td><td valign="top">The run is in progress.</td></tr><tr><td valign="top">Finished</td><td valign="top">The run completed.</td></tr><tr><td valign="top">Failed</td><td valign="top">The run completed with an error.</td></tr><tr><td valign="top">Shares a target with another schedule</td><td valign="top">The schedule publishes to the same target as another schedule at an overlapping time.</td></tr></tbody></table>

{% hint style="info" %}
**Note**

See [Resolving Conflicts](multiple-schedules.md#resolving-conflicts) for more information about how a Sync Schedule handles overlaps.
{% endhint %}
