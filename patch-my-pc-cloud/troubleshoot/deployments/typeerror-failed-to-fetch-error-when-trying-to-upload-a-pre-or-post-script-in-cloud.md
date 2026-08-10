# "TypeError: Failed to fetch" error when trying to upload a Pre or Post Script in Cloud

_Applies to: Patch My PC Cloud_

### SYMPTOMS

I am trying to upload a Pre (or Post) script, but I get the following error:

**Error - TypeError: Failed to fetch**

![Error - TypeError: Failed to fetch](/_images/image-(934).png)

### CAUSE

This error can happen if your pre/post script contains either of the following variables:

`"${env:ProgramFiles(x86)}"`

`"${env:ProgramFiles}"`

This issue is not caused by the Patch My PC (PMPC) Cloud portal but by Cloudflare, who are incorrectly identifying them as a false-positive and blocking the upload as they think the script is a Log4j exploit.

### RESOLUTION

As Cloudflare is causing this issue, we cannot implement a fix. We are actively working with them to try to resolve this false positive.

In the meantime, to work around this issue, use the following replacements in your affected scripts:

<table><thead><tr><th valign="top">Replace all instances of…</th><th valign="top">With...</th></tr></thead><tbody><tr><td valign="top"><code>"${env:ProgramFiles(x86)}"</code></td><td valign="top"><code>"$($env:SystemDrive)\Program Files (x86)"</code></td></tr><tr><td valign="top"><code>"${env:ProgramFiles}"</code></td><td valign="top"><code>"$($env:SystemDrive)\Program Files"</code></td></tr></tbody></table>