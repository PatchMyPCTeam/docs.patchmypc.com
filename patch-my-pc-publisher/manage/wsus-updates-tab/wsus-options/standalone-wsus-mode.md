# Standalone WSUS Mode section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Standalone WSUS Mode** section on the **WSUS Options** tab of Patch My PC (PMPC) Publisher configures Standalone WSUS Mode when Publisher integrates directly with WSUS without Microsoft Configuration Manager (ConfigMgr).

<figure><img src="../../../../.gitbook/assets/image (1046).png" alt="&#x27;Standalone WSUS Mode&#x27; section" width="563"><figcaption></figcaption></figure>

This mode is intended only for environments that manage updates using WSUS standalone. It is not required and should not be enabled when ConfigMgr manages software updates.

## Make updates appear in the WSUS console. This option isn’t needed if using Configuration Manager

Checking the **Make updates appear in the WSUS console. This option isn’t needed if using Configuration Manager** checkbox (unchecked by default) enables Standalone WSUS Mode, which controls whether locally published third party updates are visible in the WSUS console.&#x20;

When Standalone WSUS Mode is enabled, Publisher marks updates as locally published so they appear in the WSUS console and can be viewed and managed directly in WSUS.

{% hint style="danger" %}
**Important**

If ConfigMgr is present and managing software updates, you should not check this checkbox.
{% endhint %}

## Use SYSTEM account when connecting to the SQL database or define a custom account below

The **Use SYSTEM account when connecting to the SQL database or define a custom account below** checkbox controls how Publisher connects to the WSUS SQL database when Standalone WSUS Mode is enabled.

{% hint style="success" %}
**Tip**

If your WSUS database uses the Windows Internal Database (WID), the database connection options are read-only. In this scenario, you don't need or use SQL credentials.
{% endhint %}

If checked, Publisher connects to the WSUS database using the local SYSTEM account of the machine where Publisher is installed. This is the recommended and default option for most WSUS standalone deployments, as the SYSTEM account typically already has the required permissions to access the WSUS database.

If you don't check this box, you can specify a custom SQL login instead by entering the credentials in the **SQL Login** and **SQL Password** fields. This may be required in environments where WSUS uses a remote SQL Server or where security policies restrict SYSTEM account access. In that case, the specified SQL account must have sufficient permissions to read and update the WSUS database.

{% hint style="info" %}
**Note**

For updates published before WSUS Standalone mode was enabled, use the [Modify Updates Wizard](modify-published-updates.md) to make those updates appear in the WSUS console using the **Show in WSUS** option.
{% endhint %}

## SQL Permissions Required <a href="#h-sql-permissions-required-to-publish-update-information-to-the-database" id="h-sql-permissions-required-to-publish-update-information-to-the-database"></a>

When Publisher syncs run, if the SUSDB is remote from the Standalone WSUS server, you must grant specific permissions to the computer account where Publisher is installed so that it can update information.

Use the script below to grant the required permissions, replacing the computer account values with those appropriate to your environment.

Edit the script as needed, then run it as a SQL query in SQL Server Management Studio.

```sql
USE SUSDB
GO

-- Replace CONTOSO\ServerName$ with the appropriate value for your environment
DECLARE @UserName nvarchar(128) = 'CONTOSO\ServerName$'

DECLARE @QuotedUserToGrant nvarchar(128) = QUOTENAME(@UserName);

IF NOT EXISTS(SELECT principal_id FROM sys.server_principals WHERE name = @UserName) BEGIN
DECLARE @LoginSQL as varchar(500);
SET @LoginSQL = 'CREATE LOGIN '+ @QuotedUserToGrant + ' FROM WINDOWS';
EXEC (@LoginSQL);
END

IF NOT EXISTS(SELECT principal_id FROM sys.database_principals WHERE name = @UserName) BEGIN
DECLARE @UserSQL as varchar(500);
SET @UserSQL = 'CREATE USER ' + @QuotedUserToGrant + ' FOR LOGIN ' + @QuotedUserToGrant;
EXEC (@UserSQL);
END

DECLARE @PermissionsSQL as varchar(500);
SET @PermissionsSQL = 'GRANT UPDATE ON [dbo].[tbUpdate] ([IsLocallyPublished]) TO ' + @QuotedUserToGrant +
'GRANT SELECT ON [dbo].[tbUpdate] ([UpdateID]) TO ' + @QuotedUserToGrant;
EXEC (@PermissionsSQL);
```
