# Manage Usage Limits in your Patch My PC Cloud Company

_Applies to: Patch My PC Cloud_

As Patch My PC (PMPC) Cloud is hosted on Cloud infrastructure, it has several usage limits which are determined by the type of license your PMPC Cloud company is running.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>See [Cloud Product Limits](../../../product-limits.md) for more information.</p>
</blockquote>

The _Usage_ feature is designed to help you monitor these usage limits so you can ensure you do not exceed them.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>The **Usage** tab is not available to MSPs and their child companies.</p>
</blockquote>

To see the usage information for your PMPC Cloud Company:

1. Navigate to **Settings | Company**

![Navigating to "Settings | Company"](/_images/image-(3399).png "Navigating to “Settings | Company”")

2. On the **Company** page, click the **Usage** tab.

![Clicking the "Usage" tab](/_images/image-(3400).png "Clicking the “Usage” tab")

The **Usage Info** for this company is shown, which is explained below.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>The usage information displayed is determined by the user role assigned to the user viewing the **Usage** tab. For example, a user assigned the **Custom App Admin** role will not see any of the deployment-related usage information.</p>
<p>See [Cloud User Roles Reference](../users/user-roles-reference.md) for more information.</p>
<p>Also, any devices managed by Microsoft Defender for Endpoint (MDE) are not included in device counts.</p>
</blockquote>

!["Usage" information](/_images/image-(3414).png "“Usage&#x22; information")

<table><thead><tr><th width="211" valign="top">Field</th><th valign="top">Shows the...</th></tr></thead><tbody><tr><td valign="top">License Type</td><td valign="top">Type of PMPC License this company is running, which determines the limits.</td></tr><tr><td valign="top">Number of Devices</td><td valign="top">Total number of active devices for the last year.</td></tr><tr><td valign="top">Windows Deployments</td><td valign="top">The number of Windows deployments that have been created out of the total allowed.</td></tr><tr><td valign="top">macOS Deployments</td><td valign="top"><p>The number of macOS deployments that have been created out of the total allowed.</p><p></p><p><mark style="color:blue;"><strong>NOTE:</strong></mark></p><p>If you do not have the macOS license feature enabled, the usage will show as <strong>N/A</strong>.</p><p></p><p>You can click <strong>Request a Quote</strong> if you would like a quote for managing your macOS devices using PMPC Cloud.</p></td></tr><tr><td valign="top">Number of Custom Apps</td><td valign="top">The number of Custom Apps you have created out of the total allowed.</td></tr><tr><td valign="top">Max Storage Size (GB)</td><td valign="top">Total upload size of all files.</td></tr><tr><td valign="top">Deployments with Files</td><td valign="top">Total number of deployments you have created with extra files out of the total allowed.</td></tr></tbody></table>

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Most usage values are updated dynamically. For example, if you create or delete something affected by a limit (such as a deployment), the usage information updates in real-time. The only exception to this is the **Number of Devices**, which is updated hourly.</p>
<p>The color used to display each limit helps you easily see what your utilization rate is:</p>
<p>* Green if you are using less than 50%</p>
<p>* Yellow if you are using between 50% and 99%</p>
<p>* Red if you have reached the limit.</p>
<p>If any item exceeds 90% utilization, a warning banner is displayed in the Portal, warning you of this.</p>
</blockquote>