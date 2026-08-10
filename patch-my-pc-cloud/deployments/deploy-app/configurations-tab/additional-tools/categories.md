# Configure Categories in a Patch My PC Cloud Deployment

_Applies to: Patch My PC Cloud_

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Using the **Categories** tool is optional.</p>
</blockquote>

The **Categories** tool of the Patch My PC (PMPC) Cloud deployment wizard allows you to leverage Intune App Categories (Categories) in your deployments to help users find apps in the Company Portal.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>See the <a href="https://learn.microsoft.com/en-us/mem/intune/apps/apps-add#create-and-edit-categories-for-apps">Create and edit categories for apps</a> section of <a href="https://learn.microsoft.com/en-us/mem/intune/apps/apps-add">Add apps to Microsoft Intune</a> for more information on App Categories.</p>
</blockquote>

To add a Category to a deployment:

1. Add the [**Categories** tool](../#adding-additional-tools).
2. Click the **Categories** tool.

![Clicking the 'Categories' tool](/_images/image-(639).png "Clicking the &#x27;Categories&#x27; tool")

3. Go to Step 6. to add a new category or in the **Add Category** field, either:
   1. Start typing the name of the relevant Category, then click the checkbox beside it to select it.
   2. Click the dropdown to see a list of existing Categories and click the relevant checkbox(es) to select it.

![Selecting the checkbox beside the relevant categories](/_images/image-(641).png "Selecting the checkbox beside the relevant categories")

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>You can click the **X** beside a Category in the **Add Category** field to delete it from the list.</p>
</blockquote>

4. Repeat this process to add any additional categories.
5. Go to to step 8. if you do not want to add a new Category.
6. To add a new Category, type its name in the **Add Category** field.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>You can create up to 200 categories per Intune tenant. Each category name must:</p>
<p>* Be unique</p>
<p>* Be less than 255 characters</p>
<p>* Not contain the backslash (**\\**) or quote (**"**) characters</p>
<p>* Not be the name of a script.</p>
</blockquote>

![Typing the name of the new Category in the 'Add Category' field](/_images/image-(642).png "Typing the name of the new Category in the &#x27;Add Category&#x27; field")

7. Press `ENTER` and the **Success – The category “<**_**category\_name>**_**” has been created** notification is shown, confirming the new category has been added to both Intune and this deployment.

![](/_images/image-(643).png)

The number of categories selected is shown beside the **Categories** tool.

![The number of categories selected is shown beside the 'Categories' tool](/_images/image-(644).png "The number of categories selected is shown beside the &#x27;Categories&#x27; tool")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>See [Check App Categories](../../../../technical-references/intune-reference/check-app-categories-in-intune.md) for details on how to check within Intune that the Categories defined in the deployment have been assigned correctly.</p>
<p>Also:</p>
<p>* If different Categories are configured in the portal and Intune admin center they are combined to be the same.</p>
<p>* If a Category is created in the portal and then removed from the Intune admin center, it will be re-added by the portal.</p>
<p>* Categories are also copied forward to a new version of an app.</p>
</blockquote>

## Next Steps

If you do not want to configure any additional settings, click **Next** to move to the [Assignments](../../assignments-tab.md) tab.

Otherwise, navigate to the relevant tool to configure the required settings, which are explained in the relevant section.