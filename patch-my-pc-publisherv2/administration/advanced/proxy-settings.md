# Proxy Settings

_Applies to: Patch My PC Publisher V2.x_

## Overview

The **Proxy Settings** section allows the Publisher to use a proxy server for outbound network connectivity.

![Proxy Settings](../../../.gitbook/assets/image-\(3931\).png)

When configured, most Publisher operations use this proxy to download content and communicate with external services. For exceptions related to WSUS and timestamping behavior, see [WSUS and Timestamping Considerations](proxy-settings.md#wsus-and-timestamping-considerations).

## Proxy Mode

* **Don’t use proxy**\
  The Publisher connects directly to the internet without using a proxy.
* **Use proxy settings below**\
  The Publisher uses the proxy configuration defined in this section for supported outbound connections.

## Proxy Configuration Fields

* **URL**\
  Specifies the proxy server address. This can be a hostname or IP address.
* **Port**\
  Specifies the port used by the proxy server. The default value is 8080.

## **Use Authentication**

The Publisher runs under the SYSTEM account by default. When proxy authentication is not enabled, outbound traffic uses the computer account identity.\
\
In environments where the proxy does not support computer account authentication, or where explicit identity based auditing is required, proxy authentication can be configured using a dedicated service account.

* **Login**\
  Specifies the username used for proxy authentication.
* **Password**\
  Specifies the password associated with the proxy authentication account.

> \*\*Important\*\*
>
> Even when proxy authentication is enabled in the Publisher, timestamping operations use the Windows Cryptographic API and rely on the proxy configured at the SYSTEM level, not the Publisher proxy settings. For exceptions and special considerations related to WSUS and timestamping behavior, see \[WSUS and Timestamping Considerations]\(proxy-settings.md#wsus-and-timestamping-considerations).

## WSUS and Timestamping Considerations

When publishing third party updates to WSUS, update CAB files are timestamped using the Windows Cryptographic API. This process is performed under the SYSTEM account on the server.

Because of this behavior:

* The Cryptographic API uses the proxy configured at the SYSTEM level, not the proxy settings configured in the Publisher.
* If the SYSTEM account does not have internet access, timestamping can fail.
* If the SYSTEM proxy requires authentication, timestamping can also fail, as the Cryptographic API does not support interactive proxy authentication.

To confirm which proxy settings apply to the SYSTEM account, see [Verifying the SYSTEM Proxy Configuration](proxy-settings.md#verifying-the-system-proxy-configuration), which explains how to view the effective proxy used during WSUS timestamping.

## Verifying the SYSTEM Proxy Configuration

Use PsExec from Sysinternals to open a SYSTEM level command prompt and view the proxy configuration applied to the SYSTEM account.

To do this:

1. Download **PsExec** from the Sysinternals website.\
   [http://technet.microsoft.com/en-us/sysinternals/bb897553](http://technet.microsoft.com/en-us/sysinternals/bb897553)
2. Extract PsExec to a local folder.
3. Open **Command Prompt** as an administrator.
4. From the folder where PsExec was extracted, run the following command to open a SYSTEM level command prompt.

```
.\psexec.exe -s -i cmd.exe
```

5. In the SYSTEM command prompt, run the following command.

```
netsh winhttp show proxy
```

This output shows the proxy configuration that will be used by WSUS and the Windows Cryptographic API during update signing and timestamping.

> \*\*Important\*\*
>
> Ensure the SYSTEM proxy allows direct or unauthenticated access to the external endpoints used for timestamping. WSUS performs timestamping using the Windows Cryptographic API under the SYSTEM account, and this process does not support interactive or negotiated proxy authentication. If proxy authentication is mandatory, configure bypass rules or allow direct access for timestamping endpoints to prevent publishing failures.
