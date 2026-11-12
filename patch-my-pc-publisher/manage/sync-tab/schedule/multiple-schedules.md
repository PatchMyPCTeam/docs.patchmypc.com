# Configure Multiple Schedules in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

{% hint style="danger" %}
**PRIVATE PREVIEW**

This feature is currently available only through an invitation-only Private Preview, as both the feature and the documentation are under development, incomplete, and subject to change.

Please do not share links to these docs with others outside of the Private Preview.

Once this feature is released, it will be announced, and this banner will be removed.
{% endhint %}

Multiple _Sync Schedules_ can be configured in Patch My PC (PMPC) Publisher. Each schedule requires a unique name and can be configured with settings for recurrence, targets, and overlapping behavior, if required.

For example, you can sync Microsoft Intune Updates every 6 hours and publish to Microsoft Configuration Manager (ConfigMgr) once a week.

## To view the current Sync Schedules

Navigate to **Sync** | **Schedule** to view the list of current sync schedules.

<figure><img src="../../../../.gitbook/assets/image (1550).png" alt="List of current sync schedules" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

If the Multiple Schedule feature is not enabled for your Publisher license, only a [single schedule](schedule.md) will be visible.
{% endhint %}

## To add a Sync Schedule

{% stepper %}
{% step %}
### **Click + Add schedule**

<figure><img src="../../../../.gitbook/assets/image (1551).png" alt="Clicking &#x27;+ Add schedule&#x27;" width="563"><figcaption></figcaption></figure>

The current **Default schedule** is duplicated.

{% hint style="success" %}
**Tip**

You can also copy an existing Sync Schedule by clicking **Duplicate** and then amending it's properties to create a new schedule.
{% endhint %}
{% endstep %}

{% step %}
### Enter a unique name

In the **Name** field, enter a unique name for the schedule.

<figure><img src="../../../../.gitbook/assets/image (1558).png" alt="Enter a unique name for the schedule in the &#x27;Name&#x27; field" width="563"><figcaption></figcaption></figure>
{% endstep %}

{% step %}
### Select the schedule type

<table><thead><tr><th width="112" valign="top">Type</th><th width="155.3333740234375" valign="top">Default</th><th valign="top">Runs</th></tr></thead><tbody><tr><td valign="top">Hourly</td><td valign="top">Every 4 hours</td><td valign="top">Every set number of hours.</td></tr><tr><td valign="top">Daily</td><td valign="top">7:00 PM</td><td valign="top">Once a day at the set time.</td></tr><tr><td valign="top">Weekly</td><td valign="top">Monday</td><td valign="top">Once a week on the set day and time.</td></tr><tr><td valign="top">Monthly</td><td valign="top">Day 1</td><td valign="top">Once a month on the set day, from 1 to 31.</td></tr><tr><td valign="top">Custom</td><td valign="top">Second Monday</td><td valign="top">On a ranked weekday of the month, such as the second Tuesday, with an optional offset.</td></tr></tbody></table>
{% endstep %}

{% step %}
### Configure Sync options

Configure the relevant sync settings (which vary depending by sync type), such as days and times.

{% hint style="info" %}
**Note**

If you chose **Monthly**, if the day does not exist in a shorter month, check the next run time before you save.

Use **Custom** to run relative to a weekday in the month. For example, to sync the day after Patch Tuesday, select **Second**, **Tuesday**, and an offset of one day.

1. Select **Custom**.
2. Select **First**, **Second**, **Third**, **Fourth**, or **Last**.
3. Select the weekday.
4. Enter an offset from zero to six days.
5. Enter the time.
{% endhint %}
{% endstep %}

{% step %}
### Configure to run a missed scheduled sync (optional)

Decide whether you want to enable the **Run a missed scheduled sync on startup** option (disabled by default). Enabling this option forces Publisher to catch up as soon as possible if the service was offline at the scheduled time. This setting is not affected by manual.

<figure><img src="../../../../.gitbook/assets/image (1560).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
### Select which platforms this schedule syncs

Under the **Which platforms this schedule syncs** section, select the relevant targets that this schedule will sync.

{% hint style="info" %}
**Note**

Only those targets enabled in Publisher will appear.
{% endhint %}

<figure><img src="../../../../.gitbook/assets/image (1566).png" alt=""><figcaption></figcaption></figure>

<table><thead><tr><th width="176.888916015625" valign="top">Target</th><th valign="top">Includes...</th></tr></thead><tbody><tr><td valign="top">WSUS</td><td valign="top">Publishing to WSUS.</td></tr><tr><td valign="top">ConfigMgr</td><td valign="top">Publishing applications to ConfigMgr.</td></tr><tr><td valign="top">Intune Apps</td><td valign="top">Publishing apps to Intune.</td></tr><tr><td valign="top">Intune Updates</td><td valign="top">Publishing updates to Intune.</td></tr><tr><td valign="top">Only priority updates</td><td valign="top">Only updates that meet the priority thresholds on the <a href="../configuration.md">Configuration</a> tab.</td></tr><tr><td valign="top">Intune tenants</td><td valign="top">Only the selected Intune tenants. If you select none, the schedule covers all enabled tenants.</td></tr></tbody></table>
{% endstep %}

{% step %}
### Review any conflicts

There are several reasons that conflicts can occur in a Sync Schedule, as detailed [Resolving Conflicts](multiple-schedules.md#resolving-conflicts).
{% endstep %}

{% step %}
### Click **Apply**

To save the new Sync Schedule, click **Apply**.

The new Sync Schedule appears under the list of configured schedules.

<figure><img src="../../../../.gitbook/assets/image (1583).png" alt="Newly added Sync Schedule" width="563"><figcaption></figcaption></figure>
{% endstep %}
{% endstepper %}

## Resolving Conflicts

Two schedules overlap when they are due to run at the same time and publish to the same target, such as WSUS, ConfigMgr, or an Intune tenant. Overlapping runs do not run at the same time.

When the selected schedule overlaps with another, the **This schedule overlaps with 1 other schedule** message is shown, explaining the overlapping schedule and the target they share.

<figure><img src="../../../../.gitbook/assets/image (1570).png" alt="Overlapping schedule" width="563"><figcaption></figcaption></figure>

You then have the option of either configuring one of the following two options or clicking [Go to schedule](multiple-schedules.md#go-to-schedule) to edit the conflicting schedule:

* **Wait, then run**\
  When selected, the run waits until the earlier run finishes, then starts.<br>
* **Skip this run**\
  The run is skipped. The schedule runs again at its next scheduled time.

### Go to schedule

Clicking **Go to schedule** opens the other schedule. To see when the runs overlap, click **View timeline**.&#x20;

<figure><img src="../../../../.gitbook/assets/image (1579).png" alt="Clicking &#x27;View timeline&#x27; " width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

See [Timeline](../timeline.md) for more information on working with the Timeline.

Also, overlapping messages are a warning only. You can save a Sync Schedule that overlaps with another one.
{% endhint %}

## Schedules running in parallel

Sync Schedules that publish to different targets can run at the same time. When this applies, a message such as **Runs alongside 2 schedules** lists them.&#x20;

<figure><img src="../../../../.gitbook/assets/image (1591).png" alt="Parallel schedules" width="563"><figcaption></figcaption></figure>

Publisher runs up to three scheduled syncs at the same time.

## Working with Sync Schedules

The following actions can be performed on a Sync Schedule:

* **Remove**\
  Clicking **Remove** deletes the Sync Schedule
* **Enabled**\
  Disabling the **Enabled** option disables the Sync Schedule and prevents it from running

{% hint style="info" %}
**Note**

Disabling a Sync Schedule does not prevent it from being run manually.
{% endhint %}
