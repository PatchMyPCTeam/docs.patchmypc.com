# Configure Install Parameters in a Patch My PC Cloud Deployment

_Applies to: Patch My PC Cloud_

The **Install Parameters** tool of the Patch My PC (PMPC) Cloud deployment wizard allows you to configure the following installation parameters and arguments:

* [Install Command Line](install-parameters.md#install-command-line)
* [Additional Argument](install-parameters.md#additional-argument)

## Install Command Line

This field shows any default installation parameters detected in the app's metadata in our App Catalog.

{% hint style="info" %}
**Note**

This field cannot be modified.
{% endhint %}

## Additional Argument

This field allows you to provide additional arguments to be appended to the installation command line. These can override the Patch My PC arguments in some cases (typically for MSI arguments).

{% hint style="info" %}
**Note**

If you specify a parameter that is already included in the **Install Command Line** field, you will see a warning that this has already been detected, and you should remove it.

<img src="../../../../../.gitbook/assets/image (719).png" alt="Already detected parameter" data-size="original">

This field is limited to a maximum of 2,048 characters. See [Supported Variables in Publisher and PMPC Cloud](../../../../../patch-my-pc-product-reference/supported-variables.md) for a list of the variables we support in this field.
{% endhint %}

## Next Steps

If you do not want to configure any additional settings, click **Next** to move to the [Assignments](../../assignments-tab.md) tab.

Otherwise, navigate to the relevant tool to configure the required settings, which are explained in the relevant section.

<figure><img src="../../../../../.gitbook/assets/image (1).png" alt="Clicking &#x27;Next&#x27;" width="563"><figcaption></figcaption></figure>
