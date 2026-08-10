# Custom App Requirements for Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

Patch My PC (PMPC) Custom Apps allow you to package and manage your own applications alongside the Patch My PC catalog.

Publisher integrates with [Patch My PC Cloud](../../patch-my-pc-cloud/) to retrieve Custom App metadata and publish it into your environment using your existing publishing workflows.

## Requirements

> \*\*Important\*\*
>
> These requirements only apply if you are publishing Custom Apps through Publisher to either Microsoft ConfigMgr or Intune.

To publish Custom Apps to either Microsoft ConfigMgr or Intune using Publisher, you must meet **all** of the following requirements:

* Be using Publisher version 2.1.20.0 or later.
* Have an active Enterprise Plus, Enterprise Premium, or MSP subscription.
* Your organization must be [onboarded](custom-app-requirements.md#step-1-onboard-to-patch-my-pc-cloud) to PMPC Cloud by creating a Cloud Company.
* Publisher must be [connected](custom-app-requirements.md#step-2-connect-publisher-to-the-patch-my-pc-cloud-company) to your Cloud Company.

> \*\*Note\*\*
>
> Customers with a Managed Service Provider (MSP) or MSP Plus subscription can connect Publisher to only one PMPC Cloud company. We recommend connecting Publisher to the MSP Parent Cloud company, rather than an individual MSP customer Cloud company, to ensure proper management and visibility of the Custom Apps made available to Publisher.

> \*\*Important\*\*
>
> Publisher is not required if you only plan to deploy your Custom Apps from PMPC Cloud.

## Step 1: Onboard to Patch My PC Cloud

1. Sign in or sign up to **Patch My PC Cloud**.
2. Create or select your **Cloud Company**

> \*\*Note\*\*
>
> See \[Onboard to Patch My PC Cloud]\(../../patch-my-pc-cloud/onboard-cloud.md) for more details.

## Step 2: Connect Publisher to your Patch My PC Cloud Company

If you plan to publish Custom Apps or use Cloud-integrated features from Publisher, you must create a Cloud connection.

1. Open **Patch My PC Publisher**.
2. Navigate to **Administration | Cloud Connections**.
3. Select **Add a Connection**
4. Sign in using your PMPC Cloud credentials.
5. Complete the connection wizard and confirm the connection status.

Once connected, Publisher can securely communicate with PMPC Cloud for supported features.

> \*\*Note\*\*
>
> See \[Add a Connection in Patch My PC Cloud]\(../../patch-my-pc-cloud/manage/settings/connections/add-connection.md) for more details.

## Multiple Cloud Companies

If the account used to sign in is associated with multiple PMPC Cloud companies, a selection window will appear.

![Select a Cloud Company](/_images/image-(4140).png)

Select the appropriate company from the list and click **OK** to complete the connection process.