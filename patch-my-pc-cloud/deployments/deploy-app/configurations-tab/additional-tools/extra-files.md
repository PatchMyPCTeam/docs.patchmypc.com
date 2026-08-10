# Configure Extra Files in a Patch My PC Cloud Deployment

_Applies to: Patch My PC Cloud_

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Using the **Extra Files** tool is optional.</p>
</blockquote>

The **Extra Files** tool of the Patch My PC (PMPC) Cloud deployment wizard allows you to upload additional configuration files for a deployment.

To add extra folders and/or files:

1. Add the [**Extra Files** tool](../#adding-additional-tools).
2. Click the **Extra Files** tool.

![Clicking the 'Extra Files' tool](/_images/image-(3635).png "Clicking the &#x27;Extra Files&#x27; tool")

3. Either:
   1. Drag and drop the relevant folders or files to the relevant area.
   2. Click the relevant button to browse to and select the relevant folders or files.

!['Extra Files' section](/_images/image-(3639).png "&#x27;Extra Files&#x27; section")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>See [Unsupported File Names and Extensions for Extra Files](../../../../technical-references/unsupported-file-names-and-extensions-in-cloud.md) for a list of filenames and extensions we do not support for upload.</p>
<p>Also, adding a folder will add any files and folders (including their files) within the selected folder.</p>
<p>We support uploading files with the same name, provided they are in different folders. We also support uploading folders with the same name, provided the selected paths are unique.</p>
</blockquote>

4.  Click **Upload** when your browser prompts you to upload the content.\
    <br>

    ![Clicking "Upload" when prompted to upload the content](/_images/image-(848).png "Clicking &#x22;Upload&#x22; when prompted to upload the content")

    \
    The hash will be calculated for any folders/files you upload, which will appear at the bottom of the **Extra Files** section.

![Additional folders/files to be uploaded appearing at the bottom of the 'Extra Files' section](/_images/image-(3640).png "Additional folders/files to be uploaded appearing at the bottom of the &#x27;Extra Files&#x27; section")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>The total number of extra folders/files is not limited, but their total size must not exceed the storage limits for your license type. See [Product Limitations](../../../../product-limits.md)  for more details.</p>
<p>Also, if the **Installer Type** on the **General Information** page is set to **`.msi`**, the **MST File** section will be shown, allowing you to upload a single MST file. This file must have the **`.mst`** extension.</p>
<p>!['Add MST File'](/_images/image-(3641 "'Add MST File'").png>)</p>
<p>\*\*</p>
<p>Uploading a **`.mst`** file automatically adds the following to the **Additional Argument** field of the **Install Parameters** section:</p>
<p>**`TRANSFORMS=[<`**_**`mstfile>`**_**`].mst`**</p>
<p>where **`<`**_**`mstfile>`**_ is the name of the uploaded MST file.</p>
</blockquote>

5. Repeat the above steps to add any additional folders/files as required.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Once a deployment has been successfully created, you can add or remove any additional folders or files as required.</p>
</blockquote>

## Next Steps

If you do not want to configure any additional settings, click **Next** to move to the [Assignments](../../assignments-tab.md) tab.

Otherwise, navigate to the relevant tool to configure the required settings, which are explained in the relevant section.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>If you upload [Extra Files](extra-files.md) as part of your Patch My PC (PMPC) Cloud Deployment, you can reference those files in any of the [Scripts](scripts/) in the same deployment by building a path relative to the script's current location. See [Referencing Extra Files in Scripts](../../../technical-references/reference-external-scripts.md) for more information.</p>
</blockquote>