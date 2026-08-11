# Overview of Update Rings in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

The _Update Rings_ feature of Patch My PC (PMPC) Cloud allows you to deploy apps and updates in a phased manner across your Intune estate.

For example, you may want to deploy software to a pilot group of users/devices to ensure it functions as expected. Then, after a set period of time, you want to deploy the update to a wider group of users/devices and pause a set amount of time to check for issues. Then finally, if there are no issues, deploy the update to the remaining users/devices in scope for the deployment.

Although this approach increases the amount of time it takes to deploy software, it can reduce the impact of deploying software with unforeseen issues that impacts your business in undesirable ways.

{% hint style="info" %}
**Notes**

* Update Rings do not use Intune's built-in capability to create delayed assignments using Availability and Deadlines.
* The use of Update Rings is optional and is controlled at the individual deployment level.
* See our [Update Ring Forecaster](https://www.youtube.com/watch?v=RelJPqWIGno) YouTube video for an explanation of Update Rings, plus how to use our free [Get-UpdateRingForecast](https://github.com/PatchMyPCTeam/Community-Scripts/blob/main/Other/Reports/Get-UpdateRingForecast.ps1) script on GitHub which creates an interactive HTML visualization of app update deployment rings for staged rollouts. It calculates and displays a schedule based on specified parameters and helps you understand your version rollout cadence across different environments.
{% endhint %}

{% hint style="success" icon="user-check" %}
**Learning Hub**

See the [How Update Rings Work in Patch My PC Cloud](https://patchmypc.com/learning-hub/how-update-rings-work-in-patch-my-pc-cloud/) video on our Learning Hub for a practical walkthrough of how Update Rings work, including how to enable them and how overlapping updates are handled.
{% endhint %}
