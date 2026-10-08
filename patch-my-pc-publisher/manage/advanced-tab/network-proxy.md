# Network and Proxy category of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Network and Proxy** category on the **Advanced** tab of Patch My PC (PMPC) Publisher allows Publisher to use a proxy server for outbound network connectivity.

<figure><img src="../../../.gitbook/assets/image (1371).png" alt="&#x27;Network and Proxy&#x27; category" width="563"><figcaption></figcaption></figure>

When configured, most Publisher operations use this proxy to download content and communicate with external services.&#x20;

{% hint style="info" %}
**Note**

For exceptions related to WSUS and timestamping behavior, see [WSUS and Timestamping Considerations](network-proxy.md#wsus-and-timestamping-considerations).
{% endhint %}

The **PROXY SETTINGS** section allows you to configure the following settings:

* [Proxy Mode](network-proxy.md#proxy-mode)
* [Use authentication](network-proxy.md#use-authentication)
* [Proxy server](network-proxy.md#proxy-server)
* [Proxy credentails](network-proxy.md#proxy-credentials)

## Proxy mode

This **Proxy mode** section has the following two options:

* **Don’t use proxy (default)**\
  Publisher connects directly to the internet without using a proxy.
* **Use proxy settings**\
  Publisher uses the proxy configuration defined in this section for supported outbound connections.

## **Use Authentication**

By default, Publisher runs under the SYSTEM account. When proxy authentication is not enabled, outbound traffic uses the computer account identity.\
\
In environments where the proxy does not support computer account authentication, or where explicit identity-based auditing is required, proxy authentication can be configured using a dedicated service account.

## Proxy server

This **Proxy server** section allows you to configure:

* **URL**\
  Specifies the proxy server address. This can be a hostname or IP address.
* **Port**\
  Specifies the port used by the proxy server. The default value is 8080.

## Proxy credentials

This **Proxy credentials** section contains the following two fields:

* **Login**\
  Specifies the username used for proxy authentication.
* **Password**\
  Specifies the password associated with the proxy authentication account.

{% hint style="danger" %}
**Important**

Even when proxy authentication is enabled in Publisher, timestamping operations use the Windows Cryptographic API and rely on the proxy configured at the SYSTEM level, not Publisher's proxy settings. For exceptions and special considerations related to WSUS and timestamping behavior, see [WSUS and Timestamping Considerations](network-proxy.md#wsus-and-timestamping-considerations).
{% endhint %}

## WSUS and Timestamping Considerations

When publishing third party updates to WSUS, update CAB files are timestamped using the Windows Cryptographic API. The server performs this process under the SYSTEM account.

Because of this behavior:

* The Cryptographic API uses the proxy configured at the SYSTEM level, not the proxy settings configured in Publisher.
* If the SYSTEM account does not have internet access, timestamping can fail.
* If the SYSTEM proxy requires authentication, timestamping can also fail, as the Cryptographic API does not support interactive proxy authentication.

To confirm which proxy settings apply to the SYSTEM account, see [Verifying the SYSTEM Proxy Configuration](network-proxy.md#verifying-the-system-proxy-configuration), which explains how to view the effective proxy used during WSUS timestamping.

## Verifying the SYSTEM Proxy Configuration

Use PsExec from Sysinternals to open a SYSTEM-level command prompt and view the proxy configuration applied to the SYSTEM account.

To do this:

1. Download **PsExec** from the Sysinternals website.\
   [http://technet.microsoft.com/en-us/sysinternals/bb897553](http://technet.microsoft.com/en-us/sysinternals/bb897553)
2. Extract PsExec to a local folder.
3. Open **Command Prompt** as an administrator.
4. From the folder where PsExec was extracted, run the following command to open a SYSTEM-level command prompt.

```
.\psexec.exe -s -i cmd.exe
```

5. In the **SYSTEM** command prompt, run the following command.

```
netsh winhttp show proxy
```

This output shows the proxy configuration that WSUS and the Windows Cryptographic API will use during update signing and timestamping.

{% hint style="danger" %}
**Important**

Ensure the SYSTEM proxy allows direct or unauthenticated access to the external endpoints used for timestamping. WSUS performs timestamping using the Windows Cryptographic API under the SYSTEM account, and this process does not support interactive or negotiated proxy authentication. If proxy authentication is mandatory, configure bypass rules or allow direct access for timestamping endpoints to prevent publishing failures.
{% endhint %}
