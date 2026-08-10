# Scheduling section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Scheduling** section of the **Sync Schedule** tab of the Patch My PC (PMPC) Publisher allows you to configure multiple scheduling options to control how often the publishing service runs.

!['Scheduling' section](/_images/image-(4861).png "&#x27;Scheduling&#x27; section")

The available options are:

* **Daily (Default)**\
  Use this option to run the publishing service once per day. You configure the time using hour and minute selectors and choose **AM** or **PM**. The sync will start within five minutes of the configured time.
* **Weekly**\
  Use this option to run the publishing service once per week. You select the day of the week and the time. The sync runs on the chosen weekday at the specified time.
* **The (Custom)**\
  Use this option to run the publishing service on a specific weekday pattern. You select the occurrence (first, second, third, or last), then select the weekday and time. An optional offset in days can be applied to shift the sync earlier or later than the calculated date.
* **Monthly**\
  Use this option to run the publishing service once per month. You specify the day of the month and the time.
* **Hourly**\
  Use this option to run the publishing service at a recurring hourly interval. You specify the number of hours between each sync. The schedule begins as soon as the service starts and continues at the defined interval.
* **Disable Sync Schedule**\
  Use this option to prevent the publishing service from running automatically. When selected, all publishing actions require a [manual sync](sync-status.md#run-publishing-service-sync). This is useful for testing or tightly controlled publishing environments.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>Publisher uses a single, global Sync Schedule that applies across all tabs and products. You cannot configure different Sync Schedules per platform or product.</p>
</blockquote>

The **Next scheduled sync** field shows the date and time the next scheduled Sync Schedule will run so you can check your understanding of how you think you've configured the Sync Schedule with how Publisher will actually run it.