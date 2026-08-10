# Timestamp Options

_Applies to: Patch My PC Publisher V2.x_

## Overview

The **Timestamp Options** control how the Publisher applies digital timestamps when signing scripts and CAB files. Timestamping ensures that signatures remain valid after the signing certificate expires and is a recommended best practice for both applications and updates.

![Timestamp Options](/_images/image-(175).png)

> \*\*Note\*\*
>
> For a detailed technical explanation of how timestamping works, including certificate trust, CAB signing, and troubleshooting scenarios, see the following blog post at [https://patchmypc.com/blog/demystifying-timestamping-securing-scripts-cab](https://patchmypc.com/blog/demystifying-timestamping-securing-scripts-cab)

## Timestamp Server URL

The Timestamp Server URL defines the timestamp authority used during signing. By default, the Publisher uses the DigiCert timestamp service:

```
http://timestamp.digicert.com
```

The **Use Default** option automatically configures the recommended timestamp server. A custom timestamp server can be specified if required by organizational policy.

## Enforce Timestamping

When **Enforce Timestamping** is enabled, publishing will fail if timestamping cannot be completed successfully. When this option is not enabled, a timestamping failure is treated as a non terminating error and publishing will continue.

## WSUS and SYSTEM account behavior

When publishing third party updates to WSUS, update CAB files are timestamped using the Windows Cryptographic API. This process runs under the SYSTEM account on the server.

Because of this behavior, the Cryptographic API uses the proxy configuration defined for the SYSTEM account, not the proxy settings configured in the Publisher.

If the SYSTEM account does not have internet access, timestamping can fail. If the SYSTEM proxy requires authentication, timestamping can also fail because the Cryptographic API does not support interactive proxy authentication.

To validate which proxy settings apply, see [Verifying the SYSTEM Proxy Configuration](proxy-settings.md#verifying-the-system-proxy-configuration).