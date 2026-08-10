---
description: >-
  Getting started with Configuration Manager Apps. Please note, this portion of
  the guide is for base installations. For more in depth recommendations check
  out our configuration guides.
---

# ConfigMgr Apps

_Applies to: On-premises Publisher_

## Feature Enablement&#x20;

To activate any of the tabs in Patch My PC Publisher, the corresponding checkbox must be checked. If you do not check this option the product selection tree for the corresponding tab cannot be used.

![Enable the Configuration Manager Application Feature](<../../.gitbook/assets/image (1818).png>)

## Application Options

{% hint style="danger" %}
If you are using the **ConfigMgr Apps** tab, these options are **NOT** optional. You must configure them to be able to create applications.
{% endhint %}

The application Options button has a lot of different features. This installation guide will **not cover the options in detail** but instead give you a quick, straightforward guide to getting the product installed. For more detailed documentation, click the **more info** links in the Publisher.

Let's get started to begin, click the **Options button** next to the enablement checkbox.

<figure><img src="../../.gitbook/assets/image (2047).png" alt=""><figcaption><p>Click Options</p></figcaption></figure>

This will load the options panel in the Publisher.&#x20;

<figure><img src="../../.gitbook/assets/image (2046).png" alt=""><figcaption></figcaption></figure>

First Select the Configure[ **SMS Provider connection**](https://docs.microsoft.com/en-us/mem/configmgr/core/plan-design/hierarchy/plan-for-the-sms-provider#BKMK_PlanSMSProv). This is how you will ensure that the system where the Publisher is installed has access to the configuration manager site.

{% hint style="info" %}
Defining the SMS Provider is required, and it lets the Publisher know how to talk to your ConfigMgr site to create applications and trigger a software update point sync. By default, when a synchronization, the service will connect to ConfigMgr using SYSTEM context.

**Note**: When running the Publisher, the ConfigMgr connection will be under the context of the user running the Publisher.
{% endhint %}

After clicking the **Configure** option, the below pop-up will appear.&#x20;

<figure><img src="../../.gitbook/assets/image (2048).png" alt=""><figcaption><p>Enter the server name where the provider service is installed.</p></figcaption></figure>

Once you enter the name of the server select **Test** to validate the configuration.

<figure><img src="../../.gitbook/assets/image (2050).png" alt=""><figcaption><p>Example of validating configuration</p></figcaption></figure>

{% hint style="warning" %}
**Important**: The connection to the SMS Provider is performed using the **SYSTEM account** of the server where the Publisher is installed.

If the server that the Publisher is installed on is remote from the SMS Provider, the SYSTEM Account of the Publisher server may need to be added to the SMS Admins Group, or DCOM permissions may need to be updated ([More info](https://docs.microsoft.com/en-us/mem/configmgr/core/servers/manage/modify-your-infrastructure#configure-dcom-permissions-for-remote-configuration-manager-console-connections))
{% endhint %}

In the event the test result fails, you will instead see the following message.

![Failure message for connection as system](<../../.gitbook/assets/image (1804).png>)

If the connection fails, click **Create ConfigMgr Security Role** to automatically create a new security role with the minimum required permissions. Please see the article below for more details.

{% embed url="https://patchmypc.com/permissions-required-in-sccm-for-base-installation-packages-from-patch-my-pc#topic1" %}
Automatically create a role in ConfigMgr for Patch My PC
{% endembed %}

{% hint style="success" %}
**Tip**: If you need to create the security role, you will need to manually add the computer account to the role after it's automatically created as described [here](https://patchmypc.com/permissions-required-in-sccm-for-base-installation-packages-from-patch-my-pc).
{% endhint %}

Once you have completed a successful connection to the SMS provider select **OK** to finalize the configuration.

Next, you'll want to provide a **UNC share to store the application content**. This path needs to be accessible by the computer account of the machine running the publisher as well as the ConfigMgr site server, or a dedicated service account&#x20;

{% hint style="warning" %}
**Important**: As the Patch My PC Publisher will run in the SYSTEM context, therefore computer account the Publisher is installed on will need WRITE permissions to the share configured for source content of ConfigMgr Apps.
{% endhint %}

{% hint style="danger" %}
When you choose a path, we will create a sub-folder called **Applications** and then create a folder for each **vendor** and **product** in use. Keep this in mind when selecting the UNC path you will use to store source files.
{% endhint %}

![Applications sub-folder auto created](<../../.gitbook/assets/image (1969).png>)

The above configuration would create the below **folder structure s**imilar to the structure below.

![Folder structor for application content](<../../.gitbook/assets/image (1962).png>)

Below are the default settings which will work fine for most setups. Our product provides a lot of customization options.

![Example Simple Setup](<../../.gitbook/assets/image (1967).png>)

To learn the details about all items on this page, check out the **article below**.

{% embed url="https://patchmypc.com/application-creation-options" %}

Once you have the base options selected, you are ready to check out a simple application for testing. We recommend using 7-zip. Its small size makes it ideal for testing. Use the search icon in the bottom right or the **Ctrl+F** key combination to search for **Igor**

![Example selected application](<../../.gitbook/assets/image (1894).png>)

Select **Apply**. We do provide a large number of **right-click options to fully customize the application installation process,** those steps as described in the article below.

{% embed url="https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications" %}
