---
description: >-
  Create, view, and revoke personal access tokens for the Cloud Customer API in
  the Patch My PC portal.
noIndex: true
noRobotsIndex: true
---

# Create a personal access token

[Back to the Cloud Customer API overview](https://docs.patchmypc.com/patch-my-pc-cloud-api)

A personal access token (PAT) lets your scripts, services, and pipelines call the Patch My PC Cloud Customer API without anyone at the keyboard. You create, view, and revoke PATs in the Patch My PC portal. You then exchange a PAT for a short-lived access token, as described in [Authentication](authentication.md).

## Before you begin

* Make sure you can open **Settings** > **Access Tokens** in the Patch My PC portal. If you don't see **Access Tokens**, ask an administrator for access.
* Decide which [scopes](create-a-personal-access-token.md#choose-scopes) your job needs. A token can never do more than the person who created it, so you can only grant scopes that your own account is allowed to use.

## Open the Access Tokens page

1. Sign in to the Patch My PC portal.
2. Go to **Settings** > **Access Tokens**.

The **Personal Access Tokens** page lists the tokens for your company.

![The Personal Access Tokens page in Settings](<../.gitbook/assets/access-tokens-list (1).png>)

| Column                   | Shows                                                                                               |
| ------------------------ | --------------------------------------------------------------------------------------------------- |
| **Name**                 | The name you gave the token.                                                                        |
| **Token ID**             | The token's identifier. This isn't the token value, which is never shown again after you create it. |
| **Scopes**               | What the token is allowed to do.                                                                    |
| **Created**              | When the token was created.                                                                         |
| **Expires**              | When the token stops working.                                                                       |
| **Last Used**            | When the token was last used, or **Never** if it hasn't been used.                                  |
| **Status**               | **Active**, **Expired**, or **Revoked**.                                                            |
| Trash icon (last column) | Revokes the token.                                                                                  |

Revoked tokens are hidden by default. Select **Show revoked** to include them.

## Create a token

1. On the **Personal Access Tokens** page, select **Create Token**.
2.  In the **Create Personal Access Token** dialog, fill in the fields:

    | Field               | What to enter                                                                                                                 |
    | ------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
    | **Name**            | Required. A name that describes what the token is for, for example `nightly-catalog-report`. Up to 100 characters.            |
    | **Scopes**          | Required. Select at least one scope. For help choosing, see [Choose scopes](create-a-personal-access-token.md#choose-scopes). |
    | **Expires In Days** | The token's lifetime, from 1 to 365 days. If you leave it blank, the token lasts 90 days.                                     |

    ![The Create Personal Access Token dialog](<../.gitbook/assets/create-token-dialog (1).png>)
3. Select **Create**.
4. In the **Token Created** dialog, select **Copy**, and store the token value somewhere safe, for example in Azure Key Vault or your pipeline's secret variables.
5.  Select **Done**.

    ![The Token Created dialog, with the token value hidden](<../.gitbook/assets/token-created-dialog (1).png>)

{% hint style="warning" %}
The token value is shown only once. After you close the **Token Created** dialog, you can't retrieve it again. If you lose it, create a new token and revoke the old one.
{% endhint %}

Treat the token like a password: keep it in a secret store, and never write it to source control or logs.

## Choose scopes

Scopes limit what a token can do. Select only the scopes your job needs.

| Scope in the portal              | Scope value                  | Lets the token                                                                                           |
| -------------------------------- | ---------------------------- | -------------------------------------------------------------------------------------------------------- |
| **Read applications**            | `appcatbroker:apps:read`     | Search applications, read application details and files, and list your connections.                      |
| **Create & update applications** | `appcatbroker:apps:write`    | Create, update, edit, and delete custom applications. Also includes the access of **Read applications**. |
| **Deploy applications**          | `appcatbroker:apps:deploy`   | Read, create, edit, sync, pause, redeploy, and delete deployments, and manage deployment templates.      |
| **Read customer info**           | `appcatbroker:customer:read` | Read your account information and usage limits.                                                          |

The scope value is what the API reports in error responses and what the reference pages list under each operation's required scope.

You can only grant scopes that your own account is allowed to use. The portal can show a scope you aren't allowed to grant as unavailable, and a token is never granted a scope beyond your permissions, so check the **Scopes** column after you create a token. If you need a scope you can't grant, ask an administrator for the permission, or ask someone who has it to create the token.

You can't change the scopes of an existing token. To change them, create a new token with the scopes you need, update your automation to use it, and revoke the old token.

## Revoke a token

Revoke a token when you no longer need it, when you replace it, or if you think it was exposed.

1. On the **Personal Access Tokens** page, find the token.
2. At the end of the token's row, select the revoke (trash) icon.
3.  When you're asked to confirm, select **Yes**.

    ![The confirmation to revoke a token](<../.gitbook/assets/revoke-token-confirm (1).png>)

Revoking takes effect immediately: any automation using the token loses access. You can't undo a revocation.

## Replace a token before it expires

A token stops working when it expires. To avoid an interruption:

1. Create a new token with the same scopes.
2. Update your secret store or pipeline variable with the new value.
3. Confirm your automation runs with the new token.
4. Revoke the old token.

## Next steps

* [Authentication](authentication.md): exchange the token for an access token and send it with each request.
* [Automate with a personal access token](guides/automate-with-a-personal-access-token.md): run a scheduled job with a token.
