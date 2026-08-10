# Configure Dependencies in a Patch My PC Cloud Deployment

_Applies to: Patch My PC Cloud_

> \*\*Note\*\*
>
> Using the \*\*Dependencies\*\* tool is optional.

The **Dependencies** tool of the Patch My PC (PMPC) Cloud deployment wizard allows you to create dependencies within a deployment, whereby the app being deployed requires one or more other apps to have already been installed on the targeted resource before it can be deployed.

If the required app(s) (known as the _parent_) have not already been installed on the device, they will automatically be installed before the app that is being deployed (known as the _child app_) is installed.

> \*\*Important\*\*
>
> Before you can create an App Dependency in a PMPC Cloud deployment, the deployment for the parent app(s) must:
>
> \* exist already
>
> \* have been deployed successfully
>
> The parent app can be packaged without assignments and used in a Dependency chain rule, provided the parent app is deployed first.
>
> Also, apps that have not been successfully deployed (such as those with a status of \*\*Failed\*\*, \*\*Retrying\*\*, \*\*Processing\*\*, etc.) cannot be used to create an app dependency, nor can apps with \*\*Uninstall\*\* or \*\*Update Only\*\* assignments.

> \*\*Note\*\*
>
> Like Intune, we do not support circular dependencies (i.e. App A has a dependency on App B, and App B has a dependency on App A).
>
> As per Intune, you can create a maximum of 100 dependencies, which includes the dependencies of any included dependencies, as well as the app itself. See [Step 5: Dependencies](https://learn.microsoft.com/en-us/mem/intune/apps/apps-win32-add#step-5-dependencies) of [Add, assign, and monitor a Win32 app in Microsoft Intune](https://learn.microsoft.com/en-us/mem/intune/apps/apps-win32-add) for more information.
>
> Also, the parent app must have been deployed successfully before you can create a dependency between apps.

To add a dependency:

1. Add the [**Dependencies** tool](../#adding-additional-tools).

> \*\*Note\*\*
>
> If we are aware that an app requires a dependency, we automatically add the \*\*Dependencies\*\* tool with a yellow dot after the tool name. If you click the \*\*Dependencies\*\* tool, we show you the name of the app we recommend you add as a dependency for this deployment.
>
> !\[Auto adding the 'Dependencies' tool if we know an app has a dependency, including the name of the app]\(/\_images/image-(3652 "Auto adding the 'Dependencies' tool if we know an app has a dependency, including the name of the app").png>)

2. Click the **Dependencies** tool.

![Clicking the 'Dependencies' tool](../../../../../.gitbook/assets/image-\(3642\).png)

3. From the **Add Dependencies** field, either:
   1. Start typing the name of the relevant app that this app depends on already being successfully installed on the target device.
   2. Click the dropdown and select the relevant app that this app depends on already being successfully installed on the target device.

![Selecting the relevant app that this app depends on already being successfully installed on the target device](../../../../../.gitbook/assets/image-\(3643\).png)

The selected app appears under the **Parent Deployment** section.

![Selected app appearing under the 'Parent Deployment' section](../../../../../.gitbook/assets/image-\(3644\).png)

> \*\*Note\*\*
>
> Click the trashcan beside the relevant app under the \*\*Parent Deployment\*\* section to delete a dependency.

4. Repeat Step 3. to add any additional dependencies.

> \*\*Tip\*\*
>
> Once a dependency has been configured, you can view it as part of the app’s properties in the Microsoft Intune admin center.
>
> !\[Viewing dependencies for an app in the Microsoft Intune admin center]\(/\_images/image-(1041 "Viewing dependencies for an app in the Microsoft Intune admin center").png>)
>
> For more information, see [Step 5: Dependencies](https://learn.microsoft.com/en-us/mem/intune/apps/apps-win32-add#step-5-dependencies) of [Add, assign, and monitor a Win32 app in Microsoft Intune](https://learn.microsoft.com/en-us/mem/intune/apps/apps-win32-add).

> \*\*Note\*\*
>
> If a dependency is set up in the Intune admin center between an app managed by PMPC Cloud and an app managed directly in Intune, we will always copy-forward any dependencies from the PMPC Cloud app whenever we update the PMPC Cloud app.

> \*\*Warnings\*\*
>
> If we encounter any problems with app dependencies, we display a yellow exclamation mark (“\*\*!\*\*”) warning. Hovering over this will display more information.
>
> !\[]\(/\_images/image-(1036).png)
>
> We typically generate warnings in the following scenarios:
>
> \* If a dependency fails to be created. In this case, a warning is shown on the impacted child app(s) at the deployment level.
>
> \* If a dependency fails to be carried forward. In this case, a warning is shown on the impacted child app(s) at the deployment level.
>
> \* When multiple parent dependencies exist, any warnings will specify which particular dependency failed to be created to help you troubleshoot the issue.
>
> If an entire deployment fails before the dependencies stage is reached, no warnings are shown, as we only show warnings for successful deployments.

## Next Steps

If you do not want to configure any additional settings, click **Next** to move to the [Assignments](../../assignments-tab.md) tab.

Otherwise, navigate to the relevant tool to configure the required settings, which are explained in the relevant section.
