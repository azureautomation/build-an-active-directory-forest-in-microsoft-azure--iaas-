Build an Active Directory Forest in Microsoft Azure (IaaS)
==========================================================

            
**WHAT **
Creates a Windows Server 2012 R2 Active Directory forest in Microsoft Azure. Ideal for testing.
 
As a minimum will create a forest with one domain and one domain controller. Additional domain controllers can be specified. Additional member servers and client workstations can also be added (MSDN subscription required for client workstations).

Can be executed as an Azure Automation run book or a stand alone script.
 
 

**    **



**RUN AS A RUN BOOK... **
AZURE AUTOMATION ASSETS
 

The following are required if you wish to execute the script as an Azure Automation runbook:
 

1. An Automation variable asset called 'AzureSubscriptionId' that contains the GUID for this Azure subscription. To use an asset with a different name you can pass the asset name as a runbook input parameter or change the default value for the input parameter.
 

2. An Automation credential asset called 'AzureCredential' that contains the Azure AD user credential with authorization for this subscription. To use an asset with a different name you can pass the asset name as a runbook input parameter or change the
 default value for the input parameter.
 
3. The 'Runbook' switch must be activated with a value of 'true'.
 

![Image](https://github.com/azureautomation/build-an-active-directory-forest-in-microsoft-azure-(iaas)/raw/master/capture116.png)

 
  
 
**Even Newer and Even More Improved Formula: Build an Active Directory Forest in Microsoft Azure (IaaS) II**
 
[http://blogs.technet.com/b/poshchap/archive/2016/04/01/even-newer-and-even-more-improved-formula-build-an-active-directory-forest-in-microsoft-azure-iaas.aspx](http://blogs.technet.com/b/poshchap/archive/2016/04/01/even-newer-and-even-more-improved-formula-build-an-active-directory-forest-in-microsoft-azure-iaas.aspx)
 

 
**RUN AS A SCRIPT...**
 
**SCRIPT - EXAMPLE 1**
.\Azure_AD_Build.ps1 -ServicePrefix 'NIMBUS' `
                                   -Location 'North Europe' `
                                   -AdminUser 'CloudAdmin' `
                                   -AdminPassword '2BYlKZ9pWN' `
                                   -ForestFqdn 'contoso.com' `
                                   -Domain 'contoso' `
                                   -DcCount 4 `
                                   -MemberCount 1 `
                                   -W7ClientCount 1 `
                                   -W8ClientCount 1 `
                                   -W10ClientCount 1 `
                                   -ClassCSubnetNumber 11
 
Creates a virtual network and storage account in the 'North Europe' data centre location both prefixed with 'NIMBUS'. The virtual network has one subnet - 10.0.11.0/28.
Creates a forest called contoso.com with 4 Windows Server 2012 R2 domain controllers, 1 Windows Server 2012 R2 member server, 1 Windows 7 Enterprise (x64) client, 1 Windows 8.1 Enterprise (x64) client and 1 Windows 10 Enterprise (x64) client (MSDN
 subscription required for client operating systems).

An Azure DNS object is created for the first DC on 10.011.4. The domain controllers will each have an additional 20GB data drive, with host caching disabled, for the NTDS and SYSVOL folders. The domain controllers will also have a static Azure vNet IP
 set. Creates a domain administrator and, where appropriate a local administrator account called 'CloudAdmin', with a password of '2BYlKZ9pWN'. Sets the DSRM password as '2BYlKZ9pWN'.
 
A certificate for each host will be imported to the local computer's 'Trusted Root Certificate Store' to allow seamless connectivity using PS Remoting.
 
 
 
**SCRIPT - EXAMPLE 2 **
.\Azure_AD_Build.ps1 -ServicePrefix 'FARRCLOUD' `
                                   -AdminUser 'CloudAdmin' `
                                   -AdminPassword '2BYlKZ9pWN'
 
Creates a virtual network and storage account in the 'West Europe' data centre location both prefixed with 'FARRCLOUD'. The virtual network has one subnet - 10.0.10.0/28.
Creates a forest called adatum.com with 1 Windows Server 2012 R2 domain controller. An Azure DNS object is created for the DC on 10.0.10.4. The domain controller will have an additional 20GB data drive, with host caching disabled, for the NTDS and SYSVOL
 folders. The domain controller will also have a static Azure vNet IP set. Creates a domain administrator account called 'CloudAdmin', with a password of '2BYlKZ9pWN'. Sets the DSRM password as '2BYlKZ9pWN'.
 
A certificate for the domain controller will be imported to the local computer's 'Trusted Root Certificate Store' to allow seamless connectivity using PS Remoting.
 
 
 
GETTING STARTED... 
  
**How to install and configure Azure PowerShell**
 
[https://azure.microsoft.com/en-us/documentation/articles/powershell-install-configure/](https://azure.microsoft.com/en-us/documentation/articles/powershell-install-configure/)
 
 
 

**Configure an Azure Automation Account - Part 1 - Start Me Up
**
[http://blogs.technet.com/b/poshchap/archive/2016/02/12/configure-an-azure-automation-account-part-1.aspx](http://blogs.technet.com/b/poshchap/archive/2016/02/12/configure-an-azure-automation-account-part-1.aspx)


 
 

**Configure an Azure Automation Account - Part 2 - Credentials and Variables**
[ ](http://blogs.technet.com/b/poshchap/archive/2016/02/19/configure-an-azure-automation-account-part-2.aspx)
[http://blogs.technet.com/b/poshchap/archive/2016/02/19/configure-an-azure-automation-account-part-2.aspx](http://blogs.technet.com/b/poshchap/archive/2016/02/19/configure-an-azure-automation-account-part-2.aspx)
 

  

**Configure an Azure Automation Account - Part 3 - Validation Run Book**
 
[http://blogs.technet.com/b/poshchap/archive/2016/02/26/configure-an-azure-automation-account-part-3.aspx](http://blogs.technet.com/b/poshchap/archive/2016/02/26/configure-an-azure-automation-account-part-3.aspx)
[ ](http://blogs.technet.com/b/poshchap/archive/2016/02/26/configure-an-azure-automation-account-part-3.aspx)
  
Also, take a look here for more on the Virtual Network configuration stuff:

**NEW & IMPROVED FORMULA: Build an AD DS Forest in Azure**

[http://blogs.technet.com/b/poshchap/archive/2015/01/30/new-amp-improved-formula-build-an-ad-ds-forest-in-azure.aspx](http://blogs.technet.com/b/poshchap/archive/2015/01/30/new-amp-improved-formula-build-an-ad-ds-forest-in-azure.aspx)

** **

And, here, for some stuff on remoting to Azure:

**Managing Azure VMs with PS Remoting**

[http://blogs.technet.com/b/poshchap/archive/2014/09/12/ps-remoting-import-azure-winrm-certificate.aspx](http://blogs.technet.com/b/poshchap/archive/2014/09/12/ps-remoting-import-azure-winrm-certificate.aspx)

 

**Create Azure Cloud Service Remote Desktop Connection Manager Group File (.rdg)**

[http://blogs.technet.com/b/poshchap/archive/2015/09/18/create-azure-cloud-service-remote-desktop-connection-manager-file-rdg.aspx](http://blogs.technet.com/b/poshchap/archive/2015/09/18/create-azure-cloud-service-remote-desktop-connection-manager-file-rdg.aspx)** *** *

 

Finally, here, for some stuff on keeping the Azure PS modules up to date:

**Automagically Keep the Azure PowerShell Module Up-To-Date**

[http://blogs.technet.com/b/poshchap/archive/2016/01/15/automagically-keep-the-azure-powershell-module-up-to-date.aspx](http://blogs.technet.com/b/poshchap/archive/2016/01/15/automagically-keep-the-azure-powershell-module-up-to-date.aspx)

 

 

**UPDATE**
29/01/2015
* added ability to merge additional virtual network configuration with any existing configuration so that script can be used to create a forest with a non-vanilla subscription
* added ability to specify class C subnet number for the new virtual network

24/02/2015
* added the ability to spin up Win7 and Win8 clients
* made the script verbose by default
17/03/2015
* added additional parameter validation on the -ServicePrefix parameter to check that the name doesn't already exist

16/09/2015
* added ability to spin up W10 clients
* fixed an issue with retrieval of W7 / W8 VM images
* updated data centre locations
12/01/2016
* added -Runbook switch so script can be executed as an Azure Automation runbook
08/03/2016
* fixed a couple of issues since adding W10 clients and the Azure runbook mode

 



 

 




        
    
TechNet gallery is retiring! This script was migrated from TechNet script center to GitHub by Microsoft Azure Automation product group. All the Script Center fields like Rating, RatingCount and DownloadCount have been carried over to Github as-is for the migrated scripts only. Note : The Script Center fields will not be applicable for the new repositories created in Github & hence those fields will not show up for new Github repositories.
