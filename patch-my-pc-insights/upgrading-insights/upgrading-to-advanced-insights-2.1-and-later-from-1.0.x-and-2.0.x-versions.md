# Upgrading to Advanced Insights 2.1 and later from 1.0.x and 2.0.x versions

_Applies to: Patch My PC Advanced and Patch Insights_

Version 2.1 of Advanced Insights removes SQL Server dependency. Advanced Insights configuration data previously stored in SQL Server will now be maintained in a SQLite database which is stored in _%ProgramData%\AdvancedInsights\Data\Api\AdvancedInsightsConfig.db_

Example upgrade summary page when migrating from SQL to SQLite db:

![Advanced Insights Upgrade](/_images/image-(4345).png)

All data will be migrated to this new database from SQL Server when the application first starts up following upgrade.

Once this is complete (you can confirm this by logging into Advanced Insights post-install) you can safely remove the PMPCAdvancedInsights SQL database. If you had installed SQL Express to support this requirement, this can also be removed.