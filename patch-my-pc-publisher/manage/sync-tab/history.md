# History in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **History** tab of the **Sync** tab of Patch My PC (PMPC) Publisher lets you see which syncs ran, whether they succeeded, and which schedule started them. You can also export sync history to share or keep a record.

## To open the History tab

Navigate to **Sync** **|** **History.**

<figure><img src="../../../.gitbook/assets/image (1605).png" alt="&#x27;Sync history&#x27; tab" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

History is available whether or not the Multiple schedule feature is enabled. Publisher keeps sync history for 60 days.
{% endhint %}

The list of **Recent syncs** is shown, listing the syncs that ran on this Publisher in the last seven days, newest first.

<table><thead><tr><th width="181.22216796875" valign="top">Column</th><th valign="top">Description</th></tr></thead><tbody><tr><td valign="top">When</td><td valign="top">When the sync started.</td></tr><tr><td valign="top">Status</td><td valign="top"><strong>Succeeded</strong> or <strong>Failed</strong>.</td></tr><tr><td valign="top">Schedule/Run type</td><td valign="top">The schedule that started the sync, or <strong>Manual</strong> for a sync you started manually. See Run a manual sync.</td></tr></tbody></table>

## To export the sync history

1. Navigate to **Sync | History**.
2. From the **Format** dropdown, select the required format for the report.
3. If you selected **HTML report** in step 2, select which syncs to export from the **Include** dropdown.

{% hint style="info" %}
**Note**

A JSON export always includes every sync on record.
{% endhint %}

4. Click **Export**.
5. Choose where to save the file.

## Include options

The following options are available from the **Include** dropdown:

* **All syncs**\
  Exports every sync on record.
* **Last sync**\
  Exports the most recent sync.
* **Last X syncs**\
  Exports the number of recent syncs you enter in the **Count** field, up to **500**.
* **Date range**\
  Exports syncs between the dates you enter in **From** and **To**.
