---
title: Maken, wijzigen of een virtueel netwerk van Azure-peering verwijderen | Microsoft Docs
description: Informatie over het maken, wijzigen of verwijderen van een virtueel netwerk peering.
services: virtual-network
documentationcenter: na
author: jimdial
manager: jeconnoc
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/09/2018
ms.author: jdial;anavin
ms.openlocfilehash: 0dc19abcf010f5c0bc50534941e7b80a9665869e
ms.sourcegitcommit: 4723859f545bccc38a515192cf86dcf7ba0c0a67
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 02/11/2018
---
# <a name="create-change-or-delete-a-virtual-network-peering"></a>Maken, wijzigen of een virtueel netwerk-peering verwijderen

Informatie over het maken, wijzigen of verwijderen van een virtueel netwerk peering. Virtueel netwerk peering, kunt u virtuele netwerken zijn verbonden via de Azure-backbone-netwerk. Zodra de peer is ingesteld, worden de virtuele netwerken nog steeds beheerd als afzonderlijke resources. Als u niet bekend bent met het virtuele netwerk peering bent, raden wij aan lezen de [peering Virtual network-overzicht](virtual-network-peering-overview.md) en het uitvoeren van de [maken van een virtueel netwerk peering zelfstudie](virtual-network-create-peering.md), voordat de taken in dit artikel is voltooid.

Peering van virtuele netwerken in dezelfde regio's is algemeen beschikbaar. Virtuele netwerken in verschillende regio's is momenteel in preview-peering. Zie [virtuele netwerk updates](https://azure.microsoft.com/en-us/updates/?product=virtual-network) voor beschikbare regio's. U moet [registreren van uw abonnement voor de preview](virtual-network-create-peering.md).

> [!WARNING]
> Peerings van virtuele netwerken die in dit scenario worden gemaakt, hebben mogelijk niet dezelfde mate van beschikbaarheid en betrouwbaarheid als scenario's waarbij een versie met algemene beschikbaarheid wordt gebruikt. Sommige functies van gekoppelde virtuele netwerken zijn mogelijk beperkt of zijn niet beschikbaar in alle Azure-regio's. Controleer de pagina [Azure Virtual Network-updates](https://azure.microsoft.com/updates/?product=virtual-network) voor de meest recente meldingen over de beschikbaarheid en de status van deze functie.
>

## <a name="before-you-begin"></a>Voordat u begint

De volgende taken uitvoeren voordat u stappen uitvoert in elke sectie van dit artikel:

- Als u nog een Azure-account hebt, zich aanmelden voor een [gratis proefaccount](https://azure.microsoft.com/free).
- Als u de portal gebruikt, open https://portal.azure.com en meld u aan met uw Azure-account.
- Als u de PowerShell-opdrachten voor het uitvoeren van taken in dit artikel, ofwel de opdrachten uitvoert in de [Azure Cloud Shell](https://shell.azure.com/powershell), of door te voeren PowerShell vanaf uw computer. Azure Cloud Shell is een gratis interactieve shell waarmee u de stappen in dit artikel kunt uitvoeren. In deze shell zijn algemene Azure-hulpprogramma's vooraf geïnstalleerd en geconfigureerd voor gebruik met uw account. Deze zelfstudie vereist de Azure PowerShell-moduleversie 5.2.0 of hoger. Voer `Get-Module -ListAvailable AzureRM` de geïnstalleerde versie vinden. Als u PowerShell wilt upgraden, raadpleegt u [De Azure PowerShell-module installeren](/powershell/azure/install-azurerm-ps). Als u PowerShell lokaal uitvoert, moet u ook `Login-AzureRmAccount` uitvoeren om verbinding te kunnen maken met Azure.
- Als u Azure-opdrachtregelinterface (CLI)-opdrachten voor het uitvoeren van taken in dit artikel, ofwel de opdrachten uitvoert in de [Azure Cloud Shell](https://shell.azure.com/bash), of door het uitvoeren van de CLI vanaf uw computer. Deze zelfstudie vereist de Azure CLI versie 2.0.26 of hoger. Voer `az --version` de geïnstalleerde versie vinden. Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren](/cli/azure/install-azure-cli). Als u de Azure CLI lokaal uitvoert, moet u ook uitvoeren `az login` geen verbinding maken met Azure.

## <a name="create-a-peering"></a>Een peering maken

>[!NOTE]
>Voordat u maakt een peering, zorg ervoor dat u hebt uw familiarized de [vereisten en beperkingen](#requirements-and-constraints) en [vereist machtigingen](#permissions).
>

1. Voer in het zoekvak boven aan de portal *virtuele netwerken* in het zoekvak. Wanneer **virtuele netwerken** wordt weergegeven in de zoekresultaten, selecteer deze. Selecteer niet **virtuele netwerken (klassiek)** als deze wordt weergegeven in de lijst als u een peering van een virtueel netwerk te implementeren via het klassieke implementatiemodel niet maken.
2. Selecteer het virtuele netwerk in de lijst die u maken van een peering wilt voor.
3. Selecteer het virtuele netwerk dat u maken van een peering wilt voor in de lijst met virtuele netwerken.
4. Onder **instellingen**, selecteer **Peerings**.
5. Selecteer **+ toevoegen**. 
6. <a name="add-peering"></a>Typ of Selecteer waarden voor de volgende instellingen:
    - **Naam:** de naam voor de peering moet uniek zijn binnen het virtuele netwerk.
    - **Virtueel netwerk implementatiemodel:** selecteren welke deployment model voor het virtuele netwerk dat u wilt met peer via is geïmplementeerd.
    - **Ik weet mijn resource-ID:** hebt u leestoegang tot het virtuele netwerk dat u wilt met peer, laat u dit selectievakje uitgeschakeld. Als er geen leestoegang tot het virtuele netwerk of een abonnement dat u wilt met peer, schakel dit selectievakje in. Voer de volledige resource-ID van het virtuele netwerk dat u wilt met peer in de **Resource-ID** vak die werden weergegeven wanneer u het selectievakje ingeschakeld. De resource-ID die u moet voor een virtueel netwerk dat in de dezelfde Azure bestaat [regio](https://azure.microsoft.com/regions) als dit virtuele netwerk. Als u wilt een virtueel netwerk selecteert in een andere regio [registreren van uw abonnement voor de preview.](virtual-network-create-peering.md) De volledige resource-ID op /subscriptions/ lijkt<Id>/resourceGroups/ < resource-group-name > /providers/Microsoft.Network/virtualNetworks/ < virtuele-netwerk-name >. U kunt de resource-ID voor een virtueel netwerk ophalen door de eigenschappen voor een virtueel netwerk weer te geven. Zie voor meer informatie over de eigenschappen voor een virtueel netwerk, [virtuele netwerken beheren](virtual-network-manage-network.md#view-vnet).
    - **Abonnement:** selecteert u de [abonnement](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) van het virtuele netwerk dat u wilt dat als peer dienen. Een of meer abonnementen worden vermeld, afhankelijk van hoeveel abonnementen uw account leestoegang tot heeft. Als u gecontroleerd of de **Resource-ID** selectievakje, deze instelling is niet beschikbaar.
    - **Virtueel netwerk:** Selecteer het virtuele netwerk dat u wilt dat als peer dienen. U kunt een virtueel netwerk gemaakt via de Azure-implementatiemodel selecteren. Als u wilt een virtueel netwerk selecteert in een andere regio [registreren van uw abonnement voor de preview.](virtual-network-create-peering.md) U moet beschikken over leestoegang aan het virtuele netwerk om te worden weergegeven in de lijst. Als een virtueel netwerk wordt vermeld, maar lichter gekleurd weergegeven, is het mogelijk is de adresruimte voor het virtuele netwerk met de adresruimte voor dit virtuele netwerk overlapt. Als het virtuele netwerk adresruimten elkaar overlappen, ze kunnen niet worden ingesteld als peer. Als u gecontroleerd of de **Resource-ID** selectievakje, deze instelling is niet beschikbaar.
    - **Toestaan van toegang tot het virtuele netwerk:** Selecteer **ingeschakeld** (standaard) als u wilt inschakelen van communicatie tussen de twee virtuele netwerken. Inschakelen van communicatie tussen virtuele netwerken kunt resources die zijn verbonden met een virtueel netwerk met elkaar communiceren met de bandbreedte en de latentie als ze zijn verbonden met hetzelfde virtuele netwerk. Alle communicatie tussen bronnen in de twee virtuele netwerken is via het particuliere netwerk van Azure. De **VirtualNetwork** standaardlabel voor netwerkbeveiligingsgroepen omvat het virtuele netwerk en het virtuele netwerk peer is ingesteld. Lees voor meer informatie over beveiliging groep standaard netwerktags de [netwerk beveiligingsgroepen overzicht](virtual-networks-nsg.md#default-tags) artikel.  Selecteer **uitgeschakelde** als u niet dat verkeer wilt toe aan het peered virtuele netwerk. U kunt bijvoorbeeld selecteren **uitgeschakelde** als u een virtueel netwerk met een ander virtueel netwerk hebt brengen, maar soms wilt uitschakelen van netwerkverkeer tussen de twee virtuele netwerken. U kunt in-/ uitschakelen handiger vindt dan verwijderen en opnieuw maken van peerings. Wanneer deze instelling is uitgeschakeld, verkeersstroom niet tussen de peered virtuele netwerken.
    - **Toestaan van doorgestuurd verkeer:** Schakel dit selectievakje in zodat verkeer *doorgestuurd* door een virtueel netwerkapparaat in een virtueel netwerk (die niet afkomstig zijn van het virtuele netwerk) naar de stroom met dit virtuele netwerk via een peering . Denk bijvoorbeeld drie virtuele netwerken met de naam Spoke1 Spoke2 en Hub. Een peering bestaat tussen elke spoke virtueel netwerk en het virtuele netwerk Hub, maar peerings niet bestaan tussen de spoke virtuele netwerken. Een virtueel netwerkapparaat wordt geïmplementeerd in het virtuele netwerk Hub en de gebruiker gedefinieerde routes worden toegepast op elke spoke virtueel netwerk dat verkeer tussen de subnetten via het virtuele netwerkapparaat routeren. Als dit selectievakje niet is ingeschakeld voor de peering tussen elke spoke virtueel netwerk en het virtuele netwerk hub, verkeersstroom niet tussen de virtuele netwerken spoke omdat de hub is het verkeer tussen virtuele netwerken doorsturen. Inschakelen van deze mogelijkheid kunt u de doorgestuurd verkeer via de peering, creëert ze geen een gebruiker gedefinieerde routes of virtuele netwerkapparaten. Gebruiker gedefinieerde routes en virtuele netwerkapparaten worden afzonderlijk gemaakt. Meer informatie over [gebruiker gedefinieerde routes](virtual-networks-udr-overview.md#user-defined). U hoeft niet te controleren met deze instelling als verkeer wordt doorgestuurd tussen virtuele netwerken via een Azure VPN-Gateway.
    - **Gateway-doorvoer toestaan:** Schakel dit selectievakje in als u een virtuele netwerkgateway is gekoppeld aan dit virtuele netwerk hebt en wilt toestaan dat verkeer van de peered virtueel netwerk via de gateway stromen. Dit virtuele netwerk kan bijvoorbeeld worden gekoppeld aan een on-premises netwerk via een virtuele netwerkgateway. De gateway kan een ExpressRoute- of VPN-gateway zijn. Dit selectievakje inschakelt, kunt verkeer van de peered virtueel netwerk via de gateway die is gekoppeld aan dit virtuele netwerk naar de on-premises netwerk stromen. Als u dit selectievakje inschakelt, is het peered virtuele netwerk geen een gateway is geconfigureerd. De peered virtuele netwerk moet hebben de **externe gateways gebruiken** selectievakje gecontroleerd bij het instellen van de peering van het virtuele netwerk in dit virtuele netwerk. Als u laat dit selectievakje uitgeschakeld (standaard), verkeer uit het virtuele netwerk brengen nog steeds stromen in dit virtuele netwerk, maar kan niet door een virtuele netwerkgateway is gekoppeld aan dit virtuele netwerk stromen. 
    
    Naast het doorsturen van verkeer naar een on-premises netwerk, kan een VPN-gateway doorsturen van netwerkverkeer tussen virtuele netwerken die brengen met het virtuele netwerk dat de gateway, zonder de virtuele netwerken dat is moet worden ingesteld als peer met elkaar. Dit is handig als u wilt gebruiken een VPN-gateway in een hub (Zie de hub en spoke-voorbeeld beschreven voor **doorgestuurd verkeer toestaan**) virtuele netwerk verkeer leiden tussen spoke virtuele netwerken die niet zijn gekoppeld met elkaar. Meer informatie over [virtuele netwerkgateways](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#s2smulti). Dit scenario vereist de implementatie van de gebruiker gedefinieerde routes die de virtuele netwerkgateway als het volgende hoptype opgeeft. Meer informatie over [gebruiker gedefinieerde routes](virtual-networks-udr-overview.md#user-defined). U kunt een VPN-gateway alleen opgeven als een volgend hoptype in een door de gebruiker gedefinieerde route, u kunt een ExpressRoute-gateway als het volgende hoptype in een door de gebruiker gedefinieerde route opgeven.

        You cannot enable this option if you're peering a virtual network (Resource Manager) with a virtual network (classic). Though the traffic flows between the two virtual networks, the virtual network (classic) traffic cannot flow through a network gateway attached to the virtual network (Resource Manager). 

    - **Externe gateways gebruiken:** Schakel dit selectievakje in zodat het verkeer van dit virtuele netwerk door een virtuele netwerkgateway gekoppeld aan het virtuele netwerk u bent peering met stromen. Het virtuele netwerk dat u bent peering met heeft bijvoorbeeld een VPN-gateway gekoppeld waarmee de communicatie met een on-premises netwerk.  Dit selectievakje inschakelt, kunt verkeer van dit virtuele netwerk via de VPN-gateway gekoppeld aan het peered virtuele netwerk. Als u dit selectievakje inschakelt, het peered virtuele netwerk moet een virtuele netwerkgateway is gekoppeld en moet de **toestaan gateway onderweg** selectievakje ingeschakeld. Als u niets in dit vak uitgeschakeld (standaard), het verkeer van de peered virtueel netwerk kunt nog steeds in dit virtuele netwerk, maar het kan niet verloopt via een virtuele netwerkgateway gekoppeld aan deze virtuele netwerk. 
Slechts één peering voor dit virtuele netwerk, kan deze instelling is ingeschakeld hebben.
U kunt deze instelling niet gebruiken als u al een gateway is geconfigureerd in uw virtuele netwerk.
        U kunt deze optie niet inschakelen als u een virtueel netwerk (Resource Manager) met een virtueel netwerk (klassiek) bent peering. Hoewel de verkeersstromen tussen de twee virtuele netwerken, kan niet het virtuele (Resource Manager)-netwerkverkeer via een netwerkgateway is gekoppeld aan het virtuele netwerk (klassiek) stromen.

7. Klik op de **OK** knop het subnet toevoegen aan het virtuele netwerk dat u hebt geselecteerd.

### <a name="commands"></a>Opdrachten

- Azure CLI: [az network vnet-peering maken](/cli/azure/network/vnet/peering#create)
- PowerShell: [Add-AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/add-azurermvirtualnetworkpeering)

### <a name="scenarios"></a>Scenario's

Peering in virtuele netwerken kan tot stand worden gebracht tussen virtuele netwerken die zijn gemaakt via hetzelfde implementatiemodel of via verschillende implementatiemodellen die tot hetzelfde abonnement of tot verschillende abonnementen behoren. Voer een stapsgewijze zelfstudie voor een van de volgende scenario's:
 
|Azure-implementatiemodel  | Abonnement  |
|---------|---------|
|Beide in Resource Manager |[Hetzelfde](virtual-network-create-peering.md)|
| |[Verschillend](create-peering-different-subscriptions.md)|
|Eén in Resource Manager, één klassiek     |[Hetzelfde](create-peering-different-deployment-models.md)|
| |[Verschillend](create-peering-different-deployment-models-subscriptions.md)|

## <a name="view-or-change-peering-settings"></a>Peering instellingen weergeven of wijzigen

1. Voer in het zoekvak boven aan de portal *virtuele netwerken* in het zoekvak. Wanneer **virtuele netwerken** wordt weergegeven in de zoekresultaten, selecteer deze. Selecteer niet **virtuele netwerken (klassiek)** als deze wordt weergegeven in de lijst als u een peering van een virtueel netwerk te implementeren via het klassieke implementatiemodel niet maken.
2. Selecteer het virtuele netwerk in de lijst die u wilt wijzigen van de peering-instellingen voor.
3. Selecteer in de lijst met virtuele netwerken, het virtuele netwerk dat u wilt wijzigen van de peering-instellingen voor.
4. Onder **instellingen**, selecteer **Peerings**.
5. Klik op de peering die u wilt weergeven of wijzigen van instellingen voor.
6. De juiste instelling wijzigen. Meer informatie over de opties voor elke instelling in [stap 6](#add-peering) van een peering maken. 

    >[!NOTE]
    >Voordat u maakt een peering, zorg ervoor dat u hebt uw familiarized de [vereisten en beperkingen](#requirements-and-constraints) en [vereist machtigingen](#permissions).
    >

7. Klik op **Opslaan**.

**Opdrachten**

Azure CLI: [az vnet peering lijst met netwerken](/cli/azure/network/vnet/peering#az_network_vnet_peering_list) naar lijst peerings voor een virtueel netwerk [az network vnet-peering weergeven](/cli/azure/network/vnet/peering#az_network_vnet_peering_show) om weer te geven van instellingen voor een specifieke peering en [az network vnet-peering bijwerken ](/cli/azure/network/vnet/peering#az_network_vnet_peering_update) peering instellingen te wijzigen. |
- PowerShell: [Get-AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/get-azurermvirtualnetworkpeering) peering weergave-instellingen op te halen en [Set AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/set-azurermvirtualnetworkpeering) om instellingen te wijzigen.

## <a name="delete-a-peering"></a>Een peering verwijderen

Wanneer een peering wordt verwijderd, loopt de peered virtueel netwerk niet meer verkeer van een virtueel netwerk. Wanneer u virtuele netwerken die zijn geïmplementeerd via Resource Manager brengen, wordt in elk virtueel netwerk heeft een peering aan het virtuele netwerk. Hoewel het verwijderen van de peering van een virtueel netwerk, schakelt de communicatie tussen de virtuele netwerken, worden niet verwijderd de peering van het virtuele netwerk. De status peering in het virtuele netwerk bestaat voor de peering **verbroken**. U kan niet opnieuw maken de peering totdat u opnieuw de peering in het eerste virtuele netwerk en de status van de peering beide wijzigingen van virtuele netwerken maken *verbonden*. 

Als u wilt dat virtuele netwerken om te communiceren soms, maar niet altijd, in plaats van het verwijderen van een peering, kunt u instellen de **toestaan van toegang tot het virtuele netwerk** instelt op **uitgeschakelde** in plaats daarvan. Voor meer informatie over hoe, lees stap 6 van de [maken van een peering](#create-peering) sectie van dit artikel. Wellicht eenvoudiger dan verwijderd en opnieuw gemaakt peerings netwerktoegang en uitschakelen.

1. Voer in het zoekvak boven aan de portal *virtuele netwerken* in het zoekvak. Wanneer **virtuele netwerken** wordt weergegeven in de zoekresultaten, selecteer deze. Selecteer niet **virtuele netwerken (klassiek)** als deze wordt weergegeven in de lijst als u een peering van een virtueel netwerk te implementeren via het klassieke implementatiemodel niet maken.
2. Selecteer het virtuele netwerk in de lijst die u verwijderen van een peering wilt voor.
3. Selecteer het virtuele netwerk dat u een peering wilt voor verwijderen uit de lijst van virtuele netwerken.
4. Onder **instellingen**, selecteer **Peerings**.
5. Aan de rechterkant van de peering die u wilt verwijderen, selecteert u **...** , selecteer **verwijderen**, selecteer daarna **Ja** peering van het eerste virtuele netwerk verwijderen.
6. De vorige stappen voor het verwijderen van de peering van het virtuele netwerk in de peering te voltooien.

**Opdrachten**

- Azure CLI: [az network vnet peering verwijderen](/cli/azure/network/vnet/peering#az_network_vnet_peering_delete)
- PowerShell: [Remove-AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/remove-azurermvirtualnetworkpeering)

## <a name="requirements-and-constraints"></a>Vereisten en beperkingen 

- De virtuele netwerken die u peer moeten niet-overlappende IP-adresruimtes hebben.
- U kan niet toevoegen-adresbereiken aan of te verwijderen-adresbereiken in de adresruimte van een virtueel netwerk van zodra een virtueel netwerk is gekoppeld aan een ander virtueel netwerk. Als u wilt toevoegen of verwijderen-adresbereiken, verwijderen van de peering, toevoegen of verwijderen van de adresbereiken, maakt u opnieuw de peering. Als u wilt toevoegen-adresbereiken aan of verwijderen van adresbereiken van virtuele netwerken, Zie [virtuele netwerken beheren](virtual-network-manage-network.md).
- U kunt twee virtuele netwerken te implementeren via Resource Manager of een virtueel netwerk is geïmplementeerd via Resource Manager met een virtueel netwerk te implementeren via het klassieke implementatiemodel peer. U kunt geen peer twee virtuele netwerken die zijn gemaakt met behulp van het klassieke implementatiemodel. Als u niet bekend met Azure-implementatiemodellen bent, leest u de [begrijpen Azure-implementatiemodellen](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artikel. U kunt [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) gebruiken om twee virtuele netwerken te koppelen die zijn gemaakt via het klassieke implementatiemodel.
- Wanneer u twee virtuele netwerken koppelt die zijn gemaakt via Resource Manager, moet voor elk virtueel netwerk een peering worden geconfigureerd. 
    - *Gestarte:* bij het maken van de peering naar het tweede virtuele netwerk van het eerste virtuele netwerk, de status van de peering is *gestarte*. 
    - *Verbonden:* bij het maken van de peering van het tweede virtuele netwerk naar het eerste virtuele netwerk, de status van de peering is *verbonden*. Als u de status van de peering voor het eerste virtuele netwerk bekijkt, ziet u de status ervan is gewijzigd van *gestarte* naar *verbonden*. De peering is niet tot stand gebracht totdat de status van de peering voor beide virtuele netwerk peerings *verbonden*.
- Wanneer een virtueel netwerk via Resource Manager gemaakt met een virtueel netwerk gemaakt met behulp van het klassieke implementatiemodel peering, configureert u alleen een peering voor het virtuele netwerk dat is geïmplementeerd via Resource Manager. U kunt voor een virtueel netwerk (klassiek) of tussen twee virtuele netwerken die zijn geïmplementeerd via het klassieke implementatiemodel peering niet configureren. Bij het maken van de peering van het virtuele netwerk (Resource Manager) aan het virtuele netwerk (klassiek), de status van de peering is *Updating*, wordt binnenkort worden gewijzigd in *verbonden*.
- Een peering tot stand is gebracht tussen twee virtuele netwerken. Peerings zijn niet transitief. Als u peerings tussen maakt:
    - VirtualNetwork1 & VirtualNetwork2
    - VirtualNetwork2 & VirtualNetwork3

  Er is geen peering tussen VirtualNetwork1 en VirtualNetwork3 via VirtualNetwork2. Als u maken van een virtueel netwerk peering tussen VirtualNetwork1 en VirtualNetwork3 wilt, hebt u een peering tussen VirtualNetwork1 en VirtualNetwork3 maken.
- Namen in virtuele netwerken peer is ingesteld met standaard Azure-naamomzetting kan niet worden omgezet. Voor het omzetten van namen in andere virtuele netwerken, moet u een aangepaste DNS-server. Lees voor meer informatie over het instellen van uw eigen DNS-server, de [naamomzetting met uw eigen DNS-server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) artikel.
- Bronnen in beide virtuele netwerken in de peering kunnen met elkaar communiceren met de bandbreedte en de latentie alsof ze zich in hetzelfde virtuele netwerk. De grootte van elke virtuele machine heeft echter een eigen maximale netwerkbandbreedte. Lees de artikelen over de grootte van virtuele machines voor [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) of [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) voor meer informatie over de maximale netwerkbandbreedte voor verschillende groottes van virtuele machines.
- U kunt virtuele netwerken via Resource Manager geïmplementeerd die zich in de dezelfde of verschillende abonnementen op hetzelfde niveau.
- U kunt virtuele netwerken die zijn geïmplementeerd via verschillende implementatiemodellen die zich in dezelfde of verschillende abonnementen op hetzelfde niveau. 
- De abonnementen die beide virtuele netwerken in moeten zijn gekoppeld aan dezelfde Azure Active Directory-tenant. Als u nog een AD-tenant hebt, kunt u snel [maken van een](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch). U kunt een [VPN-Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) twee virtuele netwerken die bestaan uit verschillende abonnementen die zijn gekoppeld aan verschillende Active Directory-tenants verbinding maken.
- Een virtueel netwerk kan worden ingesteld als peer met een ander virtueel netwerk en ook worden verbonden met een ander virtueel netwerk met een virtueel netwerk van Azure-gateway. Wanneer u virtuele netwerken zijn verbonden via peering en een gateway, wordt verkeer tussen virtuele netwerken loopt via de peeringconfiguratie in plaats van de gateway.
- Er wordt een nominaal bedrag in rekening gebracht voor inkomend en uitgaand verkeer dat gebruikmaakt van een virtueel netwerk-peering. Zie de pagina [prijzen](https://azure.microsoft.com/pricing/details/virtual-network) voor meer informatie.

## <a name="permissions"></a>Machtigingen

De accounts die u gebruikt voor het maken van een virtueel netwerk peering moeten de benodigde rol of machtiging hebben. Bijvoorbeeld, als u twee virtuele netwerken met de naam myVnetA en myVnetB zijn peering, uw account moet worden toegewezen aan de volgende minimale rol of machtiging voor elke virtuele netwerk:
    
|Virtueel netwerk|Implementatiemodel|Rol|Machtigingen|
|---|---|---|---|
|myVnetA|Resource Manager|[Inzender voor netwerken](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
| |Klassiek|[Inzender voor klassieke netwerken](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|N/A|
|myVnetB|Resource Manager|[Inzender voor netwerken](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|
||Klassiek|[Inzender voor klassieke netwerken](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Microsoft.ClassicNetwork/virtualNetworks/peer|

Meer informatie over [ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) en het toewijzen van specifieke machtigingen voor [aangepaste rollen](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (alleen voor Resource Manager).

## <a name="next-steps"></a>Volgende stappen

Meer informatie over het maken van een [hub-en-spoke-netwerktopologie](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering)
