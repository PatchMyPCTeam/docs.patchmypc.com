# Network and Proxy category of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Network and Proxy** category on the **Advanced** tab of Patch My PC (PMPC) Publisher allows Publisher to use a proxy server for outbound network connectivity.

<figure><img src="../../../.gitbook/assets/image (1371).png" alt="&#x27;Network and Proxy&#x27; category" width="563"><figcaption></figcaption></figure>

When configured, most Publisher operations use this proxy to download content and communicate with external services.&#x20;

{% hint style="danger" %}
**Important**

Configuring a proxy in Publisher does not automatically configure the Windows proxy settings used by WSUS and Windows certificate operations. In a proxy-only environment, downloads may succeed while certificate revocation checks or timestamping fail. See **Windows Proxy Settings for Certificate Operations** below.
{% endhint %}

The **PROXY SETTINGS** section allows you to configure the following settings:

* [Proxy Mode](network-proxy.md#proxy-mode)
* [Use authentication](network-proxy.md#use-authentication)
* [Proxy server](network-proxy.md#proxy-server)
* [Proxy credentials](network-proxy.md#proxy-credentials)

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

## **Windows Proxy Settings for Certificate Operations**

Publisher uses Windows components for certificate validation, signing and timestamping. These operations can use proxy settings separate from those configured in Publisher.

{% hint style="info" %}
**Note**

If your environment requires a proxy for Internet access, configure the relevant Windows proxy settings so these operations can reach their endpoints.

With [**Enforce timestamping**](integrations-platform.md#enforce-timestamping) enabled, access to the timestamp server is required. When disabled, Publisher should continue signing without a timestamp if the server is unavailable.

Revocation connectivity warnings do not prevent publishing when followed by **“validated with warnings.”**
{% endhint %}

There are two Windows proxy configurations to distinguish:

| Configuration                                                    | Publisher-related operations                                                           |
| ---------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| Windows Internet Options, commonly called WinINET proxy settings | Certificate revocation checks and timestamping ConfigMgr and Intune detection scripts. |
| WinHTTP proxy settings                                           | WSUS API operations, including update CAB signing and timestamping connectivity.       |

### **Proxy authentication considerations**

Windows certificate and WSUS operations run under the Publisher service account, SYSTEM by default, and cannot respond to interactive proxy authentication prompts. Credentials configured in Publisher do not automatically apply to these operations.

Ensure your proxy permits the service account to access the required certificate and timestamp endpoints. If authentication prevents access, work with your network team to configure an appropriate authentication policy, allow unauthenticated access to those endpoints through the proxy, or permit approved direct access.

{% hint style="info" %}
**Note**

Publisher, WinINET and WinHTTP use separate proxy configurations. Changing Publisher’s proxy settings does not automatically update either Windows configuration.

Configure WinINET settings for the Publisher service account, which is SYSTEM by default. The basic WinHTTP proxy settings are machine-wide and can be configured from an elevated Command Prompt.
{% endhint %}

## Certificate revocation checks and script timestamping

Certificate revocation checks for the Patch My PC catalog and timestamping operations for ConfigMgr and Intune detection scripts follow the Windows Internet Options proxy settings for the account performing the operation.

In environments where direct Internet access is blocked, configure these settings for the Publisher service account, which runs as **SYSTEM** by default, and ensure the WinINET proxy permits access to the required certificate and timestamp endpoints.

| Endpoint                        | Purpose                               |
| ------------------------------- | ------------------------------------- |
| `http://cacerts.digicert.com`   | Intermediate certificate downloads    |
| `http://crl3.digicert.com`      | Certificate revocation list downloads |
| `http://crl4.digicert.com`      | Certificate revocation list downloads |
| `http://ocsp.digicert.com`      | Online certificate status checks      |
| `http://timestamp.digicert.com` | Default script timestamp server       |

These URLs require HTTP access on port 80. If you configure a different timestamp server, you may also need to allow access to that server and the CRL and OCSP endpoints associated with its certificate chain.

## Configuring the WinINET Proxy for Certificate Revocation Checks and Script Signing

Certificate revocation checks and script timestamping use Windows Internet Options (WinINET) proxy settings. Configure these for the service account for the Patch My PC Publisher Service. The SYSTEM account is used by default.

To do this:

1. Download **PsExec** from the Sysinternals website.\
   [http://technet.microsoft.com/en-us/sysinternals/bb897553](http://technet.microsoft.com/en-us/sysinternals/bb897553)
2. Extract PsExec to a local folder.
3. Open **Command Prompt** as an administrator.
4. From the folder where PsExec was extracted, run the following command to open a SYSTEM-level command prompt.

```
.\PsExec.exe -s -i cmd.exe
```

5. In the **SYSTEM** command prompt, run the following command.

```
rundll32.exe shell32.dll,Control_RunDLL inetcpl.cpl
```

6. Select **Connections > LAN settings**.
7. Enter your organisation’s proxy address and port. Preserve any required bypass settings.
8. Click **OK** in both windows and close the SYSTEM command prompt.
9. Restart the Publisher service.

## Configuring the WinHTTP Proxy for WSUS API Operations

WSUS API operations use Windows HTTP Services (WinHTTP) proxy settings. Configure these at the machine level using an elevated Command Prompt. These settings apply to all accounts, including SYSTEM.

To do this:

1. Open **Command Prompt** as an **administrator.**
2.  Run the following command to view the current proxy configuration:

    ```
    netsh winhttp show proxy
    ```
3.  Configure the proxy using your organisation’s proxy address and port:

    ```
    netsh winhttp set proxy proxy-server="proxy.example.com:8080"
    ```

    Replace `proxy.example.com:8080` with your proxy details.
4.  Verify the updated configuration:

    ```
    netsh winhttp show proxy
    ```
