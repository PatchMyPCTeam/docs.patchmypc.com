# Insights External Services Dell Warranty API

_Applies to: Patch My PC Advanced Insights_

Advanced Insights (this is not relevant for Patch Insights) can access device warranty information from a variety of vendors. For access to Dell warranty information you will need an API key provided by Dell. The process to apply for a key is shown here.

First you will browse to [https://techdirect.dell.com](https://techdirect.dell.com/) and register or log in, you will need to be associated with your Dell Company account. Once all that is sorted you can select to go to the APIs section.

![](/_images/image-(1293).png "Dell Tech API")

![](/_images/image-(1289).png "Dell Tech Request API Key")

![](/_images/image-(1562).png "Dell API Client ID")

![](/_images/image-(1563).png "Dell API Client Secret")



<blockquote class="wp-block-quote">
<p>Advanced Insights makes a single API call for every 100 Dell clients when importing warranty information. To estimate the number of API calls you will require, we recommend specify 1% of the total Dell client device count.</p>
</blockquote>

Once you have successfully obtained your API key log into Advanced Insights and navigate to the Administration area. Go to Settings - External Services and check the "Is Enabled" and "Enable Warranty Caching" option.&#x20;

Enter the provided Dell warranty text for Client ID, Client Secret and click save all.

\*Please only enter in the text in-between the brackets for the API Client Secret.

![](/_images/image-(1561).png "Example of Dell API Client ID and Client Secret")