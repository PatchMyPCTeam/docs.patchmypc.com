# Customize Content Download and Log Save Location

_Applies to: Patch My PC Publisher V2.x_

## Overview

By default, the Publisher downloads content and writes logs to locations derived from the system and installation context.&#x20;

<figure><img src="../../../.gitbook/assets/image (3946).png" alt="Customize Content Download and Log Save Location" width="557"><figcaption></figcaption></figure>

Because the Publisher runs under the SYSTEM account, default paths may not always align with organizational requirements for disk usage, monitoring, or security tooling.

The Customize Content Download and Log Save Location options allow you to override these defaults by specifying custom folders for:

* Temporary content downloads used during publishing
* The Publisher log folder

{% hint style="info" %}
**Note**

These settings apply only to the Publisher and do not affect client-side installations.
{% endhint %}

## Set a Custom Folder for Temporary Downloads

By default, content files are downloaded temporarily to %TEMP% during publishing operations. Since the Publisher runs under the SYSTEM context, this typically resolves to:

```
C:\Windows\Temp
```

This screenshot shows the Publisher using `C:\Windows\Temp` as a temporary scratch location while preparing packages during a publishing sync.

<figure><img src="../../../.gitbook/assets/image (3947).png" alt="Temporary Downloads Folder" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

Temporary content downloaded to this location is automatically removed once publishing operations complete.
{% endhint %}

## Set a Custom Folder for PatchMyPC.log

The Publisher writes service and operational logs to disk to support troubleshooting, auditing, and support diagnostics.

By default, Publisher logs are stored within the installation directory of the Patch My PC Publishing Service:

*   **Newer Publisher versions:**\
    Logs, including PatchMyPC.log, are stored in a dedicated **`Logs`** subfolder under the Publisher install directory.\
    Example:

    ```
    C:\Program Files\Patch My PC\Patch My PC Publishing Service\Logs
    ```
* **Older Publisher versions:**\
  The primary **PatchMyPC.log** file may still be located directly in the root of the Publishing Service installation directory rather than the `Logs` subfolder.

Because the Publisher runs under the SYSTEM account, the computer account of the server hosting the Publishing Service must have write permissions to the configured log folder. If permissions are insufficient, logging may fail.

