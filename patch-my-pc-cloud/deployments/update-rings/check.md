# Check an Update Rings has been created in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

In Patch My PC (PMPC) Cloud, the [Delayed](update-ring-types.md#delayed-update-rings) option for Update Rings doesn’t create an Update Ring until any configured delay has passed.

As a result, you cannot edit a deployment that uses Delayed Update Rings until all rings have been created.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>If you try editing a deployment that uses Delayed Update Rings and not all of the rings have been completed, you will see the following error:</p>
<p>[Error - Editing is not allowed until all rings are created after the configured delay.](../../troubleshoot/update-rings/error-editing-is-not-allowed-until-all-rings-are-created-after-the-configured-delay-cloud-error.md)</p>
</blockquote>

To determine if a specific Update Ring has been created:

1. Use the [Edit a deployment](../manage-deployments/edit.md) process to navigate to the properties page of the deployment.
2.  Each Update Ring is represented by a separate tab and the status of the ring shows you whether it has been created or not:\
    \
    • **Success –** The ring has been created.\
    • **Scheduled –** The ring has not been created.\
    \
    In the following example, **Ring 1** has been created as it has a status of **Success**.<br>

    !["Ring 1" has been created as it has a status of "Success".](/_images/image-(1115).png "“Ring 1” has been created as it has a status of “Success”.")

    \
    However, as **Ring 2** has a status of **Scheduled**, it has yet to be created as the configured delay has not passed.<br>

    !["Ring 2" has a status of Scheduled meaning it has yet to be created as the configured delay has not passed.](/_images/image-(1116).png "“Ring 2” has a status of Scheduled meaning it has yet to be created as the configured delay has not passed.")

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>If you look in the top right-hand corner of the deployment, the timestamp shows when the deployment was created. From this and looking at the number of days delay configured for a ring, you can work out when a specific ring will be created.</p>
</blockquote>