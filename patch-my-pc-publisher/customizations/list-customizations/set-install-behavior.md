# Set Install Behavior option in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_&#x41;vailable at level: All Custom Products, All Products, Vendor, Product_\
_&#x41;vailable on tab: ConfigMgr Apps_

> \*\*Important\*\*
>
> This article has not been updated for Version 3.x. Once it has, this banner will be removed.

The **Set Install Behavior** right-click option in Patch My PC (PMPC) Publisher allows the Publisher to define which running processes must be closed for a ConfigMgr application installation to succeed.

These executables are applied to the deployment type’s **Install Behavior** settings and control how ConfigMgr responds when an application is in use during an install.

!['Install Behavior' tab in the application's deployment type properties](/_images/image-(4739).png)

> \*\*Important\*\*
>
> We strongly recommend using the \[Manage Conflicting Processes]\(manage-conflicting-processes/) right-click option to notify users about running applications. This option provides greater configuration flexibility and control, allowing you to deliver a smoother and more predictable user experience during application installations and updates.

## Deployment Behavior

### Available Deployments

If any of the specified executables are running when the user initiates the installation from Software Center, the installation will fail.

![Available Deployments](/_images/image-(107).png)

The user is notified and must close the application before retrying the install.

![Install Behavior User Notification from the Software Center](/_images/image-(108).png)

### Required Deployments

If the executable remains running, the required installation will fail. If an installation fails due to a running executable, the failure reason can be reviewed in **CIAgent.log** on the client device.

!['CIAgent.log' on the client device](/_images/image-(4740).png)