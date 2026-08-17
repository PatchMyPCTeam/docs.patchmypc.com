# Insights External Services HP Warranty (Workforce Experience)

_Applies to: Patch My PC Advanced Insights_

{% hint style="danger" %}
We currenly do not support HP Warranty API. Only HP Proactive Insights API and Workforce Experience. Please speak with HP about allowing software vendors to use the HP Warranty API.
{% endhint %}

{% hint style="danger" %}
You will need to be a HP Workforce Experience customer for warranty collection to work, please speak to your HP representative about becoming a customer.
{% endhint %}

Advanced Insights (this is not relevant for Patch Insights) can access device warranty information from a variety of vendors. For access to HP warranty information you will need to sign up to HP Workforce Experience, enroll all the HP devices you want to collect warranty data on and set up a developer account to access the warranty data.

## Developer account creation

First, we will create the developer account needed to interact with the HP Workforce Experience api.

### Initial setup

#### API Enrolment

{% hint style="info" %}
The url for the HP developer portal is [https://developers.hp.com/](https://developers.hp.com/)
{% endhint %}

First, you will need to create an account if you do not have one already. If you have a HPID for HP Workforce Experience, you can use this account.

{% hint style="danger" %}
Once you have registered, you will need to request access to the HP Proactive Insights APIs tech group for your developer account. The group required is HP Proactive Insights and not HP Warranty API. We do not currently support the HP Warranty API at this time.
{% endhint %}

### Creating credentials

{% hint style="info" %}
The link to generate api credentials is: [https://developers.hp.com/group/1275/manage-credentials/apis](https://developers.hp.com/group/1275/manage-credentials/apis)
{% endhint %}

Please visit the link above to open the credentials generation page. You will be show the following options below. Click Get Credentials in the HP Proactive Insights Analytics section.

<figure><img src="../.gitbook/assets/image (2639).png" alt=""><figcaption><p>Link location to create api credentials</p></figcaption></figure>

{% hint style="warning" %}
If the page has an error screen like shown below, HP have not enrolled your developer account in the HP Proactive Insights APIs tech group. Please contact HP again to have your account enrolled in the HP Proactive Insights API tech group.
{% endhint %}

<figure><img src="../.gitbook/assets/hp no api.png" alt="This image showcases the Hp Proactive Insights API web page, with the error You do not have appropriate permissions (role) to access any of this Tech Groups published Apis"><figcaption><p>HP enrolment error</p></figcaption></figure>

#### Credentials creation flow

<figure><img src="../.gitbook/assets/image (2640).png" alt=""><figcaption><p>Credentials creation form</p></figcaption></figure>

You will need to provide the following information:

1. Credentials name: We recommend "Advanced Insight Warranty"
2. Description: We recommend "API Keys for Advanced Insight Warranty"
3. Developer Redirect Url: This will be used by HP to redirect when you log in. This needs to be your Advanced Insights in the following format _https://FQDN:PORT/app/main/view/warranty_. Example https://contoso.local:444/app/main/view/warranty
4. Client ID: Leave blank
5. Tick Read Checkbox

<figure><img src="../.gitbook/assets/image (2641).png" alt=""><figcaption><p>Complete example of credentials creation</p></figcaption></figure>

Click create and you will be redirected back to the previous page.

#### Viewing app

<figure><img src="../.gitbook/assets/image (2643).png" alt=""><figcaption><p>Green banner showing creation was successful</p></figcaption></figure>

Once you have been redirected, there will be a green success banner on top of the page. Please now click the "My API Credentials" link in the banner.

<figure><img src="../.gitbook/assets/image (2644).png" alt=""><figcaption><p>App listing with newly created app</p></figcaption></figure>

Now click on the newly created app by click the app name, this will load the app details page.

<figure><img src="../.gitbook/assets/image (2646).png" alt=""><figcaption><p>App details page</p></figcaption></figure>

Here you will see information about the newly created app.

We need to copy

1. The API ClientId
2. The API Secret (click "Show Secret" to get this entry)

{% hint style="warning" %}
It's a good idea to double check that the Redirect URL is correct. You can come back to this page if you receive a redirect URL error when trying to authenticate. You will also want to change the URL if your installation FQDN of Advanced Insights changes in the future.
{% endhint %}

### HP Settings in Advanced Insights

We now need to copy API ClientId and API Secret to Advanced Insights.

1. Go to Administration -> Settings -> External Services
2. Based on the location of the HP Workforce Experience portal you used, select US or EU.
3. Copy and paste the API Client ID into the Client ID input
4. Copy and paste the API Client Secret into the Client Secret input
5. Save settings.

<figure><img src="../.gitbook/assets/3.jpg" alt="Settings page in Advanced Insights"><figcaption><p>Settings page in Advanced Insights</p></figcaption></figure>

{% hint style="info" %}
The app client secret has an expiration date of one year from the date of creation. Please make a note of when this key will need to be rotated.
{% endhint %}

## Register for HP Workforce Experience

{% hint style="warning" %}
If you are already a HP Workforce Experience customer, you may not need to do the registration steps below but you will need access to the HP Workforce Experience Portal.

HP has two versions of HP Workforce Experience, one for US (and ASIA) customers and one for EU customers.

You will need to sign up to the appropriate version based on your companies location.

Mistakes here will cause issues in the future. Here are the access urls.

US portal: [https://admin.hp.com/](https://admin.hp.com/)

EU portal: [https://eu.admin.hp.com/](https://eu.admin.hp.com/)
{% endhint %}

<figure><img src="../.gitbook/assets/image (2577).png" alt=""><figcaption><p>HP Workforce Experience welcome page</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (2579).png" alt=""><figcaption><p>Sign up or login using either a Microsoft Account to or HPID account</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (2581).png" alt=""><figcaption><p>Create HP Workforce Experience Account</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (2582).png" alt=""><figcaption><p>Account creation dialog</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (2583).png" alt=""><figcaption><p>Accepting the ToS</p></figcaption></figure>

## Using HP Workforce Experience

When you have registered and logged in, you will be greeted by the home experience of HP Workforce Experience.\
On the left hand side, you will need to click "Assets" to begin importing your HP devices into HP Workforce Experience.

<figure><img src="../.gitbook/assets/image (2540).png" alt=""><figcaption><p>HP Workforce Experience homepage with assets link highlighted</p></figcaption></figure>

### Importing devices

HP Workforce Experience allows you to import your device using four different mechanisms. Currently **only Intune Import and Asset enrolment allow for warranty data collection**, manual and csv upload do not trigger warranty collection by design. To begin importing devices, please click the "Add" button in the top left of the page.

<figure><img src="../.gitbook/assets/image (2542).png" alt=""><figcaption><p>Assets page with assets imported</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (2543).png" alt=""><figcaption><p>Add button for device import</p></figcaption></figure>

### Intune import

To begin importing from Intune, please click the Intune Import button then click next.

<figure><img src="../.gitbook/assets/image (2545).png" alt=""><figcaption><p>The import modal, please click Intune Import then next</p></figcaption></figure>

You will be now asked to provide your Intune Domain Name, this can be found by going to the Intune portal, clicking Tenant Administration on the left hand menu and copying the Tenant name from the Tenant Status page.

<figure><img src="../.gitbook/assets/image (2546).png" alt=""><figcaption><p>Location of tenant domain name, via Intune portal.</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (2547).png" alt=""><figcaption><p>Adding our tenant domain name to HP.</p></figcaption></figure>

You will now be greeted by the Microsoft Login flow, please log in using your microsoft credenitals as normal. You will be then presented the list of permission HP requests to perform the Intune import.

{% hint style="warning" %}
All of the permissions requested by HP is for the HP Workforce Experience platform. They are not defined/requested by Patch My PC. Advanced Insights does not use or read any of your Intune data.
{% endhint %}

<figure><img src="../.gitbook/assets/fixed.png" alt=""><figcaption><p>Permissions required by HP.</p></figcaption></figure>

Once you have accepted the permission, the connection to Intune will be completed by HP.

You will now be asked if you wish to import Assets from Intune Groups, or to import all of your assets.

{% hint style="info" %}
We recommend you use the Group functionality, as this allows you to only provide HP the devices you wish to collect warranty information on. Only use full import if you really want every device in HP Workforce Experience as it is vendor agnostic and will collect all competing vendor devices.
{% endhint %}

We shall continue using Group import only.

When you click on Import assets only from Intune groups, you will be presented with a full list of all your groups in Intune. You can filter out the groups you want to import and you can import multiple groups. Select the groups you want to import and click Import.

<figure><img src="../.gitbook/assets/image (2549).png" alt=""><figcaption><p>Filtered group for HP devices only</p></figcaption></figure>

Intune will now begin importing your selected devices. You will receive a notification on begin and completion of the import.

<figure><img src="../.gitbook/assets/image (2551).png" alt=""><figcaption></figcaption></figure>

You can also check progress by navigating to the logs link on the left hand side.

### Asset Enrolment

To enrol your device by Asset Enrolment, please use the following HP documentation to distribute the agent.

[Via SCCM](https://hp.service-now.com/workforceexperience?id=kb_article\&sysparm_article=KB0011362)

[Via Intune](https://hp.service-now.com/workforceexperience?id=kb_article\&sysparm_article=KB0011387)

{% hint style="success" %}
Once the devices are imported, HP Workforce Experience will begin collecting warranty information. This process can take some time, depending on how many devices you have imported.
{% endhint %}

## Collecting Warranty

Collecting warranty in Advanced Insights works in the same way as the other providers, but you will need to log into HP on bulk caching.

Navigate to the warranty dashboard.

To begin, click the "Bulk Processing" statistic to begin re-caching warranty.

<figure><img src="../.gitbook/assets/3.jpg" alt="Warranty dashboard"><figcaption><p>Warranty dashboard</p></figcaption></figure>

You will be asked to log in to HP, click yes and Advanced Insights will go to HP to log in.

<figure><img src="../.gitbook/assets/4.jpg" alt="HP login warning"><figcaption><p>HP login warning</p></figcaption></figure>

{% hint style="danger" %}
If you receive a redirect url is incorrect error. Please go back to your developer app and check the redirect url provided.
{% endhint %}

{% hint style="success" %}
Once you have logged in, HP will redirect you back to Advanced Insights and warranty will begin caching warranty data.
{% endhint %}

<figure><img src="../.gitbook/assets/image (2538).png" alt=""><figcaption><p>HP Warranty data listed in Advanced Insights</p></figcaption></figure>
