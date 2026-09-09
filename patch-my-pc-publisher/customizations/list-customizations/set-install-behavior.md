# Set Install Behavior option in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_&#x41;vailable at level: All Custom Products, All Products, Vendor, Product_\
_&#x41;vailable on tab: ConfigMgr Apps_

The **Set Install Behavior** right-click option in Patch My PC (PMPC) Publisher lets Publisher define which running processes must close for a ConfigMgr application installation to succeed.

These executables are applied to the deployment type’s **Install Behavior** settings and control how ConfigMgr responds when an application is in use during an install.

<figure><img src="../../../.gitbook/assets/image (4739).png" alt="&#x27;Install Behavior&#x27; tab in the application’s deployment type properties" width="476"><figcaption></figcaption></figure>

{% hint style="danger" %}
**Important**

We strongly recommend using the [Manage Conflicting Processes](manage-conflicting-processes/) right-click option to notify users about running applications. This option provides more configuration flexibility and control, helping deliver a smoother, more predictable user experience during application installations and updates.
{% endhint %}

## Deployment Behavior

### Available Deployments

If any of the specified executables are running when the user initiates the installation from Software Center, the installation will fail.

<figure><img src="../../../.gitbook/assets/image (107).png" alt="Available Deployments" width="563"><figcaption></figcaption></figure>

The user is notified and must close the application before retrying the install.

<figure><img src="../../../.gitbook/assets/image (108).png" alt="Install Behavior User Notification from the Software Center" width="473"><figcaption></figcaption></figure>

### Required Deployments

If the executable remains running, the required installation will fail. If an installation fails because an executable is running, you can review the failure reason in **CIAgent.log** on the client device.

<figure><img src="../../../.gitbook/assets/image (4740).png" alt="&#x27;CIAgent.log&#x27; on the client device" width="563"><figcaption></figcaption></figure>
