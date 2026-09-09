---
description: Tracking Task Sequence execution
---

# Advanced Insights "OS Deployment" Dashboard

<figure><img src="../../.gitbook/assets/image (4788).png" alt=""><figcaption><p>OS Deployment Dashboard</p></figcaption></figure>

The Advanced Insights OS Deployment Dashboard helps you track Task Sequence performance and status over time. The default view shows two week's execution history for all Task Sequences with Boot Media assosicated to them. The timescale can be extended using the calendar picker.

The OS Deployment Activity chart shows a breakdown of execution time, and status per-day for all selected Task Sequences. This can be filtered to a specific Task Sequence using the chart picker below. Clicking any chart segment will show all OS builds completed on that day.

The OS Deployment Activity table lists each device built, completion time and status. Clicking any individual machine takes you to the Device View OSD Tab. This view shows the status for each task completed during the Task Sequence execution on that device.

<figure><img src="../../.gitbook/assets/image (4789).png" alt=""><figcaption><p>Device view showing OS Deployment Activity</p></figcaption></figure>

Where a task has additional script output, the info icon shows the verbose script output.

The bottom left table shows a comparison of all Task Sequences and their overall performance statistics.

Finally, the bottom right table shows a view of all errors ocurring in all Task Sequences. This view can help optimize Task Sequence performance and identify where post-imaging remediation may be required to ensure devices are built to standard.
