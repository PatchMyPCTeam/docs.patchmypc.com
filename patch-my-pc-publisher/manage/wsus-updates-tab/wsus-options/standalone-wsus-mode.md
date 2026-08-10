# Standalone WSUS Mode section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>This article has not been updated for Version 3.x. Once it has, this banner will be removed.</p>
</blockquote>

**Standalone WSUS Mode** is used when the Patch My PC (PMPC) Publisher is integrated directly with WSUS without ConfigMgr.

![Standalone WSUS Mode](/_images/image-(93).png "Standalone WSUS Mode")

This mode is intended only for environments that manage updates using WSUS standalone. It is not required and should not be enabled when ConfigMgr is used to manage software updates.

Standalone WSUS Mode controls whether locally published third party updates are visible in the WSUS console. When this mode is enabled, the Publisher marks updates as locally published so they appear in the WSUS console and can be viewed and managed directly in WSUS.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>If ConfigMgr is present and managing software updates, WSUS Standalone Mode should remain disabled.</p>
</blockquote>

## **Use SYSTEM Account**

The **Use SYSTEM account** option controls how the Publisher connects with the WSUS SQL database when WSUS Standalone Mode is enabled.

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>If your WSUS database uses the Windows Internal Database (WID), the database connection options are read only. In this scenario, no SQL credentials are required or used.</p>
</blockquote>

When selected, the Publisher connects to the WSUS database using the local SYSTEM account of the machine where the Publisher is installed. This is the recommended and default option for most WSUS standalone deployments, as the SYSTEM account typically already has the required permissions to access the WSUS database.

If this option is not selected, you can specify a custom SQL login instead. This may be required in environments where WSUS uses a remote SQL Server or where security policies restrict SYSTEM account access. In that case, the specified SQL account must have sufficient permissions to read and update the WSUS database.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>For updates published before WSUS Standalone mode was enabled, use the [Modify Updates Wizard](../../../../patch-my-pc-publisherv2/administration/updates/options/modify-published-updates.md) to make those updates appear in the WSUS console using the **Show in WSUS** option.</p>
</blockquote>

## SQL Permissions Required <a href="#h-sql-permissions-required-to-publish-update-information-to-the-database" id="h-sql-permissions-required-to-publish-update-information-to-the-database"></a>

When the Publisher Sync runs, if the SUSDB is remote from the WSUS Standalone server, you would have to grant specific permissions to the computer account where the Publisher is installed for it to be able to update information.

The script below can be used to grant the required permissions. Replace the computer account values with the ones appropriate to your environment.

Edit the script as needed and run it as a SQL query using SQL Server Management Studio.

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