# "WARNING: Some or all identity references could not be translated" in the Client.log

_Applies to: Patch My PC Client_

## SYMPTOMS

Why do I see warnings like the following every 24 hours in the Patch My PC Client log (**C:\ProgramData\PatchMyPC\Logs\Client.log**):

`WARNING: Some or all identity references could not be translated.`\
`Exception: System.Security.Principal.IdentityNotMappedException: Some or all identity references could not be translated.`\
`at System.Security.Principal.SecurityIdentifier.Translate(IdentityReferenceCollection sourceSids, Type targetType, Boolean forceSuccess)`\
`at System.Security.Principal.SecurityIdentifier.Translate(Type targetType)`\
`at PatchMyPC.Agent.Modules.DeviceInventory.Providers.Windows.ComputedInventory.UserProfileProvider.GetAccountName(String sid) in D:\a\1\s\Modules\PatchMyPC.Agent.Modules.DeviceInventory\Providers\Windows\ComputedInventory\UserProfileProvider.cs:line 66 PatchMyPC.Agent.Modules.DeviceInventory, Version=1.0.50.19, Culture=neutral, PublicKeyToken=null 10/17/2025 8:28:42 AM 16 (0x0010)`\
`llationToken cancellationToken) in D:\a\1\s\Modules\PatchMyPC.Agent.Modules.StateManagement\Communicat`i`ons\WebApiStateChannel.cs:line 54`

## CAUSE

This issue can be caused by numerous factors, such as:

* Network problems
* Switching Intune tenants
* If the referenced account has been deleted from Active Directory/Entrad ID

It can also occur when we attempt to look up an account's "friendly" name (typically during inventory actions where we record user info, such as user apps, local groups, etc.).&#x20;

If the account is not a local account and the device is using Active Directory, this involves a lookup to Active Directory to resolve the account SID to an account name. When that process fails due to a lack of permissions or network connectivity, then this error is output.

## RESOLUTION

This is a very uncommon scenario because most of the clients we service are not Active Directory joined because they are Intune devices.

Due to the various potential causes of this error, there is no one resolution other than checking for causes such as those detailed in the [Cause ](warning-some-all-identity-references-translated.md#cause)section.
