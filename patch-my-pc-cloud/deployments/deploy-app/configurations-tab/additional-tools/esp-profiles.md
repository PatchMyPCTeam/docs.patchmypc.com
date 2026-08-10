# Configure ESP Profiles in a Patch My PC Cloud Deployment

_Applies to: Patch My PC Cloud_

> \*\*Note\*\*
>
> Using the \*\*ESP Profiles\*\* tool is optional.

The **ESP Profiles** tool of the Patch My PC (PMPC) Cloud deployment wizard allows you to configure your deployments created in our portal to be part of one or more profiles configured on the Enrollment Status Page (ESP) of the Microsoft Intune admin center.

> \*\*Note\*\*
>
> See [Set up the Enrollment Status Page](https://learn.microsoft.com/en-us/mem/intune/enrollment/windows-enrollment-status) for more details about the ESP and working with ESP profiles.

To configure a PMPC Cloud deployment to use an ESP Profile:

1. Add the [**ESP Profiles** tool](../#adding-additional-tools).
2. Ensure the ESP Profile(s) you want this deployment to belong to have already been created in Intune.

> \*\*Note\*\*
>
> At the time of writing, Intune supports a maximum of 51 profiles plus the default profile (so 52 in total) per tenant.

3. Click the **ESP Profiles** tool.

![Clicking the 'ESP Profiles' tool](/_images/image-(634).png)

4. In the **Add Profile** field, either:
   1. Start typing the name of the relevant ESP Profile, then click the checkbox beside it to select it.
   2. Click the dropdown to see a list of existing ESP Profiles and click the checkboxes beside the relevant profiles to select them.

![Adding ESP Profiles](/_images/image-(635).png)

> \*\*Note\*\*
>
> If an ESP Profile already contains the maximum of 100 apps, you will be unable to select it from the dropdown. If you hover over it, you'll see the \*\*Total limit reached\*\* tooltip.
>
> !\['Total limit reached' tooltip]\(/\_images/image-(636 "'Total limit reached' tooltip").png>)

The selected ESP Profile(s) are added to the **Add Profile** field.

![Selected ESP Profile(s) added to the 'Add Profile' field](/_images/image-(637).png)

> \*\*Tip\*\*
>
> You can click the \*\*X\*\* beside an ESP Profile in the \*\*Add Profile\*\* field to delete it from the list.
>
> Also, the number in brackets shows the number of apps currently added to an ESP Profile, with 100 being the maximum.

> \*\*Note\*\*
>
> See \[Check ESP Profiles]\(../../../../technical-references/intune-reference/check-esp-profiles-in-intune.md) for details on how to check within Intune that a PMPC Cloud deployment has been successfully added to an ESP Profile.

5. Repeat this process to add any additional ESP Profiles.

The number of ESP Profiles selected is shown beside the **ESP Profiles** tool.

![Number of ESP Profiles selected shown beside the 'ESP Profiles' tool](/_images/image-(638).png)

> \*\*Note\*\*
>
> To avoid potential conflicts, we highly recommend creating all deployments within the PMPC Cloud portal and using the ESP Profiles feature to control which apps belong to which ESP profiles. You should only use the \*\*Enrollment Status Page\*\* in the Intune admin center to create an ESP Profile.
>
> Other important points about ESP Profiles:
>
> \* They are currently unavailable on macOS.
>
> \* Different ESP Profiles can be used in different Update Rings if required.
>
> \* If you edit an ESP Profile that is used in a deployment that uses Update Rings, the changes will only be applied to the version of the deployment that is applied to the ring with the lowest delay.
>
> \* If during a Sync Schedule the number of apps within an ESP Profile exceeds 100, we do not fail the deployment. The deployment will be completed with any new versions being assigned. However, we will display a warning indicator in the portal and the message \\
>
> \\
>
> “\*\*Failed to add application with version “<\*\*\_\*\*version\\\_number\*\*\_\*\*>” to “<\*\*\_\*\*esp\\\_profile\\\_name\*\*\_\*\*>\*\*”.

## Next Steps

If you do not want to configure any additional settings, click **Next** to move to the [Assignments](../../assignments-tab.md) tab.

Otherwise, navigate to the relevant tool to configure the required settings, which are explained in the relevant section.