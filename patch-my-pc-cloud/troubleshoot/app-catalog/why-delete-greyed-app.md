# Why is the 'Delete' option greyed out for an app in Patch My PC Cloud?

_Applies to: Patch My PC Cloud_

### SYMPTOMS

I am trying to delete an app from the Patch My PC (PMPC) Cloud App Catalog.

But when I click on the app and open its properties, the **Delete** option is greyed out.

![](/_images/image-(2654).png)

### CAUSE

This is because the app has one or more active deployments. You cannot delete an app that has active deployments.

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>If you put your mouse over the **Delete** button, the mouseover text actually tells you:</p>
<p>**This app has deployments. Please delete those first.**</p>
</blockquote>

### RESOLUTION

To resolve this issue, delete any existing deployments for the app by following the [Delete a Deployment](../../deployments/manage-deployments/delete.md) process. Once these have been deleted successfully, you will be able to delete the app.