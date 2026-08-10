# “Intune connection with the same Id found in another environment” error in Cloud

_Applies to: Intune Apps for Cloud_

### SYMPTOMS

When I click **Connect** in the **Environments** node to connect my Patch My PC (PMPC) Cloud portal to Intune, after accepting the permissions, I see the following:

**Error**

**Intune connection with the same Id found in another environment**

<figure><img src="../../../.gitbook/assets/image (2455).png" alt="&#x22;Intune connection with the same Id found in another environment&#x22;"><figcaption></figcaption></figure>

### CAUSE

This error is telling you that this Intune tenant is already connected to a different PMPC Cloud Company.

At present, you can only have an Intune tenant connected to one PMPC Cloud.

### RESOLUTION

You need to decide which PMPC Company you want to be connected to this Intune tenant.

Then either disconnect Intune from the other PMPC company so you can use it with this one or setup a new Intune tenant to use with this company.
