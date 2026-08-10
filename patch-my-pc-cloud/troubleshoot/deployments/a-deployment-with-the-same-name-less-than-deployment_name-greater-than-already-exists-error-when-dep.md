# “A deployment with the same name \<deployment\_name> already exists” error when deploying a Cloud app

_Applies to: Intune Apps for Cloud_

### SYMPTOMS

When I deploy software using Intune Apps for Cloud (Intune Apps), why am I seeing the following error:

**Error**

**A deployment with the same name <**_**deployment\_name**_**> already exists.**

![](/_images/image-(2157).png)

### CAUSE

This message is telling you that you already have a deployment with the same name.

### RESOLUTION

Ensure the **Display Name** for your deployment is unique.&#x20;

If you want to deploy the same software with the same configuration but to different Entra ID groups, follow the [Deploying the same App with multiple configurations](../../deployments/technical-references/deploy-same-app.md) process.