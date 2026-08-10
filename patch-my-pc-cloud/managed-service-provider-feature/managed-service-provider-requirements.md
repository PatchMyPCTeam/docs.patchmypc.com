# Managed Service Provider Requirements

_Applies to: Patch My PC Cloud_

To use the Managed Service Provider (MSP) feature of Patch My PC (PMPC) Cloud:

* The parent MSP company needs to be [onboarded to PMPC Cloud](../onboard-cloud.md).

{% hint style="info" %}
**Note**

Once the parent MSP company has been onboarded to PMPC Cloud, you can navigate to **Settings | Environments** and click the vertical ellipsis (**⋮**) beside the expiry date followed by **Activate License** to activate your MSP License without having to connect to Intune first.\
\
<img src="../../.gitbook/assets/image (3482).png" alt="Activating a PMPC Cloud license" data-size="original">\
\
The child company to be managed by the MSP company does not need to be onboarded to PMPC Cloud, as the parent company will complete this when it starts managing the child company.
{% endhint %}

* The parent MSP company will need to be configured to use an [MSP Plus license](license-the-managed-service-provider-feature.md).
* The MSP onboarding the child company will need the credentials of an account with the Global Administrator role in the child company’s Intune tenant to be managed.
