# Custom App Requirements

_Applies to: Patch My PC Publisher V2.x_

## Overview

Patch My PC Custom Apps allow you to package and manage your own applications alongside the Patch My PC catalog. The Publisher integrates with [Patch My PC Cloud](https://docs.patchmypc.com/patch-my-pc-cloud) to retrieve Custom App metadata and publish it into your environment using your existing publishing workflows. The requirements below explicitly apply only if you are publishing Custom Apps through the on-premises Publisher to either ConfigMgr or Intune.

## Requirements

To publish Custom Apps to either ConfigMgr or Intune using the the Publisher, you must meet **all** of the following requirements:

* Publisher version 2.1.20.0 or later.
* An active Enterprise Plus, Enterprise Premium, or MSP subscription.
* Your organization must be [onboarded ](custom-app-requirements.md#step-1-onboard-to-patch-my-pc-cloud)to Patch My PC Cloud by creating a Cloud Company.
* The Publisher must be [connected ](custom-app-requirements.md#step-2-connect-the-publisher-to-patch-my-pc-cloud)to the Cloud Company.

> \*\*Note\*\*
>
> Customers with an MSP or MSP Plus subscription can connect the Publisher to only one Patch My PC Cloud company. We recommend connecting the Publisher to the MSP parent Cloud company, rather than an individual MSP customer Cloud company, to ensure proper management and visibility of the Custom Apps made available to the Publisher.

> \*\*Important\*\*
>
> If you only plan to deploy your Custom Apps from Patch My PC Cloud, the Publisher is not required.

## Step 1: Onboard to Patch My PC Cloud

1. Sign in or sign-up to **Patch My PC Cloud**.
2. Create or select your **Cloud Company**

For detailed onboarding instructions, see [https://docs.patchmypc.com/patch-my-pc-cloud/onboard-to-cloud](https://docs.patchmypc.com/patch-my-pc-cloud/onboard-to-cloud).

## Step 2: Connect the Publisher to the Patch My PC Cloud Company

If you plan to publish Custom Apps or use Cloud-integrated features from the on-premises Publisher, you must create a Cloud connection.

1. Open **Patch My PC Publisher**.
2. Navigate to **Administration > Cloud Connections**.
3. Select **Add a Connection**.
4. Sign in using your Patch My PC Cloud credentials.
5. Complete the connection wizard and confirm the connection status.

Once connected, the Publisher can securely communicate with Patch My PC Cloud for supported features.

For detailed connection steps, see [https://docs.patchmypc.com/patch-my-pc-cloud/cloud-administration/manage-cloud-connections/add-a-connection](https://docs.patchmypc.com/patch-my-pc-cloud/cloud-administration/manage-cloud-connections/add-a-connection).

### Multiple Cloud Companies

If the account used to sign in is associated with multiple Patch My PC Cloud companies, a selection window will appear.

![Select a Cloud Company](/_images/image-(4140).png)

Select the appropriate company from the list and click OK to complete the connection process.