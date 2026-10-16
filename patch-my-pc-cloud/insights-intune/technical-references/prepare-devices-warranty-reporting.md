# Prepare Devices for Warranty Reporting in Patch My PC Advanced Insights for Intune

_Applies to: Advanced Insights for Intune_

The Patch My PC (PMPC) Client collects warranty data that manufacturer software publishes locally on Windows devices. Configure the relevant manufacturer component before you expect warranty data to appear in the **Warranty** tab on the **Hardware** page.

{% hint style="info" %}
**Note**

Warranty reporting requires a Patch My PC Enterprise Premium license.
{% endhint %}

## Supported manufacturers

The device client currently collects warranty data for the following manufacturers.

<table><thead><tr><th width="130" valign="top">Manufacturer</th><th width="230" valign="top">Required component</th><th width="91" valign="top">Source</th><th valign="top">Data source location</th></tr></thead><tbody><tr><td valign="top">Dell</td><td valign="top">Dell Command | Monitor</td><td valign="top">WMI</td><td valign="top"><code>DCIM_AssetWarrantyInformation</code> in <code>root\DCIM\SYSMAN</code></td></tr><tr><td valign="top">HP</td><td valign="top">HP Client Management Script Library (HPCMSL), with warranty data populated</td><td valign="top">WMI</td><td valign="top"><code>HP_Warranty</code> in <code>root\HP\InstrumentedServices\v1</code></td></tr><tr><td valign="top">Lenovo</td><td valign="top">Lenovo Commercial Vantage, with warranty publishing enabled</td><td valign="top">WMI</td><td valign="top"><code>Lenovo_WarrantyElement</code> in <code>root\Lenovo</code></td></tr></tbody></table>

{% hint style="info" %}
**Note**

The device client checks the Windows manufacturer value before it runs a provider. A device from another manufacturer does not run the Dell, HP, or Lenovo provider.
{% endhint %}

## Before you begin

Confirm that:

* The Patch My PC Client is installed and enrolled.
* The manufacturer component has published warranty data on the device.
* The device can complete its normal inventory upload to PMPC Cloud.



{% hint style="info" %}
**Note**

The warranty inventory schedule comes from Patch My PC policy. You do not need to create a separate scheduled task.
{% endhint %}

## Configure Dell devices

The device client reads warranty data captured by **Dell Command | Monitor**.

1. Install **Dell Command | Monitor** on each supported Dell device using your normal device-management process.
2. Allow **Dell Command | Monitor** to populate its warranty data.
3. Allow the next PMPC warranty inventory run to complete.

The device client reads these Dell fields when available:

* Warranty name
* Identifying number
* Warranty duration
* Start date
* End date
* Last refreshed date

If the WMI class is missing, the device client reports that the Dell dependency is missing. If the class exists but contains no records, **Dell Command | Monitor** may not have refreshed the warranty data yet.

{% hint style="info" %}
**Note**

The PMPC Client reads existing Dell warranty data. It does not install **Dell Command | Monitor** or run any executables.
{% endhint %}

## Configure HP devices

The device client reads warranty data that the **HP Client Management Script Library (CMSL)** publishes through HP Instrumented Services.

1. Install **HP CSML** using HP's supported deployment method.
2. Open an elevated PowerShell session.
3.  Run the **HP CMSL** warranty command:

    ```powershell
    Get-HPWarrantyInfo
    ```
4.  Confirm that HP populated the warranty class:

    ```powershell
    Get-CimInstance `
        -Namespace 'root\HP\InstrumentedServices\v1' `
        -ClassName 'HP_Warranty'
    ```
5. Confirm that the command returns one or more warranty records.
6. Allow the next Patch My PC warranty inventory run to complete.

The device client reads these HP fields when available:

* Service type
* Serial number
* Warranty start date
* Warranty end date
* Last HPCMSL check

{% hint style="info" %}
**Note**

The Patch My PC Client reads existing HP warranty data. It does not install **HP CMSL** or run `Get-HPWarrantyInfo`.
{% endhint %}

If the WMI class is missing, the device client reports that the HP dependency is missing. If the class exists but contains no records, **HP CMSL** may not have refreshed the warranty data yet.

## Configure Lenovo Commercial Vantage to expose warranty information in WMI

Patch My PC can collect Lenovo warranty information from Windows Management Instrumentation (WMI). Before warranty information can be collected, **Lenovo Commercial Vantage** must be installed and configured to publish warranty data to WMI.

{% hint style="info" %}
**Lenovo Commercial Vantage** _cannot_ coexist on the device with Lenovo Consumer Vantage.&#x20;
{% endhint %}

Lenovo stores warranty information in the `ROOT\Lenovo` namespace using the following classes:

```
Lenovo_WarrantyInformation
Lenovo_WarrantyElement
```

{% hint style="info" %}
**Note**

Installing **Lenovo Commercial Vantage** alone does not enable warranty information in WMI. Lenovo also requires the `wmi.warranty` policy to be enabled.
{% endhint %}

### Requirements

The device must have **Lenovo Commercial Vantage** installed. This can be achieved by deploying the **Lenovo Vantage Service** application from the PMPC Cloud Catalog. The application uses Lenovo's full Commercial Vantage installation command:

```
VantageInstaller.exe Install -Vantage
```

This installs the Commercial Vantage application, the **Critical Service for Lenovo Vantage**, and the required Vantage add-ins.

### Configure the warranty WMI policy

Create a deployment for **Lenovo Vantage Service** in PMPC Cloud with the following settings:

1. Open the deployment.
2. Go to **Configurations**.
3. Expand **Scripts**.
4. Under **Install Scripts**, add a **Post-Install** script.
5. Add the PowerShell script below.

```powershell
$PolicyPath = 'HKLM:\SOFTWARE\Policies\Lenovo\Commercial Vantage'

# Create the Commercial Vantage policy key if it does not already exist
New-Item -Path $PolicyPath -Force | Out-Null

# Enable writing Lenovo warranty information to WMI
New-ItemProperty `
    -Path $PolicyPath `
    -Name 'wmi.warranty' `
    -PropertyType DWord `
    -Value 1 `
    -Force | Out-Null

# Restart the Lenovo Vantage Service so the new policy is processed
$Service = Get-Service -Name 'LenovoVantageService' -ErrorAction SilentlyContinue

if ($Service) {
    Restart-Service -Name 'LenovoVantageService' -Force
}
```

The resulting registry configuration is:

```
HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Lenovo\Commercial Vantage

wmi.warranty    REG_DWORD    1
```

### Allow time for Lenovo to populate WMI

Warranty information is not populated immediately after the policy is enabled.

In Patch My PC testing, Commercial Vantage populated the Lenovo warranty WMI classes approximately five minutes after the Lenovo Vantage Service was restarted.

{% hint style="danger" %}
**Important**

The five-minute delay is observed behavior during testing and should not be treated as a guaranteed Lenovo service-level interval. Allow several minutes before validating the WMI data.
{% endhint %}

### Verify the configuration

#### To confirm the registry policy

Run:

```powershell
Get-ItemProperty `
    'HKLM:\SOFTWARE\Policies\Lenovo\Commercial Vantage' `
    -Name 'wmi.warranty'
```

Expected value:

```
wmi.warranty : 1
```

#### To confirm the Lenovo warranty WMI classes

After allowing **Lenovo Commercial Vantage** time to retrieve and publish the warranty information, run:

```powershell
Get-CimClass -Namespace root\Lenovo |
    Where-Object CimClassName -like '*Warranty*' |
    Select-Object CimClassName
```

Expected output:

```
CimClassName
------------
Lenovo_WarrantyInformation
Lenovo_WarrantyElement
```

#### To view the warranty summary

```powershell
Get-CimInstance `
    -Namespace root\Lenovo `
    -ClassName Lenovo_WarrantyInformation |
    Format-List *
```

#### To view individual warranty entitlements

```powershell
Get-CimInstance `
    -Namespace root\Lenovo `
    -ClassName Lenovo_WarrantyElement |
    Format-List *
```

### Troubleshooting

#### To confirm **Lenovo Commercial Vantage** is installed

Run:

```powershell
Get-AppxPackage -AllUsers -Name 'E046963F.LenovoSettingsforEnterprise'
```

A successful **Lenovo Commercial Vantage** installation should return a package named:

```
E046963F.LenovoSettingsforEnterprise
```

The **Consumer Lenovo Vantage** application uses a different package identity:

```
E046963F.LenovoCompanion
```

{% hint style="info" %}
If `E046963F.LenovoCompanion` is present instead of `E046963F.LenovoSettingsforEnterprise`, the device is using the consumer Lenovo Vantage application rather than Commercial Vantage.
{% endhint %}

#### To confirm the Lenovo Vantage Service is running

Run:

```powershell
Get-Service LenovoVantageService
```

The service normally appears in Windows Services as:

```
Critical Service for Lenovo Vantage
```

If the registry policy is present but the warranty WMI classes are still missing, restart the service:

```powershell
Restart-Service LenovoVantageService
```

Then wait several minutes and check WMI again.

#### To confirm the WMI namespace exists

Run:

```powershell
Get-CimClass -Namespace root\Lenovo -ErrorAction SilentlyContinue |
    Select-Object CimClassName
```

If `ROOT\Lenovo` does not exist immediately after installation or service restart, wait several minutes and retry.

### Expected result

Once **Lenovo Commercial Vantage** has processed the policy and completed the warranty lookup, the following classes should be available under `ROOT\Lenovo`:

* `Lenovo_WarrantyInformation`
* `Lenovo_WarrantyElement`

Patch My PC can then use these classes to discover Lenovo warranty information from the endpoint.

## How the device client collects warranty data

On each scheduled warranty inventory run, the device client:

1. Checks whether warranty inventory is enabled for the device.
2. Selects a provider that matches the device manufacturer.
3. Reads warranty records from the manufacturer's local WMI or CIM class.
4. Maps each manufacturer entitlement to a warranty record.
5. Sends only changes through the normal inventory delta pipeline.

When warranty inventory is disabled, the device client skips collection and leaves previously reported warranty data unchanged.

When a provider fails after previously reporting warranty data, the device client retains the last known records and marks their source as failed. This prevents a temporary manufacturer-component failure from deleting the last known warranty dates.

## Warranty source status

_Warranty source status_ explains whether the device client could read the manufacturer data source. It is separate from any warranty status displayed in the table.

<table><thead><tr><th width="190" valign="top">Source status</th><th valign="top">Meaning</th></tr></thead><tbody><tr><td valign="top">Success</td><td valign="top">The device client read the manufacturer's source and returned warranty data.</td></tr><tr><td valign="top">Dependency missing</td><td valign="top">The manufacturer applies to the device, but the required WMI or CIM class is missing. Install or configure the required manufacturer component.</td></tr><tr><td valign="top">Failed</td><td valign="top">The provider applies to the device, but the collection attempt failed. The device client retains previously reported warranty records when possible.</td></tr><tr><td valign="top">Unknown</td><td valign="top">The source has no recorded collection outcome.</td></tr></tbody></table>

A supported device might not have warranty data in the table when its source status is **Dependency missing** or **Failed** and no previous record is available.

## To verify collection

After the next warranty inventory run:

1. Open the **Hardware** page and click the **Warranty** tab.
2. Search for the device.
3. Confirm that the warranty name, start date, end date, and source match the manufacturer data.
4. If the device has no warranty data, verify the WMI or CIM class again and review the Patch My PC Client log.

The Patch My PC Client writes warranty collection messages to `Client.log`.
