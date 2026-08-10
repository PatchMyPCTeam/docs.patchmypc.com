# Configure Return Codes in a Patch My PC Cloud Deployment

_Applies to: Patch My PC Cloud_

The **Return Codes** tool of the Patch My PC (PMPC) Cloud deployment wizard allows you to configure _Return Codes_ for a deployment (a _Return Code_ is a numerical code an app typically logs and reports once it has completed running its installer).

You can manage Return Codes from within the properties of a:

* Deployment
* Custom App

> \*\*Note\*\*
>
> See the \[Configuration ]\(../../../../custom-apps/create-a-custom-app/custom-apps-configuration-tab.md)section of \[Create a Custom App]\(../../../../custom-apps/create-a-custom-app/) for details on how to configure Return Codes within the properties of a Custom App.
>
> Also, macOS apps also do not support Return Codes.

To manage Return Codes for a Deployment:

1. Click the **Return Codes** tool.

![Clicking the 'Return Codes' tool](../../../../../.gitbook/assets/image-\(657\).png)

> \*\*Note\*\*
>
> The number beside the \*\*Return Codes\*\* tool shows the number of return codes currently configured for the app being deployed.

The default Return Codes defined for the app are shown, plus any defined for the app if this is a Custom App.

![Default return codes](../../../../../.gitbook/assets/image-\(659\).png)

> \*\*Note\*\*
>
> If a vendor supplies a list of Return Codes for their app, we include it. If they don’t, we automatically populate the list of Return Codes with industry-standard codes.

3. If you do not want to add a new Return Code, proceed to Step 5.
4. To add a new Return Code for this deployment, enter the numerical value in the **Return Code** field, select its meaning from the **Code type** dropdown, then click **Add**.

![Adding a new Return Code](../../../../../.gitbook/assets/image-\(766\).png)

The new Return Code is added to the list.

![New Return Code added to the list.](../../../../../.gitbook/assets/image-\(767\).png)

5. If you do not want to edit a Return Code, go to Step 9.
6. To edit a Return Code, click the pencil icon beside it.

![Clicking the pencil icon beside a Return Code to edit it.](../../../../../.gitbook/assets/image-\(768\).png)

7. Make any required changes.
8. Click the green tick to save your changes.

![Clicking the green tick to save your changes](../../../../../.gitbook/assets/image-\(769\).png)

The **Code type** field is updated.

!["Code type" field updated.](../../../../../.gitbook/assets/image-\(770\).png)

9. To delete a Return Code, click the red trash can beside the relevant code.

> \*\*Note\*\*
>
> You cannot delete either the default Return Codes for a deployment or any that have been added as part of the Custom App’s configuration. However, you can edit them.
>
> If you add a Return Code to a deployment, you will be able to edit or delete it from the deployment if required.

> \*\*Important\*\*
>
> If the Return Codes you define in a deployment differ/conflict with those defined for a Custom App, the Return Codes defined on the deployment take precedence.

![Deleting a Return Code](../../../../../.gitbook/assets/image-\(771\).png)

The code is deleted from the list.

![Code deleted from the list](../../../../../.gitbook/assets/image-\(772\).png)

## Next Steps

If you do not want to configure any additional settings, click **Next** to move to the [Assignments](../../assignments-tab.md) tab.

Otherwise, navigate to the relevant tool to configure the required settings, which are explained in the relevant section.

![Clicking 'Next'](../../../../../.gitbook/assets/image-\(662\).png)
