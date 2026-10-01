# SQL Configuration section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **SQL CONFIGURATION** section on the **Scan ConfigMgr** tab of Patch My PC (PMPC) Publisher defines how Publisher connects to Microsoft Configuration Manager (ConfigMgr) and where it stores application source content.

<figure><img src="../../../../.gitbook/assets/image (1261).png" alt="&#x27;SQL CONFIGURATION&#x27; section" width="563"><figcaption></figcaption></figure>

## Site Database Server

To configure the scan, Publisher needs the name of the site database server and database name used by ConfigMgr. You can find this information in the ConfigMgr console by navigating to:

**Monitoring | System Status | Site Status**

<figure><img src="../../../../.gitbook/assets/image (1096).png" alt="Monitoring | System Status | Site Status" width="563"><figcaption></figcaption></figure>

Select the **Site database server** site system role. The details shown here provide the correct values to enter into Publisher.

<figure><img src="../../../../.gitbook/assets/image (1262).png" alt="Site Database Server" width="563"><figcaption></figcaption></figure>

By default, no **Limiting Collection** is specified. When you leave this field empty, the scan for supported products runs against **All Systems**.

Optionally, you can limit the scan scope by selecting a specific device collection using the browse button.

{% hint style="info" %}
**Note**

When you select a device collection, only the hardware inventory (HINV) data for devices in that collection is evaluated. This can significantly reduce scan time in large environments or when you want to validate a specific subset of devices rather than scanning the entire estate.
{% endhint %}

## Connect to ConfigMgr SQL Database As

The **Scan ConfigMgr** tab runs direct SQL queries against your ConfigMgr site database to inventory installed software. This scan _does not_ use the SMS Provider, so the account performing the scan must have the appropriate SQL permissions on the ConfigMgr database.

<figure><img src="../../../../.gitbook/assets/image (1263).png" alt="&#x27;Connect to ConfigMgr SQL Database As&#x27; section" width="563"><figcaption></figcaption></figure>

Publisher supports multiple ways to authenticate to SQL, allowing flexibility depending on where Publisher is installed and which account has the required permissions:

* [Service Account](sql-configuration.md#service-account)
* [SQL Authentication](sql-configuration.md#sql-authentication)
* [Run interactive scan as logged in user](sql-configuration.md#run-interactive-scan-as-logged-in-user)

### **Service Account**

The **Service Account** option (the default) uses the account under which the Publisher service is running. By default, the Publisher service runs as **SYSTEM**. This option is recommended:

* When Publisher is installed on the site server.
* Windows authentication is used.
* No credentials need to be entered.

{% hint style="info" %}
**Note**

When Publisher is installed on the ConfigMgr site server, the **SYSTEM** account typically already has the required read permissions on the ConfigMgr database views. In most environments, you don't need additional SQL configuration.
{% endhint %}

### **SQL Authentication**

The **SQL Authentication** option allows you to specify a SQL login and password. This option is recommended:

* You want to use SQL authentication instead of Windows authentication.
* If you want to use a SQL login (which needs read access to the required ConfigMgr database views).

This option is less common and generally not recommended unless Windows authentication cannot be used.

### **Run interactive scan as logged in user**

When the **Run interactive scan as logged in user** option is enabled, the scan runs using the currently logged-in user’s Windows credentials instead of Publisher's service account. This option is recommended:

* For troubleshooting permission issues.
* Can be helpful when testing access before granting permissions to the service account.

This option requires the logged-in user to have the necessary SQL SELECT permissions on the required ConfigMgr views.

{% hint style="danger" %}
**Important**

This option does not change how scheduled scans run; it only applies to the interactive scan being executed.
{% endhint %}

{% hint style="info" %}
**Note**

See [Microsoft SQL Permission Requirements](../../../requirements/configmgr-requirements/permissions.md#microsoft-sql-permission-requirements) for more information.
{% endhint %}
