# Setup the Patch My PC Publisher Remote User Interface

_Applies to: Patch My PC Publisher V3.x_

{% hint style="danger" %}
**PRE-RELEASE DOCUMENTATION**

This documentation is for a pre-release feature still under development and, therefore, incomplete. As a result, both functionality and documentation are subject to change.

Once this feature is released, it will be announced, and this banner will be removed.
{% endhint %}

Setting up the Patch My PC (PMPC) Publisher _Remote User Interface (UI)_ feature involves the following two steps:

1. [Enabling external access on the server](setup.md#enabling-external-access-on-the-server)
2. [Connecting to the Settings console from a workstation](setup.md#connecting-to-the-settings-console-from-a-workstation)

## Enabling external access on the server

{% hint style="info" %}
**Note**

This process only needs to be completed once.
{% endhint %}

On the computer running the Publisher **PatchMyPCService**:

1. Sign in as an administrator.
2. Open Publisher's Settings console on the server.
3. Navigate to **Settings | Advanced | Config API External Access**.
4. Choose the **hostname** clients will use to reach this server. Use the fully qualified domain name (for example **publisher.contoso.com**), as the name has to match the server certificate.
5. Choose the **port** the service listens on for remote connections.
6. Ensure the chosen port in open on the server's firewall.
7. Make a note of both the chosen hostname and port, as each administrator needs the same hostname and port.
8. Select the **server certificate** to secure the connection, then click **Apply**.

{% hint style="info" %}
**Note**

As binding the certificate needs elevation, you may see a User Account Control prompt.
{% endhint %}

If you do not yet have a suitable certificate, see [Using a Different Computer](technical-references/using-different-computer.md) for details of the certificate requirements and how to create or request one.

## Connecting to the Settings console from a workstation

On each administrator's workstation:

1. Install or open Publisher's Settings console on the workstation.
2. Navigate to **Settings | Advanced | Remote Service Connection**.
3. Enter the **server FQDN** and **port** noted in [Enabling external access on the server](setup.md#enabling-external-access-on-the-server).
4. Click **Test Connection**. This confirms the workstation can reach the service and that the certificate is valid.
   * For a certificate issued by your domain certificate authority, the test succeeds on its own, and the Settings console adopts the server's certificate automatically - you do not have to browse for a file.
   * For a self-signed certificate, select the server's certificate (a **.cer** file or by thumbprint) so the console can verify it.
5. Click **Apply** to save the connection.
   * For a self-signed certificate, clicking **Apply** adds the certificate to your Trusted Root store so future connections are trusted automatically. The confirmation tells you this happened.
   * For a certificate that your domain already trusts, nothing is installed.

The connection is saved to your Windows profile on that workstation. The next time you launch the console, it connects to the server automatically.
