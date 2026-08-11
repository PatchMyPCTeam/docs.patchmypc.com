# Multiple Administrators and the Patch My PC Publisher Remote User Interface

_Applies to: Patch My PC Publisher V3.x_

{% hint style="danger" %}
**PRE-RELEASE DOCUMENTATION**

This documentation is for a pre-release feature still under development and, therefore, incomplete. As a result, both functionality and documentation are subject to change.

Once this feature is released, it will be announced, and this banner will be removed.
{% endhint %}

As more than one administrator can open the Patch My PC (PMPC) Publisher Settings console against the same server at once (locally and on the server from remote workstations), Publisher coordinates who is allowed to edit and who is connected as a read-only observer, to prevent people overwriting each other's changes.

## Editing versus read-only

* The administrator who holds the _Editing session_ has full read/write access and can save changes.
* Any additional connections are opened in read-only mode. Read-only administrators can navigate and view everything they have permission to, but the **Save** and **Apply** buttons and other actions that change settings are blocked.
* The number of editors allowed at once depends on how your organization has configured the Publisher:
  * **Single-editor** (default) **-** One editing session. Everyone else is read-only.
  * **Multi-editor -** Up to five editing sessions at once. Additional connections are read-only.

{% hint style="danger" %}
**Important**

You do not choose this mode. The Settings console simply tells you whether your session is editing or read-only when you connect.
{% endhint %}

## What read-only administrators see

* A clear indicator that the session is read-only.
* If you try an action that would change settings, Publisher stops it and explains that the session is read-only. This includes the obvious **Save** and **Apply** buttons as well as less obvious actions such as import wizards, test-and-save buttons, and connection changes.

{% hint style="info" %}
**Note**

Read-only mode prevents conflicting saves. It does not reduce what you are _permitted_ to do - your [Access and Permissions](access-permissions-reference.md) still apply on top.
{% endhint %}

## Viewing other Connections

The footer of the settings window has a **session information** icon that is always available. Clicking it allows you to see who is currently connected, including:

* How many editing sessions are in use out of the maximum.
* Each administrator's account and computer.
* How long each session has been open, and how long it has been idle.

## Taking over an idle Editing session

If you are read-only because someone else is editing, you can take over the editing session once that session has been idle for at least 5 minutes. This prevents you from interrupting someone who is actively working, while still letting you reclaim a session that was left open.

To take over an editing session:

1. Open the session information dialog.
2. Sessions that have been idle long enough are selectable. Sessions still in active use are shown but marked as not yet idle.
3. Select the idle session you want to take over and confirm. You become the editor, and the other session drops to read-only.

{% hint style="info" %}
**Note**

There is one shortcut to this rule: an administrator working directly on the server can immediately take over a session without waiting for the 5-minute idle period. This lets an on-site operator always reclaim control of their own server.
{% endhint %}

## Sessions that are left open

When sessions are left open:

* A session that becomes free (someone closes the Settings console, or their connection drops) is released automatically, and a waiting read-only administrator is promoted to editor within moments.
* A session that is left idle for a long time (30 minutes by default) can be cleaned up automatically by the server, but only when another administrator is actually waiting for a session. If no one is waiting, an idle session is ignored.
* If your connection briefly drops and you reconnect, Publisher recognizes you and cleans up your previous session so you are not double-counted.

## Tips for multi-admin environments

In multi-admin environments:

* Close the Settings console when you are finished to free the editing session for others.
* Use the session information dialog before assuming a session is stuck - it tells you whether the current editor is active or idle.
* If your organization frequently has several administrators editing at once, ask whoever manages Publisher whether the multi-editor mode is enabled.
