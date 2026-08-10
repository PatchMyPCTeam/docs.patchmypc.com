# ConfigMgr Software Update Point Selection for Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

Patch My PC (PMPC) Publisher should be installed on the top-level Software Update Point (SUP) in your Microsoft ConfigMgr environment.

The top-level SUP is the WSUS instance that typically (but not exclusively) synchronizes directly with the Microsoft Update catalog and is responsible for authoring update metadata before it is replicated downstream.

Publishing updates at the top-level SUP ensures that third-party update metadata flows correctly to all downstream SUPs/WSUS servers, enabling client devices, regardless of which SUP/WSUS instance they scan against, to successfully scan for, install, and report compliance on third-party updates.

> \*\*Note\*\*
>
> In more complex or highly customized environments, it is possible to install Publisher on a SUP that is not the top-level one. However, this requires very careful WSUS and SUP configuration to ensure update metadata is correctly authored and replicated downstream as expected.
>
> These scenarios are uncommon and should only be implemented with a clear understanding of ConfigMgr/WSUS synchronization behavior, as misconfiguration can prevent clients from detecting or reporting on third-party updates.

> \*\*Important\*\*
>
> Installing Publisher on a downstream SUP will prevent third-party update metadata from flowing correctly, which can result in clients connected to an upstream SUP being unable to scan for or report compliance on published third-party updates.

## Identifying the top-level SUP

The top-level SUP is typically (but not exclusively) the SUP that synchronizes directly with Microsoft Update.

In most environments, this is the first SUP installed when more than a single Site System with the SUP role is configured.

In a Central Administration Site (CAS) hierarchy, the CAS SUP is typically the top-level SUP.

Consider the following scenarios to help you select the correct Site System on which to install Publisher:

* [Scenario 1: Single SUP, Microsoft Update is the Synchronization Source](selection.md#scenario-1-single-sup-microsoft-update-is-the-synchronization-source)
* [Scenario 2: Multiple SUP's, Microsoft Update is the Synchronization Source](selection.md#scenario-2-multiple-sups-microsoft-update-is-the-synchronization-source)
* [Scenario 3: Multiple SUP's, Microsoft Update is _not_ the Synchronization Source](selection.md#scenario-3-multiple-sups-microsoft-update-is-not-the-synchronization-source)

### Scenario 1: Single SUP, Microsoft Update is the Synchronization Source

In this example, a single Site System **cm.lab.local** holds the SUP role and is considered the top-level SUP as its synchronization source is Microsoft Update.

![Single SUP top-level SUP](/_images/image-(375).png)

### Scenario 2: Multiple SUP's, Microsoft Update is the Synchronization Source

In this example, multiple Site Systems hold the SUP role, but **bb-cm1** is considered the top-level SUP as its synchronization source is Microsoft Update.

![Multiple SUPs top-level SUP](/_images/image-(376).png)

### Scenario 3: Multiple SUP's, Microsoft Update is _not_ the Synchronization Source

In this example, the upstream synchronization source is not Microsoft Update, but **sus.lab2.local**. This is common in environments where the WSUS server that synchronizes with the Microsoft Update catalog is located in a DMZ.

Even in this configuration, **sus01.lab2.local** is still considered the top-level SUP as it is the authoritative source for update metadata within ConfigMgr.

![Multiple SUPs top-level SUP, non-Microsoft source](/_images/image-(377).png)