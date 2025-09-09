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

![Enable the Configuration Manager Application Feature](/_images/image (1116).png>)

## Application Options

<blockquote class="wp-block-quote">
<p>If you are using the <strong>ConfigMgr Apps</strong> tab, these options are <strong>NOT</strong> optional. You must configure them to be able to create applications.</p>
</blockquote>

The application Options button has a lot of different features. This installation guide will <strong>not cover the options in detail</strong> but instead give you a quick, straightforward guide to getting the product installed. For more detailed documentation, click the <strong>more info</strong> links in the Publisher.

Let's get started to begin, click the <strong>Options button</strong> next to the enablement checkbox.

![](/_images/image-(1345).png "Click Options")

This will load the options panel in the Publisher.&#x20;

![](/_images/image-(1344).png "")

First Select the Configure[ <strong>SMS Provider connection</strong>](https://docs.microsoft.com/en-us/mem/configmgr/core/plan-design/hierarchy/plan-for-the-sms-provider#BKMK_PlanSMSProv). This is how you will ensure that the system where the Publisher is installed has access to the configuration manager site.

<blockquote class="wp-block-quote">
<p>Defining the SMS Provider is required, and it lets the Publisher know how to talk to your ConfigMgr site to create applications and trigger a software update point sync. By default, when a synchronization, the service will connect to ConfigMgr using SYSTEM context.</p>
<p><strong>Note</strong>: When running the Publisher, the ConfigMgr connection will be under the context of the user running the Publisher.</p>
</blockquote>

After clicking the <strong>Configure</strong> option, the below pop-up will appear.&#x20;

![](/_images/image-(1346).png "Enter the server name where the provider service is installed.")

Once you enter the name of the server select <strong>Test</strong> to validate the configuration.

![](/_images/image-(1348).png "Example of validating configuration")

<blockquote class="wp-block-quote">
<p><strong>Important</strong>: The connection to the SMS Provider is performed using the <strong>SYSTEM account</strong> of the server where the Publisher is installed.</p>
<p>If the server that the Publisher is installed on is remote from the SMS Provider, the SYSTEM Account of the Publisher server may need to be added to the SMS Admins Group, or DCOM permissions may need to be updated (<a href="https://docs.microsoft.com/en-us/mem/configmgr/core/servers/manage/modify-your-infrastructure#configure-dcom-permissions-for-remote-configuration-manager-console-connections">More info</a>)</p>
</blockquote>

In the event the test result fails, you will instead see the following message.

![Failure message for connection as system](/_images/image (1102).png>)

If the connection fails, click <strong>Create ConfigMgr Security Role</strong> to automatically create a new security role with the minimum required permissions. Please see the article below for more details.

{% embed url="https://patchmypc.com/permissions-required-in-sccm-for-base-installation-packages-from-patch-my-pc#topic1" %}
Automatically create a role in ConfigMgr for Patch My PC
{% endembed %}

<blockquote class="wp-block-quote">
<p><strong>Tip</strong>: If you need to create the security role, you will need to manually add the computer account to the role after it's automatically created as described <a href="https://patchmypc.com/permissions-required-in-sccm-for-base-installation-packages-from-patch-my-pc">here</a>.</p>
</blockquote>

Once you have completed a successful connection to the SMS provider select <strong>OK</strong> to finalize the configuration.

Next, you'll want to provide a <strong>UNC share to store the application content</strong>. This path needs to be accessible by the computer account of the machine running the publisher as well as the ConfigMgr site server, or a dedicated service account&#x20;

<blockquote class="wp-block-quote">
<p><strong>Important</strong>: As the Patch My PC Publisher will run in the SYSTEM context, therefore computer account the Publisher is installed on will need WRITE permissions to the share configured for source content of ConfigMgr Apps.</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>When you choose a path, we will create a sub-folder called <strong>Applications</strong> and then create a folder for each <strong>vendor</strong> and <strong>product</strong> in use. Keep this in mind when selecting the UNC path you will use to store source files.</p>
</blockquote>

![Applications sub-folder auto created](/_images/image (1267).png>)

The above configuration would create the below <strong>folder structure s</strong>imilar to the structure below.

![Folder structor for application content](/_images/image (1260).png>)

Below are the default settings which will work fine for most setups. Our product provides a lot of customization options.

![Example Simple Setup](/_images/image (1265).png>)

To learn the details about all items on this page, check out the <strong>article below</strong>.

{% embed url="https://patchmypc.com/application-creation-options" %}

Once you have the base options selected, you are ready to check out a simple application for testing. We recommend using 7-zip. Its small size makes it ideal for testing. Use the search icon in the bottom right or the <strong>Ctrl+F</strong> key combination to search for <strong>Igor</strong>

![Example selected application](/_images/image (1192).png>)

Select <strong>Apply</strong>. We do provide a large number of <strong>right-click options to fully customize the application installation process,</strong> those steps as described in the article below.

{% embed url="https://patchmypc.com/custom-options-available-for-third-party-updates-and-applications" %}