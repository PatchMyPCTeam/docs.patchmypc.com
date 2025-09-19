# Role Scope Tags (optional)

_Applies to: Patch My PC Cloud_

{% hint style="info" %}
**Note**

Using the **Role Scope Tags** tool is optional.
{% endhint %}

The **Role Scope Tags** tool of the Patch My PC (PMPC) Cloud deployment wizard allows you to leverage Intune Role Scope Tags (Scope Tags) in your deployments to help control which Intune admins can manage a specific deployment.

{% hint style="warning" %}
**Important**

Before you can use a Scope Tag in a PMPC Cloud deployment, it must have already been created in the Intune admin center. Follow the [To create a scope tag](https://learn.microsoft.com/en-us/mem/intune/fundamentals/scope-tags#to-create-a-scope-tag) process of [Use role-based access control (RBAC) and scope tags for distributed IT](https://learn.microsoft.com/en-us/mem/intune/fundamentals/scope-tags) for more details and information on Scope Tags.

If you manage Intune using PMPC Cloud, you should avoid performing any actions in the Intune admin center that can be performed in PMPC Cloud, as doing so will cause unwanted behavior.
{% endhint %}

To add Role Scope tag&#x73;**:**

1. Click the **Role Scope Tags** tool.

!\[]\(/\_images/image-(78 "").png "")

2. Scroll down to the **Role Scope Tags** section.

!\[]\(/\_images/image-(79 "").png "")

3. In the **Profile Name** field, either:
   1. Start typing the name of the relevant Scope Tag, then click the checkbox beside it to select it.
   2. Click the dropdown to see a list of existing Scope Tags and click the relevant checkbox(es) to select it.

!\[]\(/\_images/image-(80 "").png "")

{% hint style="success" %}
**Tip**

You can click the **X** beside a Scope Tag in the **Profile Name** field to delete it.
{% endhint %}

{% hint style="info" %}
**Note**

See [Check Scope Tag Assignments](../../../cloud-reference/intune-reference/check-scope-tag-assignments-in-intune.md) for details on how to check within Intune that the Scope Tags defined in the deployment have been assigned correctly.
{% endhint %}

4. If you do not want to configure any of the optional tabs under the **Tools** section, click **Next** to move to the [Assignments](../cloud-assignments-deployment-tab.md) tab.\
   \
   Otherwise, click on the relevant tab under **Tools** to configure the required settings, which are explained in the relevant process.

!\[]\(/\_images/image-(81 "").png "")
