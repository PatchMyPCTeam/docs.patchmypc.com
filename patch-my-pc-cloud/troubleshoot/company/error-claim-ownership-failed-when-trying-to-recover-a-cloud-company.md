# "Error - Claim Ownership Failed" when trying to recover a Cloud Company

_Applies to: Patch My PC Cloud_

### SYMPTOMS

I can no longer access my Patch My PC (PMPC) Cloud Company as the only admin has left and no other users have been created with the **Full Admin with Access Management** role.

I have tried running through the [Recover Your Company](../../manage/settings/company-settings/recover-company.md) process, but after entering the requested information, I see the following:

**Error**

**Claim Ownership Failed**

!["Error - Claim Ownership Failed"](/_images/image-(2661).png "“Error - Claim Ownership Failed”")

### CAUSE

This error can occur for several reasons, such as:

1. You have entered invalid data to attempt the recovery.
2. You are trying to recover a PMPC Company from the wrong Entra ID tenant.

### RESOLUTION

To resolve this issue:

1. Verify you are entering the right values in the correct fields of the **Claim Ownership** wizard.
2. Verify that the last five characters shown for the company you are trying to recover match the last five characters of the Entra ID tenant (the **Directory (tenant) ID**).

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>You only have three attempts to complete the **Claim Ownership** wizard. After the third failed attempt, you will see the following error:</p>
<p>**You've reached the maximum number of claim ownership attempts. Please try again later.**</p>
<p>You will be locked out and prevented from attempting the recovery for 12 hours.</p>
</blockquote>