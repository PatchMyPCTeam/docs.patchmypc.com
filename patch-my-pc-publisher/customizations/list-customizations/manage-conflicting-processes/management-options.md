# Management Options section of Manage Conflicting Processes in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_&#x41;vailable at level: All Custom Products, All Products, Vendor, Product_\
_&#x41;vailable on tab: WSUS Updates, ConfigMgr Apps, Intune Apps, Intune Updates_

The **Management Options** section of **Manage Conflicting Processes** in Patch My PC (PMPC) Publisher allows you to:

* Control which running processes are evaluated for conflicting process management.
* Configure notification branding.

<figure><img src="../../../../.gitbook/assets/image (752).png" alt="&#x27;Management Options&#x27; section" width="502"><figcaption></figcaption></figure>

## Manage Process List

The _Process List_ defines the executable names that are checked when determining whether an application is in use during an update.

The default process list is populated automatically based on the processes defined in the Patch My PC catalog for the selected product. These defaults represent processes known to prevent the application from updating successfully while running.

You can:

* Add additional process names if your environment uses processes that should also be considered conflicting.
* Remove processes if required, although this is generally not recommended unless you are certain the process does not interfere with updates.

### To manage the process list

1. Right-click the relevant product in the Product Tree and select **Manage Conflicting Processes**.
2. On the **Manage Conflicting Processes** screen, click **Manage Process List**.

<figure><img src="../../../../.gitbook/assets/image (800).png" alt="Clicking &#x27;Manage Process List&#x27;" width="524"><figcaption></figcaption></figure>

3. On the **Select processes for blocking process management** screen, review the default processes shown. These are populated automatically from the Patch My PC catalog.

<figure><img src="../../../../.gitbook/assets/image (801).png" alt="&#x27;Select processes for blocking process management&#x27; screen" width="375"><figcaption></figcaption></figure>

4. To add an additional process name, click the '**+**' icon.
5. To remove an existing process, click the process, then click the '**-**' icon.

{% hint style="success" %}
**Tip**

Clicking **Reset** restores the list to the default processes defined in the Patch My PC catalog.
{% endhint %}

6. Click **OK** to save changes.

## Manage Default Settings

Clicking the **Manage Default Settings** button opens the **Conflicting Process UI Settings** screen which is used to customize the end-user notification experience shown when an application must be closed to complete an update.

<figure><img src="../../../../.gitbook/assets/image (811).png" alt="&#x27;Conflicting Process UI Settings&#x27; screen" width="450"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

See [Conflicting Process UI Settings](conflicting-process-ui-settings-window.md) for more information.
{% endhint %}
