# ARM support in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

Patch My PC (PMPC) Cloud supports deploying Advanced RISC Machine (ARM) apps to ARM devices.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>ARM support is currently limited to a few apps deployed via Patch My PC Cloud (we are adding more) and is in Public Preview in our On-premises Publisher.</p>
</blockquote>

You will see ARM support in the following features/areas of PMPC Cloud:

* [Filter by Architecture](arm-support.md#filter-by-architecture)
* [Deploy an App](arm-support.md#deploy-an-app)
* [Discovery](arm-support.md#discovery)
* [Binary Free Apps](arm-support.md#binary-free-apps)
* [MSP App Sets](arm-support.md#msp-app-sets)

## Filter by Architecture

Now, when you click the Filter button and select the **Architecture** dropdown, you will see the **ARM** option.

!["ARM" option in the "Architecture" dropdown](/_images/image-(3470).png "“ARM” option in the “Architecture” dropdown")

Checking this checkbox and clicking **Apply All Filters** will filter the App Catalog to only those apps that can be deployed to ARM devices.

!["ARM" filtered list of apps.](/_images/image-(3471).png "“ARM” filtered list of apps.")

## Deploy an App

When you [Deploy an App using Cloud](deployments/deploy-app/), if an app supports ARM, you will see **ARM** listed under the **Architecture** field on the properties page of the app.

!["ARM" listed under the "Architecture" field on the properties page of an app.](/_images/image-(3472).png "“ARM” listed under the “Architecture” field on the properties page of an app.")

When you click **Deploy**, **ARM** will be shown as an option under the **Architecture** section.

!["ARM" listed under the "Architecture" field on the properties page of an app.](/_images/image-(3473).png "“ARM” listed under the “Architecture” field on the properties page of an app.")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>We currently do not support creating Custom Apps for ARM.</p>
<p>Architecture-specific apps may report as Installed on devices with a different architecture due to a known detection script limitation. This is a reporting issue only and does not result in any software being installed. See <a href="https://patchmypc.com/kb/arm64-update-may-show-as-installed-on-x64-devices/">ARM64 update may show as Installed on x64 devices</a> for details and a recommended workaround.</p>
</blockquote>

## Discovery

Discovery now supports both the discovery and deployment of ARM apps.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>See [Discovery in Cloud](discovery/) for more information.</p>
</blockquote>

## Binary Free Apps

When you [Upload the app installer](binary-free-apps/deploy-a-binary-free-app.md#upload-the-app-installer) as part of creating a Binary Free App, if the app supports ARM, on the **General Information** tab, you will see **ARM** listed under the **Architecture** setting.

!["ARM" listed under the "Architecture" field on the "General Information" tab of a Binary Free App.](/_images/image-(3474).png "“ARM” listed under the “Architecture” field on the “General Information” tab of a Binary Free App.")

## MSP App Sets

If you are a Managed Service Provider (MSP) using MSP App Sets, when you [add an app to an App Set](managed-service-provider-feature/msp-app-sets/create-an-msp-app-set.md#adding-apps-to-the-app-set), if the app supports ARM, you will see **ARM** listed under the **Architecture** field on the **General Information** tab.

!["ARM" listed under the "Architecture" field on the properties page of an app.](/_images/image-(3475).png "“ARM” listed under the “Architecture” field on the properties page of an app.")