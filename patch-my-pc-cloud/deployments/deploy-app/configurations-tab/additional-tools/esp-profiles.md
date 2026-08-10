# Configure ESP Profiles in a Patch My PC Cloud Deployment

_Applies to: Patch My PC Cloud_

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Using the **ESP Profiles** tool is optional.</p>
</blockquote>

The **ESP Profiles** tool of the Patch My PC (PMPC) Cloud deployment wizard allows you to configure your deployments created in our portal to be part of one or more profiles configured on the Enrollment Status Page (ESP) of the Microsoft Intune admin center.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>See <a href="https://learn.microsoft.com/en-us/mem/intune/enrollment/windows-enrollment-status">Set up the Enrollment Status Page</a> for more details about the ESP and working with ESP profiles.</p>
</blockquote>

To configure a PMPC Cloud deployment to use an ESP Profile:

1. Add the [**ESP Profiles** tool](../#adding-additional-tools).
2. Ensure the ESP Profile(s) you want this deployment to belong to have already been created in Intune.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>At the time of writing, Intune supports a maximum of 51 profiles plus the default profile (so 52 in total) per tenant.</p>
</blockquote>

3. Click the **ESP Profiles** tool.

![Clicking the 'ESP Profiles' tool](/_images/image-(634).png "Clicking the &#x27;ESP Profiles&#x27; tool")

4. In the **Add Profile** field, either:
   1. Start typing the name of the relevant ESP Profile, then click the checkbox beside it to select it.
   2. Click the dropdown to see a list of existing ESP Profiles and click the checkboxes beside the relevant profiles to select them.

![Adding ESP Profiles](/_images/image-(635).png "Adding ESP Profiles")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>If an ESP Profile already contains the maximum of 100 apps, you will be unable to select it from the dropdown. If you hover over it, you'll see the **Total limit reached** tooltip.</p>
<p>!['Total limit reached' tooltip](/_images/image-(636 "'Total limit reached' tooltip").png>)</p>
</blockquote>

The selected ESP Profile(s) are added to the **Add Profile** field.

![Selected ESP Profile(s) added to the 'Add Profile' field](/_images/image-(637).png "Selected ESP Profile(s) added to the &#x27;Add Profile&#x27; field")

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>You can click the **X** beside an ESP Profile in the **Add Profile** field to delete it from the list.</p>
<p>Also, the number in brackets shows the number of apps currently added to an ESP Profile, with 100 being the maximum.</p>
</blockquote>

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>See [Check ESP Profiles](../../../../technical-references/intune-reference/check-esp-profiles-in-intune.md) for details on how to check within Intune that a PMPC Cloud deployment has been successfully added to an ESP Profile.</p>
</blockquote>

5. Repeat this process to add any additional ESP Profiles.

The number of ESP Profiles selected is shown beside the **ESP Profiles** tool.

![Number of ESP Profiles selected shown beside the 'ESP Profiles' tool](/_images/image-(638).png "Number of ESP Profiles selected shown beside the &#x27;ESP Profiles&#x27; tool")

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>To avoid potential conflicts, we highly recommend creating all deployments within the PMPC Cloud portal and using the ESP Profiles feature to control which apps belong to which ESP profiles. You should only use the **Enrollment Status Page** in the Intune admin center to create an ESP Profile.&#x20;</p>
<p>Other important points about ESP Profiles:</p>
<p>* They are currently unavailable on macOS.</p>
<p>* Different ESP Profiles can be used in different Update Rings if required.</p>
<p>* If you edit an ESP Profile that is used in a deployment that uses Update Rings, the changes will only be applied to the version of the deployment that is applied to the ring with the lowest delay.</p>
<p>* If during a Sync Schedule the number of apps within an ESP Profile exceeds 100, we do not fail the deployment. The deployment will be completed with any new versions being assigned. However, we will display a warning indicator in the portal and the message \</p>
<p>\</p>
<p>“**Failed to add application with version “<**_**version\_number**_**>” to “<**_**esp\_profile\_name**_**>**”.</p>
</blockquote>

## Next Steps

If you do not want to configure any additional settings, click **Next** to move to the [Assignments](../../assignments-tab.md) tab.

Otherwise, navigate to the relevant tool to configure the required settings, which are explained in the relevant section.