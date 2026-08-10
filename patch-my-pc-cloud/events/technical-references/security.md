# Events reference for Security Events in Patch My PC Cloud

_Applies to: Patch My PC Cloud_

This article lists the various that are generated with the **Security** severity by Patch My PC (PMPC) Cloud.

| Title                                                                                                                  | Category   | Operation Type | Generated when                                                           |
| ---------------------------------------------------------------------------------------------------------------------- | ---------- | -------------- | ------------------------------------------------------------------------ |
| Company Ownership Approved for  <_user\_name_>                                                                         | Access     | Approved       | A user successfully completed the "Recover Your Company" process.        |
| Company Ownership Rejected for  <_user\_name_>                                                                         | Access     | Rejected       | A user failed to complete the "Recover Your Company" process.            |
| Customer Support Settings Updated for Company <_company\_name_>                                                        | Company    | Updated        | The settings for a company are updated.                                  |
| Group role with id <_entra\_id\_security\_group\_id_> was created with role <_user\_role\_assigned_>                   | Group Role | Created        | When an Entra ID Security Group is added to the portal                   |
| Group Role Removed                                                                                                     | Group Role | Removed        | When an Entra ID Security Group is removed from the portal               |
| Group role with name <_group\_name_> and id <_entra\_id\_security\_group\_id_> was changed to role <_new\_user\_role_> | Group Role | Updated        | When the role of an Entra ID Security Group is changed within the portal |
| Intune Connection Added                                                                                                | Intune     | Connected      | An Intune tenant is connected to the portal.                             |
| Intune Connection Removed                                                                                              | Intune     | Disconnected   | An Intune tenant is disconnected from the portal.                        |
| Invitation Sent to <_user\_name_>                                                                                      | Invitation | Created        | A user invitation is sent.                                               |
| Preview Features Setting Updated by \<user\_name>                                                                      | Company    | Updated        | A user changes the **Preview Features** setting for a company            |
| User Account Created for <_user\_name_>                                                                                | User       | Created        | A user is created.                                                       |
| <_user\_name_> Removed by <_admin\_name_>                                                                              | User       | Removed        | A user is deleted.                                                       |
| <_user\_name_> Role Changed by <_admin\_name_>\`                                                                       | User       | Role changed   | A user's role is changed.                                                |
