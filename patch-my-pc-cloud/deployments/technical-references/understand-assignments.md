# Understand Patch My PC Cloud Assignments

_Applies to: Patch My PC Cloud_

As detailed in ["Assignments" tab of a Patch My PC Cloud Deployment](../deploy-app/assignments-tab.md) and [Create a Deployment without Assignments in Patch My PC Cloud](deployment-without-assignments.md), there are several different types of assignments you can configure for a Patch My PC (PMPC) Cloud deployment.

<figure><img src="../../../.gitbook/assets/image (61).png" alt="Assignment types" width="563"><figcaption></figcaption></figure>

This article focuses on some caveats and considerations specific to configuring assignments, which, if overlooked, can sometimes lead to errors.

## Assignments types

To quickly recap from the public documentation, there are two ways to deploy applications:

* [Apps with Assignments Configured in the Cloud Portal](understand-assignments.md#apps-with-assignments-configured-in-the-cloud-portal)
* [Apps without assignments](understand-assignments.md#apps-without-assignments)

### Apps with Assignments Configured in the Cloud Portal

These deployments can use four assignment types:

* **Required -** The software installation is enforced on targeted devices.
* **Available -** The software appears in the Company Portal for users to install.
* **Uninstall -** The software is removed from targeted devices.
* **UpdateOnly -** Installs a new version only if an older version is already present. Selecting this creates a new Win32 app for the update.

#### Key Point

The Cloud Portal is the source of truth for these deployments. All edits should be made in the Portal, not manually in Intune.

* By default, the Cloud Portal checks daily for new software versions.
* If you make manual changes in Intune, packaging a new version from the Portal can fail.
* Following the Portal as the source of truth ensures your assignments are applied correctly and avoids deployment errors.

### Apps without Assignments

These apps allow manual control in Intune and come in two types:

* **Install App –** A base installation. You can assign it in Intune as **Required**, **Available**, or **Uninstall**.
* **UpdateOnly App –** A conditional Win32 update. Intune evaluates whether a device has an older version installed before applying the update.

#### Key Point

For these apps, Intune is the source of truth. You manage assignments manually in Intune, and the Portal does not enforce them.

* If the **Copy-Forward** option is enabled, the Portal will copy these manual assignments to new versions automatically.
* If **Copy-Forward** is not enabled, assignments are not carried over, and you must manage them manually for each new version.
* Once a deployment is created without assignments in the Portal, you cannot switch it later to a deployment with pre-configured Cloud Portal assignments. You must create a new deployment if you want that functionality.
