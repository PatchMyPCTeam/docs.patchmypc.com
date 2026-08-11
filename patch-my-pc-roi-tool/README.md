# Patch My PC ROI Tool documentation

Official product documentation for the Patch My PC Return on Investment Tool

The Patch My PC Return on Investment (ROI) tool helps identify the products supported in the current Patch My PC catalog that are in use in your environment.

> \*\*Note\*\*
>
> At this time, the ROI Tool does not support Intune scanning for GCC High and DoD tenants

![](../.gitbook/assets/image-\(1980\).png)

## Download

You can download the latest version of the ROI tool from the below webpage:

{% embed url="https://patchmypc.com/features-benefits-and-roi" %}

## How Does it Work?

The ROI tool scans your Configuration Manager and/or your Intune environment for application inventory. It then compares this inventory data against our latest list of [Supported Products](https://patchmypc.com/supported-products) to show you the applications we can support in your environment.

## Data Use

This section will detail the data the ROI tool uses.

### Intune

All of your data remains in your environment and is not shared with anyone, including Patch My PC.

When you choose **Scan Intune**, you will be prompted to approve an Enterprise Application (see [#what-permissions-are-required](./#what-permissions-are-required "mention") for more information.)

This uses **delegated permissions**; the Patch My PC ROI tool does not harvest any of your Intune data, and it is not stored anywhere other than in your tenant. It simply allows the tool to connect to your Intune tenant on your behalf.

After logging in, it then uses Microsoft's Graph API to retrieve the same inventory data displayed in the **Discovered Apps** report within the Intune console.

You read more about Intune's Discovered Apps software inventory here:

{% embed url="https://learn.microsoft.com/en-us/mem/intune/apps/app-discovered-apps" %}
Intune discovered apps
{% endembed %}

Click the below to be taken directly to your Intune tenant's Discovered Apps report:

{% embed url="https://intune.microsoft.com/#view/Microsoft_Intune_DeviceSettings/AppsMonitorMenu/~/discoveredApps" %}
Intune Admin Center: Monitor | Discovered apps
{% endembed %}

### Configuration Manager

All of your data remains in your environment and is not shared with anyone, including Patch My PC.

When you choose **Scan ConfigMgr**, the tool queries the below local WMI classes, assumed to be the SMS Provider in the Configuration Manager environment:

* `SMS_G_System_INSTALLED_SOFTWARE`
* `SMS_G_System_ADD_REMOVE_PROGRAMS`
* `SMS_G_System_ADD_REMOVE_PROGRAMS_64`

## User Experience

Assuming the permissions required below are satisfied, running the tool will allow the user to click on the Scan Intune or Scan ConfigMgr buttons:

The interface will update dynamically as the tool runs, showing progress as it scans all inventory. In testing the tool requires around 1 minute for every 5,000 clients.

The Your Apps tile shows the number of applications in your environment which have been found in the Patch My PC current catalog. This is the number of apps which Patch My PC could provide management of in your environment today.

The Annual Quote tile shows the list price of the license version selected, this can be Enterprise Premium (default) or Enterprise Plus.

The Annual Hours and Annual Cost savings tiles show an estimate of the impact of using Patch My PC to handle your application updates over a manual approach. The parameters used to create these estimates can be edited in the bottom right section of the tool to reflect your cost and experience.

Clicking the Request Quote or Schedule Demo buttons will take you to the Patch My PC website to complete a short form requesting one of these services. Where possible we will pass the parameters from the tool into these forms to save you some time.

## What Permissions are Required?

This section will detail what permissions are required to run the ROI tool in your Intune or Configuration Manager environment.

### Intune

* **Application Administrator**
* **DeviceManagementManagedDevices.Read.All**

To scan Intune you must accept the application's request to read your Intune data. The account approving the request must have at least the "**Application Administrator"** role in azure. The Tool's access to this data will only persist for as long as you keep your session open (1 hour max).

![](../.gitbook/assets/image-\(1983\).png)

> \*\*Note\*\*
>
> You do not need to check the optional \*\*Consent on behalf of your organization\*\* checkbox, which is only visible to Global or Application administrators.
>
> However, if you are a Global or Application administrator and want to accept the request to read the profile for all users in your tenant and prevent this message from being displayed for them, you should check it.
>
> Either way, checking or unchecking this checkbox does not affect the ROI tool functionality.
>
> Once you accept the permissions, you will not see this dialog box again on subsequent sign-ins.

> You can click the down arrow beside each permission to get more information.

Once the app registration is approved, subsequent executions will ask for a run-as account only. This account requires, as a minimum, Intune **DeviceManagementManagedDevices.Read.All** rights.

![](../.gitbook/assets/image-\(1981\).png)

### Configuration Manager

* **Read-only Analyst**

To scan Configuration Manager the tool **must be run on your SMS Provider Server.** By default, this will be your primary site or CAS. The account running the tool must have at least the **"Read-only Analyst"** role in Configuration Manager.
