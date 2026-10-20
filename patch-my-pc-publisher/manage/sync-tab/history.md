---
description: >-
  Review recent syncs in Patch My PC Publisher and export sync history as an
  HTML report or JSON file.
hidden: true
---

# History

Use the **History** page in Patch My PC Publisher (Publisher) to see which syncs ran, whether they succeeded, and which schedule started them. You can also export sync history to share or keep a record.

To open the page, go to **Sync** > **History**.

<figure><img src="../../../.gitbook/assets/image (1498).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**History** is available whether or not the multiple schedule feature is enabled. Publisher keeps sync history for 60 days.
{% endhint %}

### Recent syncs

**Recent syncs** lists the syncs that ran on this Publisher in the last seven days, newest first.

| Column                  | Description                                                                                               |
| ----------------------- | --------------------------------------------------------------------------------------------------------- |
| **When**                | When the sync started.                                                                                    |
| **Status**              | **Succeeded** or **Failed**.                                                                              |
| **Schedule / Run type** | The schedule that started the sync, or **Manual** for a sync you started manually. See Run a manual sync. |

### Export sync history

**Export sync history** shows how many syncs are on record and the date of the oldest one.

1. Go to **Sync** > **History**.
2. In **Format**, select **HTML report** or **JSON**.
3. If you selected **HTML report**, in **Include**, select which syncs to export.
4. Select **Export**.
5. Choose where to save the file.

| **Include** option | Exports                                                       |
| ------------------ | ------------------------------------------------------------- |
| **All syncs**      | Every sync on record.                                         |
| **Last sync**      | The most recent sync.                                         |
| **Last X syncs**   | The number of recent syncs you enter in **Count**, up to 500. |
| **Date range**     | Syncs between the dates you enter in **From** and **To**.     |

A JSON export always includes every sync on record.

### Related pages

* Schedule
* Timeline
