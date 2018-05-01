# SharePoint Server 2016 Azure PowerShell Build

SharePoint Server 2016 PowerShell build scripts and procedure for a 2 server farm in Azure

## Procedure

### Prerequisites

* Update settings.psd1 configuration file
  * Azure subscription details
  * Naming details for all servers/accounts/dns e.t.c
* PowerShell v5 minimum installed locally
  
### Script Run Order

* Remotely
  * 01-SVR-Create-VMs(Remote).ps1 // Create Azure Virtual Machines (loops through all servers)
  * 02-SVR-Enable-VMWinRM(Remote).ps1 // Enable PowerShell Remote Access in Azure VMs (loops through all servers)
* On Active Directory Server (copy settings and script to server)
  * 03-AD-Create-ActiveDirectory.ps1 // Create AD Forrest, DNS
  * 04-AD-Add-DNSRecords.ps1 // Create DNS Records
  * 05-AD-Add-ServiceAccounts.ps1 // Create all service accounts
  * 06-AD-Add-UsersAndGroups.ps1 // Create OUs, Groups, Users(Employees)
  * 07-AD-Set-GPOSettings.ps1 // Set Domain Group Policy Settings
  * 08-AD-Set-SPNs.ps1 // Add SPN records
  * 09-AD-SMBShare.ps1 // Create SMB Network Share, Open Browser to download files
  * 10-AD-Set-KerberosDelegationTrustforServer.ps1 // Server Kerberos delegation
  * 11-AD-Set-ReplicationDirectoryDelegation // UPS Service Account Delegation Rights
* Remotely
  * 12-SVR-Set-ServerDefaultConfiguration(Remote).ps1 // Default Server Config (loops through all servers)
  * 13-SVR-Join-ServersToDomain(Remote).ps1 // Join all servers to domain (loops through all servers)
