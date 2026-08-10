# Add the Executable Name(s) in the Deployment Type’s Install Behavior

_Applies to: Patch My PC Publisher V2.x_\
_&#x41;vailable at level: All Custom Products, All Products, Vendor, Product_\
_&#x41;vailable on tab: ConfigMgr Apps_

## Overview

The **Add the Executable Name(s) in the Deployment Type’s Install Behavior** option allows the Publisher to define which running processes must be closed for a ConfigMgr application installation to succeed.

![Add the Executable Name(s) in the Deployment Type's Install Behavior](/_images/image-(105).png)

These executables are applied to the deployment type’s **Install Behavior** settings and control how ConfigMgr responds when an application is in use during an install.

![Install Behavior](/_images/image-(106).png)

> \*\*Important\*\*
>
> We strongly recommend using the \[Manage Conflicting Processes]\(manage-conflicting-processes/) right-click option to notify users about running applications. That option provides greater flexibility and control, allowing for a smoother and more predictable user experience during installations and updates.

## Deployment Behavior

### Available Deployments

If any of the specified executables are running when the user initiates the installation from Software Center, the installation will fail.

![Available Deployments](/_images/image-(107).png)

The user is notified and must close the application before retrying the install.

![Install Behavior User Notification from the Software Center](/_images/image-(108).png)

### Required Deployments

If the executable remains running, the required installation will fail. If an installation fails due to a running executable, the failure reason can be reviewed in **CIAgent.log** on the client device.

![Install Behavior failure in CIAgent.log](/_images/image-(109).png)