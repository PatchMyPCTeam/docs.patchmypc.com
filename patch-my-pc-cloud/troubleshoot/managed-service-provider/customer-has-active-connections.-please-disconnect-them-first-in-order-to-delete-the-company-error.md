# “Customer has active connections. Please disconnect them first in order to delete the company” error

_Applies to: Patch My PC Cloud_

### SYMPTOMS

I am trying to delete a child Patch My PC (PMPC) Cloud company of a Managed Service Provider (MSP) company.

However, when I try, I get the following error:

**Error**

**Customer has active connections. Please disconnect them first in order to delete the company**

!["Customer has active connections. Please disconnect them first in order to delete the company" error](/_images/image-(1076).png "“Customer has active connections. Please disconnect them first in order to delete the company” error")

### CAUSE

This is because the child company has an active Intune connection.

### RESOLUTION

To resolve this issue:

1. Switch to the child company.
2. Follow the [Deleting an Intune tenant connection](/broken/pages/RoXhXa1jcXhIcPcKJk05#deleting-an-intune-tenant-connection) process, after which you will be able to [delete the child company](../../managed-service-provider-feature/managed-service-provider-administration/manage-msp-companies/remove-a-company-from-being-managed-cloud-msp.md#delete-a-child-company).