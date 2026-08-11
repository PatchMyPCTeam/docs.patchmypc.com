# Manage AI Usage in your Patch My PC Cloud Company

_Applies to: Patch My PC Cloud_

> \*\*Important\*\*
>
> This documentation is for a pre-release feature still under development and, therefore, incomplete. As a result, both functionality and documentation are subject to change.
>
> Once this feature is released, it will be announced and this banner removed.

> \*\*Note\*\*
>
> AI-assisted functionality in PMPC Cloud is optional and can be disabled at any time.

Patch My PC (PMPC) Cloud leverages artificial intelligence (AI) in a limited, targeted way to support specific workflows, improving feature accuracy while ensuring customers remain fully in control of when AI is used.

AI is used as a supporting capability, not as an autonomous system. It does not take any actions in your environment, deploy applications, modify content, or make publishing decisions. Instead, it is used to help interpret complex inputs and provide additional context to features that would otherwise rely solely on static pattern matching or rule-based logic.

> \*\*Note\*\*
>
> For frequently asked questions about AI usage for PSADT app migration, please visit the Patch My PC Trust Center at [https://trust.patchmypc.com/faq#psadt-migration--ai-usage-faq](https://trust.patchmypc.com/faq#psadt-migration--ai-usage-faq)

## AI Usage in PSADT App Migration

During [PSADT app migrations](../../../migration/), we often encounter scripts whose installers cannot be easily or reliably parsed. Real-world PSADT scripts commonly include complex logic, variables, conditional branches, and multiple execution paths, which makes traditional pattern-matching approaches unreliable.

In these scenarios, AI is used as a parsing and interpretation aid, not a decision-maker. Its role is to analyze the install section of a PSADT script and help identify the primary installer being leveraged for installation. This allows PMPC Cloud to more accurately match the application to the PMPC App Catalog during migration.

To toggle AI usage:

1. Navigate to **Settings | Company**
2. Scroll down to the **AI Usage** section.

![Scrolling down to the 'AI Usage' section](/_images/image-(528 "Scrolling down to the 'AI Usage' section") (1).png>)

3. Click the **Enable AI Usage** slider to enable it.

![Clicking the 'Enable AI Usage' slider to enable it](/_images/image-(527 "Clicking the 'Enable AI Usage' slider to enable it") (1).png>)

4. Click **Save** to save your changes.

![Clicking 'Save' to save your changes](/_images/image-(529 "Clicking 'Save' to save your changes") (1).png>)

The **Success - Company information updated** notification is shown.

!['Success - Company information updated' notification](/_images/image-(530 "'Success - Company information updated' notification") (1).png>)