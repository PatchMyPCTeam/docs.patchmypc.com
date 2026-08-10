# About the "General Information" tab of a Patch My PC Cloud Deployment

_Applies to: Patch My PC Cloud_

The **General Information** tab of the Patch My PC (PMPC) Cloud deployment wizard allows you to configure various general settings (explained below) for how you want the app to be deployed.

> \*\*Note\*\*
>
> If an app has multiple variants with different version numbers, you will see a yellow triangle with an exclamation mark next to the \*\*Version\*\* number. This is a warning to you to double-check that you are deploying the correct version.

!['General Information' tab](../../../.gitbook/assets/image-\(3528\).png)

Once you have finished configuring the relevant options, go to [Next Steps](general-information-tab.md#next-steps).

## Apply Template

Allows you to apply a [Template](../use-template.md) of pre-configured settings to this deployment.

> \*\*Important\*\*
>
> If you apply a Template to a Deployment and a setting in the Template conflicts with a setting configured in App Catalog, you will see an error.
>
> For example, you have configured a Requirement Rule in a Template and then applied the Template to a deployment. If the setting in App Catalog conflicts with that in the Template, you will see an error indicating the minimum acceptable value to which it should be configured. You will need to change the relevant setting to dismiss the error before you can continue.

## Connection

Shows the type of connection. Currently, we only support connections to Intune.

## Display Name

The unique name for this deployment. This is also the name of the app as it will appear on the target devices.

> \*\*Note\*\*
>
> This \*\*Display Name\*\* has to be unique per operating system. For example, you can have two deployments for the same app if one is targeted to macOS and the other Windows. You cannot have two deployments with the same name if they are both targeted to either macOS or Windows.

## Language

Multiple language entries will be present if the vendor offers separate installers for that language. For example, an EXE installer for en-US, de-DE, etc. The majority of installers are multi-language (one installer, multiple languages), and the software can be configured in different languages by:

* Specifying additional installation parameters
* Configuring .config or .xml files
* Setting registry values.

In such cases, it is the vendor that determines the level of support and the behavior.

## Architecture

The architecture of the installer to be deployed:

* 64-bit installers can only be installed on 64-bit devices
* 32-bit installers can typically be installed on either 32-bit or 64-bit devices.
* Unspecified installers typically contain install logic for both architectures.

## Install Context

The context in which to install the application:

* **System –** Available to all users.
* **User –** Available only to the specific user.

## Installer Type

The available installer types you can choose from to install this app.

### **Windows Installer Types**

We currently support the following Windows installer types:

* .exe
* .msi

> \*\*Note\*\*
>
> If the \*\*.msi\*\* option is greyed out, it's probably because this is a \[Binary Free]\(../../binary-free-apps/binary-free-apps-overview.md) app, i.e. you need to manually download the installer from the vendor and create it in PMPC Cloud as a \[Binary Free App]\(../../binary-free-apps/deploy-a-binary-free-app.md) (the "\*\*Upload the required installer via 'Manage Files' to enable selection of this variant\*\*" message indicates this).

* .msp

> \*\*Note\*\*
>
> As per the tooltip, if you select the \*\*msp\*\* installer type, you will only be able to create a deployment with an \*\*Update Only\*\* assignment. If you want to create a deployment using the other assignment types, you will need to select the \*\*exe\*\* installer.

### **macOS Installer Types**

We currently support the following macOS installer types:

* .dmg
* .pkg

## Next Steps

Once you have finished configuring the relevant options, click **Next** to move to the [Configurations ](configurations-tab/)tab.

![Clicking 'Next' to move to the 'Configurations' page](../../../.gitbook/assets/image-\(3529\).png)
