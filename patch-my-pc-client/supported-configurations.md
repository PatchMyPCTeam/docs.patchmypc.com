# Supported configurations for the Patch My PC Client

_Applies to: Patch My PC Client_

The Patch My PC (PMPC) Client supports the following configurations:

* [Operating Systems](supported-configurations.md#operating-systems)
* [Transport Layer Security (TLS)](supported-configurations.md#transport-layer-security-tls)

## Operating Systems

The Patch My PC (PMPC) Client is supported on the following versions of Microsoft Windows.&#x20;

| Windows Version                | Editions                        |
| ------------------------------ | ------------------------------- |
| Windows 11                     | Enterprise, Pro, and Education  |
| Windows 11 LTSC 2024           | Enterprise                      |
| Windows 10                     | Enterprise, Pro, and Education  |
| Windows 10 LTSC 2019 and 2021  | Enterprise                      |

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>The PMPC Client can be installed on supported 64-bit versions of Windows, including ARM64 via emulation.</p>
<p>Windows versions that have reached End of Servicing or End of Support are not officially supported by the PMPC Client, but may continue to function.</p>
</blockquote>

## Transport Layer Security (TLS)

The PMPC Client does not require a specific version of Transport Layer Security (TLS), which is typically set by the operating systems on which it runs.

Our client will negotiate the highest TLS version supported by itself and our services, which is TLS 1.3 and is the default from Windows 10 21H2 onwards.