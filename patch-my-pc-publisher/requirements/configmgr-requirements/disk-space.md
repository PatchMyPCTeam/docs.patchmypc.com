# ConfigMgr Disk Space Requirements for  Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_

The **120 GB** overall disk space requirement listed on our [core Publisher requirements](../core-requirements.md) page accounts for the space needed by Patch My PC (PMPC) Publisher to download and package vendor installers before they are published, as well as for the Windows Operating system.

When publishing applications to Microsoft ConfigMgr, additional space is required in multiple locations.

ConfigMgr requires space for the application Content Source and the Distribution Points (DPs) you intend to deploy content to. The number of retained app versions you intend to keep will also determine the overall amount of disk space required.&#x20;

{% hint style="success" %}
**Tip**

120 GB is an estimate based on enabling approximately 700 products in Publisher. The average application size (calculated from all apps in our catalog), is around 180 MB, with individual apps ranging from 1 MB to 1.9 GB.
{% endhint %}

The following table illustrates the estimated disk space requirements based on the number of applications you plan to enable in Publisher and the number of retained versions you choose to keep.

{% hint style="danger" %}
**Important**

These estimates are based on the average application size across our catalog. Please note that actual sizes can vary significantly, with individual apps ranging from 1 MB to 1.9 GB. These numbers should therefore be used for illustrative purposes only.

As ConfigMgr uses single-instance storage within the Content Library on each DP, meaning duplicate files are stored only once per DP. This can reduce actual disk usage compared to the estimates shown below. However, as storage savings depend on application overlap and version similarity, single-instance storage is not factored into these rough calculations.
{% endhint %}

<table><thead><tr><th width="137" valign="top">Enabled Apps</th><th width="142" valign="top">Retained Apps</th><th valign="top">Content Source</th><th width="137" valign="top">Each DP</th></tr></thead><tbody><tr><td valign="top">250</td><td valign="top">0</td><td valign="top">40.0 GB</td><td valign="top">40.0 GB</td></tr><tr><td valign="top">250</td><td valign="top">1</td><td valign="top">80.0 GB</td><td valign="top">80.0 GB</td></tr><tr><td valign="top">250</td><td valign="top">2</td><td valign="top">120.0 GB</td><td valign="top">120.0 GB</td></tr><tr><td valign="top">250</td><td valign="top">3</td><td valign="top">160.0 GB</td><td valign="top">160.0 GB</td></tr><tr><td valign="top">500</td><td valign="top">0</td><td valign="top">90.0 GB</td><td valign="top">90.0 GB</td></tr><tr><td valign="top">500</td><td valign="top">1</td><td valign="top">180.0 GB</td><td valign="top">180.0 GB</td></tr><tr><td valign="top">500</td><td valign="top">2</td><td valign="top">270.0 GB</td><td valign="top">270.0 GB</td></tr><tr><td valign="top">500</td><td valign="top">3</td><td valign="top">360.0 GB</td><td valign="top">360.0 GB</td></tr><tr><td valign="top">750</td><td valign="top">0</td><td valign="top">130.0 GB</td><td valign="top">130.0 GB</td></tr><tr><td valign="top">750</td><td valign="top">1</td><td valign="top">260.0 GB</td><td valign="top">260.0 GB</td></tr><tr><td valign="top">750</td><td valign="top">2</td><td valign="top">390.0 GB</td><td valign="top">390.0 GB</td></tr><tr><td valign="top">750</td><td valign="top">3</td><td valign="top">520.0 GB</td><td valign="top">520.0 GB</td></tr><tr><td valign="top">1000</td><td valign="top">0</td><td valign="top">180.0 GB</td><td valign="top">180.0 GB</td></tr><tr><td valign="top">1000</td><td valign="top">1</td><td valign="top">360.0 GB</td><td valign="top">360.0 GB</td></tr><tr><td valign="top">1000</td><td valign="top">2</td><td valign="top">540.0 GB</td><td valign="top">540.0 GB</td></tr><tr><td valign="top">1000</td><td valign="top">3</td><td valign="top">720.0 GB</td><td valign="top">720.0 GB</td></tr></tbody></table>
