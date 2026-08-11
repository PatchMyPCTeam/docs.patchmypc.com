# Notifications

_Applies to: Patch My PC Publisher V2.x_

## Overview

In a multi-tenant configuration, notification behavior differs between email and webhook notifications. It is important to understand how each type is scoped.

## Email Notifications

Only a single email configuration, on the [Alerts tab](../../alerts/), can be defined for the entire Publisher instance. This configuration applies to all tenants.

If an MSP enables email notifications, the configured email address will receive a single notification after each synchronization cycle. That email will contain publishing details for all tenants processed during that sync.

The email clearly separates activity by tenant so administrators can see which applications or updates were published for each customer.

![Multi-tenant Email Notifications](../../../../.gitbook/assets/image-\(4125\).png)

> \*\*Note\*\*
>
> Email notifications cannot be configured per tenant. It is not possible to send separate synchronization emails to individual customer email addresses. For this reason, MSPs typically configure a centralized operations or service mailbox to receive synchronization notifications.

## Webhook Notifications

Webhook notifications _do_ support per-tenant configuration.

When configuring webhook notifications, you can specify which tenant the webhook applies to. This allows you to create separate webhook entries for different tenants configured in the Publisher.

Each webhook can have:

* A different webhook URL
* A different notification level
* Independent scope and event configuration

This enables flexible notification routing. For example:

* Webhook notifications can be sent to the MSP parent company.
* Webhook notifications can be sent directly to individual MSP customers.

Within the webhook configuration window, use the **Tenant Selection** section to control scope. If no tenants are selected, the webhook applies to all tenants. If one or more tenants are selected, the webhook applies only to the selected tenants.

![Tenant Specific Webhook Notifications](../../../../.gitbook/assets/image-\(4128\).png)

This provides granular control over how and where notifications are delivered in a multi-tenant Publisher scneario.

For detailed guidance on how to create and configure a webhook in the Publisher, see [Webhook Notifications](../../alerts/webhook-notifications/).
