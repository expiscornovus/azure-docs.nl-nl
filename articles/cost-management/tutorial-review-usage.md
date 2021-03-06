---
title: Gebruik en kosten bekijken in Azure Cost Management | Microsoft Docs
description: "Bekijk gebruik en kosten om trends bij te houden, inefficiëntie te detecteren en waarschuwingen te maken."
services: cost-management
keywords: 
author: bandersmsft
ms.author: banders
ms.date: 01/30/2018
ms.topic: tutorial
ms.service: cost-management
ms.custom: mvc
manager: carmonm
ms.openlocfilehash: 72c5c9ff13577e7b4008c42133742d8de4904ae0
ms.sourcegitcommit: 9d317dabf4a5cca13308c50a10349af0e72e1b7e
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 02/01/2018
---
# <a name="review-usage-and-costs"></a>Gebruik en kosten bekijken

Azure Cost Management van Cloudyn geeft gebruik en kosten weer, zodat u trends kunt bijhouden, inefficiëntie kunt detecteren en waarschuwingen kunt maken. Alle gegevens over gebruik en kosten worden weergegeven in Cloudyn-dashboards en -rapporten. Aan de hand van de voorbeelden in deze zelfstudie bekijkt u het gebruik en de kosten met behulp van dashboards en rapporten. In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Gebruiks- en kostentrends bijhouden
> * Inefficiënt gebruik detecteren
> * Waarschuwingen maken voor ongebruikelijke uitgaven of te hoge uitgaven



## <a name="open-the-cloudyn-portal"></a>De Cloudyn-portal openen

U bekijkt het gebruik en de kosten in de Cloudyn-portal. Open de Cloudyn-portal vanuit de Azure Portal of ga naar https://azure.cloudyn.com en meld u aan.

## <a name="track-usage-and-cost-trends"></a>Gebruiks- en kostentrends bijhouden

U houdt de werkelijke uitgaven voor gebruik en kosten bij met rapporten om trends in de loop van de tijd te identificeren. Als u trends wilt bekijken, gebruikt u het rapport Actual Cost Over Time (Werkelijke kosten in de loop van de tijd). Klik op het rapportmenu bovenaan in de portal en klik op **Cost** > **Cost Analysis** > **Actual Cost Over Time**. Wanneer u het rapport voor het eerst opent, zijn er geen groepen of filters op toegepast.

Hier volgt een voorbeeldrapport:

![voorbeeldrapport](./media/tutorial-review-usage/actual-cost01.png)

Het rapport toont alle uitgaven gedurende de afgelopen 30 dagen. Als u alleen uitgaven voor Azure-services wilt weergeven, past u de groep Service toe en filtert u op alle Azure-services. In de volgende afbeelding ziet u de gefilterde services.

![gefilterde services](./media/tutorial-review-usage/actual-cost02.png)

In het voorgaande voorbeeld is vanaf 2017-08-31 minder geld uitgegeven dan daarvoor. Deze kostentrend zet zich ongeveer negen dagen voort voor de verschillende services. Daarna zijn de uitgaven vergelijkbaar met daarvoor. Te veel kolommen kunnen een duidelijke trend echter moeilijk zichtbaar maken. U kunt de rapportweergave wijzigen in een lijn- of vlakdiagram om de gegevens in andere weergaven te zien. In de volgende afbeelding wordt de trend duidelijker weergegeven.

![trend in rapport](./media/tutorial-review-usage/actual-cost03.png)

In het voorbeeld ziet u duidelijk dat de kosten van Azure Storage afnemen vanaf 2017-08-31, terwijl de uitgaven voor andere Azure-services gelijk bleven. Wat veroorzaakte deze verlaging in de uitgaven? In dit voorbeeld waren enkele werknemers met vakantie, zodat ze de Storage-service niet gebruikten.

Zie [Analyzing your cloud billing data vs. time with Azure Cost Management by Cloudyn](https://youtu.be/7LsVPHglM0g) als u een zelfstudievideo wilt bekijken over het bijhouden van gebruiks- en kostentrends.

## <a name="detect-usage-inefficiencies"></a>Inefficiënt gebruik detecteren

Optimalisatierapporten verbeteren de efficiëntie, optimaliseren het gebruik en vinden manieren om geld te besparen dat u uitgeeft aan uw cloudresources. Ze zijn vooral handig voor kosteneffectieve aanbevelingen betreffende afmetingen om zo niet-actieve of dure VM's te helpen verminderen.

Een veelvoorkomend probleem waarmee organisaties te maken krijgen wanneer ze resources naar de cloud verplaatsen, is hun virtualisatiestrategie. Ze hanteren vaak een benadering die vergelijkbaar is met de benadering die ze hanteren voor het maken van virtuele machines voor de on-premises virtualisatieomgeving. En ze gaan ervan uit dat de kosten afnemen wanneer ze hun lokale VM's ongewijzigd naar de cloud verplaatsen. Deze aanpak levert echter waarschijnlijk geen kostenbesparing op.

Het probleem is dat al voor de bestaande infrastructuur is betaald. Als gebruikers dat willen, kunnen ze grote VM's maken en houden, die al dan niet actief zijn, waarbij dit weinig gevolgen heeft. Als grote of niet-actieve VM's naar de cloud worden verplaatst, zullen de kosten echter waarschijnlijk *toenemen*. Kostentoewijzing voor resources is belangrijk wanneer u een overeenkomst sluit met een cloudserviceprovider. U moet betalen voor datgene waartoe u zich verplicht, of u de resource nu volledig gebruikt of helemaal niet.

Het rapport Cost Effective Sizing Recommendations (Aanbevelingen voor kosteneffectieve aanpassingen van de afmetingen) identificeert jaarlijkse besparingen door de capaciteit van VM-exemplaren te vergelijken met historische gegevens over hun CPU- en geheugengebruik.  

Klik op het rapportmenu bovenaan in de portal en klik op **Optimizer** > **Pricing Optimization** > **Cost Effective Sizing Recommendations**. Filter de provider op Azure om alleen Azure-VM's te bekijken. Hier ziet u een voorbeeldafbeelding.

![Azure-VM's](./media/tutorial-review-usage/sizing01.png)

In dit voorbeeld kan $ 3.114 worden bespaard door de aanbevelingen voor het wijzigen van de VM-exemplaartypen op te volgen. Klik op het plusteken (+) onder **Details** voor de eerste aanbeveling. Hier vindt u meer informatie over de eerste aanbeveling.

![details van de aanbeveling](./media/tutorial-review-usage/sizing02.png)

Bekijk de id's van de VM-exemplaren door te klikken op het plusteken naast **List of Candidates**.

![Lijst met kandidaten](./media/tutorial-review-usage/sizing03.png)

Zie [Optimizing VM Size in Azure Cost Management by Cloudyn](https://youtu.be/1xaZBNmV704) als u een zelfstudievideo wilt bekijken over het detecteren van inefficiënt gebruik.

## <a name="create-alerts-for-unusual-spending"></a>Waarschuwingen maken voor ongebruikelijke uitgaven

U kunt belanghebbenden automatisch waarschuwen als er sprake is van afwijkende bestedingen of kans op budgetoverschrijding. U kunt snel en eenvoudig waarschuwingen maken met behulp van rapporten die waarschuwingen op basis van budget en kostendrempels ondersteunen.

U maakt een waarschuwing voor elke uitgave met behulp van een kostenrapport. In dit voorbeeld gebruikt u het rapport Actual Cost Over Time (Werkelijke kosten in de loop van de tijd) om u te waarschuwen wanneer de uitgaven voor een Azure-VM het totale budget naderen. Klik op het rapportmenu bovenaan in de portal en klik op **Cost** > **Cost Analysis** > **Actual Cost Over Time**. Stel **Groups** in op **Service** en stel **Filter on the service** in op **Azure/VM**. Klik rechtsboven in het rapport op **Actions** en selecteer **Schedule report**.

Gebruik het tabblad **Scheduling** om uzelf een e-mail met het rapport te sturen met de gewenste frequentie. Eventuele labels, groepen en filters die u gebruikt, worden toegepast op het rapport dat u per e-mail wordt toegezonden. Klik op het tabblad **Theshold** en selecteer **Actual Cost vs. Threshold**. Als u had een totaal budget van $ 500.000 hebt en een melding wilt ontvangen wanneer de kosten in de buurt van de helft komen, maakt u een **rode waarschuwing** op $ 250.000 en een **gele waarschuwing** op $ 240.000. Kies vervolgens het aantal achtereenvolgende waarschuwingen. Wanneer u het totaal aantal waarschuwingen dat u hebt opgegeven, hebt ontvangen, worden er geen extra waarschuwingen meer verzonden. Sla het geplande rapport op.

![voorbeeldrapport](./media/tutorial-review-usage/schedule-alert01.png)

U kunt ook de drempeloptie Cost Percentage vs. Budget kiezen om waarschuwingen te maken. Als u deze optie kiest, kunt u budgetpercentages in plaats van bedragen gebruiken.


## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u het volgende geleerd:

> [!div class="checklist"]
> * Gebruiks- en kostentrends bijhouden
> * Inefficiënt gebruik detecteren
> * Waarschuwingen maken voor ongebruikelijke uitgaven of te hoge uitgaven


In de volgende zelfstudie leert u hoe u toegang tot gegevens beheert.

> [!div class="nextstepaction"]
> [Toegang tot gegevens beheren](tutorial-user-access.md)
