---
title: Azure Data Lake Analytics beheren met Azure-opdrachtregelinterface | Microsoft Docs
description: Informatie over het beheren van Data Lake Analytics-accounts, gegevensbronnen, taken en gebruikers met Azure CLI
services: data-lake-analytics
documentationcenter: 
author: SnehaGunda
manager: Kfile
ms.assetid: 4e5a3a0a-6d7f-43ed-aeb5-c3b3979a1e0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/29/2018
ms.author: sngun
ms.openlocfilehash: edaedaa517a672cd4bad5dc35527f4595ab4a85f
ms.sourcegitcommit: 9d317dabf4a5cca13308c50a10349af0e72e1b7e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 02/01/2018
---
# <a name="manage-azure-data-lake-analytics-using-azure-command-line-interface-cli"></a>Azure Data Lake Analytics beheren met Azure-opdrachtregelinterface (CLI)

[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Informatie over het beheren van Azure Data Lake Analytics-accounts, gegevensbronnen, gebruikers en taken met de Azure CLI. Als u wilt zien management onderwerpen met een ander hulpprogramma, klikt u op het tabblad select bovenaan.


**Vereisten**

Voordat u deze zelfstudie begint, hebt u de volgende bronnen:

* Een Azure-abonnement. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).

* Azure CLI. Zie [Azure CLI installeren en configureren](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest).

   * Download en installeer de **pre-release** [Azure CLI-hulpprogramma’s](https://github.com/MicrosoftBigData/AzureDataLake/releases) om deze demo te voltooien.

* Verifiëren met behulp van de `az login` opdracht in en selecteer het abonnement dat u wilt gebruiken. Zie [Verbinding maken met een Azure-abonnement met Azure CLI](/cli/azure/authenticate-azure-cli) voor meer informatie over verificatie met een werk- of schoolaccount.

   ```azurecli
   az login
   az account set --subscription <subscription id>
   ```

   U kunt nu toegang tot de opdrachten Data Lake Analytics en Data Lake Store. Voer de volgende opdracht voor een lijst met de Data Lake Store en Data Lake Analytics-opdrachten:

   ```azurecli
   az dls -h
   az dla -h
   ```

## <a name="manage-accounts"></a>Accounts beheren

Voordat u een Data Lake Analytics-taken uitvoert, moet u een Data Lake Analytics-account hebben. In tegenstelling tot Azure HDInsight betaalt niet u voor een Analytics-account wanneer deze een taak niet wordt uitgevoerd. U betaalt alleen voor de tijd wanneer deze een taak wordt uitgevoerd.  Zie voor meer informatie [overzicht van Azure Data Lake Analytics](data-lake-analytics-overview.md).  

### <a name="create-accounts"></a>Accounts maken

Voer de volgende opdracht om een Data Lake-account te maken 

   ```azurecli
   az dla account create --account "<Data Lake Analytics account name>" --location "<Location Name>" --resource-group "<Resource Group Name>" --default-data-lake-store "<Data Lake Store account name>"
   ```

### <a name="update-accounts"></a>Bijwerken van accounts

De volgende opdracht werkt u de eigenschappen van een bestaande Data Lake Analytics-Account

   ```azurecli
   az dla account update --account "<Data Lake Analytics Account Name>" --firewall-state "Enabled" --query-store-retention 7
   ```

### <a name="list-accounts"></a>Lijst van accounts

Lijst met Data Lake Analytics-accounts binnen een specifieke resourcegroep

   ```azurecli
   az dla account list "<Resource group name>"
   ```

## <a name="get-details-of-an-account"></a>Details van een account ophalen

   ```azurecli
   az dla account show --account "<Data Lake Analytics account name>" --resource-group "<Resource group name>"
   ```

### <a name="delete-an-account"></a>Een account verwijderen

   ```azurecli
   az dla account delete --account "<Data Lake Analytics account name>" --resource-group "<Resource group name>"
   ```

## <a name="manage-data-sources"></a>Gegevensbronnen beheren

Data Lake Analytics ondersteunt momenteel de volgende twee gegevensbronnen:

* [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md)
* [Azure Storage](../storage/common/storage-introduction.md)

Wanneer u een Analytics-account maakt, moet u een Azure Data Lake Storage-account moet het standaardopslagaccount toewijzen. De standaard Data Lake storage-account wordt gebruikt voor het opslaan van taak metagegevens en taak controlelogboeken. Nadat u een Analytics-account hebt gemaakt, kunt u extra Data Lake Storage-accounts en/of Azure Storage-account toevoegen. 

### <a name="find-the-default-data-lake-store-account"></a>Het Data Lake Store-standaardaccount vinden

U ziet de Data Lake Store-standaardaccount gebruikt door het uitvoeren van de `az dla account show` opdracht. Standaard-accountnaam wordt vermeld onder de eigenschap defaultDataLakeStoreAccount.

   ```azurecli
   az dla account show --account "<Data Lake Analytics account name>"
   ```

### <a name="add-additional-blob-storage-accounts"></a>Aanvullende Blob storage-accounts toevoegen

   ```azurecli
   az dla account blob-storage add --access-key "<Azure Storage Account Key>" --account "<Data Lake Analytics account name>" --storage-account-name "<Storage account name>"
   ```

> [!NOTE]
> Alleen Blob storage korte namen worden ondersteund. Gebruik geen FQDN-naam, bijvoorbeeld 'myblob.blob.core.windows.net'.
> 

### <a name="add-additional-data-lake-store-accounts"></a>Extra Data Lake Store-accounts toevoegen

De volgende opdracht updates van de opgegeven Data Lake Analytics-account met een extra Data Lake Store-account:

   ```azurecli
   az dla account data-lake-store add --account "<Data Lake Analytics account name>" --data-lake-store-account-name "<Data Lake Store account name>"
   ```

### <a name="update-existing-data-source"></a>Bestaande gegevensbron bijwerken

Een bestaande sleutel voor Blob storage-account bijwerken:

   ```azurecli
   az dla account blob-storage update --access-key "<New Blob Storage Account Key>" --account "<Data Lake Analytics account name>" --storage-account-name "<Data Lake Store account name>"
   ```

### <a name="list-data-sources"></a>Lijst van gegevensbronnen:

Overzicht van de Data Lake Store-accounts:

   ```azurecli
   az dla account data-lake-store list --account "<Data Lake Analytics account name>"
   ```

Overzicht van de Blob storage-account:

   ```azurecli
   az dla account blob-storage list --account "<Data Lake Analytics account name>"
   ```

![Gegevensbron voor Data Lake Analytics-lijst](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-data-source.png)

### <a name="delete-data-sources"></a>Gegevensbronnen verwijderen:
Een Data Lake Store-account verwijderen:

   ```azurecli
   az dla account data-lake-store delete --account "<Data Lake Analytics account name>" --data-lake-store-account-name "<Azure Data Lake Store account name>"
   ```

Een Blob storage-account verwijderen:

   ```azurecli
   az dla account blob-storage delete --account "<Data Lake Analytics account name>" --storage-account-name "<Data Lake Store account name>"
   ```

## <a name="manage-jobs"></a>Taken beheren
U moet een Data Lake Analytics-account hebben voordat u een taak kunt maken.  Zie voor meer informatie [beheren Data Lake Analytics-accounts](#manage-accounts).

### <a name="list-jobs"></a>Taken weergeven

   ```azurecli
   az dla job list --account "<Data Lake Analytics account name>"
   ```

   ![Gegevensbron voor Data Lake Analytics-lijst](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-jobs.png)

### <a name="get-job-details"></a>Taakdetails van de ophalen

   ```azurecli
   az dla job show --account "<Data Lake Analytics account name>" --job-identity "<Job Id>"
   ```

### <a name="submit-jobs"></a>Verzenden van taken

> [!NOTE]
> De laagste prioriteit van een taak is 1000 en de standaard graad van parallelle uitvoering voor een taak is 1.
> 
   ```azurecli
   az dla job submit --account "<Data Lake Analytics account name>" --job-name "<Name of your job>" --script "<Script to submit>"
   ```

### <a name="cancel-jobs"></a>Taken annuleren
Gebruik de opdracht lijst zoeken naar de taak-id en gebruik vervolgens annuleren om te annuleren de taak.

   ```azurecli
   az dla job cancel --account "<Data Lake Analytics account name>" --job-identity "<Job Id>"
   ```

## <a name="use-azure-resource-manager-groups"></a>Azure Resource Manager-groepen gebruiken
Toepassingen bestaan in het algemeen uit meerdere onderdelen, bijvoorbeeld een web-app, database, databaseserver, opslag en services van derden. Azure Resource Manager kunt u werken met de resources in uw toepassing als groep, aangeduid als een Azure-resourcegroep. U kunt implementeren, bijwerken, bewaken of verwijdert alle resources voor uw toepassing in een enkele, gecoördineerde bewerking. Voor implementatie gebruikt u een sjabloon. Deze sjabloon kan voor verschillende omgevingen worden gebruikt, zoals testen, faseren en productie. U kunt facturering voor uw organisatie verduidelijken door de samengevoegde kosten voor de hele groep weer te geven. Zie [Overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) voor meer informatie. 

Een Data Lake Analytics-service kan de volgende onderdelen bevatten:

* Azure Data Lake Analytics-account
* Vereiste standaard Azure Data Lake Storage-account
* Aanvullende Azure Data Lake Storage-accounts
* Extra Azure Storage-accounts

U kunt al deze onderdelen onder één Resource Manager-groep zodat ze gemakkelijker te beheren.

![Azure Data Lake Analytics-account en opslag](./media/data-lake-analytics-manage-use-portal/data-lake-analytics-arm-structure.png)

Een Data Lake Analytics-account en de afhankelijke storage-accounts moeten in dezelfde Azure-datacenter worden geplaatst.
De Resource Manager-groep kan echter in een ander datacenter worden geplaatst.  

## <a name="see-also"></a>Zie ook
* [Overzicht van Microsoft Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [Aan de slag met Data Lake Analytics met Azure Portal](data-lake-analytics-get-started-portal.md)
* [Azure Data Lake Analytics beheren met Azure Portal](data-lake-analytics-manage-use-portal.md)
* [Azure Data Lake Analytics-taken bewaken en problemen oplossen met Azure Portal](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

