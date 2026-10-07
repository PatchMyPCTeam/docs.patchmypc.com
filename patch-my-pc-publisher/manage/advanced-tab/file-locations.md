---
hidden: true
---

# File Locations category of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

By default, Patch My PC (PMPC) Publisher downloads content and writes logs to locations derived from the system and installation context.

As Publisher runs under the **SYSTEM** account, default paths may not always align with organizational requirements for disk usage, monitoring, or security tooling.

<figure><img src="../../../.gitbook/assets/image (1372).png" alt="&#x27;File Locations&#x27; category" width="563"><figcaption></figcaption></figure>

The **File Locations** category on the **Advanced** tab allows you to customize:

* [Content Download Location](file-locations.md#customize-content-download-location)
* [Service Log Location](file-locations.md#customize-service-log-location)
* [Log File Size and Retention](file-locations.md#log-file-size-and-retention-1)

{% hint style="info" %}
**Note**

These settings apply only to Publisher and do not affect client-side installations.
{% endhint %}

## Customize Content Download Location

The **CUSTOMIZE CONTENT DOWNLOAD LOCATION** section allows you to configure settings related to content Publisher downloads.

<figure><img src="../../../.gitbook/assets/image (1374).png" alt="&#x27;CUSTOMIZE CONTENT DOWNLOAD LOCATION&#x27; section" width="498"><figcaption></figcaption></figure>

### Downloads folder

By default, content files are downloaded temporarily to `%Temp%` during publishing operations. Since Publisher runs under the **SYSTEM** context, this typically resolves to:

```
C:\Windows\Temp
```

This following screenshot shows Publisher using `C:\Windows\Temp` as a temporary scratch location while preparing packages during a publishing sync.

<figure><img src="../../../.gitbook/assets/image (3947).png" alt="Temporary Downloads Folder" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

Temporary content downloaded to this location is automatically removed once publishing operations complete.
{% endhint %}

To configure a different location, enter/browse to the required location, select it, then click **Apply** to save your changes.

## Customize Service Log Location

The **CUSTOMIZE SERVICE LOG LOCATION** section allows you to configure the **Service log folder** setting.

<figure><img src="../../../.gitbook/assets/image (1376).png" alt="&#x27;CUSTOMIZE SERVICE LOG LOCATION&#x27; section" width="499"><figcaption></figcaption></figure>

Publisher writes service and operational logs to disk to support troubleshooting, auditing, and support diagnostics.

By default, Publisher logs are stored within the installation folder of the Patch My PC Publishing Service:

*   **Newer Publisher versions:**\
    Logs, including **PatchMyPC.log**, are stored in a dedicated **`Logs`** subfolder under the Publisher installation folder. For example:<br>

    ```
    C:\Program Files\Patch My PC\Patch My PC Publishing Service\Logs
    ```
* **Older Publisher versions:**\
  The primary **PatchMyPC.log** file may still be located directly in the root of the Publishing Service installation directory rather than the `Logs` subfolder.

As Publisher runs under the **SYSTEM** account, the computer account of the server hosting the Publishing Service must have write permissions to the configured log folder. If permissions are insufficient, logging may fail.

To configure a different location (not recommended, as adopting the default location makes troubleshooting easier), enter/browse to the required location, select it, then click **Apply** to save your changes.

## Log File Size and Retention

The **LOG FILE SIZE AND RETENTION** section allows you to configure the following settings:

* [Logs to retain](file-locations.md#logs-to-retain-1)
* [Max size (MB)](file-locations.md#max-size-mb)

<figure><img src="../../../.gitbook/assets/image (1377).png" alt="&#x27;LOG FILE SIZE AND RETENTION&#x27; section" width="495"><figcaption></figcaption></figure>

### Logs to retain

The **Logs to retain** setting specifies how many log files to keep before overwriting older logs.

{% hint style="info" %}
**Note**

We recommend setting **Logs to retain** to **10**. Publisher log files are relatively small, and retaining additional history is extremely valuable when troubleshooting issues or providing support, as it preserves publishing context that may otherwise be lost.
{% endhint %}

### Max size (MB)

The **Max size (MB)** setting specifies the maximum size of each individual log file before a new log is created.

{% hint style="info" %}
**Note**

We recommend setting **Max size (MB)** to **10**. Publisher log files are relatively small, and retaining additional history is extremely valuable when troubleshooting issues or providing support, as it preserves publishing context that may otherwise be lost.
{% endhint %}
