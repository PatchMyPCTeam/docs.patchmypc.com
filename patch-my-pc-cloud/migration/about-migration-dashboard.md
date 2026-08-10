# About the ConfigMgr to Intune App Migration for Patch My PC Cloud Migration Dashboard

_Applies to: Patch My PC Cloud_

When you click the **Migration** node in the Patch My PC (PMPC) Cloud Portal, the **Migration** page opens with the **Dashboard** tab selected by default, which provides an overview of the detected ConfigMgr applications.

![Migration Dashboard](/_images/image-(23).png "Migration Dashboard")



## Dashboard tab

The dashboards are:

<table data-header-hidden><thead><tr><th valign="top"></th><th valign="top"></th><th valign="top"></th><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top"><a href="about-migration-dashboard.md#configmgr-apps">ConfigMgr Apps</a></td><td valign="top"><p><a href="about-migration-dashboard.md#cves-detected">CVEs Detected</a></p><p></p></td><td valign="top"><p><a href="about-migration-dashboard.md#migration-status">Migration Status</a></p><p></p></td><td valign="top"><p><a href="about-migration-dashboard.md#not-supported-apps">Unsupported Apps</a></p><p></p></td><td valign="top"><a href="about-migration-dashboard.md#app-update-status">App Update Status</a></td></tr></tbody></table>

### ConfigMgr Apps

Provides a breakdown of detected ConfigMgr applications by match type.&#x20;

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>See the **Match Type** field in the [Apps tab](about-migration-dashboard.md#apps-tab) section below for more information on how apps are matched.</p>
</blockquote>

### CVEs Detected

This chart shows the number of known vulnerabilities (CVEs) associated with applications discovered in your ConfigMgr environment.

If we recognize the hash of a ConfigMgr app, we check whether that hash is associated with any published CVEs. If matches are found, the CVEs are grouped by severity (Critical, High, Medium, Low).

In the screenshot example, we found:

* 1 x Critical CVE
* 12 x High-severity CVEs
* 6 x Medium severity CVEs
* 2 x Low severity CVEs

Giving us a total of 21 CVEs across all ConfigMgr applications, where we recognized the hash of the installer.

### Migration Status

Shows the total number of ConfigMgr applications discovered and their current migration progress.

### Unsupported Apps

Displays the number of ConfigMgr applications that cannot be migrated, with reasons based on validation errors.

### App Update Status

Displays ConfigMgr applications in your environment that are out of date.

## 'Apps' tab

From the **Migration Dashboard**, you can click the **Apps** tab to see a list of the ConfigMgr applications that have been detected with their associated information.

![Migration Dashboard Apps Tab](/_images/image-(3676).png "Migration Dashboard Apps Tab")

<table><thead><tr><th width="125.888916015625" valign="top">Field</th><th valign="top">Description</th></tr></thead><tbody><tr><td valign="top">Match Type</td><td valign="top"><p>The result of our attempt to match the ConfigMgr application to an app in our App Catalog, which will be one of the following:</p><p></p><ul><li><strong>Catalog App –</strong> We have successfully matched the ConfigMgr application to a version in our catalog. These apps can be deployed into Intune as a PMPC App and kept up to date by us for you.</li><li><strong>Custom App –</strong> We have been unable to successfully match the ConfigMgr application to a version in our catalog, but we can still help you migrate it to Intune.</li><li><strong>Publisher App –</strong> We have identified that the application was created by Patch My PC Publisher. These apps are not supported for migration.</li><li><strong>Multiple Matches -</strong> We have found multiple matches in our catalog to the app that is to be migrated.</li><li><strong>Unsupported –</strong> We cannot migrate the ConfigMgr application. See <br><a href="technical-references/unsupported-reasons.md">Migration Not Supported Reasons</a> for more details.<br><br><mark style="color:green;"><strong>TIP:</strong></mark><br>You can hover over the “<strong>(i)</strong>” for an unsupported match type to see why it is unsupported for migration.</li></ul></td></tr><tr><td valign="top">Matched App</td><td valign="top">The name of the app we have matched the ConfigMgr application to in our catalog.</td></tr><tr><td valign="top">Status</td><td valign="top"><p>The migration status of the ConfigMgr application, which will be one of the following:</p><p></p><ul><li><strong>Not Started –</strong> The migration process has not been started.</li><li><strong>Pending –</strong> The migration process has been initiated.</li><li><strong>Importing -</strong> The app is currently being processed by the Publisher and is being imported to the PMPC Cloud Portal.</li><li><strong>In Progress –</strong> The migration is in progress.</li><li><strong>Migrated –</strong> The application has been successfully migrated to PMPC Cloud.</li><li><strong>Failed</strong> - The migration encountered an error.</li></ul></td></tr><tr><td valign="top">Info</td><td valign="top">If there are further information/warnings about this application that we want you to review (e.g. we’ve detected a setting in the ConfigMgr application we cannot migrate), a warning triangle is displayed in the <strong>Info</strong> column.<br><br>The triangle includes a number indicating the number of warnings. If you hover your mouse over the triangle, you will see a summary. If you click the triangle, it opens the properties of the application and displays the triangle beside the items we are warning you about.<br><br>Clicking the triangle shows more details you should review before continuing the application migration.</td></tr></tbody></table>

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>The last column displays the **Migrate** button, which you click to migrate the application.</p>
<p>If there are multiple matches for the application, the **Migrate** button will show as either of the following:</p>
<p>* Without a down arrow if we’ve matched the app to at least one Public app, but not a Custom App. When you click **Migrate**, the Migration Wizard starts, allowing you to choose the relevant app to migrate this application to.</p>
<p>* With a down arrow, which, when clicked, shows a dropdown with two options:</p>
<p>* **Migrate as Catalog**, which either shows the single matching app or the available multiple matches to the Catalog apps from which you can select the one you want to migrate this app to.</p>
<p>* **Migrate as Custom**, will start the migration of the app as a Custom App without the option to select any other app.</p>
<p>Also note that the **Migrate** button will be unavailable if:</p>
<p>* The application cannot be migrated or has already been migrated to PMPC Cloud.</p>
<p>* You do not have the correct license for your PMPC Cloud Company.</p>
</blockquote>