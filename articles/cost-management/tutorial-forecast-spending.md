---
title: Uitgaven voorspellen met Azure Cost Management | Microsoft Docs
description: Lees hoe u uitgaven kunt voorspellen met behulp van historische gegevens van gebruik en uitgaven.
services: cost-management
keywords: 
author: bandersmsft
ms.author: banders
ms.date: 01/30/2018
ms.topic: tutorial
ms.service: cost-management
ms.custom: mvc
manager: carmonm
ms.openlocfilehash: 03624efc419efe46aef472007b438442ce22eb9c
ms.sourcegitcommit: 9d317dabf4a5cca13308c50a10349af0e72e1b7e
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 02/01/2018
---
# <a name="forecast-future-spending"></a>Toekomstige uitgaven voorspellen

Azure Cost Management van Cloudyn helpt u bij het voorspellen van toekomstige uitgaven aan de hand van historische gegevens van gebruik en uitgaven. U gebruikt rapporten van Cloudyn om gegevens van alle geschatte kosten weer te geven. De voorbeelden in deze zelfstudie laten zien hoe u kostenschattingen kunt controleren met behulp van de rapporten. In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Toekomstige uitgaven voorspellen

## <a name="forecast-future-spending"></a>Toekomstige uitgaven voorspellen

Cloudyn bevat rapporten voor kostenschatting om u helpen bij het voorspellen van uitgaven op basis van uw gebruik in de loop der tijd. Het hoofddoel van de rapporten is ervoor te zorgen dat uw kostentrends niet de verwachtingen van uw organisatie overschrijden. U gebruikt hiervoor de rapporten Current Month Projected Cost en Annual Projected Cost. Beide rapporten tonen de verwachte toekomstige uitgaven als uw gebruik relatief gelijk blijft met het gebruik over de 30 laatste dagen.

Het rapport Current Month Projected Cost toont de kosten van uw services. De geschatte kosten worden bepaald aan de hand van de kosten aan het begin van de maand en van de vorige maand. Klik in het menu Reports boven aan de portal op **Cost** > **Projection and Budget** > **Current Month Projected Cost**. In de volgende afbeelding ziet u een voorbeeld.

![geschatte kosten voor de huidige maand](./media/tutorial-forecast-spending/project-month01.png)

In het voorbeeld kunt u zien voor welke services de uitgaven het hoogst zijn. De kosten voor Azure waren lager dan voor AWS. Als u kostenschattingen wilt zien voor virtuele machines van Azure, selecteert u **Azure/VM** in de lijst **Filter**.

![Geschatte kosten voor virtuele machines van Azure voor de huidige maand](./media/tutorial-forecast-spending/project-month02.png)

Volg dezelfde voorgaande basisstappen om te kijken naar de maandelijkse verwachte kosten voor andere services waarin u geïnteresseerd bent.

Het rapport Annual Projected Cost bevat de geëxtrapoleerde kosten van uw services voor de volgende twaalf maanden.

Klik in het menu Reports boven aan de portal op **Cost** > **Projection and Budget** > **Annual Projected Cost**. In de volgende afbeelding ziet u een voorbeeld.

![rapport met jaarlijkse geschatte kosten](./media/tutorial-forecast-spending/project-annual01.png)

In het voorbeeld kunt u zien voor welke services de uitgaven het hoogst zijn. Net als in het voorbeeld voor een maand zijn de kosten voor Azure lager dan de kosten voor AWS. Als u kostenschattingen wilt zien voor virtuele machines van Azure, selecteert u **Azure/VM** in de lijst **Filter**.

![jaarlijkse geschatte kosten van virtuele machines](./media/tutorial-forecast-spending/project-annual02.png)

In de afbeelding hierboven worden de jaarlijkse kosten van virtuele machines van Azure geschat op $ 28.374.

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie heeft u het volgende geleerd:

> [!div class="checklist"]
> * Toekomstige uitgaven voorspellen


Ga naar de volgende zelfstudie als u wilt leren hoe u kosten kunt beheren met kostentoewijzing en showback-rapporten.

> [!div class="nextstepaction"]
> [Kosten beheren met kostentoewijzing en showback-rapporten](tutorial-manage-costs.md)
