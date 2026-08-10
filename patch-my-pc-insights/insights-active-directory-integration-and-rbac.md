---
description: Using AD accounts for authentication into Advanced Insights
---

# Insights Active Directory Integration & RBAC

_Applies to: Patch My PC Advanced and Patch Insights_

Advanced and Patch Insights support integration with Active Directory for user authentication. This feature is enabled by an administrator in **Administration** > **Settings** > **User management**. Once enabled, this will ensure that any users signing in can use their AD username and password. If users have an RBAC role defined in Configuration Manager, Advanced Insights will adhere to that role, only showing the clients they are permitted to view.

![User management settings tab](/_images/7.png "User management settings tab")

To enable Active Directory authentication capabilities:

1. Check the box for **Enable Active Directory Authentication**
2. Optionally Enter your **Active Directory domain name** (normally only required if the authenticating domain is different from the domain the Advanced Insights server is installed in)
3. Optionally Enter a username and password used to connect to Active Directory, this is only required if the Advanced Insights App Pool identity (Local System by default) has been restricted from reading Active Directory, which is uncommon

<blockquote class="wp-block-quote">
<p>The username and password under the domain name are **optional**.&#x20;</p>
<p>By default, we will use the computer account of the Advanced Insights server to authenticate active directory requests.</p>
</blockquote>

After you have entered these details, you can now log in with your Active Directory UPN or username.

<blockquote class="wp-block-quote">
<p>The account MUST have a valid Firstname and Surname set in its AD properties. Without this an error will be logged in the Advanced insights API log stating <mark style="color:red;">"Cannot insert the value NULL into column 'Name'"</mark></p>
</blockquote>

If this is your first time logging in to Advanced Insights, you will receive whatever role is assigned as "**default**" or roles your Active Directory Group membership assigns.

You can read more about assigning roles to Active Directory Groups in the article below:

{% content-ref url="advanced-insights-active-directory-group-to-role-assignment.md" %}
[advanced-insights-active-directory-group-to-role-assignment.md](advanced-insights-active-directory-group-to-role-assignment.md)
{% endcontent-ref %}