# Update Ring Progression in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

If your Patch My PC (PMPC) Update Rings are configured with longer delays, a new version of a product may be released while an older version is still moving through the rings.

This is not a problem, as when a newer version becomes available, PMPC Cloud does not restart or override the Update Ring process already in progress.

Each version of the software must complete the full Update Ring lifecycle independently. In other words, version _n_ will finish all rings exactly as configured, and version _n+1_ will follow the same path when its turn begins.

The diagram below illustrates how each version progresses through the rings independently.

<figure><img src="../../../.gitbook/assets/image (60).png" alt="Example scenario for Patch My PC Cloud Update Rings" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

See the [Patch My PC Update Rings: Mastering Phased Rollouts in Intune | Tips for a Better User Experience](https://www.youtube.com/watch?v=jgfErZIzNhQ) on our YouTube channel for more details.
{% endhint %}

## Update Rings forecast

To help you predict how your Update Rings will progress, we provide a [PowerShell script](https://github.com/PatchMyPCTeam/Community-Scripts/blob/main/Other/Reports/Get-UpdateRingForecast.ps1) that generates an HTML report. This report gives you a clear visual overview of your current Update Rings configuration and how each ring is expected to advance.

{% hint style="info" %}
**Note**

See the [Update Ring Forecaster](https://www.youtube.com/watch?v=RelJPqWIGno) on our YouTube channel for a detailed walkthrough of the script and the report.
{% endhint %}
