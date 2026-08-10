---
description: Using a Advanced Insights with a Proxy Server
---

# Insights Proxy Support

_Applies to: Patch My PC Advanced and Patch Insights_

Advanced Insights supports http, socks4 and socks5 network proxies.

Please add the correct protocol to the start of your proxies' network address e.g. http://x.x.x.x, socks4://x.x.x.x, socks5://x.x.x.x.\
Ports can be added at the end of the network address e.g. http://x.x.x.x:1234"

### Adding a proxy server in the Welcome page

If Advanced Insights cannot automatically access our licensing service at https://api.patchmypc.com we will automatically prompt for you to supply proxy details.

![](../.gitbook/assets/image-\(1765\).png)

### Adding a proxy server in the Settings page

Proxy configuration can also be added in the Administration - Settings - External Services tab

![](../.gitbook/assets/image-\(1766\).png)

> \*\*Note\*\*
>
> If you are changing proxy settings, you will need to restart the Advanced Insights Controller and Warranty websites on the server you have Advanced Insights installed to reload the proxy settings.
