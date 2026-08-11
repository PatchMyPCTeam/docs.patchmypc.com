# Configure Return Codes in a Patch My PC Cloud Deployment

_Applies to: Patch My PC Cloud_

The **Return Codes** tool of the Patch My PC (PMPC) Cloud deployment wizard allows you to configure _Return Codes_ for a deployment (a _Return Code_ is a numerical code an app typically logs and reports once it has completed running its installer).

You can manage Return Codes from within the properties of a:

* Deployment
* Custom App

{% hint style="info" %}
**Note**

See the [Configuration ](../../../../custom-apps/create-a-custom-app/custom-apps-configuration-tab.md)section of [Create a Custom App](../../../../custom-apps/create-a-custom-app/) for details on how to configure Return Codes within the properties of a Custom App.

Also, macOS apps also do not support Return Codes.
{% endhint %}

To manage Return Codes for a Deployment:

1. Click the **Return Codes** tool.

<figure><img src="../../../../../.gitbook/assets/image (657).png" alt="Clicking the &#x27;Return Codes&#x27; tool" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

The number beside the **Return Codes** tool shows the number of return codes currently configured for the app being deployed.
{% endhint %}

The default Return Codes defined for the app are shown, plus any defined for the app if this is a Custom App.

<figure><img src="../../../../../.gitbook/assets/image (659).png" alt="Default return codes" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Note**

If a vendor supplies a list of Return Codes for their app, we include it. If they don’t, we automatically populate the list of Return Codes with industry-standard codes.
{% endhint %}

3. If you do not want to add a new Return Code, proceed to Step 5.
4. To add a new Return Code for this deployment, enter the numerical value in the **Return Code** field, select its meaning from the **Code type** dropdown, then click **Add**.

<figure><img src="../../../../../.gitbook/assets/image (766).png" alt="Adding a new Return Code" width="436"><figcaption></figcaption></figure>

The new Return Code is added to the list.

<figure><img src="../../../../../.gitbook/assets/image (767).png" alt="New Return Code added to the list." width="419"><figcaption></figcaption></figure>

5. If you do not want to edit a Return Code, go to Step 9.
6. To edit a Return Code, click the pencil icon beside it.

<figure><img src="../../../../../.gitbook/assets/image (768).png" alt="Clicking the pencil icon beside a Return Code to edit it." width="419"><figcaption></figcaption></figure>

7. Make any required changes.
8. Click the green tick to save your changes.

<figure><img src="../../../../../.gitbook/assets/image (769).png" alt="Clicking the green tick to save your changes" width="422"><figcaption></figcaption></figure>

The **Code type** field is updated.

<figure><img src="../../../../../.gitbook/assets/image (770).png" alt="“Code type” field updated." width="420"><figcaption></figcaption></figure>

9. To delete a Return Code, click the red trash can beside the relevant code.

{% hint style="info" %}
**Note**

You cannot delete either the default Return Codes for a deployment or any that have been added as part of the Custom App’s configuration. However, you can edit them.

If you add a Return Code to a deployment, you will be able to edit or delete it from the deployment if required.
{% endhint %}

{% hint style="danger" %}
**Important**

If the Return Codes you define in a deployment differ/conflict with those defined for a Custom App, the Return Codes defined on the deployment take precedence.
{% endhint %}

<figure><img src="../../../../../.gitbook/assets/image (771).png" alt="Deleting a Return Code" width="420"><figcaption></figcaption></figure>

The code is deleted from the list.

<figure><img src="../../../../../.gitbook/assets/image (772).png" alt="Code deleted from the list" width="425"><figcaption></figcaption></figure>

## Next Steps

If you do not want to configure any additional settings, click **Next** to move to the [Assignments](../../assignments-tab.md) tab.

Otherwise, navigate to the relevant tool to configure the required settings, which are explained in the relevant section.

<figure><img src="../../../../../.gitbook/assets/image (662).png" alt="Clicking &#x27;Next&#x27;" width="563"><figcaption></figcaption></figure>
