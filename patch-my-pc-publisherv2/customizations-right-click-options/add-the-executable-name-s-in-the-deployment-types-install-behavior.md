# Add the Executable Name(s) in the Deployment Type’s Install Behavior

_Applies to: Patch My PC Publisher V2.x_\
_Available at level: All Custom Products, All Products, Vendor, Product_
\
_Available on tab: ConfigMgr Apps_

## Overview

The **Add the Executable Name(s) in the Deployment Type’s Install Behavior** option allows the Publisher to define which running processes must be closed for a ConfigMgr application installation to succeed.&#x20;

![Add the Executable Name(s) in the Deployment Type's Install Behavior](/_images/image-(105).png "Add the Executable Name(s) in the Deployment Type’s Install Behavior")

These executables are applied to the deployment type’s **Install Behavior** settings and control how ConfigMgr responds when an application is in use during an install.

![Install Behavior](/_images/image-(106).png "Install Behavior")

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>We strongly recommend using the [Manage Conflicting Processes](manage-conflicting-processes/) right-click option to notify users about running applications. That option provides greater flexibility and control, allowing for a smoother and more predictable user experience during installations and updates.</p>
</blockquote>

## Deployment Behavior

### Available Deployments&#xD;

If any of the specified executables are running when the user initiates the installation from Software Center, the installation will fail.&#x20;

![Available Deployments](/_images/image-(107).png "Available Deployments")

The user is notified and must close the application before retrying the install.

![Install Behavior User Notification from the Software Center](/_images/image-(108).png "Install Behavior User Notification from the Software Center")

### Required Deployments&#xD;


If the executable remains running, the required installation will fail. If an installation fails due to a running executable, the failure reason can be reviewed in **CIAgent.log** on the client device.

![Install Behavior failure in CIAgent.log](/_images/image-(109).png "Install Behavior failure in CIAgent.log")