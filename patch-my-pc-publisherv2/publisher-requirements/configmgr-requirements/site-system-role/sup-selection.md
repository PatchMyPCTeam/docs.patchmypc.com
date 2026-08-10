# SUP Selection

_Applies to: Patch My PC Publisher V2.x_

## Overview

The Publisher should be installed on the top-level Software Update Point (SUP) in your ConfigMgr environment. The top-level SUP is the WSUS instance that typically, but not exclusively, synchronizes directly with the Microsoft Update catalog and is responsible for authoring update metadata before it is replicated downstream.

Publishing updates at the top-level SUP ensures that third-party update metadata flows correctly to all downstream SUPs/WSUS servers. This facilitates client devices, regardless of which SUP/WSUS instance they scan against, to successfully scan for, install, and report compliance on third-party updates.

> \*\*Note\*\*
>
> In more complex or highly customized environments, it is possible to install the Publisher on a non–top-level SUP. However, this requires very careful WSUS and SUP configuration to ensure update metadata is correctly authored and replicated downstream as expected. These scenarios are uncommon and should only be implemented with a clear understanding of ConfigMgr/WSUS synchronization behavior, as misconfiguration can prevent clients from detecting or reporting on third-party updates.

> \*\*Important\*\*
>
> Installing the Publisher on a downstream SUP will prevent third-party update metadata from flowing correctly, which can result in clients connected to a upstream SUP from being unable to scan for or report compliance on published third-party updates.

## How to identify the top-level SUP

* The top-level SUP is typically, but not exclusively, the SUP that synchronizes directly with Microsoft Update.
* In most environments, this is the first SUP installed when more than a single site system with the SUP role is configured..
* In a CAS hierarchy, the Central Administration Site (CAS) SUP is typically the top-level SUP.

Consider the following scenarios to help you select the correct site-system to install the Publisher.

### Scenario 1 - Single SUP, Microsoft Update is the Synchronization Source

In the example below, there is a single site system that holds the SUP role. cm.lab.local is considered the top-level SUP because its synchronization source is Microsoft Update.

![Single SUP top-level SUP](../../../../.gitbook/assets/image-\(375\).png)

### Scenario 2 - Multiple SUP's, Microsoft Update is the Synchronization Source

In the example below, there are multiple site systems that holds the SUP role. bb-cm1 is considered the top-level SUP because its synchronization source is Microsoft Update.

![Multiple SUPs top-level SUP](../../../../.gitbook/assets/image-\(376\).png)

### Scenario 3 - Multiple SUP's, Microsoft Update is _not_ the Synchronization Source

In the example below, the upstream synchronization source is not Microsoft Update, but sus.lab2.local. This is common in environments where the WSUS server that synchronizes with the Microsoft Update catalog is located in a DMZ. Even in this configuration, sus01.lab2.local is still considered the top-level SUP, as it is the authoritative source for update metadata within ConfigMgr.

![Multiple SUPs top-level SUP, non-Microsoft source](../../../../.gitbook/assets/image-\(377\).png)
