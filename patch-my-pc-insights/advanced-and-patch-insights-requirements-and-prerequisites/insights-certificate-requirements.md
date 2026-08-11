# Insights Certificate Requirements

_Applies to: Patch My PC Advanced and Patch Insights_

Advanced Insights needs a valid SSL certificate to install and function. **(the installer will verify the certificate is valid).**

Supported Certificate types:

* Server host (FQDN) standard certificate.
* Wildcard certificate.
* Custom CNAME / Alias certificate.
* Self-signed certificate.

The certificate must meet the following minimum requirements:

* Support HTTPS / SSL.
* Has private key.
* Valid in-date (not expired).
* Enhanced key usage includes "Server Authentication".
* Only modern signature types are supported (e.g. SHA256). Legacy / weak signature algorithms, for example; 'SHA1', 'MD2', 'MD4', 'MD5 are not supported.
* Subject Alternative Name (SAN). The certificate SAN requirements depend on the chosen deployment configuration for the Advanced Insights URL.
  * **Scenario 1 - Server Host name certificate.**
    * For Advanced Insights URL deployment using **server host name** (e.g. _https://server01.contoso.local_) the certificate SAN must contain an entry which matches the FQDN of the host server where Advanced Insights is installed.
  * **Scenario 2 - Wildcard certificate.**
    * For Advanced Insights URL deployment using a **wildcard certificate**, an entry must be included in the certificate SAN that represents the wildcard certificate. e.g. ' _\*contoso.local_'.
  * **Scenario 3 - CNAME / Alias certificate.**
    * For Advanced Insights URL deployment using a **CNAME / Alias,** (e.g. _https://AdvancedInsights.contoso.local_) the certificate SAN must contain an entry which represents the CNAME / Alias. e.g. '_AdvancedInsights.contoso.local'._

> When using a \*\*CNAME / Alias\*\* or \*\*Wilcard\*\* certificate for custom Advanced Insights deployment URL, ensure that DNS has been updated to include an entry which represents the chosen CNAME / Alias.
>
> \_Example:\_
>
> !\[]\(/\_images/image-(1726).png>)

Certificate SAN values can be also verified within the certificate properties.

_Examples:_

![](../../.gitbook/assets/image-\(1727\).png)

![](../../.gitbook/assets/image-\(1728\).png)

![](../../.gitbook/assets/image-\(1729\).png)

> On the Windows Server OS which will host Advanced Insights, the following PowerShell script can be executed to list supported certificates.

{% code lineNumbers="true" %}
```powershell
# Advanced Insights valid certificate check.
Param()

$CertsToExclude = @("ConfigMgr SQL Server Identification Certificate","WMSVC-SHA2")

# Get the FQDN of the machine
[System.Net.Dns]:/_images/GetHostEntry(-env-COMPUTERNAME).hostname

# Certificate filtering

# Algorithms to exclude
$Weakhash = @('SHA1', 'SHA1RSA', 'MD2', 'MD4', 'MD5')

$certs = Get-ChildItem -Path Cert:\LocalMachine\My |
    Where-Object {
        ($_.SignatureAlgorithm.FriendlyName -notin $Weakhash) -and
        ($_.EnhancedKeyUsageList | Where-Object { $_.ObjectId -eq "1.3.6.1.5.5.7.3.1"} ) -and
        ($_.NotAfter -gt (Get-Date)) -and
        ($_.HasPrivateKey -eq $true) -and
        ($_.FriendlyName -notin $CertsToExclude) -and
        (
            ($_.Extensions | Where-Object { $_.Oid.Value -eq "2.5.29.17" }) -and
            ($sanExtension = $_.Extensions | Where-Object { $_.Oid.Value -eq "2.5.29.17" }) -and
            ($sanNames = $sanExtension.Format(0) -split ', ' | ForEach-Object { $_.Split('=')[1].Trim() })
            
        ) -and
        (Test-Certificate -Cert $_ -Policy SSL)
    } -ErrorAction SilentlyContinue

#$certs.Extensions

Write-Host "############### The following certificates are suitable for Advanced Insights: ###############"`n
foreach ($cert in $certs) {

$SelfSigned = $false    
if ($cert.Issuer -eq $cert.Subject) {
$SelfSigned = $true
}

$sanExtension = $cert.Extensions | Where-Object { $_.Oid.Value -eq "2.5.29.17" }

$sanNames = $sanExtension.Format(0) -split ', ' | ForEach-Object { $_.Split('=')[1].Trim() }

Write-Host "Certificate Friendly Name: $($cert.FriendlyName)
Certificate Thumbprint: $($cert.Thumbprint)
Enhanced Key Usage: $($cert.EnhancedKeyUsageList)
Certitifcate validity: $($cert.NotAfter)
Private Key present: $($cert.HasPrivateKey)
Subject Alternative Name (SAN): $($sanNames)
Signature Algorithm: $($cert.SignatureAlgorithm.FriendlyName)
Self signed Certificate: $($SelfSigned)" `n
}

# List certificates not captured in $certs
$allCerts = Get-ChildItem -Path Cert:\LocalMachine\My
$uncapturedCerts = $allCerts | Where-Object { $_ -notin $certs }

# Output the uncaptured certificates and their unmatched properties
if ($uncapturedCerts.Count -gt 0) {
    Write-Host "############### The following certificate properties are checked: ###############`n
    1. Enhanced Key Usage
    2. Certitifcate validity
    3. Private Key present
    4. Certificate in exclude list
    5. Subject Alternative Name (SAN)
    6. 'Test-Certificate -Policy SSL' cmdlet is used to check certificate is valid for SSL and root cert can be validated
    7. Signature Algorithm = sha256RSA (Minimum)" `n

    Write-Host "############### The following certificates have one or more property values which are not suitable for Advanced Insights: ###############"`n -ForegroundColor Yellow
    foreach ($cert in $uncapturedCerts) {
        Write-Host "Certificate Friendly Name: $($cert.FriendlyName)
        Certificate Thumbprint: $($cert.Thumbprint)"

        Write-Host "Unsuitable Certificate Properties:"

        # Check Key Usage details
        $SANObjID = $cert.EnhancedKeyUsageList | Where-Object { $_.ObjectId -eq '1.3.6.1.5.5.7.3.1'}        
        if (!$SANObjID) {
            Write-Host "1. Enhanced Key Usage (requires 'Server Authentication') value found: $($cert.EnhancedKeyUsageList)"
        }
        if ($cert.NotAfter -le (Get-Date)) {
            Write-Host "2. A valid, in date certificate is required: Expiration Date found: $($cert.NotAfter)"
        }
        if ($cert.HasPrivateKey -ne $true) {
            Write-Host "3. Private Key present?: Not Found"
        }
        if ($cert.FriendlyName -in $CertsToExclude) {
            Write-Host "4. Certificate in exclude list: Friendly Name: $($cert.FriendlyName)"
        }

        # Check SAN extension
        $sanExtension = $cert.Extensions | Where-Object { $_.Oid.Value -eq "2.5.29.17" }
        if (!$sanExtension) {
            Write-Host "5. Subject Alternative Name (SAN) requires at least one entry matches the server FQDN or is a wildcard which matches the server domain name e.g. '*.internaldomain.local. SAN value(s):: Not Found"
        } else
        
        {
            $sanNames = $sanExtension.Format(0) -split ', ' | ForEach-Object { $_.Split('=')[1].Trim() }
[string]:/_images/IsNullOrEmpty(-sanNames))
                Write-Host "5 Subject Alternative Name (SAN) requires at least one entry matches the server FQDN or is a wildcard which matches the server domain name e.g. '*.internaldomain.local. SAN value(s): $($sanNames -join ', ')"
                }
        }
        

        if (!(Test-Certificate -Cert $cert -Policy SSL)) {
            Write-Host "6. Test-Certificate SSL Policy: Failed"
        }
        if ($cert.SignatureAlgorithm.FriendlyName -in $Weakhash) {
            Write-Host "7. Certificate signature algorithm requires a minimum of SHA256 RSA. Legacy / weak algorithms e.g. 'SHA1', 'MD2', 'MD4', 'MD5 are not supported. Signature Algorithm found: $($cert.SignatureAlgorithm.FriendlyName)"`n
        }
        Write-Host
    } Write-Host "############### Certificate Check End ###############"
} else {
    Write-Host "No uncaptured certificates found."
}
```
{% endcode %}

Example PowerShell outputs:

![](../../.gitbook/assets/image-\(2014\).png)

![](../../.gitbook/assets/image-\(2015\).png)

> \*\*Self-signed certificate use.\*\*
>
> When deploying Advanced Insights using a self-signed certificate, the installer will automatically create the certificate using the server host name value to create the Advanced Insights URL.
>
> Example:
>
> \_https://server01.contoso.local\_
>
> We don't recommend using a self-signed certificate long-term in production as it won't be trusted by other client browsers by default.\\
>
> \\
>
> You can replace a self-signed certificate or modify the certificate in use using the Add/Remove Programs "Change" option as detailed \[here]\(../modify-insights/modify-insights-ssl-certificate.md).
