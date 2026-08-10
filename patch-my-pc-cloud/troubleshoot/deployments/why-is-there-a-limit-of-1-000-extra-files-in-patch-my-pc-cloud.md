# Why is there a limit of 1,000 Extra Files in Patch My PC Cloud?

_Applies to: Patch My PC Cloud_

The Patch My PC (PMPC) Cloud Portal enforces a limit of 1,000 files per Custom App or Deployment with Extra Files. As this limit includes the primary installer, it is effectively 999 Extra Files + the installer. This limit exists to protect browser stability and prevent crashes during upload.

## Why is there a 1,000-file limit?

When you upload files using the Cloud Portal, the browser must perform client-side processing for each file before and during upload. In particular, the Portal creates a hashing worker for each file to compute its hash.&#x20;

With very large selections, too many workers can run in parallel, causing memory usage spikes, and the browser can hit an out-of-memory condition and crash.

To avoid this, the Cloud Portal blocks uploads beyond the limit and shows a clear validation message instead of letting the browser freeze or crash.

## What You Will See

If you try to select more than 1,000 files, the upload is blocked and you will see an error similar to:

**"You have selected too many files (available: 1000)"**

!['You have selected too many files (available: 1000)'](/_images/image-(4387).png "&#x27;You have selected too many files (available: 1000)&#x27;")

## Workaround: ZIP the folder and extract during deployment

If your scenario requires thousands of files (for example, a folder with \~3,000 files totaling a few GB), the recommended workaround is:

1. [Compress the folder into a single ZIP file](why-is-there-a-limit-of-1-000-extra-files-in-patch-my-pc-cloud.md#compress-the-folder-into-a-single-zip-file)
2. [Upload the ZIP as an Extra File ](why-is-there-a-limit-of-1-000-extra-files-in-patch-my-pc-cloud.md#upload-the-zip-as-an-extra-file)
3. [Extract the ZIP during deployment using a Pre-Install script](why-is-there-a-limit-of-1-000-extra-files-in-patch-my-pc-cloud.md#extract-the-zip-during-deployment-using-a-pre-install-script)

### Step 1: Compress the folder into a single ZIP file

Create a ZIP archive of the extra files either manually or using the following PowerShell script.

```
# Define the path to the folder you want to compress$sourceFolderPath = "C:\temp\MyFolder"
# Define the path where the zip archive should be created$zipFilePath = "C:\Temp\MyFolder.zip"
# Create the zip archiveCompress-Archive -Path $sourceFolderPath -DestinationPath $zipFilePath -Force -ErrorAction 'Stop'
```

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>Ensure you keep the same folder structure that your installer expects. If the installer needs files “next to it” in the cache folder, make sure they end up in the same relative location after extraction.</p>
</blockquote>

### Step 2: Upload the ZIP as an Extra File&#x20;

Upload **MyFolder.zip** as an Extra File in your Custom App or Deployment.

### Step 3: Extract the ZIP during deployment using a Pre-Install script

Whilst deploying the app, use the [Scripts](../../deployments/deploy-app/configurations-tab/additional-tools/scripts/pre-install-scripts.md) configuration tool and configure [this](https://github.com/PatchMyPCTeam/Community-Scripts/blob/main/Install/Pre-Install/Extract%20Zip/README.md) script as a pre-install script.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>Always test your scripts thoroughly outside of the Cloud Portal first.</p>
</blockquote>

## Notes and Considerations

By following this approach, you are exchanging many small files for one ZIP + extraction at install time. This is typically much more reliable for browsers and upload flows.