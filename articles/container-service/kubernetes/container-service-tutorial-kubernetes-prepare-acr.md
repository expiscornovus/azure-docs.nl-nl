---
title: 'Zelfstudie Azure Container Service: ACR voorbereiden'
description: 'Zelfstudie Azure Container Service: ACR voorbereiden'
services: container-service
author: neilpeterson
manager: timlt
ms.service: container-service
ms.topic: tutorial
ms.date: 09/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: ea2574a64c5ae5c10680ad0da7e06ffe12cc72cb
ms.sourcegitcommit: eeb5daebf10564ec110a4e83874db0fb9f9f8061
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 02/03/2018
---
# <a name="deploy-and-use-azure-container-registry"></a>Azure Container Registry implementeren en gebruiken

[!INCLUDE [aks-preview-redirect.md](../../../includes/aks-preview-redirect.md)]

Azure Container Registry (ACR) is een op Azure gebaseerd, persoonlijk register voor installatiekopieën van Docker-container. Deze zelfstudie, deel twee van zeven, beschrijft het implementeren van een Azure Container Registry-exemplaar en het pushen een containerinstallatiekopie naar dat exemplaar. Dit zijn de uitgevoerde stappen:

> [!div class="checklist"]
> * Een exemplaar van Azure Container Registry (ACR) implementeren
> * Een containerinstallatiekopie voor ACR taggen
> * De installatiekopie uploaden naar ACR

In volgende zelfstudies wordt dit ACR-exemplaar geïntegreerd met een Kubernetes-cluster Azure Container Service. 

## <a name="before-you-begin"></a>Voordat u begint

In de [vorige zelfstudie](./container-service-tutorial-kubernetes-prepare-app.md) hebt u een containerinstallatiekopie voor een eenvoudige Azure Voting-toepassing gemaakt. Als u de installatiekopie voor de Azure Voting-toepassing niet hebt gemaakt, ga dan terug naar [Zelfstudie 1: Containerinstallatiekopieën maken](./container-service-tutorial-kubernetes-prepare-app.md).

Voor deze zelfstudie moet u de versie Azure CLI 2.0.4 of later uitvoeren. Voer `az --version` uit om de versie te bekijken. Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli). 

## <a name="deploy-azure-container-registry"></a>Azure Container Registry implementeren

Wanneer u een Azure Container Registry implementeert, hebt u eerst een resourcegroep nodig. Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.

Een resourcegroep maken met de opdracht [az group create](/cli/azure/group#az_group_create). In dit voorbeeld wordt er een resourcegroep met de naam `myResourceGroup` gemaakt in de regio `westeurope`.

```azurecli
az group create --name myResourceGroup --location westeurope
```

Maak een Azure Container Registry met de opdracht [az acr create](/cli/azure/acr#az_acr_create). De naam van een containerregister **moet uniek zijn**.

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Basic
```

In de rest van deze zelfstudie gebruiken we `<acrname>` als tijdelijke aanduiding voor de naam van het containerregister.

## <a name="container-registry-login"></a>Aanmelden bij het containerregister

Gebruik de opdracht [az acr login](https://docs.microsoft.com/cli/azure/acr#az_acr_login) om u aan te melden bij het ACR-exemplaar. Geef de unieke naam op van het containerregister toen dat werd gemaakt.

```azurecli
az acr login --name <acrName>
```

De opdracht retourneert een bericht dat de aanmelding is gelukt.

## <a name="tag-container-images"></a>Containerinstallatiekopieën taggen

Als u een lijst met huidige installatiekopieën wilt weergeven, gebruikt u de opdracht [docker images](https://docs.docker.com/engine/reference/commandline/images/).

```bash
docker images
```

Uitvoer:

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front             latest              4675398c9172        13 minutes ago      694MB
redis                        latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask               788ca94b2313        9 months ago        694MB
```

Elke containerinstallatiekopie moet worden getagd met de loginServer-naam van het register. Deze tag wordt gebruikt voor routering bij het pushen van containerinstallatiekopieën naar een installatiekopieregister.

Voer de volgende opdracht uit om de naam van de loginServer op te vragen.

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

Tag nu de `azure-vote-front`-installatiekopie met de loginServer van het containerregister. Voeg bovendien `:v1` toe aan het eind van de naam van de installatiekopie. Deze tag geeft de versie van de installatiekopie aan.

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:v1
```

Na het taggen voert u [Docker-installatiekopieën] (https://docs.docker.com/engine/reference/commandline/images/) uit om de bewerking te verifiëren.

```bash
docker images
```

Uitvoer:

```bash
REPOSITORY                                           TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front                                     latest              eaf2b9c57e5e        8 minutes ago       716 MB
mycontainerregistry082.azurecr.io/azure-vote-front   v1            eaf2b9c57e5e        8 minutes ago       716 MB
redis                                                latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask                           flask               788ca94b2313        8 months ago        694 MB
```

## <a name="push-images-to-registry"></a>Installatiekopieën naar het register pushen

Push de `azure-vote-front`-installatiekopie naar het register. 

In het volgende voorbeeld vervangt u de naam van de ACR-loginServer door de naam van de loginServer uit uw omgeving.

```bash
docker push <acrLoginServer>/azure-vote-front:v1
```

Dit duurt enkele minuten duren.

## <a name="list-images-in-registry"></a>Installatiekopieën vermelden in het register

U kunt een lijst met installatiekopieën die naar Azure Container Registry zijn gepusht, retourneren met de opdracht [az acr repository list](/cli/azure/acr/repository#az_acr_repository_list). Werk de opdracht bij met de naam van het ACR-exemplaar.

```azurecli
az acr repository list --name <acrName> --output table
```

Uitvoer:

```azurecli
Result
----------------
azure-vote-front
```

Gebruik vervolgens de opdracht [az acr repository show-tags](/cli/azure/acr/repository#show-tags) om de tags voor een specifieke installatiekopie weer te geven.

```azurecli
az acr repository show-tags --name <acrName> --repository azure-vote-front --output table
```

Uitvoer:

```azurecli
Result
--------
v1
```

Bij het voltooien van de zelfstudie is de containerinstallatiekopie opgeslagen in een persoonlijk Azure Container Registry-exemplaar. Deze installatiekopie wordt vanuit ACR geïmplementeerd naar een Kubernetes-cluster in volgende zelfstudies.

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie is een Azure Container Registry voorbereid voor gebruik in een ACS Kubernetes-cluster. De volgende stappen zijn voltooid:

> [!div class="checklist"]
> * Er is een Azure Container Registry-exemplaar geïmplementeerd
> * Er is een containerinstallatiekopie voor ACR getagd
> * De installatiekopie is geüpload naar ACR

Ga naar de volgende zelfstudie voor informatie over het implementeren van een Kubernetes-cluster in Azure.

> [!div class="nextstepaction"]
> [Kubernetes-cluster implementeren](./container-service-tutorial-kubernetes-deploy-cluster.md)