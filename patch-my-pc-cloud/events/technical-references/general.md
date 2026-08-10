# Events reference for General Events in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

This article lists the various that are generated with the **General** severity by Patch My PC (PMPC) Cloud for the following categories:

|                                       |                                               |                                                   |
| ------------------------------------- | --------------------------------------------- | ------------------------------------------------- |
| [Application](general.md#application) | [Client](general.md#client)                   | [Company](general.md#company)                     |
| [Environment](general.md#environment) | [Intune Branding](general.md#intune-branding) | [Intune Deployment](general.md#intune-deployment) |
| [License](general.md#license)         | [MSP Invite](general.md#msp-invite)           | [Publisher](general.md#publisher)                 |

## Application

| Title                                                                               | Operation Type | Generated when...                                                                                                                                                                           |
| ----------------------------------------------------------------------------------- | -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Application <_app\_name_> Created                                                   | Created        | An app is created                                                                                                                                                                           |
| Application <_app\_name_> Changed by <_user\_name_>                                 | Updated        | An app is updated                                                                                                                                                                           |
| Application <_app\_name_> Removed by <_user\_name_>                                 | Removed        | An app is removed                                                                                                                                                                           |
| Intune Application Discovered                                                       | Created        | Created the first time Discovery is run in your PMPC Company                                                                                                                                |
| Intune Discovered Applications Refreshed                                            | Updated        | Created whenever someone clicks Refresh Data to refresh your discovery data.                                                                                                                |
| Managed Company Relationship for <_child\_company\_name_> Removed by <_user\_name_> | Removed        | <p>A child company is unlinked from a parent MSP company</p><p><br><mark style="color:blue;"><strong>NOTE</strong></mark><br>This event is shown on both the parent and child companies</p> |

## Client

| Title                                                      | Operation Type | Generated when...                                                                                             |
| ---------------------------------------------------------- | -------------- | ------------------------------------------------------------------------------------------------------------- |
| Client Deployment Created for _\<preview\_or\_production>_ | Created        | PMPC Client has been deployed                                                                                 |
| Client Deployment Updated for _\<preview\_or\_production>_ | Updated        | List of Entra ID Groups PMPC Client deployed to has been updated or the **Uninstall Client** feature is used. |
| Client Deployment Deleted for _\<preview\_or\_production>_ | Removed        | PMPC Client deployment is deleted                                                                             |

## Company

| Title                                                              | Operation Type | Generated when...                    |
| ------------------------------------------------------------------ | -------------- | ------------------------------------ |
| Company  <_company\_name>_ Created by <_user\_name>_               | Created        | A company is created                 |
| Company  <_company\_name>_ Updated by <_user\_name>_               | Updated        | A company is updated                 |
| Managed Company <_child\_company\_name_> Created by <_user\_name_> | Created        | A child company of an MSP is created |

## Environment

| Title                                     | Operation Type | Generated when...         |
| ----------------------------------------- | -------------- | ------------------------- |
| Environment <_environment\_name_> Updated | Updated        | An environment is updated |

## Intune Branding

| Title                                              | Operation Type | Generated when...                    |
| -------------------------------------------------- | -------------- | ------------------------------------ |
| Custom Branding <_branding\_app\_name_> Created    | Created        | A Branding App is created.           |
| Custom Branding <_branding\_app\_name_> Recreated  | Recreated      | A Branding App is recreated.         |
| Custom Branding <_branding\_app\_name_> Deleted    | Removed        | A Branding App is deleted.           |
| Custom Branding <_branding\_app\_name_> Updated    | Updated        | A Branding App is updated.           |
| Default Branding - <_branding\_app\_name_> Created | Created        | The default Branding App is created. |
| Default Branding - <_branding\_app\_name_> Deleted | Removed        | The default Branding App is deleted. |

## Intune Deployment

| Title                                                                    | Operation Type | Generated when...                             |
| ------------------------------------------------------------------------ | -------------- | --------------------------------------------- |
| Deployment <_deployment\_name_> Created                                  | Created        | An Intune deployment is created.              |
| Deployment <_deployment\_name_> Deleted                                  | Removed        | An Intune deployment is removed.              |
| Deployment <_deployment\_name_> Recreated                                | Recreated      | An Intune deployment is recreated.            |
| Deployment <_deployment\_name_> was updated by scheduled synchronization | Synchornized   | A deployment is updated by the Sync Schedule. |

## License

| Title                 | Operation Type | Generated when...                           |
| --------------------- | -------------- | ------------------------------------------- |
| macOS (Trial) Applied | Applied        | A macOS trial begins                        |
| macOS (Full) Applied  | Applied        | A full (not trial) macOS license is applied |

## MSP Invite

| Title                                             | Operation Type | Generated when...                                 |
| ------------------------------------------------- | -------------- | ------------------------------------------------- |
| Invitation Accepted by _\<users\_email\_address>_ | Approved       | A user accepts an invitation to an MSP company    |
| Invitation Sent to _\<users\_email\_address>_     | Created        | An invitation to an MSP company is sent to a user |
| Invitation Deleted by _\<users\_email\_address>_  | Removed        | A user deletes an invitation to an MSP company    |
| Invitation Declined by _\<users\_email\_address>_ | Rejected       | A user declines an invitation to an MSP company   |

## Publisher

| Title                        | Operation Type | Generated when...                                     |
| ---------------------------- | -------------- | ----------------------------------------------------- |
| Publisher Connection Added   | Connected      | Publisher is connected to the PMPC Cloud portal.      |
| Publisher Connection Removed | Disconnected   | Publisher is disconnected from the PMPC Cloud portal. |