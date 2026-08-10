# Overview of the Patch My PC Publisher Remote User Interface

_Applies to: Patch My PC Publisher V3.x_

<blockquote class="wp-block-quote">
<p>**PRE-RELEASE DOCUMENTATION**</p>
<p>This documentation is for a pre-release feature still under development and, therefore, incomplete. As a result, both functionality and documentation are subject to change.</p>
<p>Once this feature is released, it will be announced, and this banner will be removed.</p>
</blockquote>

Patch My PC (PMPC) Publisher consists of two parts:

* **Windows "PatchMyPCService" service -** Which performs key tasks such as cataloging third-party updates and publishing them to Microsoft WSUS, Configuration Manager (ConfigMgr), and Intune. This runs on a server, usually under the **SYSTEM** context or a dedicated service account.
* **Settings console -** Also known as the _user interface_, which is where you configure products, schedules, connections, and options.

Traditionally, the Settings console had to be run directly on the server. The _Remote UI_ feature of Publisher removes that requirement, meaning you can now run the Settings console on your own workstation and connect to the **PatchMyPCService** across the network.

## Benefits of using the Remote UI

Using Remote UI offers the following benefits:

* **No more signing in to the server -** Publisher can be managed from your workstation instead of opening a remote desktop session to the server every time.
* **Delegate safely -** Specific administrators can be delegated to manage only the areas of the Publisher they are responsible for (for example, only WSUS, or only Intune), without granting them administrative rights on the server itself.
* **Fits secure environments -** Remote UI only talks to your own Publisher service. It does not need direct Internet access, even to download product or service updates, as these flow through the **PatchMyPCService**.

## How it works

* The **PatchMyPCService** exposes a small, secure management interface on the server.
* Your Settings console connects to that interface using Integrated Windows Authentication, i.e., the same sign in your computer already uses for file shares and other domain resources. You are identified by your Windows account; no password is typed or stored by Publisher.
* Every privileged action still happens on the server, performed by the **PatchMyPCService**. The Settings console simply asks the **PatchMyPCService** to read or change settings on your behalf.
* Your level of access is decided by the groups your user account belongs to on the server (see [Access and Permissions Reference](technical-references/access-permissions-reference.md) for more information).

## Running Publisher Locally versus Remotely

There are two supported scenarios for running Publisher:

<table><thead><tr><th width="288.4444580078125" valign="top">Scenario</th><th valign="top">What happens</th></tr></thead><tbody><tr><td valign="top"><strong>PatchMyPCService</strong> and Settings console on the same server</td><td valign="top">The Settings console talks to the <strong>PatchMyPCService</strong> locally. This path is always available and needs no certificate.</td></tr><tr><td valign="top">Settings console on a different computer (Remote UI)</td><td valign="top">The Settings console connects across the network over HTTPS. This requires remote access to be turned on and a server certificate to be in place (see <a href="technical-references/using-different-computer.md">Using a Different Computer</a> for more information).</td></tr></tbody></table>