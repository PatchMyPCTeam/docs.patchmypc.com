# Add an External App to Patch My PC Cloud

_Applies to: Patch My PC Cloud_

{% hint style="danger" %}
**Important**

This feature is currently only available through an invitation-only Private Preview, as both it and the documentation are under development, incomplete, and subject to change.

Please do not share links to these docs with others outside of the Private Preview.

Once this feature is released, it will be announced, and this banner will be removed.
{% endhint %}

To add an app to the **External** catalog in Patch My PC (PMPC) Cloud:

1. From the PMPC Cloud Portal, navigate to **App Catalog | External**
2.  On the External catalog page, click **Add App**<br>

    <figure><img src="../../../.gitbook/assets/image (4530).png" alt="Clicking ‘Add App’" width="563"><figcaption></figcaption></figure>

    \
    The list of apps in the public WinGet repository is displayed.<br>

    <figure><img src="../../../.gitbook/assets/image (4531).png" alt="List of apps in the public WinGet repository" width="563"><figcaption></figcaption></figure>

{% hint style="success" %}
**Tip**

Use the **Search** box and filters to help you more easily find the app you want to add.
{% endhint %}

{% hint style="info" %}
**Note**

If an app is already in the PMPC catalog, it will be shown with **PUBLIC APP** beside it, and you will be unable to re-add it. This is because it is better for you to use the curated version we maintain in the **Patch My PC** catalog Vs a non-curated version. Just hover over **PUBLIC APP** and click **Go to App** to open the app in our catalog.

<img src="../../../.gitbook/assets/image (4532).png" alt="‘PUBLIC APP’ in the External catalog" data-size="original">

Also, if an app is shown as **UNSUPPORTED**, it means this app is currently unsupported by the **External** catalog, which could be for many [reasons](add-external-app.md#reasons-apps-appear-as-unsupported) .
{% endhint %}

3. Click **Add** beside the required app.

<figure><img src="../../../.gitbook/assets/image (4533).png" alt="Clicking ‘Add’ beside the required app." width="563"><figcaption></figcaption></figure>

**ADDED** appears next to the app, along with the **Success – External app added** notification.

<figure><img src="../../../.gitbook/assets/image (4534).png" alt="‘ADDED’ appears next to the app, along with the ‘Success – External app added’ notification." width="563"><figcaption></figcaption></figure>

4. Keep clicking **Add** beside any other apps you want to add.
5. Once you have finished adding all the required apps, click the **X** in the top-right corner.

<figure><img src="../../../.gitbook/assets/image (4535).png" alt="Clicking ‘X’ in the top right-hand corner." width="563"><figcaption></figcaption></figure>

The External catalog is redisplayed with the added app(s).

<figure><img src="../../../.gitbook/assets/image (4536).png" alt="External catalog redisplayed with the added app(s)." width="563"><figcaption></figcaption></figure>

## Reasons apps appear as UNSUPPORTED

Apps can appear as **UNSUPPORTED** in the **External** catalog for many reasons:

* The app's manifest does not contain sufficient metadata (such as a product code or display name), which is required to build detection rules correctly. If this information is missing, it can lead to installation and detection issues on end-user devices, which is why we mark the app as **UNSUPPORTED**.
* The app has no supported installer types (all variants are PORTABLE or MSIX).
* The app uses a version format that is unsupported.

## Next Steps

Now you have added an app(s) to the **External** catalog, you can [deploy it](deploy-external-app.md).
