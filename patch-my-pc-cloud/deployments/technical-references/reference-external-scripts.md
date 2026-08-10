# Reference External Scripts in a Patch My PC Cloud Deployment

_Applies to: Patch My PC Cloud_

If you upload [Extra Files](../deploy-app/configurations-tab/additional-tools/extra-files.md) as part of your Patch My PC (PMPC) Cloud Deployment, you can reference those files in any of the [Scripts](../deploy-app/configurations-tab/additional-tools/scripts/) in the same deployment by building a path relative to the script's current location.&#x20;

This ensures your script can reliably locate the files you uploaded, whether they are in the root or a subfolder.

Below are examples for referencing a file named `file_to_be_copied.txt`, either from the script root or a subfolder called `MyFolder`.

## PowerShell (.ps1)

To reference additional files you’ve uploaded, use `$PSScriptRoot\file_to_be_copied.txt` or `$PSScriptRoot\MyFolder\file_to_be_copied.txt` if the file is in a subfolder.

For example:

```
# File in script root
Copy-Item -Path "$PSScriptRoot\file_to_be_copied.txt" -Destination "C:\TargetFolder"

# File in subfolder
Copy-Item -Path "$PSScriptRoot\MyFolder\file_to_be_copied.txt" -Destination "C:\TargetFolder"
 
```

## Batch / CMD (.bat / .cmd)

To reference additional files you’ve uploaded, use `%~dp0file_to_be_copied.txt` or `%~dp0MyFolder\file_to_be_copied.txt` if the file is in a subfolder.

For example:

```
:: File in script root
copy "%~dp0file_to_be_copied.txt" "C:\TargetFolder"

:: File in subfolder
copy "%~dp0MyFolder\file_to_be_copied.txt" "C:\TargetFolder" 
```

## VBScript (.vbs)

To reference additional files you’ve uploaded, use `scriptDir & "\file_to_be_copied.txt"` or `scriptDir & "\MyFolder\file_to_be_copied.txt"` if the file is in a subfolder.

For example:

```
Set fso = CreateObject("Scripting.FileSystemObject")
scriptDir = fso.GetParentFolderName(WScript.ScriptFullName)

' File in script root
fso.CopyFile scriptDir & "\file_to_be_copied.txt", "C:\TargetFolder\"

' File in subfolder
fso.CopyFile scriptDir & "\MyFolder\file_to_be_copied.txt", "C:\TargetFolder\" 
```

<br>
