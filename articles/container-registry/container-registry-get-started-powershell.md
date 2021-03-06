---
title: 'Snelstartgids: een persoonlijk Docker-register in Azure maken met PowerShell'
description: Leer snel hoe u een persoonlijk Docker-containerregister maakt met behulp van PowerShell.
services: container-registry
author: neilpeterson
manager: timlt
ms.service: container-registry
ms.topic: quickstart
ms.date: 02/12/2018
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 80b5055dee35cd6efe62ee949c05aef386a3ba14
ms.sourcegitcommit: b32d6948033e7f85e3362e13347a664c0aaa04c1
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 02/13/2018
---
# <a name="create-an-azure-container-registry-using-powershell"></a>Een Azure Container Registry maken met behulp van PowerShell

Azure Container Registry is een beheerde service voor Docker-containerregisters die wordt gebruikt voor het opslaan van installatiekopieën van persoonlijke Docker-containers. In deze handleiding vindt u instructies voor het maken van een Azure Container Registry-exemplaar met behulp van PowerShell.

Voor deze snelstartgids is moduleversie 3.6 of later van Azure PowerShell vereist. Voer `Get-Module -ListAvailable AzureRM` uit om de versie te bekijken. Als u PowerShell wilt installeren of upgraden, raadpleegt u [De Azure PowerShell-module installeren](/powershell/azure/install-azurerm-ps).

Docker moet ook lokaal zijn geïnstalleerd. Docker biedt pakketten die eenvoudig Docker configureren op elk [Mac][docker-mac]-, [Windows][docker-windows]- of [Linux][docker-linux]-systeem.

## <a name="log-in-to-azure"></a>Meld u aan bij Azure.

Meld u aan bij uw Azure-abonnement met de opdracht `Login-AzureRmAccount` en volg de instructies op het scherm.

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a>Een resourcegroep maken

Maak een Azure-resourcegroep met de opdracht [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Een resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location EastUS
```

## <a name="create-a-container-registry"></a>Een containerregister maken

Maak een ACR-exemplaar met de opdracht [New-AzureRMContainerRegistry](/powershell/module/containerregistry/New-AzureRMContainerRegistry).

De registernaam moet uniek zijn binnen Azure en mag 5 tot 50 alfanumerieke tekens bevatten. In het volgende voorbeeld wordt *myContainerRegistry007* gebruikt. Werk deze waarde bij naar een unieke waarde.

```powershell
$registry = New-AzureRMContainerRegistry -ResourceGroupName "myResourceGroup" -Name "myContainerRegistry007" -EnableAdminUser -Sku Basic
```

## <a name="log-in-to-acr"></a>Aanmelden bij ACR

Voordat u installatiekopieën van containers gaat pushen en pullen, moet u zich aanmelden bij het ACR-exemplaar. Gebruik eerst de opdracht [Get-AzureRmContainerRegistryCredential](/powershell/module/containerregistry/get-azurermcontainerregistrycredential) om de beheerdersreferenties voor het ACR-exemplaar op te halen.

```powershell
$creds = Get-AzureRmContainerRegistryCredential -Registry $registry
```

Gebruik vervolgens de opdracht [docker login][docker-login] om u aan te melden bij het ACR-exemplaar.

```bash
docker login $registry.LoginServer -u $creds.Username -p $creds.Password
```

De opdracht retourneert `Login Succeeded` nadat deze is voltooid. Mogelijk ziet u een waarschuwing die het gebruik van de parameter `--password-stdin` aanraadt. Hoewel buiten het bestek van dit artikel, wordt u deze best practice aangeraden. Zie de verwijzing voor de opdracht [docker login][docker-login] voor meer informatie.

## <a name="push-image-to-acr"></a>Installatiekopie naar ACR overdragen met een push-bewerking

Als u een installatiekopie naar een Azure Container Registry wilt pushen, moet u eerst over een installatiekopie beschikken. Voer, indien nodig, de volgende opdracht uit om een vooraf gemaakte installatiekopie op te halen uit Docker Hub.

```bash
docker pull microsoft/aci-helloworld
```

De installatiekopie moet zijn getagd met de naam van de ACR-aanmeldingsserver. Voer de opdracht [Get-AzureRmContainerRegistry](/powershell/module/containerregistry/Get-AzureRmContainerRegistry) uit om de naam van de aanmeldingsserver van het ACR-exemplaar te retourneren.

```powershell
Get-AzureRmContainerRegistry | Select Loginserver
```

Label de installatiekopie met de opdracht [docker tag][docker-tag]. Vervang *acrLoginServer* door de naam van de aanmeldingsserver van het ACR-exemplaar.

```bash
docker tag microsoft/aci-helloworld <acrLoginServer>/aci-helloworld:v1
```

Gebruik ten slotte [docker push][docker-push] om de installatiekopieën naar het ACR-exemplaar te pushen. Vervang *acrLoginServer* door de naam van de aanmeldingsserver van het ACR-exemplaar.

```bash
docker push <acrLoginServer>/aci-helloworld:v1
```

## <a name="clean-up-resources"></a>Resources opschonen

U kunt de opdracht [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) gebruiken om de resourcegroep, het ACR-exemplaar en alle containerinstallatiekopieën te verwijderen, wanneer u ze niet meer nodig hebt.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a>Volgende stappen

In deze snelstartgids hebt u een Azure Container Registry met de Azure-opdrachtregelinterface gemaakt. Als u Azure Container Registry wilt gebruiken met Azure Container Instances, gaat u door naar de zelfstudie Azure Container Instances.

> [!div class="nextstepaction"]
> [Zelfstudie voor Azure Container Instances](../container-instances/container-instances-tutorial-prepare-app.md)

<!-- LINKS - external -->
[docker-linux]: https://docs.docker.com/engine/installation/#supported-platforms
[docker-login]: https://docs.docker.com/engine/reference/commandline/login/
[docker-mac]: https://docs.docker.com/docker-for-mac/
[docker-push]: https://docs.docker.com/engine/reference/commandline/push/
[docker-tag]: https://docs.docker.com/engine/reference/commandline/tag/
[docker-windows]: https://docs.docker.com/docker-for-windows/