---
title: PowerShell installeren en configureren voor Azure-Stack Quick Start | Microsoft Docs
description: Meer informatie over het installeren en configureren van PowerShell voor Azure-Stack.
services: azure-stack
documentationcenter: 
author: mattbriggs
manager: femila
editor: 
ms.assetid: 6996DFC1-5E05-423A-968F-A9427C24317C
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2018
ms.author: mabrigg
ms.openlocfilehash: ca61562607da274f0e0c7f504d1a24723210f2f7
ms.sourcegitcommit: 562a537ed9b96c9116c504738414e5d8c0fd53b1
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/12/2018
---
# <a name="get-up-and-running-with-powershell-in-azure-stack"></a>Leren werken met PowerShell in Azure-Stack

*Van toepassing op: Azure Stack geïntegreerde systemen en Azure Stack Development Kit*

Deze snelstartgids helpt u bij het installeren en configureren van een Azure-Stack-omgeving met PowerShell. Het script die wij in dit artikel verstrekken is afgestemd op de **Azure Stack operator** alleen.

Dit artikel is een verkorte versie van de stappen die worden beschreven in de [Installeer PowerShell]( azure-stack-powershell-install.md), [downloaden's]( azure-stack-powershell-download.md), en [PowerShell-omgeving voor de Azure-Stack-operatorconfigureren]( azure-stack-powershell-configure-admin.md) artikelen. Met behulp van de scripts in dit onderwerp, kunt u PowerShell instellen voor Azure-Stack-omgevingen die zijn geïmplementeerd met Azure Active Directory of Active Directory Federation Services (AD FS).  


## <a name="set-up-powershell-for-azure-active-directory-based-deployments"></a>PowerShell instellen voor implementaties op basis van Azure Active Directory

Aanmelden bij uw Azure-Stack Development Kit of een externe Windows-client als u via VPN-verbinding verbonden bent. Open een PowerShell ISE-sessie met verhoogde bevoegdheden en voer vervolgens het volgende script. Zorg ervoor dat u het bijwerken van de **TenantName**, **ArmEndpoint**, en **GraphAudience** variabelen die nodig zijn voor de configuratie van uw omgeving:

> [!IMPORTANT]
> De versie van de PowerShell-module AzureRM 1.2.11 wordt geleverd met een lijst met wijzigingen op te splitsen. Upgrade van de 1.2.10 versie, Zie de [Migratiehandleiding](https://aka.ms/azspowershellmigration).

```powershell
# Specify Azure Active Directory tenant name.
$TenantName = "<mydirectory>.onmicrosoft.com"

# Set the module repository and the execution policy.
Set-PSRepository `
  -Name "PSGallery" `
  -InstallationPolicy Trusted

Set-ExecutionPolicy RemoteSigned `
  -force

# Uninstall any existing Azure PowerShell modules. To uninstall, close all the active PowerShell sessions, and then run the following command:
Get-Module -ListAvailable -Name Azure* | `
  Uninstall-Module

# Install PowerShell for Azure Stack.
Install-Module `
  -Name AzureRm.BootStrapper `
  -Force

Use-AzureRmProfile `
  -Profile 2017-03-09-profile `
  -Force

Install-Module `
  -Name AzureStack `
  -RequiredVersion 1.2.11 `
  -Force 

# Download Azure Stack tools from GitHub and import the connect module.
cd \

invoke-webrequest `
  https://github.com/Azure/AzureStack-Tools/archive/master.zip `
  -OutFile master.zip

expand-archive master.zip `
  -DestinationPath . `
  -Force

cd AzureStack-Tools-master

Import-Module .\Connect\AzureStack.Connect.psm1

# For Azure Stack development kit, this value is set to https://adminmanagement.local.azurestack.external. To get this value for Azure Stack integrated systems, contact your service provider.
  $ArmEndpoint = "<Resource Manager endpoint for your environment>"

# For Azure Stack development kit, this value is adminvault.local.azurestack.external 
$KeyvaultDnsSuffix = "<Keyvault DNS suffix for your environment>"


# Register an AzureRM environment that targets your Azure Stack instance
  Add-AzureRMEnvironment `
    -Name "AzureStackAdmin" `
    -ArmEndpoint $ArmEndpoint

# Get the Active Directory tenantId that is used to deploy Azure Stack
  $TenantID = Get-AzsDirectoryTenantId `
    -AADTenantName $TenantName `
    -EnvironmentName "AzureStackAdmin"

# Sign in to your environment
  Login-AzureRmAccount `
    -EnvironmentName "AzureStackAdmin" `
    -TenantId $TenantID 
```

## <a name="set-up-powershell-for-ad-fs-based-deployments"></a>PowerShell instellen voor AD FS-implementaties

U kunt het volgende script gebruiken als u Azure Stack werkt wanneer verbonden met internet. Maar als u Azure-Stack zonder verbinding met internet werkt, gebruiken de [manier van PowerShell installeren verbroken](azure-stack-powershell-install.md#install-powershell-in-a-disconnected-or-a-partially-connected-scenario-with-limited-internet-connectivity) en de cmdlets voor het configureren van PowerShell blijft hetzelfde zijn als in dit script wordt weergegeven. Aanmelden bij uw Azure-Stack Development Kit of een externe Windows-client als u via VPN-verbinding verbonden bent. Open een PowerShell ISE-sessie met verhoogde bevoegdheden en voer vervolgens het volgende script. Zorg ervoor dat u het bijwerken van de **ArmEndpoint** en **GraphAudience** variabelen die nodig zijn voor de configuratie van uw omgeving:

```powershell

# Set the module repository and the execution policy.
Set-PSRepository `
  -Name "PSGallery" `
  -InstallationPolicy Trusted

Set-ExecutionPolicy RemoteSigned `
  -force

# Uninstall any existing Azure PowerShell modules. To uninstall, close all the active PowerShell sessions and run the following command:
Get-Module -ListAvailable -Name Azure* | `
  Uninstall-Module

# Install PowerShell for Azure Stack.
Install-Module `
  -Name AzureRm.BootStrapper `
  -Force

Use-AzureRmProfile `
  -Profile 2017-03-09-profile `
  -Force

Install-Module `
  -Name AzureStack `
  -RequiredVersion 1.2.11 `
  -Force 

# Download Azure Stack tools from GitHub and import the connect module.
cd \
invoke-webrequest `
  https://github.com/Azure/AzureStack-Tools/archive/master.zip `
  -OutFile master.zip

expand-archive master.zip `
  -DestinationPath . `
  -Force

cd AzureStack-Tools-master

Import-Module .\Connect\AzureStack.Connect.psm1

# For Azure Stack development kit, this value is set to https://adminmanagement.local.azurestack.external. To get this value for Azure Stack integrated systems, contact your service provider.
$ArmEndpoint = "<Resource Manager endpoint for your environment>"

# For Azure Stack development kit, this value is adminvault.local.azurestack.external 
$KeyvaultDnsSuffix = "<Keyvault DNS suffix for your environment>"

# Register an AzureRM environment that targets your Azure Stack instance
Add-AzureRMEnvironment `
    -Name "AzureStackAdmin" `
    -ArmEndpoint $ArmEndpoint

# Get the Active Directory tenantId that is used to deploy Azure Stack     
$TenantID = Get-AzsDirectoryTenantId `
    -ADFS `
    -EnvironmentName "AzureStackAdmin"

# Sign in to your environment
Login-AzureRmAccount `
    -EnvironmentName "AzureStackAdmin" `
    -TenantId $TenantID
```

## <a name="test-the-connectivity"></a>De connectiviteit testen

Nu dat u PowerShell hebt geconfigureerd, kunt u de configuratie van de testen door een resourcegroep maken:

```powershell
New-AzureRMResourceGroup -Name "ContosoVMRG" -Location Local
```

Nadat de resourcegroep is gemaakt, de **Inrichtingsstatus** eigenschap is ingesteld op **geslaagd**.

## <a name="next-steps"></a>Volgende stappen

* [CLI installeren en configureren](azure-stack-connect-cli.md)

* [Sjablonen ontwikkelen](user/azure-stack-develop-templates.md)







