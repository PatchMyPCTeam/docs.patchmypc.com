# Timestamp Options section of Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Timestamp Options** section of Patch My PC (PMPC) Publisher controls how the Publisher applies digital timestamps when signing scripts and CAB files. Timestamping ensures that signatures remain valid after the signing certificate expires and is a recommended best practice for both applications and updates.

<figure><img src="../../../.gitbook/assets/image (743).png" alt="&#x27;Timestamp Options&#x27; section" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

For a detailed technical explanation of how timestamping works, including certificate trust, CAB signing, and troubleshooting scenarios, see the following blog post at [https://patchmypc.com/blog/demystifying-timestamping-securing-scripts-cab](https://patchmypc.com/blog/demystifying-timestamping-securing-scripts-cab)
{% endhint %}

## Timestamp Server URL

The Timestamp Server URL defines the timestamp authority used during signing. By default, the Publisher uses the DigiCert timestamp service:

```
http://timestamp.digicert.com
```

The **Use Default** option automatically configures the recommended timestamp server. A custom timestamp server can be specified if required by organizational policy.

## Enforce timestamping

When **Enforce timestamping** is enabled, publishing will fail if timestamping cannot be completed successfully. When this option is not enabled, a timestamping failure is treated as a non terminating error and publishing will continue.

## WSUS and SYSTEM account behavior

When publishing third party updates to WSUS, update CAB files are timestamped using the Windows Cryptographic API. This process runs under the SYSTEM account on the server.

Because of this behavior, the Cryptographic API uses the proxy configuration defined for the SYSTEM account, not the proxy settings configured in the Publisher.

If the SYSTEM account does not have internet access, timestamping can fail. If the SYSTEM proxy requires authentication, timestamping can also fail because the Cryptographic API does not support interactive proxy authentication.

To validate which proxy settings apply, see [Verifying the SYSTEM Proxy Configuration](../../../patch-my-pc-publisherv2/administration/advanced/proxy-settings.md#verifying-the-system-proxy-configuration).
