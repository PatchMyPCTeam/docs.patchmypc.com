---
description: Instructions for removing Advanced Insights
---

# Uninstalling Insights

_Applies to: Patch My PC Advanced and Patch Insights_

To completely remove the product we will carry out the following actions:

1. Remove the Advanced Insights Inventory Extensions (if deployed)
2. Uninstall the Advanced Insights product
3. Remove the Advanced Insights database

### Removing the Inventory Extensions

You can manually remove the Inventory Extensions from a ConfigMgr Console under: Administration > Client Settings > Default Client Settings > Hardware Inventory > Set Classes ...

Carefully Select and delete each PMPC\_ Inventory Class from this window individually. This will remove them from your Hardware Inventory Schema and delete their data from the database:

<figure><img src="../.gitbook/assets/PMPC_Classes.PNG" alt=""><figcaption><p><em>*When removing manually you should also ensure to remove any existing PMPC Inventory Deployments</em></p></figcaption></figure>

### Uninstall Advanced Insights

The uninstall is automated from Settings / Add Remove programs, simply select the application and click remove.

The uninstall will leave behind some customization files, including the Advanced Insights SQLite DB. This can all be removed by deleting the following folder:

```
%ProgramData%\AdvancedInsights
```
