# Publish the Migrated App in Intune as a Suggested Patch My PC Catalog App

_Applies to: Patch My PC Cloud_

When migrating a Configuration Manager (ConfigMgr) application as a suggested Patch My PC (PMPC) Catalog App, the migration flow depends on how many catalog matches are found.

If multiple PMPC Catalog Apps match the ConfigMgr application, you are first presented with the **Matched App** step, which allows you to review the available matches and select the PMPC Catalog App to migrate to.

![Multiple suggested apps identified](../../../.gitbook/assets/image-\(3816\).png)

After you select the appropriate match, the migration continues into the deployment flow with the selected application pre-selected.

![Migration deployment flow](../../../.gitbook/assets/image-\(3817\).png)

If only a single unique PMPC Catalog App match is identified, the **Matched App** step is skipped entirely and the migration moves straight into the deployment flow with that application automatically pre-selected.

![Single suggested app is matched](<../../../.gitbook/assets/image-(325) (1).png>)

> \*\*Note\*\*
>
> Where possible, details such as architecture and installer type are inferred from the original ConfigMgr application and populated automatically to reduce manual configuration.

From this point, continue following [Publish the App in Intune as a PMPC Catalog App](publish-migrated-app-catalog-app.md), where the remaining steps of the deployment flow are completed.
