# Manage Automatic Deployment Rules option in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_&#x41;vailable at level: All Custom Products, All Products_\
_&#x41;vailable on tab: Intune Updates_

> \*\*Important\*\*
>
> This article has not been updated for Version 3.x. Once it has, this banner will be removed.

The **Manage Automatic Deployment Rules** right-click option in Patch My PC (PMPC) Publisher allows you to automatically create Intune assignments for newly published updates based on predefined catalog criteria.

Instead of assigning every update to the same Entra groups, Dynamic Assignments evaluates each update during a Publisher [synchronization](../../../patch-my-pc-publisherv2/administration/sync-schedule.md) and applies assignments only when the update matches your configured rules. This enables targeted deployment based on update attributes rather than static grouping.

> \*\*Note\*\*
>
> Dynamic Assignments are conceptually similar to Automatic Deployment Rules in ConfigMgr, but they apply to Intune Updates managed by the Publisher.

## How Dynamic Assignments Work

During each sync, the Publisher evaluates newly published Intune Updates against your configured criteria. Criteria can include attributes such as the presence of a CVE, CVE severity, keywords in the update title, or the update classification.

If an update meets the defined conditions, the Publisher automatically creates assignments for the Entra groups you specify. If an update does not meet the criteria, no assignment is created.

This approach allows different updates to follow different deployment paths based on risk, urgency, or relevance, without requiring manual assignment for each update.

> \*\*Important\*\*
>
> Intune only allows a single assignment per app per group. If the same group is targeted by both a static assignment, through the \[Manage Assignments right-click option]\(../../../patch-my-pc-publisherv2/customizations-right-click-options/manage-assignments/), and a dynamic assignment, the dynamic assignment will take precedence.

## Evaluation Criteria

Dynamic Assignments evaluate newly published updates using one or more of the following criteria.

* **Has CVE**\
  A Boolean value that evaluates whether the update has one or more CVE IDs associated with it.
* **Severity**\
  A multi select list that includes Critical, Important, Moderate, and Low.\
  **Title**\
  Plain text or regular expression strings used to match update titles. Exclusions can be defined by prefixing a value with a minus sign.
* **Update Classification**\
  A multi select list that includes Updates, Critical Updates, and Security Updates.

> \*\*Note\*\*
>
> Criteria options that allow multiple values use an \*\*OR\*\* operator. All different criteria types are joined together using an AND operator.
>
> In practical terms, this means an update must meet all selected criteria types, but only one value within each type.

> \*\*Important\*\*
>
> Dynamic Assignments are evaluated \*\*only for products that are currently enabled\*\* in Publisher Product Tree and \*\*only for the current version of a product\*\* at the time it is published.
>
> When Dynamic Assignments are used together with \[\*\*auto publishing rules\*\*]\(../../../patch-my-pc-publisherv2/administration/intune-apps-updates/form-controls/scan-intune-for-supported-products.md#auto-publishing-rules), there is an important timing consideration. During the first Publisher synchronization, auto publishing rules enable the product and publish the update. Because the product was not enabled at the start of the sync, Dynamic Assignment evaluation does not occur at that time.
>
> A \*\*second Publisher synchronization\*\* is required for Dynamic Assignments to evaluate the newly enabled product and determine whether the update meets the configured criteria for assignment.
>
> This behavior is expected and should be accounted for when designing automation workflows that combine auto publishing rules with Dynamic Assignments.

## Configure Dynamic Assignments

To configure Dynamic Assignments, follow the steps below.

1. Open the **Intune Updates** tab in Publisher.
2. Right-click All Products or All Custom Products and select Manage Dynamic Assignments.
3. Select **Add** to create a new Dynamic Assignment rule.

![New Dynamic Assignment Rule](../../../.gitbook/assets/image-\(4039\).png)

4. Enter a Name and optional Description for the rule.
5. Select one or more Property Filters to define the evaluation criteria.
6. Configure the search criteria values for each selected filter.

![New Dynamic Assignment Rule Settings](../../../.gitbook/assets/image-\(4042\).png)

7. Click **Preview** to see which updates currently match the rule.

![Preview Updates](../../../.gitbook/assets/image-\(4041\).png)

8. Click **Manage** to configure assignments for the rule.
9. Add the required Intune assignments using the standard Manage Assignments window.

![Manage Assignments](../../../.gitbook/assets/image-\(4043\).png)

10. Click **OK** to save the rule.

![Rule Configuration Complete](../../../.gitbook/assets/image-\(4044\).png)
