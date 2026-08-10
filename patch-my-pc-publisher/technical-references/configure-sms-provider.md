# Configure the SMS Provider Connection in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

> \*\*IMPORTANT\*\*
>
> This article has not been updated for Version 3.x. Once it has, this banner will be removed.

The **SMS Provider** is the interface that enables all interactions with Microsoft ConfigMgr, including actions performed in the ConfigMgr console and through supported APIs. The Patch My PC (PMPC) Publisher also relies on the SMS Provider to perform operations such as triggering SUP synchronizations, creating and modifying applications, and distributing content.

Configuring the SMS Provider connection is therefore a foundational step for enabling the Publisher to interact with ConfigMgr.

![SMS Provider Connection](/_images/image-(3956).png)

## Connection Settings

The **SMS Provider Server Name** field specifies which server hosts the SMS Provider role that the Publisher will connect to.

You can enter either:

* The ConfigMgr site server (most common), or
* A site system that has the SMS Provider role installed.

Both options are valid, as long as the specified server is hosting the SMS Provider.

You can identify which site systems host the SMS Provider site system role by navigating to **Monitoring | System Status | Component Status** in the ConfigMgr console, then filtering for **SMS\_Provider**.

![Identify an SMS Provider](/_images/image-(516).png)

> \*\*Note\*\*
>
> When connecting to ConfigMgr, either using the Publisher or the ConfigMgr remote console, the SMS Provider you connect to isn’t always the one you specified. The site server ultimately decides which SMS Provider instance is used.
>
> Even if multiple SMS Providers exist, the ConfigMgr site server’s boundaries and role placement determine the connection endpoint. This is the same behavior the ConfigMgr console uses when it discovers and connects to an SMS Provider.
>
> With this in mind, if a firewall is in place between the Publisher and any SMS Provider server in the site, ensure that the Publisher server can communicate with them all using:
>
> \* \*\*TCP 135\*\* (RPC Endpoint Mapper)
>
> \* \*\*Dynamic RPC ports\*\* (default \*\*TCP 49152–65535\*\*)
>
> Restricting firewall access to only a specific site system with the SMS Provider role may result in intermittent or unexpected connection failures.

## Required Software

To connect to the SMS Provider, the [ConfigMgr Remote Console is required](../../patch-my-pc-publisherv2/publisher-requirements/configmgr-requirements/software.md) to be installed on the same device as the Publisher. If the ConfigMgr Remote Console is not installed, the following message is also indicated in the Publisher when attempting to Configure the SMS Provider.

![ConfigMgr Remote Console Missing](/_images/image-(74).png)

The PatchMyPC.log will also indicate when the ConfigMgr Remote Console is not installed:

`An error occurred Error checking ConfigMgr connection: Unable to find the Assembly: AdminUI.WqlQueryEngine, Version=5.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35 [PatchMyPC_Core.Exceptions.ConfigApiException] HResult: -2146233088`

## Required Permissions

Access to the SMS Provider is controlled entirely by ConfigMgr security roles and scopes, not by local server or SQL permissions.

### **When no action is required (most common scenario)**

If the Publisher is installed on the ConfigMgr site server, and that server is also hosting the **SMS Provider role** (the most common deployment), no additional permission configuration is required. The Publisher runs under the local SYSTEM account and connects to the SMS Provider locally, using the same path as the ConfigMgr console would.

### **When additional configuration is required**

If the Publisher is installed remotely, the site server ultimately determines which SMS Provider instance is used. Even if Publisher is installed on a server that has the SMS Provider site system role (for example, a remote SUP), it is not guaranteed that connections will be made to that local provider. For this reason, the computer account where the Publisher is installed (DOMAIN\SERVER$) must be granted the appropriate ConfigMgr permissions, _or_ you must configure alternate credentials using a dedicated service account.

> \*\*Important\*\*
>
> If the Publisher detects that it is installed on the site server, the option to use alternate credentials to connect to the SMS Provider are disabled.

To satisfy these requirements, you can either:

* Option 1: Import a custom ConfigMgr security role with the correct permissions.
* Option 2 (Recommended): [Import the Patch My PC provided security role](configure-sms-provider.md#import-security-roles), which includes the minimum required permissions.

### Option 1: Import a Custom ConfigMgr Security Role

1. Copy the XML content provided below:

```xml
<SMS_Roles>
  <SMS_Role CopiedFromID="SMS0009R" RoleName="Patch My PC Publisher" RoleDescription="Minimum permissions for Patch My PC to create and manage Applications, Distribute Content, and perform Software Update Synchronizations - Last Updated: 04/15/2021">
    <Operations>
      <Operation GrantedOperations="1" ObjectTypeID="6"/>
      <Operation GrantedOperations="1" ObjectTypeID="29"/>
      <Operation GrantedOperations="140311" ObjectTypeID="31"/>
      <Operation GrantedOperations="3" ObjectTypeID="37"/>
      <Operation GrantedOperations="9" ObjectTypeID="42"/>
      <Operation GrantedOperations="9" ObjectTypeID="43"/>
      <Operation GrantedOperations="1027" ObjectTypeID="226"/>
    </Operations>
  </SMS_Role>
</SMS_Roles>
```

2. Save it to a file on a system where the ConfigMgr console is installed. Example file name:\
   `PatchMyPC-Publisher-SecurityRole.xml`
3. Open the **Configuration Manager console.**
4. Navigate to **Administration.**
5. Select **Security.**
6. Click **Security Roles.**
7. Click **Import Security Role.**

![Import Security Role](/_images/image-(517).png)

8. Browse to the file created in step 2.
9. Confirm the security role has been created succesfully.

![Confirm Role Created](/_images/image-(518).png)

For reference, the following permissions are configured on the **Patch My PC Publisher** custom security role:

<table><thead><tr><th width="205.4444580078125" valign="top">ConfigMgr Object</th><th valign="top">Required Permissions</th></tr></thead><tbody><tr><td valign="top">Application</td><td valign="top">Read, Modify, Delete, Create, Move Object, Set Security Scope, Modify Folder</td></tr><tr><td valign="top">Distribution Point</td><td valign="top">Read, Copy to Distribution Point</td></tr><tr><td valign="top">Distribution Point Group</td><td valign="top">Read, Copy to Distribution Point Group</td></tr><tr><td valign="top">Folder Class</td><td valign="top">Read, Modify, Create</td></tr><tr><td valign="top">Security Scopes</td><td valign="top">Read</td></tr><tr><td valign="top">Site</td><td valign="top">Read</td></tr><tr><td valign="top">Software Updates</td><td valign="top">Read, Modify</td></tr></tbody></table>

Once the **Patch My PC Publisher** security role has been imported, it must be assigned to the account that the Publisher will use to connect to the SMS Provider. This will be either the **computer account** where the Publisher is installed or a dedicated service account (when alternate credentials are required).

To assign the account to the security role:

1. Open the **ConfigMgr console**.
2. Navigate to **Administration > Security > Administrative Users**.
3. If the account to be used by the Publisher already exists, select it and choose **Properties**.\
   If the account does not exist, select **Add User or Group**.
4. Specify the account used by Publisher:
   * The **computer account** of the Publisher server (for example, `DOMAIN\PUBLISHER-SERVER$`) when Publisher runs under the local SYSTEM account, **or**
   * The **domain service account** configured in Publisher when using alternate credentials.
5. Assign the **Patch My PC Publisher** security role.
6. Assign the required **security scopes**, ensuring the account has access to **All instances of the objects that are related to the assigned security roles.**

![Assigned Security Scopes](/_images/image-(519).png)

7. Complete the wizard and apply the changes.
8. Restart the **Patch My PC Publisher** service to ensure the updated permissions are applied.

### Option 2: Import Security Roles

Patch My PC provides a ConfigMgr security role in **XML format** that has the minimum required permissions for the Publisher to create and manage applications, distribute content, and perform software update synchronizations.

This role can be imported directly into ConfigMgr if the user logged in with the Publisher application open already has the necessary permissions to create security roles in ConfigMgr.

> When importing the Patch My PC security role from the Publisher, the user currently logged in and running Publisher must have \*\*Full Administrator\*\* permissions in ConfigMgr.
>
> Once the role has been imported, Full Administrator permissions are no longer required. The Publisher connects to the SMS Provider using the assigned role and security scopes only.

1. In the **SMS Provider Connection** form, click **Import Security Role.**

![Import Security Role](/_images/image-(3957).png)

2. If the role already exists, you will be prompted to overwrite it.

![Overwrite Security Role](/_images/image-(3958).png)

3. The role is imported sucessfully.

![Security Role Imported](/_images/image-(3959).png)

#### Role Import Error

When importing the Publisher security role, the import may fail with the following message:

`An error occurred while importing the security role.`

This error occurs when the user running the Publisher does not have sufficient permissions in ConfigMgr to create or import security roles.

![Role Import Error](/_images/image-(4366).png)

The following error may be recorded in the _%ProgramFiles%\Patch My PC\Patch My PC Publishing Service\Logs\\_&#x50;atchMyPC-SmsProviderConfigMgrRepository.log:

```
An exception occurred while executing a WMI method. [Class: SMS_Role] [Method: ImportRole]. Exception: Generic failure .
SmsProviderConfigMgrRepository

An exception occurred while importing role Generic failure
Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine.WqlQueryException [-1]. Exception: Generic failure .
SmsProviderConfigMgrRepository
```

To import the Publisher security role from the Publisher, the user currently logged in and running the Publisher must have the **Full Administrator** role in ConfigMgr.

After the role is imported, Full Administrator permissions are no longer required for normal Publisher operation. The Publisher can then connect to the SMS Provider using the assigned role, security scopes, and collections.

## Test Connection

To test that the Publisher has the correct permissions to the SMS Provider, click **Test Connection.**

![Test SMS Provider Connection](/_images/image-(3960).png)

Connection activity for the SMS Provider from the Publisher can be found in the _%ProgramFiles%\Patch My PC\Patch My PC Publishing Service\Logs\PatchMyPC-SmsProviderConfigMgrRepository.log_

![PatchMyPC-SmsProviderConfigMgrRepository.log](/_images/image-(524).png)