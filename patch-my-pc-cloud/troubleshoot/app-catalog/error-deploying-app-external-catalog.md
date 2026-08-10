# Why do I get an error when deploying an app from the External catalog in Patch My PC Cloud?

_Applies to: Patch My PC Cloud_

### SYMPTOMS

I am trying to deploy an app from the **External** catalog in Patch My PC (PMPC) Cloud.

But when I click on the **Deploy** button I get an error.

### CAUSE

This could be for a number of reasons as detailed below.

### RESOLUTION

There are various reasons that deploying an app from the **External** catalog can fail:

<table><thead><tr><th valign="top">Error Notification</th><th valign="top">Generated when the...</th></tr></thead><tbody><tr><td valign="top">External installer file could not be found.</td><td valign="top">metadata for the installer is missing in the  WinGet database.</td></tr><tr><td valign="top">App version from external source could not be found.</td><td valign="top">metadata for the version of the application is missing from the WinGet database.</td></tr><tr><td valign="top">Installer version from external source could not be found.</td><td valign="top">metadata for the version of the installer is missing from the WinGet database.</td></tr><tr><td valign="top">External installer file could not be verified and may be corrupted.</td><td valign="top">hash verification for the installer file fails.</td></tr><tr><td valign="top">External installer file could not be downloaded.</td><td valign="top">installer cannot be downloaded or uploaded to blob storage (general error).</td></tr></tbody></table>