---
title: Azure beheeroplossingen | Microsoft Docs
description: Oplossingen voor opnemen verpakte beheerscenario's in Azure die klanten aan de werkruimte voor logboekanalyse toevoegen kunnen.  Dit artikel bevat informatie over hoe aangepaste oplossingen die zijn gemaakt door klanten en partners.
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 1f054a4e-6243-4a66-a62a-0031adb750d8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/01/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d46b869815fef44a8137bb5121133a1c0140ca30
ms.sourcegitcommit: d87b039e13a5f8df1ee9d82a727e6bc04715c341
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 02/21/2018
---
# <a name="working-with-management-solutions-in-azure-preview"></a>Werken met oplossingen voor beheer in Azure (Preview)
> [!NOTE]
> Dit is voorlopige documentatie voor beheeroplossingen in Azure die zich momenteel in preview.    
> 
> 

Oplossingen voor het beheer zijn verpakt beheerscenario die klanten aan Azure-omgeving toevoegen kunnen.  Naast [oplossingen die worden geleverd door Microsoft](../log-analytics/log-analytics-add-solutions.md), partners en klanten beheersystemen worden gebruikt in hun eigen omgeving of beschikbaar gesteld aan klanten via de community kunnen maken.

## <a name="finding-and-installing-management-solutions"></a>Zoeken en installeren van oplossingen voor het beheer
Er zijn meerdere methoden voor het vinden en te installeren van oplossingen voor het beheer, zoals beschreven in de volgende secties.

### <a name="azure-marketplace"></a>Azure Marketplace
Oplossingen voor het beheer door Microsoft geleverd en vertrouwde partners kunnen worden geïnstalleerd vanuit Azure Marketplace in de Azure portal.

1. Meld u aan bij Azure Portal.
2. Selecteer in het linkerdeelvenster **alle services**.
3. Een Schuif omlaag naar **oplossingen** of type *oplossingen* in de **Filter** dialoogvenster.
4. Klik op de **+ toevoegen** knop.
5. Zoeken naar oplossingen die u geïnteresseerd in een door te bladeren bent, te klikken op de **Filter** uit-knop of typen in de **Search Everthing** vak.
6. Klik op een marketplace-item om gedetailleerde informatie weer te geven.
7. Klik op **maken** openen de **oplossing toevoegen** deelvenster.
8. U wordt gevraagd naar de vereiste informatie zoals de [werkruimte voor logboekanalyse en Automation-account](#log-analytics-workspace-and-automation-account) naast de waarden voor parameters die in de oplossing.
9. Klik op **maken** voor het installeren van de oplossing.

### <a name="oms-portal"></a>OMS-Portal
Beheeroplossingen geleverd door Microsoft, kunnen worden geïnstalleerd vanuit de galerie oplossingen in de OMS-portal.

1. Aanmelden bij de OMS-portal.
2. Klik op de **galerie met oplossingen** tegel.
3. Meer informatie over de verschillende beschikbare oplossingen op de pagina Galerie met OMS-oplossingen. Klik op de naam van de oplossing die u wilt toevoegen.
4. Op de pagina voor de oplossing die u hebt gekozen, wordt gedetailleerde informatie over de oplossing weergegeven. Klik op **Add**.
5. Een nieuwe tegel voor de oplossing die u hebt toegevoegd wordt weergegeven in het overzicht van de pagina in de portal en u kunt deze gaan gebruiken nadat logboekanalyse uw gegevens verwerkt.

### <a name="azure-quickstart-templates"></a>Azure-snelstartsjablonen
Leden van de community kunnen beheeroplossingen voor Azure-Snelstartsjablonen verzenden.  Kunt u deze sjablonen voor de installatie later downloaden of controleren ze voor meer informatie over hoe [maken van uw eigen oplossingen](#creating-a-solution).

1. Volg de procedure beschreven in [werkruimte voor logboekanalyse en Automation-account](#log-analytics-workspace-and-automation-account) om een werkruimte en de account te koppelen.
2. Ga naar [Azure-Snelstartsjablonen](https://azure.microsoft.com/documentation/templates/).  
3. Zoeken naar een oplossing waarmee u geïnteresseerd bent in.
4. Selecteer de oplossing in de resultaten om de details ervan weer te geven.
5. Klik op de **implementeren in Azure** knop.
6. U wordt gevraagd naar informatie zoals de resourcegroep en locatie naast de waarden voor alle parameters in de oplossing.
7. Klik op **aankoop** voor het installeren van de oplossing.

### <a name="deploy-azure-resource-manager-template"></a>Azure Resource Manager-sjabloon implementeren
Oplossingen die u via de community of die u hebt [zelf maken](#creating-a-solution) worden geïmplementeerd als een Resource Manager-sjabloon en u kunt een van de standaardmethoden voor [implementeren van een sjabloon](../azure-resource-manager/resource-group-template-deploy-portal.md).  Opmerking voordat u de oplossing installeert, moet u maakt en koppelt de [werkruimte voor logboekanalyse en Automation-account](#log-analytics-workspace-and-automation-account).

## <a name="log-analytics-workspace-and-automation-account"></a>Log Analytics-werkruimte en de Automation-account
De meeste oplossingen vereisen een [werkruimte voor logboekanalyse](../log-analytics/log-analytics-manage-access.md) bevat weergaven en een [Automation-account](../automation/automation-security-overview.md#automation-account-overview) runbooks en verwante resources bevat. De werkruimte en de account moeten voldoen aan de volgende vereisten.

* Een oplossing kan alleen een werkruimte voor logboekanalyse en een Automation-account gebruiken.  
* De werkruimte voor logboekanalyse en de Automation-account gebruikt door een oplossing moeten worden gekoppeld aan elkaar. Een werkruimte voor logboekanalyse kan alleen worden gekoppeld aan een Automation-account en een Automation-account kan alleen worden gekoppeld aan een werkruimte voor logboekanalyse.
* De werkruimte voor logboekanalyse en de Automation-account om te worden gekoppeld, moeten zich in dezelfde resourcegroep en regio.  De uitzondering hierop is een werkruimte in de regio VS-Oost en en de Automation-account in VS-Oost 2.

### <a name="creating-a-link-between-a-log-analytics-workspace-and-automation-account"></a>Maken van een koppeling tussen een werkruimte voor logboekanalyse en een Automation-account
Hoe u de werkruimte voor logboekanalyse en de Automation-account opgeven, is afhankelijk van de installatiemethode voor uw oplossing.

* Wanneer u een oplossing van Microsoft via de OMS-portal installeert, wordt deze in de huidige werkruimte is geïnstalleerd en er zijn geen Automation-account is vereist.
* U wordt gevraagd om een werkruimte en de Automation-account en de koppeling tussen beide voor u is gemaakt tijdens de installatie van een oplossing via de Azure Marketplace.  
* Voor oplossingen buiten Azure Marketplace, moet u de werkruimte voor logboekanalyse en de Automation-account koppelen voordat de installatie van de oplossing.  U kunt dit doen door een oplossing in Azure Marketplace selecteren en klikken op de werkruimte voor logboekanalyse en de Automation-account.  U moet niet de oplossing daadwerkelijk worden geïnstalleerd omdat de koppeling wordt gemaakt als de werkruimte voor logboekanalyse en de Automation-account zijn geselecteerd.  Zodra de koppeling is gemaakt, kunt u voor een oplossing die werkruimte voor logboekanalyse en de Automation-account gebruiken. 

### <a name="verifying-the-link-between-a-log-analytics-workspace-and-automation-account"></a>Verifiëren van de koppeling tussen een werkruimte voor logboekanalyse en een Automation-account
U kunt controleren of de koppeling tussen een werkruimte voor logboekanalyse en een Automation-account met de volgende procedure.

1. Selecteer het Automation-account in de Azure-portal.
2. Als de **werkruimte** instellen in de **verwante Resources** gedeelte van het menu is ingeschakeld, moet dit account is gekoppeld aan een werkruimte voor logboekanalyse.  U kunt klikken op **werkruimte** om de details van de werkruimte te bekijken.

## <a name="listing-management-solutions"></a>Oplossingen voor het beheer van aanbieding
Gebruikt de volgende procedure om de beheeroplossingen weergeven in de werkruimten die is gekoppeld aan uw Azure-abonnement.

1. Meld u aan bij Azure Portal.
2. Selecteer in het linkerdeelvenster **alle services**.
3. Een Schuif omlaag naar **oplossingen** of type *oplossingen* in de **Filter** dialoogvenster.
4. Oplossingen die zijn geïnstalleerd in al uw werkruimten wordt weergegeven.

Houd er rekening mee dat u alleen de Microsoft-oplossingen die zijn geïnstalleerd in de huidige werkruimte met de OMS-portal kunt weergeven.

## <a name="removing-a-management-solution"></a>Een oplossing voor het beheer verwijderen
Wanneer een oplossing voor het beheer wordt verwijderd, worden alle resources in de oplossing ook verwijderd.  

1. De oplossing niet vinden in de Azure-portal met behulp van de procedure in [aanbieding oplossingen](#listing-solutions).
2. Selecteer de oplossing die u wilt verwijderen.
3. Klik op de **verwijderen** knop.

## <a name="creating-a-management-solution"></a>Maken van een beheeroplossing
Volledige informatie over het maken van oplossingen zijn beschikbaar op [om oplossingen te maken in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md). 

## <a name="next-steps"></a>Volgende stappen
* Search [Azure-Snelstartsjablonen](https://azure.microsoft.com/documentation/templates) voor voorbeelden van andere Resource Manager-sjablonen.
* Maak uw eigen [beheeroplossingen](operations-management-suite-solutions-creating.md).

