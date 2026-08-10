# Assignments Best Practice

_Applies to: Patch My PC Publisher V2.x_
\
_Available at level: All Custom Products, All Products, Vendor, Product_
\
_Available on tab: Intune Apps, Intune Updates_

## Overview

Assignment strategy varies by organization and is often driven by internal policy, regulatory requirements, or security frameworks. The guidance in this section is illustrative, not prescriptive. It provides a practical example of how assignments configured in the Publisher can be used to deliver updates in a staged and controlled manner.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>Always align assignment configuration with your own risk tolerance, compliance obligations, and operational processes.</p>
</blockquote>

## Where to Configure Assignments in the Product Tree

Assignments can be configured at multiple levels in the product tree. You can define them at the **All Products** level, the **Vendor** level, or the **Product** level. Where you choose to configure assignments has a direct impact on consistency, flexibility, and ongoing management effort.

Many customers choose to configure assignments for updates at the **All Products** level. This approach ensures that every third-party update published by the Publisher follows the same deployment strategy. It provides predictable behavior across the entire catalog and significantly reduces administrative overhead.

Assignments configured higher in the product tree are inherited by everything beneath them. This also means that changes made at a higher level can overwrite assignments that were previously configured at a lower level. For example, if you configure assignments at the Product level and later modify assignments at the Vendor or All Products level, the higher level configuration will replace the lower level assignments.

Because of this behavior, it is important to choose a clear strategy and apply it consistently.

_One_ recommended approach is to configure assignments at the **All Products** level so that all products follow the same deployment pattern. This works well for organizations that want standardized behavior across all third party updates.

An alternative approach is to avoid configuring assignments at higher levels and instead manage assignments individually at the **Product** level. This provides maximum flexibility but increases management overhead, as assignments must be reviewed and maintained for each product separately.

Whichever approach you choose, avoid mixing assignment strategies across multiple levels unless you fully understand how inheritance and overrides behave. A consistent assignment model helps prevent unintended changes and makes ongoing management more predictable.

## Phased Deployments / Update Rings

A common and effective approach is to deploy updates in phases. Otherwise known as **Phased Deployments** or **Update Rings**, where availability is consistent but enforcement is staggered using different deadlines.

![Example of a phased deployment](/_images/image-(4035).png "Example of a phased deployment")

In the example shown, 3 **Required for enrolled devices** assignments are configured at the Vendor level for all Google products on the **Intune Updates** tab. The same approach outlined here can also be applied at the All Products or individual Product level.

All rings use the same availability configuration, set to [Publishing date plus 0 days](assignments-best-practice.md#why-publishing-date-plus-0-days), ensuring content is eligible for download immediately while avoiding known Intune issues with **As soon as possible** availability.

Deadlines are then staggered per ring.

* Ring 1 uses a deadline of 3 days.
* Ring 2 uses a deadline of 10 days.
* Ring 3 uses a deadline of 17 days.

This ensures all assignments are created at publish time, but enforcement occurs progressively, 7 days between each ring.

### Ring Design Considerations

In the example above, Ring 1 typically consists of IT staff or power users who understand how to report issues quickly. These users receive updates first and act as an early warning system.

The time gap between Ring 1 and Ring 2 provides an opportunity to detect issues before broader rollout. If no issues are reported, enforcement continues automatically into later rings.

Ring 3 usually represents the widest production audience and aligns with compliance driven deadlines such as Cyber Essentials Plus, where updates must be deployed within a defined timeframe.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>The specific number of days used for each ring and the number of rings themselves should be adjusted to match your organization’s policy.</p>
<p>Striking the right balance between sufficient testing time in each ring and timely update compliance is an important consideration and will vary between environments.</p>
</blockquote>

### Why use Publishing Date Plus 0 Days?

When multiple Required assignments exist for the same application and devices belong to more than one assignment, Intune determines applicability based on availability first. If availability processing is delayed due to a known bug, deadline enforcement is also delayed because the assignment is not considered applicable until availability is reached.

In scenarios where one assignment uses **As soon as possible** and another uses a future availability time, Intune may defer both content download and subsequent deadline enforcement until the later availability time is reached.

This behavior is an Intune platform limitation and is documented in the Patch My PC blog at [https://patchmypc.com/blog/intune-asap-assignments-bug/](https://patchmypc.com/blog/intune-asap-assignments-bug/https://patchmypc.com/blog/intune-asap-assignments-bug/).

To ensure predictable deadline enforcement, avoid mixing **As soon as possible** with future availability times. A recommended approach is to configure availability as **Publishing date plus 0 days**, which sets availability to the publish time and allows both availability processing and deadline enforcement to occur as expected.

## Communication and Monitoring

The success of a phased deployment relies effective communication and monitoring.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Configure [Alerts](../../administration/alerts/) in the Publisher to notify you when new updates are published. Email notifications or webhooks should act as a signal that a new version has entered your deployment pipeline.</p>
</blockquote>

Users in the first phase/ring should be explicitly informed that they are receiving updates earlier than the wider organization and that their feedback is important. This sets expectations and encourages proactive reporting.

Communication to this group of users should explain why they are included in the first ring, and what type of feedback is expected. This may include to look out for installation issues, functional regressions, performance changes, unexpected prompts or reboots, or changes in user experience.

Providing a clear and simple feedback path is critical. First phase/ring users should know exactly how to report issues, whether through a dedicated support channel, ticket category, or internal communication tool. Reducing friction in reporting increases the likelihood that issues are surfaced quickly.

The time between the first ring and subsequent rings should be used intentionally to gather and review feedback. If no issues are reported, rollout can continue as planned. If problems are identified, assignments can be [stopped](assignments-best-practice.md#stopping-or-adjusting-a-deployment) before the update reaches a broader audience.

Effective communication and timely feedback from the first phase/ring transforms early deployment from a risk into a safety net. This approach improves confidence in updates and helps prevent widespread impact from problematic releases.

## Stopping or Adjusting a Deployment

If an update causes issues, stopping deployment is a **manual action**.

**Do not** delete the application. You may need it to perform an uninstall or rollback.

Instead, remove assignments either directly in the Intune admin center or by using the [Intune Application Manager](../../administration/intune-apps-updates/form-controls/intune-application-manager.md). This prevents further rollout while preserving control.

## Rollback and Retention Strategy

Always configure [retention](../../administration/intune-apps-updates/options/application-options.md#retention-best-practice) for Intune apps and updates. Keeping at least **one previous version** is strongly recommended.

If a deployed update causes significant problems, you can use configure a supersedence relationship to have the previous version replace the newer version. This allows the broken update to be removed and the known good version restored.

This approach provides a controlled rollback path without rebuilding applications.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>Supersedence relationships must be configured directly in the Intune admin center.</p>
</blockquote>

## Testing New Applications and Major Versions

Using **Available for enrolled devices** assignments is a recommended first stage when introducing new applications or testing new versions of existing applications.

Making applications available in the Company Portal allows administrators to manually install and test applications on demand before enforcing them broadly. This is especially useful for validating installer behavior in a production like environment.

This approach is strongly recommended for **major version upgrades**, where application behavior may change significantly between releases.

Some vendors support and maintain **multiple major versions in parallel** due to breaking changes between versions. In these cases, the Publisher catalog may contain several major versions of the same product side by side, such as multiple FortiClient VPN releases alongside a **Latest** entry.

![Major Version Testing](/_images/image-(4034).png "Major Version Testing")

For products like VPN clients, major version upgrades can affect drivers, connectivity, or security posture. Treating these upgrades as a new deployment scenario allows administrators and pilot users to verify that the new version installs correctly, functions as expected, and properly upgrades or replaces the previous version.

This stage should be treated as testing only. The goal is to validate installation behavior, user experience, and version transition before enforcement.

Once testing is complete and confidence is established, deployment can move to the next stage by adding a Required assignment with appropriate availability and deadline settings.

This staged approach reduces risk and provides a controlled path from testing to enforcement for both new applications and high impact upgrades.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>For more information about products labeled with a **Latest** suffix in the Patch My PC catalog, refer to the dedicated [Latest Products](../../publisher-reference/catalog-information.md#latest) documentation page.</p>
</blockquote>

This stage should be treated as testing only. The objective is to validate installation behavior, user experience, and version transition before enforcement.

Once testing is complete and confidence is established, the deployment can move to the next stage by adding a Required assignment with appropriate availability and deadline settings.

This staged approach reduces risk, improves visibility into potential issues, and provides a controlled path from testing to enforcement for both new applications and high impact upgrades.

## Using Autopatch Groups

If you use Microsoft Autopatch, the staged Entra groups created for first-party updates can also be reused for third-party patching.

This allows you to align early and late rings across Microsoft and third party updates. However, be mindful that third party updates are released on unpredictable schedules, unlike Microsoft’s monthly cadence.

Mixing first-party and third-party updates in the same time window can make troubleshooting more difficult. Separating rollout timing can help identify whether an issue is caused by a Microsoft update or a third party vendor update.