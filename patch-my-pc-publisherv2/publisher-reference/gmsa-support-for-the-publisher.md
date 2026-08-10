# gMSA Support for the Publisher

_Applies to: Patch My PC Publisher V2.x_

## Overview

The Publisher can run under a group Managed Service Account, also known as a gMSA.

A gMSA can be useful when the Publisher service must access network resources that do not work well with the local SYSTEM or computer account identity.

The most common example is an authenticated proxy used for downloads. By default, the Publisher service runs as local SYSTEM. When running as local SYSTEM, outbound network access uses the computer account identity. Some proxy solutions do not support or do not allow authentication from computer identities such as `DOMAIN\SERVER$`, but do allow authentication from domain service accounts.

In this scenario, running the Publisher service as a gMSA allows the Publisher to authenticate to the proxy using a domain managed service account identity while still avoiding manual password management.

### Important Consideration

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>A gMSA should not be used for the Publisher service when the Publisher is installed on the ConfigMgr site server.</p>
</blockquote>

This limitation is related to how the SMS Provider connection works.

When the Publisher is installed on the site server, the SMS Provider connection is local. Local WMI connections do not accept alternate credentials. The Publisher service connects in its own service context. When the Publisher runs as local SYSTEM on the site server, this normally works because the site server computer account already has the required inherent access.

When the Publisher runs as a gMSA, that gMSA would need to be granted ConfigMgr administrative permissions. However, ConfigMgr administrative users and security roles can not be configured for a gMSA in this scenario.

When the Publisher is installed remotely, this limitation does not apply in the same way. The Publisher can run as the gMSA, while a separate standard administrative account is configured for the SMS Provider connection.

## Recommended Configuration

When using a gMSA with the Publisher, use the following design.

* Install the Publisher on a remote site system, this would typically be the top-level SUP.
* Run the Publisher service as the gMSA.
* Add the gMSA to the local Administrators group on the Publisher server.

For ConfigMgr environments, also complete the following requirements.

* Grant the gMSA access to the Publisher content source for ConfigMgr apps.
* Grant the gMSA read access to SUSDB.
* Grant the gMSA the required ConfigMgr database read permissions for the ConfigMgr database scan wizard.
* Configure a separate user/service account for the SMS Provider connection.

## Required Permissions

### Content source

The gMSA requires read and write access to the Publishers configured ConfigMgr content source folder. This access must be granted at both the share permission level and the NTFS permission level. This allows the Publisher service to create, update, and manage content used for applications and updates.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>For more information, see [ConfigMgr Connection and Source Options](../).</p>
</blockquote>

### WSUS and Certificate Access

The gMSA must be a local administrator on the Publisher and WSUS server. This is required so the Publisher service can access the local certificate store and the WSUS signing certificate private key.

### Publisher registry access

The gMSA requires access to the Publisher registry configuration under:

```
HKLM\SOFTWARE\Patch My PC Publishing Service
```

This access is covered when the gMSA is a member of the local Administrators group on the Publisher server.

### SMS Provider

When the Publisher is installed remotely, configure a separate account for the SMS Provider connection.

* The gMSA runs the Publisher service.
* The separate administrative account is used only for the SMS Provider connection.

This account must be granted the required ConfigMgr security role, security scopes, and collection access for the actions the Publisher needs to perform.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>For more information, see [ConfigMgr Permissions](../publisher-requirements/configmgr-requirements/permissions.md).</p>
</blockquote>

### SUSDB

The gMSA must be mapped as a login in SQL Server and granted access to the SUSDB database.

Grant the gMSA the following database role on SUSDB:

```
db_datareader
```

This permission is required for the Publisher to read the third-party update and category totals in the [Modify Updates Wizard](../administration/updates/options/modify-published-updates.md).

### ConfigMgr Database Scan Wizard

If the ConfigMgr database scan wizard is used, grant the gMSA the required SELECT permissions on the ConfigMgr inventory views.

These permissions allow the Publisher to read the ConfigMgr database views needed to identify supported products and related inventory data.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>For more information, see: [Scan ConfigMgr Database for Supported Products](../administration/configmgr-apps/form-controls/scan-configmgr-database-for-supported-products.md).</p>
</blockquote>