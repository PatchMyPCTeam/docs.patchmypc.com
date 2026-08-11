# Update Republishing Options section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

> \*\*Important\*\*
>
> This article has not been updated for Version 3.x. Once it has, this banner will be removed.

The **Update Republishing Options** section in Patch My PC (PMPC) Publisher controls how republished third party updates are named. Republishing is required when an existing update needs to be replaced due to changes in content or metadata.

![Update Republishing Options](<../../../../.gitbook/assets/image-(90) (1).png>)

Common scenarios that require republishing include updates where customizations were added or modified, detection logic was corrected, or the update needs to be signed with a new code signing certificate. In general, any change that affects the update CAB file or its digital signature requires the update to be republished.

> \*\*Tip\*\*
>
> For more information on Republishing, see \[Customizations]\(../../../../patch-my-pc-publisherv2/customizations-right-click-options/).

By default, when an update is republished, the Publisher appends a timestamp to the update name indicating when the republish occurred. This makes it clear in the ConfigMgr console that the update is a republished revision and shows the exact date and time of the republish. The example shown in the image above demonstrates how a republished Google Chrome update would appear with this appended information.

If the option **Do not append republished updates with a republished datetime** is selected, the republished update keeps the original update name and no timestamp is added. The update is still republished and supersedes the previous revision (if that option was selected during republishing), but there is no visible indication in the name that a republish occurred.

> \*\*Note\*\*
>
> Republishing only applies to an existing update version. When an update is republished, the Publisher republishes the same version and creates a new revision of that update with a new Update ID.
>
> If an administrator attempts to republish an update and the specified version is not found, the Publisher does not republish. Instead, a standard publish occurs for the newer version, and it is treated as a new update rather than a republished revision.
