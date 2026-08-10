# gMSA Support in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

## Overview

Patch My PC (PMPC) Publisher can run under a group Managed Service Account (gMSA), which can be useful when the Publisher service must access network resources that do not work well with the local SYSTEM or computer account identity.

The most common example is an authenticated proxy used for downloads. By default, the Publisher service runs as local SYSTEM. When running as local SYSTEM, outbound network access uses the computer account identity. Some proxy solutions do not support or do not allow authentication from computer identities such as `DOMAIN\SERVER$`, but do allow authentication from domain service accounts.

In this scenario, running the Publisher service as a gMSA allows Publisher to authenticate to the proxy using a domain-managed service account identity whilst still avoiding manual password management.

## Important Consideration

A gMSA should not be used for the Publisher service when Publisher is installed on the ConfigMgr Site Server.

This limitation is related to how the SMS Provider connection works.

When Publisher is installed on the Site Server, the SMS Provider connection is local. Local WMI connections do not accept alternate credentials. The Publisher service connects in its own service context.

When Publisher runs as the local SYSTEM account on the Site Server, this normally works because the Site Server computer account already has the required inherent access.

When Publisher runs as a gMSA, that gMSA would need to be granted ConfigMgr administrative permissions. However, ConfigMgr administrative users and security roles cannot be configured for a gMSA in this scenario.

When Publisher is installed remotely, this limitation does not apply in the same way. Publisher can run as the gMSA, while a separate standard administrative account is configured for the SMS Provider connection.

## Recommended Configuration

When using a gMSA with Publisher, use the following configuration:

* Install Publisher on a remote Site System, typically the top-level SUP.
* Run the Publisher service as the gMSA.
* Add the gMSA to the local Administrators group on the Publisher server.

For ConfigMgr environments, also complete the following:

* Grant the gMSA access to the Publisher content source for ConfigMgr apps.
* Grant the gMSA read access to SUSDB.
* Grant the gMSA the required ConfigMgr database read permissions for the ConfigMgr database scan wizard.
* Configure a separate user/service account for the SMS Provider connection.

## Required Permissions

* [Content source](gsma-support.md#content-source)
* [WSUS and Certificate Access](gsma-support.md#wsus-and-certificate-access)
* [Publisher registry access](gsma-support.md#publisher-registry-access)
* [SMS Provider](gsma-support.md#sms-provider)
* [SUSDB](gsma-support.md#susdb)
* [ConfigMgr Database Scan Wizard](gsma-support.md#configmgr-database-scan-wizard)

### Content source

The gMSA requires read and write access to the ConfigMgr content source folder configured for Publisher.

This access must be granted at both the share and NTFS permission levels.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>See [ConfigMgr Connection and Source Options](../manage/configmgr-apps-tab/base-install-options/connection-source-options.md) for more information.</p>
</blockquote>

### WSUS and Certificate Access

The gMSA must be a local administrator on the Publisher and WSUS server. This is required so the Publisher service can access the local certificate store and the WSUS signing certificate private key.

### Publisher registry access

The gMSA requires access to the Publisher's registry configuration at:

```
HKLM\SOFTWARE\Patch My PC Publishing Service
```

This access is covered when the gMSA is a member of the local Administrators group on the Publisher server.

### SMS Provider

When Publisher is installed remotely, configure a separate account for the SMS Provider connection.

* The gMSA runs the Publisher service.
* The separate administrative account is used only for the SMS Provider connection.

This account must be granted the required ConfigMgr security role, security scopes, and collection access for the actions Publisher needs to perform.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>See [ConfigMgr Permission Requirements](../requirements/configmgr-requirements/permissions.md) for more information.</p>
</blockquote>

### SUSDB

The gMSA must be mapped as a login in SQL Server and granted access to the SUSDB database.

Grant the gMSA the following database role on SUSDB:

```
db_datareader
```

This permission is required for Publisher to read the third-party update and category totals in the [Modify Published Updates](../manage/wsus-updates-tab/wsus-options/modify-published-updates.md) wizard.

### ConfigMgr Database Scan Wizard

If the ConfigMgr database scan wizard is used, grant the gMSA the required SELECT permissions on the ConfigMgr inventory views.

These permissions allow Publisher to read the ConfigMgr database views needed to identify supported products and related inventory data.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>See [Scan ConfigMgr](../manage/configmgr-apps-tab/scan-configmgr.md) for more information.</p>
</blockquote>