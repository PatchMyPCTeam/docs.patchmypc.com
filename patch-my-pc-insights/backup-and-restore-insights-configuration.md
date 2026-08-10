# Backup and Restore Insights Configuration

_Applies to: Patch My PC Advanced and Patch Insights_

Advanced Insights stores all application configuration in a SQLite database located in the following folder:

```
%ProgramData%\AdvancedInsights\Data\Api\AdvancedInsightsConfig.db
```

Advanced Insights stores all warranty data in a SQLite database located in the following folder:

```
 %ProgramData%\AdvancedInsights\Data\Api\AdvancedInsightsWarranty.db
```

These files can be backed up by any file backup solution.&#x20;

To restore the configuration in the event of loss or server move, simply re-install Advanced Insights and copy the backup files into the same location, overwriting the blank database supplied by the installer.