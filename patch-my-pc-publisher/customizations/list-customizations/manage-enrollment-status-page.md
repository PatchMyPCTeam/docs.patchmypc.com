# Manage Enrollment Status Page option in Patch My PC Publisher

_Applies to: Patch My PC Publisher V3.x_\
_Available at level: All Custom Products, All Products, Vendor, Product_
\
_Available on tab: Intune Apps_

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>This article has not been updated for Version 3.x. Once it has, this banner will be removed.</p>
</blockquote>

The **Manage Enrollment Status Page** right-click option in Patch My PC (PMPC) Publisher allows you to associate Intune applications created by the Publisher with one or more Enrollment Status Page (ESP) profiles.

This configuration controls which applications are tracked as blocking apps during Windows Autopilot enrollment.

Only classic Enrollment Status Page (ESP) profiles are supported by this feature. It does not apply to the newer Autopilot device preparation policies found in the modern Windows Autopilot configuration experience.

The example below highlights the difference in the Intune admin center between classic **Enrollment Status Page** profiles, which are supported, and **Device preparation policies**, which are not supported for ESP association by the Publisher.

![Classic Enrollment Status Page versus Autopilot device preparation policies](/_images/image-(4050).png "Classic Enrollment Status Page versus Autopilot device preparation policies")

## Configuration

The ESP profile association is applied during the next Publisher synchronization.

If a new version of the application is published, the Publisher automatically removes the previous version it created from the ESP profile(s) and adds the newly published version instead. This ensures Autopilot always tracks the most recent version of an application published.

<blockquote class="wp-block-quote">
<p>**Important**</p>
<p>Associating an app with an ESP profile does not install the app by itself. The application must also have a Required Intune assignment targeting the device or user for it to be installed during Autopilot.</p>
</blockquote>

The available ESP profiles are retrieved from your Intune tenant. To appear in the list, an ESP profile must have **Show app and profile configuration progress** set to **Yes**.

![Show app and profile configuration progress](/_images/image-(4052).png "Show app and profile configuration progress")

Use the Select ESPs window to associate an Intune application with one or more classic Enrollment Status Page profiles.

![Select ESP Profiles](/_images/image-(4054).png "Select ESP Profiles")

To configure ESP profiles for an application:

1. Right-Click the **Manage ESP Profiles** option for the product, vendor, or product group where you want the setting applied.
2. The Select ESPs window opens and displays all eligible classic ESP profiles from your Intune tenant.
3. Use the Filter items field to quickly locate the required ESP profile.
4. Select one or more ESP profiles by checking the box next to each profile.
5. Select **OK** to save the configuration.

Products selected will added to the ESP profile as a Blocking app when the Intune application is published.

![Block device use until required apps are installed if they are assigned to the user/device](/_images/image-(4053).png "Block device use until required apps are installed if they are assigned to the user/device")