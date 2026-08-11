# Set Install Behavior option in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_Available at level: All Custom Products, All Products, Vendor, Product_\
_Available on tab: ConfigMgr Apps_

{% hint style="danger" %}
**Important**

This article has not been updated for Version 3.x. Once it has, this banner will be removed.
{% endhint %}

The **Set Install Behavior** right-click option in Patch My PC (PMPC) Publisher allows the Publisher to define which running processes must be closed for a ConfigMgr application installation to succeed.&#x20;

These executables are applied to the deployment type’s **Install Behavior** settings and control how ConfigMgr responds when an application is in use during an install.

<figure><img src="../../../.gitbook/assets/image (4739).png" alt="&#x27;Install Behavior&#x27; tab in the application’s deployment type properties" width="476"><figcaption></figcaption></figure>

{% hint style="danger" %}
**Important**

We strongly recommend using the [Manage Conflicting Processes](manage-conflicting-processes/) right-click option to notify users about running applications. This option provides greater configuration flexibility and control, allowing you to deliver a smoother and more predictable user experience during application installations and updates.
{% endhint %}

## Deployment Behavior

### Available Deployments&#xD;

If any of the specified executables are running when the user initiates the installation from Software Center, the installation will fail.&#x20;

<figure><img src="../../../.gitbook/assets/image (107).png" alt="Available Deployments" width="563"><figcaption></figcaption></figure>

The user is notified and must close the application before retrying the install.

<figure><img src="../../../.gitbook/assets/image (108).png" alt="Install Behavior User Notification from the Software Center" width="473"><figcaption></figcaption></figure>

### Required Deployments&#xD;

If the executable remains running, the required installation will fail. If an installation fails due to a running executable, the failure reason can be reviewed in **CIAgent.log** on the client device.

<figure><img src="../../../.gitbook/assets/image (4740).png" alt="&#x27;CIAgent.log&#x27; on the client device" width="563"><figcaption></figcaption></figure>
