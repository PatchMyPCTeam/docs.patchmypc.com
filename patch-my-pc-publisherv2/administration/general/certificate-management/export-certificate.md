# Export Certificate

_Applies to: Patch My PC Publisher V2.x_

The **Export Certificate** option allows you to export the currently configured code-signing certificate from to a file. This is typically used when the certificate needs to be distributed to client systems or manually trusted in additional certificate stores.

When exporting the certificate, Publisher saves it as a **`.cer` file**, which contains the **public portion of the certificate only**. The private key is **not exported**, even if the key is marked as exportable.

![](../../../../.gitbook/assets/image-\(419\).png)
