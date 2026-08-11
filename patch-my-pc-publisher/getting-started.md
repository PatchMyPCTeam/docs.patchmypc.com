# Getting Started with Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

This section helps you get up and running with Patch My PC (PMPC) Publisher by guiding you through the key decisions and setup steps required for a successful deployment.

You’ll learn how to review and validate prerequisites, determine the correct installation location for your environment, and understand how Publisher integrates with Microsoft Intune, WSUS, ConfigMgr, or a combination of these.

You’ll also be guided through the initial configuration and common customization options, ensuring Publisher aligns with your operational requirements before you begin publishing applications and updates.

{% hint style="info" %}
**Note**

If you have security or compliance questions prior to installation, we recommend reviewing the [Security](security/) section first, which provides detailed information on catalog validation, binary verification, platform trust models, software supply chain protections, amongst others.
{% endhint %}

{% stepper %}
{% step %}
## Decide where to install Publisher

Before you begin, determine where Publisher should be installed. The correct installation location depends on how you plan to use Publisher and which platforms you manage (ConfigMgr, WSUS, Intune, or a combination).

* [Where should I install the Publisher?](install/where.md)
{% endstep %}

{% step %}
## Review Publisher's requirements

The core requirements apply regardless of how you plan to use the Publisher.

* [Core Publisher Requirements](requirements/core-requirements.md)

Platform-specific requirements:

* [ConfigMgr Requirements](requirements/configmgr-requirements/)
* [Intune Requirements](requirements/intune-requirements/)
* [WSUS Requirements](requirements/wsus-requirements/)
{% endstep %}

{% step %}
## Download Publisher

* [Download the Publisher](install/download.md)
{% endstep %}

{% step %}
## Install Publisher

* [Install the Publisher](install/installing.md)
{% endstep %}

{% step %}
## Configure Publisher for your environment

Once the Publisher is installed, configure it based on how you plan to use it. Choose the scenario that best matches your environment:

* [Scenario 1: ConfigMgr - Applications only](configure/quick-start-guides/manage-configmgr-applications-only.md)
* [Scenario 2: ConfigMgr - Applications and Updates (WSUS)](configure/quick-start-guides/manage-configmgr-applications-wsus-updates.md)
* [Scenario 3: WSUS (Standalone)](configure/quick-start-guides/manage-wsus-standalone.md)
* [Scenario 4: Intune – Applications and Updates](configure/quick-start-guides/manage-intune-apps-updates.md)
* [Scenario 5: Mixed environment (ConfigMgr, WSUS, and Intune)](configure/quick-start-guides/manage-mixed-environment.md)
{% endstep %}

{% step %}
## Customize and publish applications and updates

* Once the Publisher is configured, decide which products you want to publish. Choose the scenario that best matches your environment:
  * [Scenario 1: ConfigMgr Applications](configure/product-selection-discovery/discover-configmgr-applications.md)
  * [Scenario 2: ConfigMgr/WSUS Updates](configure/product-selection-discovery/discover-configmgr-wsus-updates.md)
  * [Scenario 3: Intune Applications and Updates](configure/product-selection-discovery/discover-intune-apps-updates.md)
* [Customize products in the Publisher with Right-Click Options](customizations/)
* [Publish applications and updates](manage/sync-schedule-tab/)
{% endstep %}
{% endstepper %}
