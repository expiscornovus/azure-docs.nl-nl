---
title: Importeren van een SOAP-API en converteer deze naar REST met de Azure portal | Microsoft Docs
description: Informatie over het importeren van een SOAP-API en converteer deze naar REST met API Management.
services: api-management
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 11/22/2017
ms.author: apimpm
ms.openlocfilehash: 74935f11d5bf3c83aef46c1d41fccd81ad312acb
ms.sourcegitcommit: b854df4fc66c73ba1dd141740a2b348de3e1e028
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/04/2017
---
# <a name="import-a-soap-api-and-convert-to-rest"></a>Importeren van een SOAP-API en converteer deze naar REST

In dit artikel laat zien hoe een SOAP-API importeren en converteer deze naar de REST. Ook wordt uitgelegd hoe u kunt de API APIM testen.

In dit artikel leert u hoe:

> [!div class="checklist"]
> * Importeren van een SOAP-API en converteer deze naar REST
> * De API testen in de Azure-portal
> * De API testen in de portal voor ontwikkelaars

## <a name="prerequisites"></a>Vereisten

Voltooi de volgende Snelstartgids: [Azure API Management-exemplaar maken](get-started-create-service-instance.md)

[!INCLUDE [api-management-navigate-to-instance.md](../../includes/api-management-navigate-to-instance.md)]

## <a name="create-api"></a>Importeren en publiceren van een back-end-API

1. Selecteer **API's** uit onder **API MANAGEMENT**.
2. Selecteer **WSDL** van de **een nieuwe API toevoegen** lijst.

    ![SOAP-API](./media/restify-soap-api/wsdl-api.png)
3. In de **WSDL-specificatie**, geef de URL op waar de SOAP-API is opgeslagen.
4. Klik op **SOAP voor REST** keuzerondje. Wanneer deze optie wordt geklikt, wordt APIM probeert te maken van een automatische transformatie tussen XML en JSON. In dit geval consumenten moeten worden de API aanroept als een restful-API die resulteert in JSON. APIM is elke aanvraag converteren naar een SOAP-aanroep.

    ![SOAP naar REST](./media/restify-soap-api/soap-to-rest.png)

5. Druk op tab.

    De volgende velden ophalen gevuld met de gegevens van de SOAP-API: weergavenaam, naam, beschrijving.
6. Voeg een URL van de API-achtervoegsel. Het achtervoegsel is een naam op die deze specifieke API in dit exemplaar APIM identificeert. Er moet uniek zijn in dit exemplaar APIM.
9. De API door de API koppelen aan een product publiceren. In dit geval wordt de '*onbeperkt*' product wordt gebruikt.  Als u wilt dat voor de API worden gepubliceerd en beschikbaar voor ontwikkelaars, kunt u deze toevoegen aan een product. U kunt dit doen tijdens het maken van de API of later instellen.

    Producten zijn de koppelingen van een of meer API's. U kunt een aantal API's en ze bieden voor ontwikkelaars via de portal voor ontwikkelaars. Ontwikkelaars zich eerst abonneren op een product ze toegang krijgen tot de API. Wanneer ze zich abonneert, krijgen ze een abonnementssleutel die geschikt is voor API in dat product. Als u de APIM exemplaar gemaakt, bent u een beheerder al, zodat u bent geabonneerd op elk product standaard.

    Standaard wordt elk API Management-exemplaar geleverd met twee voorbeeldproducten:

    * **Starter**
    * **Onbeperkt**   
10. Selecteer **Maken**.

## <a name="test-the-new-apim-api-in-the-azure-portal"></a>De nieuwe APIM API testen in de Azure-portal

Bewerkingen kunnen rechtstreeks vanuit de Azure portal, die een handige manier om te bekijken en te testen van de bewerkingen van een API worden aangeroepen.  

1. Selecteer de API die u in de vorige stap hebt gemaakt.
2. Druk op de **Test** tabblad.
3. Selecteer een bewerking.

    De pagina wordt weergegeven voor queryparameters en velden voor de headers. Een van de headers is 'Ocp-Apim-Subscription-Key' voor de abonnementssleutel van het product dat is gekoppeld aan deze API. Als u het exemplaar APIM hebt gemaakt, bent u beheerder al, zodat de sleutel wordt automatisch ingevuld. 
1. Druk op **verzenden**.

    Back-end reageert met **200 OK** en bepaalde gegevens.

## <a name="call-operation"> </a>Een bewerking aanroepen vanuit de ontwikkelaarsportal

Bewerkingen kunnen ook worden aangeroepen **ontwikkelaarsportal** voor het testen van API's. 

1. Selecteer de API die u hebt gemaakt in de ' importeren en publiceren van een back-end-API ' stap.
2. Druk op **ontwikkelaarsportal**.

    De site 'Ontwikkelaarsportal' wordt geopend.
3. Selecteer de **API** die u hebt gemaakt.
4. Klik op de bewerking die u wilt testen.
5. Druk op **Try it**.
6. Druk op **verzenden**.
    
    Nadat een bewerking is aangeroepen, worden in de ontwikkelaarsportal de **antwoordstatus**, de **antwoordheaders** en eventuele **antwoordinhoud** weergegeven.

[!INCLUDE [api-management-navigate-to-instance.md](../../includes/api-management-append-apis.md)]

[!INCLUDE [api-management-define-api-topics.md](../../includes/api-management-define-api-topics.md)]

## <a name="next-steps"></a>Volgende stappen

> [!div class="nextstepaction"]
> [Transformeren en een gepubliceerde API beveiligen](transform-api.md)