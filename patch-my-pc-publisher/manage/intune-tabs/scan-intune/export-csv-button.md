# Export to CSV button in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **Export to CSV** button on the **Scan Intune** tab of Patch My PC (PMPC) Publisher exports the results displayed in the query window to a comma-separated values (CSV) file for offline review or reporting.

This button is disabled when no query results are present in the window. After you run a query with valid results, the **Export to CSV** button becomes available.

## To export the results to a CSV

1. Run a query so that results are displayed in the window, then click **Export to CSV**.

<figure><img src="../../../../.gitbook/assets/image (4152).png" alt="Export to CSV" width="563"><figcaption></figcaption></figure>

2. Click the relevant button on the **Export** dialog for the results you want to export.

<figure><img src="../../../../.gitbook/assets/image (1086).png" alt="&#x27;Export&#x27; dialog" width="306"><figcaption></figcaption></figure>

3. Select the save location, enter a file name if required.

<figure><img src="../../../../.gitbook/assets/image (4154).png" alt="Choose a save location" width="563"><figcaption></figcaption></figure>

4. Click **Save** to complete the export.

The generated CSV file includes the following columns:

* **Device Name -** The name of the device where the product was detected.
* **Product Name -** The application name as reported in inventory.
* **Product Version -** The version of the application detected on the device.
