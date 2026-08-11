---
description: Advanced Insights ConfigMgr SQL Permissions requirements
---

# Insights SQL Permission requirements

_Applies to: Patch My PC Advanced and Patch Insights_

{% hint style="info" %}
If Advanced Insights is installed on your ConfigMgr site server, then you should not need to do any SQL permissions configuration.&#x20;

The Advanced Insights IIS Application Pools can run as the local computer Identity, which has ConfigMgr SQL database access by default. If Advanced Insights is installed on the same server as Config Manager database this account will show as NT Authority\System in SSMS, else if on a different server it will show as the hostname of the server Advanced Insights is installed on.

Alternatively, a custom ID can be used. See: [advanced-insights-iis-application-pool-identity.md](advanced-insights-iis-application-pool-identity.md "mention")
{% endhint %}

Advanced Insights needs read access to the ConfigMgr SQL database. If Advanced Insights is installed on a server that is not the ConfigMgr site server, or a custom Active Directory account is used for the IIS application pools, you will need to grant some SQL permissions.

## Assigning Rights to ConfigMgr SQL

### Option 1 - Using the Advanced Insights Computer Account

1. Open SQL Management Studio and connect to the required SQL instance for your ConfigMgr database
2. Execute the following script replacing the **domain\computername** and **CM\_XXX** database name

```sql
Use Master
DECLARE @ADVINSTSERVERNAME AS VARCHAR(100)
DECLARE @CMDBNAME AS VARCHAR(100)
SET @ADVINSTSERVERNAME ='domain\computername$' -- Replace 'domain\computername$' - Example 'contoso\sccmsqlsvr$'
SET @CMDBNAME ='CM_XXX' -- Replace with the name of your ConfigMgr database name
DECLARE @LOGIN_nonquoted AS VARCHAR(100) = @ADVINSTSERVERNAME
DECLARE @LOGIN AS VARCHAR(100) = QUOTENAME(@LOGIN_nonquoted)
DECLARE @CMDBNAME_nonquoted AS VARCHAR(100) = @CMDBNAME


EXEC ('CREATE LOGIN ' + @LOGIN + ' FROM WINDOWS');
EXEC ('USE' +' '+@CMDBNAME+';' + 'CREATE USER ' + @LOGIN + ' FOR LOGIN ' + @LOGIN);
EXEC ('USE' +' '+@CMDBNAME+';' + 'ALTER ROLE db_datareader ADD MEMBER' + @LOGIN)
```

### Option 2 - Using a user account for Advanced Insights

Advanced Insights access to the Configuration Manager SQL database can be configured to use a Active Directory user account. This account is set as the IIS application pool identity.&#x20;

See: [advanced-insights-iis-application-pool-identity.md](advanced-insights-iis-application-pool-identity.md "mention")

1. Open SQL Management Studio and connect to the required SQL instance for your ConfigMgr database
2. Execute the following script replacing the **domain\username** and **CM\_XXX** database name

```sql
Use Master
DECLARE @ADVINSTSERVERNAME AS VARCHAR(100)
DECLARE @CMDBNAME AS VARCHAR(100)
SET @ADVINSTSERVERNAME ='domain\username' -- Replace 'domain\username' - Example 'contoso\john'
SET @CMDBNAME ='CM_XXX' -- Replace with the name of your ConfigMgr database name
DECLARE @LOGIN_nonquoted AS VARCHAR(100) = @ADVINSTSERVERNAME
DECLARE @LOGIN AS VARCHAR(100) = QUOTENAME(@LOGIN_nonquoted)
DECLARE @CMDBNAME_nonquoted AS VARCHAR(100) = @CMDBNAME


EXEC ('CREATE LOGIN ' + @LOGIN + ' FROM WINDOWS');
EXEC ('USE' +' '+@CMDBNAME+';' + 'CREATE USER ' + @LOGIN + ' FOR LOGIN ' + @LOGIN);
EXEC ('USE' +' '+@CMDBNAME+';' + 'ALTER ROLE db_datareader ADD MEMBER' + @LOGIN)
```
