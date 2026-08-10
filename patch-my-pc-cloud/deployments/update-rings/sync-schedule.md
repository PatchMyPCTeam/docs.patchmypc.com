# How the Sync Schedule in Patch My PC Cloud affects Update Rings

_Applies to: Patch My PC Cloud_

As the [Sync Schedule](../../manage/settings/sync-schedule.md) affects when your Portal checks for updates to your Patch My PC (PMPC) Cloud deployments, how often it runs can also affect how your Update Rings behave.

For example, if you have deployed an app that updates more frequently than your configured Sync Schedule, the ring with the lowest delay (for example, Ring 1) will have the latest suitable version applied.

Depending on how often you run your Sync Schedule and the delay between your rings, the scenario could arise where we have to skip versions to keep everything configured as per your ring strategy.

If this arises, we will not deploy a version of an app to any rings that has not been deployed to at least Ring 1. This ensures we only deploy apps to later rings that have been tested on at least one ring.

## Other Factors

Also:

* The Sync Schedule evaluates your Update Rings. When a ring’s configured Days Delay has been reached, the assignments for that ring are created.
* As Update Rings are evaluated only during the Sync Schedule, the frequency of your sync sets the minimum pace at which the rings can progress. For example, if your Sync Schedule runs weekly, the Update Rings cannot move faster than a weekly cadence.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>If you want Update Rings to be evaluated more frequently, but prefer a slower schedule for packaging new versions, you can support this request by upvoting <a href="https://ideas.patchmypc.com/ideas/PATCHMYPC-I-5986">Update rings independent of sync schedule</a> on our UserVoice page.</p>
</blockquote>

* If you create your Update Rings with an **Immediate** start time, the Sync Schedule configuration only impacts the daily update of the rings and their assignments (promotion to the new version).
* If you create your Update Rings with the **Delayed** start time, the Sync Schedule configuration impacts both the initial creation of the rings and the daily update of their assignments (promotion to the new version). For example, you create a deployment with two Update Rings with the default two-day delay between them. The first ring will be created when you deploy the software. The second ring won’t be created until two days have passed since the time the deployment was created and the next Sync Schedule run.

The following table summarizes how your [Sync Schedule](../../manage/settings/sync-schedule.md) configuration determines how you can configure the delay between Update Rings.

<table><thead><tr><th width="247.3333740234375">Sync Schedule Configured For</th><th>Delay between Rings</th></tr></thead><tbody><tr><td>Daily</td><td>Delays between rings can be configured as required.</td></tr><tr><td>Weekly</td><td><p>Ring 2 has to have a minimum delay of 7 days</p><p>Ring x has to be configured with a delay of at least 7 days apart from any other ring.</p></td></tr><tr><td>Monthly</td><td><p>Ring 2 cannot have a delay of less than 31 days</p><p>Ring x has to be configured with a delay of at least 31 days apart from any other ring.</p></td></tr></tbody></table>

These limitations ensure that the update delays align with your chosen sync frequency and is why we advise configuring your [Sync Schedule](../../manage/settings/sync-schedule.md) to run on a daily basis when using Update Rings.