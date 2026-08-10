# Disk Space

_Applies to: Patch My PC Publisher V2.x_

The **120GB** overall disk space requirement listed on our [core Publisher requirements](../core-requirements.md#disk-space) page accounts for the space needed by the Publisher to download and package vendor installers before they are published and for the Windows Operating system.

When publishing applications to ConfigMgr, additional space is required in multiple locations.

ConfigMgr requires space for the application Content Source and the Distribution Points (DPs) you intend to deploy content to. Depending on the number of retained app versions you intend to keep will also determine the overall amount of disk space required.&#x20;

<blockquote class="wp-block-quote">
<p>**Tip**</p>
<p>**120 GB** is an estimated requirement based on enabling approximately 700 products in the Publisher. The average application size, calculated from all apps in our catalog, is around 180 MB, with individual apps ranging from 1.01 MB to 1.81 GB.</p>
</blockquote>

The table below illustrates the estimated disk space requirements based on the number of applications you plan to enable in the Publisher and the number of retained versions you choose to keep. These estimates are based on the average application size across our catalog. Please note that actual sizes can vary significantly, with individual apps ranging from 1.01 MB to 1.81 GB. Therefore these numbers should be used for illustrative purposes only.

<blockquote class="wp-block-quote">
<p>**Note**</p>
<p>ConfigMgr uses single-instance storage within the Content Library on each Distribution Point, meaning duplicate files are stored only once per DP. This can reduce actual disk usage compared to the estimates shown below. However, because storage savings depend on application overlap and version similarity, single-instance storage is not factored into these rough calculations.</p>
</blockquote>

<table><thead><tr><th>Enabled Apps</th><th width="145">Retained Apps</th><th>Content Source</th><th>Each DP</th></tr></thead><tbody><tr><td>250</td><td>0</td><td>40.0 GB</td><td>40.0 GB</td></tr><tr><td>250</td><td>1</td><td>80.0 GB</td><td>80.0 GB</td></tr><tr><td>250</td><td>2</td><td>120.0 GB</td><td>120.0 GB</td></tr><tr><td>250</td><td>3</td><td>160.0 GB</td><td>160.0 GB</td></tr><tr><td>500</td><td>0</td><td>90.0 GB</td><td>90.0 GB</td></tr><tr><td>500</td><td>1</td><td>180.0 GB</td><td>180.0 GB</td></tr><tr><td>500</td><td>2</td><td>270.0 GB</td><td>270.0 GB</td></tr><tr><td>500</td><td>3</td><td>360.0 GB</td><td>360.0 GB</td></tr><tr><td>750</td><td>0</td><td>130.0 GB</td><td>130.0 GB</td></tr><tr><td>750</td><td>1</td><td>260.0 GB</td><td>260.0 GB</td></tr><tr><td>750</td><td>2</td><td>390.0 GB</td><td>390.0 GB</td></tr><tr><td>750</td><td>3</td><td>520.0 GB</td><td>520.0 GB</td></tr><tr><td>1000</td><td>0</td><td>180.0 GB</td><td>180.0 GB</td></tr><tr><td>1000</td><td>1</td><td>360.0 GB</td><td>360.0 GB</td></tr><tr><td>1000</td><td>2</td><td>540.0 GB</td><td>540.0 GB</td></tr><tr><td>1000</td><td>3</td><td>720.0 GB</td><td>720.0 GB</td></tr><tr><td></td><td></td><td></td><td></td></tr></tbody></table>