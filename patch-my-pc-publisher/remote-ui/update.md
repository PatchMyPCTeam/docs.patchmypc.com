# Update Patch My PC Publisher Remote User Interface

_Applies to: Patch My PC Publisher V3.x_

<blockquote class="wp-block-quote">
<p>**PRE-RELEASE DOCUMENTATION**</p>
<p>This documentation is for a pre-release feature still under development and, therefore, incomplete. As a result, both functionality and documentation are subject to change.</p>
<p>Once this feature is released, it will be announced, and this banner will be removed.</p>
</blockquote>

Patch My PC (PMPC) releases new versions of the Publisher regularly. If you run the Settings console remotely, as the **PatchMyPCService** and Settings console are two separate programs, they both need to be updated, which Publisher coordinates for you.

## How updates reach you

* The **PatchMyPCService** on the server checks for new versions on a schedule (approximately every hour) and, at the end of its sync cycle, when it can update itself.
* When a new version is available, the **PatchMyPCService** notifies every connected Settings console immediately that an update is available.
* Any remote Settings consoles download the update through the **PatchMyPCService**, not from the Internet. This is important for secure environments: workstations do not need their own Internet connection to download Publisher updates.

## User experience

* When a new version is available, connected Settings consoles show a notification (for example, on the **About** tab).
* Users can choose when to install the update. Approving the update downloads it through the **PatchMyPCService** and installs it.
* When the **PatchMyPCService** itself is about to update, all connected Settings consoles are warned as the **PatchMyPCService** briefly restarts as part of the update process. Users should save their work when they see the warning.

## Keeping the Settings console and Service in sync

Because the **PatchMyPCService** can update itself automatically, it can move to a newer version while an older Settings console is still connected. The notification system is designed to keep you informed so you can update the Settings console to match. If you ever see a version-mismatch message, update the Settings console to the version the **PatchMyPCService** is running.

## Controlling automatic updates

You can turn off the **PatchMyPCService**'s automatic self-installation, for example, to schedule updates during a maintenance window. It is worth understanding exactly what this setting does:

* It stops the **PatchMyPCService** from installing an update on its own at the end of a sync.
* However, it does not stop version checks or notifications. The **PatchMyPCService** still checks for new versions and still tells connected Settings consoles when one is available, so you remain aware of updates even when automatic installation is turned off.

If automatic installation is turned off, plan to apply updates manually on your own schedule.

### Tips for applying Updates

* Apply Settings console updates promptly after **PatchMyPCService** updates, so the two components are on the same version.
* If you manage several administrators, let them know when an update is coming so they can save and reconnect after the **PatchMyPCService** restarts.