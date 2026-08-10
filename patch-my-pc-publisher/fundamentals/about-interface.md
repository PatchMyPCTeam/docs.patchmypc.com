# About the Patch My PC Publisher Interface

_Applies to: Patch My PC Publisher V3.x_

The Patch My PC (PMPC) Publisher interface consists of the following tabs down the left-hand side:

<table data-search="false"><thead><tr><th width="148.99993896484375" valign="top">Tab</th><th valign="top">Used to...</th></tr></thead><tbody><tr><td valign="top">General</td><td valign="top">Provide a high-level view of Publisher’s licensing status, usage information, and other core administrative settings.</td></tr><tr><td valign="top">WSUS Updates</td><td valign="top">Configure and customize third-party updates for Microsoft Windows Server Update Services (WSUS).</td></tr><tr><td valign="top">ConfigMgr Apps</td><td valign="top">Configure and customize third-party updates for Microsoft Configuration Manager (ConfigMgr).</td></tr><tr><td valign="top">Intune Apps</td><td valign="top">Configure and customize third-party apps for Microsoft Intune.</td></tr><tr><td valign="top">Intune Updates</td><td valign="top">Configure and customize third-party updates for Microsoft Intune.</td></tr><tr><td valign="top">Sync Schedule</td><td valign="top">Control when Publisher runs an automated publishing sync.</td></tr><tr><td valign="top">Alerts</td><td valign="top">Provide visibility into publishing activity and operational events.</td></tr><tr><td valign="top">Advanced</td><td valign="top">Provide configuration options used to customize Publisher behavior beyond standard publishing settings.</td></tr><tr><td valign="top">Cloud</td><td valign="top">Connect Publisher to PMPC Cloud and manage the connection.</td></tr><tr><td valign="top">About</td><td valign="top">Show version and support information</td></tr></tbody></table>

Clicking a tab displays more relevant information in the right-hand _details_ window, and if a tab also contains child tabs, the parent tab automatically expands to reveal any child tabs.

Regardless of the tab selected, at the bottom of Publisher you will find the following items:

<table data-header-hidden><thead><tr><th valign="top"></th><th valign="top"></th><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top"><a href="about-interface.md#theme-control">Theme Control</a></td><td valign="top"><a href="about-interface.md#show-granted-permissions-shield">Show Granted Permissions Shield</a></td><td valign="top"><a href="about-interface.md#version-number">Version Number</a></td><td valign="top"><a href="about-interface.md#action-buttons">Action Buttons</a></td></tr></tbody></table>

## Theme Control

The _Theme Control_ lets you decide which theme to use to display the Publisher.

> \*\*Note\*\*
>
> See \[Switch Themes]\(switch-themes.md) for more information on how to switch themes and examples.

## Show Granted Permissions Shield

Clicking the _Show Granted Permissions_ shield (!\[Show Granted Permissions Shield]\(/\_images/image-(4585 "Show Granted Permissions Shield").png>)) at the bottom of the Publisher UI opens the read-only **Permissions** screen showing a list of every Publisher permission and whether your account currently holds it, resolved against the server you are connected to.

This works the same regardless of the Settings console being accessed locally or remotely, so you can confirm your effective access at any time.

> \*\*Note\*\*
>
> See the \[Access and Permissions Reference]\(../remote-ui/technical-references/access-permissions-reference.md) for more information about these permissions.

![](../../.gitbook/assets/image-\(4586\).png)

## Version Number

Underneath the Theme Control is the _Version_ number field showing which version of Publisher you are currently running.

For example **3.x.x.x**

## Action Buttons

The _Action Buttons_ are used as follows:

<table><thead><tr><th width="161.22222900390625" valign="top">Button</th><th valign="top">Used to...</th></tr></thead><tbody><tr><td valign="top">Logs</td><td valign="top"><a href="../manage/manage-logs.md">Manage log files in Publisher</a></td></tr><tr><td valign="top">Save and Close</td><td valign="top">Save any changes and quit Publisher.</td></tr><tr><td valign="top">Cancel</td><td valign="top">Cancel any changes and quit Publisher. If you have unsaved changes, you will be prompted to save them, if you choose to.</td></tr><tr><td valign="top">Apply</td><td valign="top">Apply (save) any changes without quitting Publisher (only available if you have made a change and not applied/saved it).</td></tr></tbody></table>
