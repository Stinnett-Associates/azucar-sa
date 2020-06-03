<h1>Introduction</h1>

<h2>Forking Azucar</h2>

This is a fork of the [Azucar project by the NCC Group](https://github.com/nccgroup/azucar) project.

We've made some custom modications to the codebase to better support Azure audits. A detailed list of those modifications will be provided soon.

<h2>About Azucar</h2>

Azucar is a multi-threaded plugin-based tool to help assess the security of Azure Cloud environment subscription. By leveraging the Azure API , Azucar automatically gathers a variety of configuration data and analyses all data relating to a particular subscription in order to determine security risks.

The script <b>will not change or modify</b> any asset deployed in the Azure subscription.

<h1>Operating System Support</h1>

As the script uses the .NET ADAL library for for authenticating the user and calling the REST APIs, only Windows OS are currently supported.  

<h1>Features</h1>

* Return a number of attributes on computers, users, groups, contacts, events, etc... from an Azure Active Directory
* Search for High level accounts in Azure Tenant, including Azure Active Directory, classic administrators and Directory Roles (RBAC)
* Multi-Threading support
* Plugin Support
* The following assets are supported by Azucar:
    * Azure SQL Databases, including MySQL and PostgreSQL databases
	* Azure Active Directory
	* Storage Accounts
	* Classic Virtual Machines
	* Virtual Machines V2
	* Security Status
	* Security Policies
	* Role Assignments (RBAC)
	* Missing Security Patches
	* Missing Security Baseline
	* Web Application Firewall
	* Network Security Groups
	* Classic Endpoints
	* Azure Security Alerts
	* Azure KeyVault


<h1>Quick Start: Setup</h2>

* Download the [Azucar-sa ZIP file](https://github.com/Stinnett-Associates/azucar-sa/archive/master.zip)
* Extract the ZIP file to a folder, such as ```c:\temp\```
  
![1](https://raw.githubusercontent.com/Stinnett-Associates/azucar-sa/master/Images/1.png)

* Holding the SHIFT key, right-click the folder background and cliend "Open PowerShell window here"

![2](https://raw.githubusercontent.com/Stinnett-Associates/azucar-sa/master/Images/2.png)

* Set the execution policy to allow the script to run. Be sure to check with any network administrators for guidance here.

```Set-ExecutionPolicy Byapss -Scope Process```

![3](https://raw.githubusercontent.com/Stinnett-Associates/azucar-sa/master/Images/3.png)

<h2> Quick Start: Running the Tool</h2>

1. Determine which element from the Azure environment will be run via the script. The default value is ```All```.

![5](https://raw.githubusercontent.com/Stinnett-Associates/azucar-sa/master/Images/5.PNG)

2. Run the script based on the specific file to be audited by entering the following command, based on the output file format.  Example Scripts:
  
  ```
  .\azucar-sa.ps1 -ExportTo CSV -Analysis All
  .\azucar-sa.ps1 -ExportTo Excel -Analysis ActiveDirectory
  ``` 


![4](https://raw.githubusercontent.com/Stinnett-Associates/azucar-sa/master/Images/4.png)
3.	If Applicable - Authorize Admin authentication credentials to proceed in running the script
4.	Select a specific Azure subscription to audit and allow script to complete

![6](https://raw.githubusercontent.com/Stinnett-Associates/azucar-sa/master/Images/6.PNG)

5.	Script results will be saved in the “Reports” folder, provide these files to the Internal Auditors  

 <br>
 <hr>
 <br>


<h1>Screenshots</h1>

![azucar](https://user-images.githubusercontent.com/5271640/38782164-3edde5ca-40ef-11e8-94e3-b8f005db139d.PNG)

<h1>Reporting</h1>

Support for exporting data driven to several formats like CSV, XML or JSON.

The following screenshot shows an example report in JSON format

![threat](https://user-images.githubusercontent.com/5271640/38782058-4779800a-40ee-11e8-8bf5-9b16500e5134.PNG)

<h1>Prerequisites</h1>

AZUCAR works out of the box with PowerShell version 3.x and .NET 4.5. You can check your Windows PowerShell version executing the command <b>$PsVersionTable:</b>

```powershell
PS C:\Users\silverhack> $psversiontable

Name                           Value
----                           -----
PSVersion                      5.1.14393.693
PSEdition                      Desktop
PSCompatibleVersions           {1.0, 2.0, 3.0, 4.0...}
BuildVersion                   10.0.14393.693
CLRVersion                     4.0.30319.42000
WSManStackVersion              3.0
PSRemotingProtocolVersion      2.3
SerializationVersion           1.1.0.1
```

You should use an account with at least read-permission on the assets you want to access. You could find more information about Role-Based Access Control in Azure by clicking [here](https://docs.microsoft.com/en-us/azure/role-based-access-control/role-assignments-portal)

<h1>Installation</h1>

You can download the latest zip by clicking [here](https://github.com/nccgroup/azucar/archive/master.zip).

Before to start, you need to unblock files. Once you have unzipped the zip file, you can use the fantastic PowerShell V3 Unblock-File cmdlet that will do this task for you:

<pre>
Get-ChildItem -Recurse c:\Azucar_V10 | Unblock-File
</pre>

<h1>Usage</h1>

To get a list of basic options and switches use:

```powershell
get-help .\azucar-sa.ps1
```

To get a list of examples use:

```powershell
get-help .\azucar-sa.ps1 -Examples
```

To get a list of all options and examples with detailed info use:

```powershell
get-help .\azucar-sa.ps1 -Detailed
```









<h1>Examples</h1>

This example retrieves information of an Azure Tenant and print results. The script will try to connect using the ADAL library, and if no credential passed, the script will try to connect using the bearer token for logged user

```powershell
.\azucar-sa.ps1 -ExportTo PRINT | Format-List
```

This example will retrieve information of an Azure Tenant and print results to a local variable. The script will try to connect using the ADAL library, and if no credential passed, the script will try to connect using the bearer token for logged user

```powershell
$data = .\azucar-sa.ps1 -AuthMode UseCachedCredentials -Verbose -WriteLog -Debug -ExportTo PRINT
```

This example will retrieve information of an Azure Tenant and print results to a local variable. The script will try to connect by using the ADAL library and will try to connect by using a cached credential

```powershell
$data = .\azucar-sa.ps1 -AuthMode Client_Credentials -Verbose -WriteLog -Debug -ExportTo PRINT
```
This example will retrieve information of an Azure Tenant and print results to a local variable. The script will try to connect by using the ADAL library and will try to connect by using the client credential flow

```powershell
.\azucar-sa.ps1 -ExportTo CSV,JSON,XML,EXCEL -AuthMode Certificate_Credentials -Certificate C:\AzucarTest\server.pfx -ApplicationId 00000000-0000-0000-0000-000000000000 -TenantID 00000000-0000-0000-0000-000000000000
```
This example will retrieve information of an Azure Tenant and export data driven to CSV, JSON, XML and Excel format into Reports folder. The script will try to connect by using the Azure Active Directory Application Certificate credential flow

```powershell
.\azucar-sa.ps1 -ExportTo CSV,JSON,XML,EXCEL -AuthMode Certificate_Credentials -Certificate C:\AzucarTest\server.pfx -CertFilePassword MySuperP@ssw0rd! -ApplicationId 00000000-0000-0000-0000-000000000000 -TenantID 00000000-0000-0000-0000-000000000000
```
This example will retrieve information of an Azure Tenant and export data driven to CSV, JSON, XML and Excel format into Reports folder. The script will try to connect by using the Azure Active Directory Application Certificate credential flow

```powershell
.\azucar-sa.ps1 -ResolveTenantDomainName microsoft.com
```
This example will try to resolve the TenantID for an specific domain name

```powershell
.\azucar-sa.ps1 -ResolveTenantUserName user@company.com
```
This example will try to resolve the TenantID for an specific username

