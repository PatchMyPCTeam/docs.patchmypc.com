# Manage MSP Events

_Applies to: Patch My PC Cloud_

The **Events** node of the parent Managed Service Provider (MSP) Patch My PC (PMPC) Cloud company only shows events that occurred in the parent company or events performed in the parent company that affect the child company. For example:

* The creation of a child company, which shows as a regular company being created on the child company, but on the parent company the following event is created:\
  \
  **"Managed company <**_**company\_name>**_**&#x20;was created."**
* The removal of the relationship between the parent company and a child company, which appears the same on both the parent and child company.

The **Events** node of the child company shows all of the events performed by both the parent company administrator on the child company and any events performed on the child company by the administrator users of that company.

{% hint style="info" %}
**Note**

Events that occur on any child companies are not replicated up to the parent company.
{% endhint %}
