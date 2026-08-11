# Getting Started

_Applies to: Patch My PC Publisher V2.x_

## Overview

This section helps you get up and running with the Publisher by guiding you through the key decisions and setup steps required for a successful deployment.

You’ll learn how to review and validate prerequisites, determine the correct installation location for your environment, and understand how the Publisher integrates with Intune, WSUS, ConfigMgr, or a combination of these.

You’ll also be guided through initial configuration and common customization options, ensuring the Publisher is aligned with your operational requirements before you begin publishing applications and updates.

{% hint style="info" %}
**Note**

If you have security or compliance questions prior to installation, we recommend reviewing the [Security section](security/) of this documentation before proceeding. It provides detailed information on catalog validation, binary verification, platform trust models, and software supply chain protections.
{% endhint %}

{% stepper %}
{% step %}
## Decide where to install the Publisher

Before you begin, determine where the Publisher should be installed. The correct installation location depends on how you plan to use the Publisher and which platforms you manage (ConfigMgr, WSUS, Intune, or a combination).

* [Where should I install the Publisher?](download-and-install.md#where-should-i-install-the-publisher)
{% endstep %}

{% step %}
## Review the Publisher requirements

The core requirements apply regardless of how you plan to use the Publisher.

* [Core Publisher Requirements](publisher-requirements/core-requirements.md)

Platform-specific requirements:

* [ConfigMgr Requirements](publisher-requirements/configmgr-requirements/)
* [WSUS Requirements](publisher-requirements/wsus-requirements/)
* [Intune Requirements](publisher-requirements/intune-requirements/)
{% endstep %}

{% step %}
## Download and install the Publisher

* [Download and Install Publisher](download-and-install.md#download-the-publisher)
{% endstep %}

{% step %}
## Configure the Publisher for your environment

Once the Publisher is installed, configure it based on how you plan to use it. Choose the scenario that best matches your environment:

* [Scenario 1: ConfigMgr - Applications only](scenario-based-guidance/installation-and-configuration/scenario-1-configmgr-applications-only.md)
* [Scenario 2: ConfigMgr - Applications and Updates (WSUS)](scenario-based-guidance/installation-and-configuration/scenario-2-configmgr-applications-and-updates-wsus.md)
* [Scenario 3: WSUS (Standalone)](scenario-based-guidance/installation-and-configuration/scenario-3-wsus-standalone.md)
* [Scenario 4: Intune – Applications and Updates](scenario-based-guidance/installation-and-configuration/scenario-4-intune-applications-and-updates.md)
* [Scenario 5: Mixed environment (ConfigMgr, WSUS and Intune)](scenario-based-guidance/installation-and-configuration/scenario-5-mixed-environment-configmgr-wsus-and-intune.md)
{% endstep %}

{% step %}
## Customize and publish applications and updates

* Once the Publisher is configured, decide which products you want to publish. Choose the scenario that best matches your environment:
  * [Scenario 1: ConfigMgr Applications](scenario-based-guidance/product-selection-and-discovery/scenario-1-configmgr-applications.md)
  * [Scenario 2: ConfigMgr / WSUS Updates](scenario-based-guidance/product-selection-and-discovery/scenario-2-configmgr-wsus-updates.md)
  * [Scenario 3: Intune Applications and Updates](scenario-based-guidance/product-selection-and-discovery/scenario-3-intune-applications-and-updates.md)
* [Customize products in the Publisher with Right-Click Options](customizations-right-click-options/)
* [Publish applications and updates](administration/sync-schedule.md)
{% endstep %}
{% endstepper %}

