---
title: "Linux-installatiekopieën toevoegen aan Azure-Stack"
description: "Meer informatie over hoe Linux installatiekopieën toevoegen aan Azure-Stack."
services: azure-stack
documentationcenter: 
author: brenduns
manager: femila
editor: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2018
ms.author: brenduns
ms.reviewer: jeffgo
ms.openlocfilehash: 6e6f9ca3b314ee2f58d8007e7ddc93ddd213e361
ms.sourcegitcommit: fbba5027fa76674b64294f47baef85b669de04b7
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 02/24/2018
---
# <a name="add-linux-images-to-azure-stack"></a>Linux-installatiekopieën toevoegen aan Azure-Stack

*Van toepassing op: Azure Stack geïntegreerde systemen en Azure Stack Development Kit*

U kunt virtuele Linux-machines (VM's) op de Stack Azure implementeren door een Linux-installatiekopie toe te voegen in de Stack Azure Marketplace. De eenvoudigste manier om een Linux-installatiekopie toevoegen aan Azure-Stack is via Marketplace-beheer. Deze installatiekopieën zijn voorbereid en getest op compatibiliteit met de Azure-Stack.

## <a name="marketplace-management"></a>Marketplace-Management

Linux-installatiekopieën downloaden vanuit Azure Marketplace, gebruik de procedures in het volgende artikel. Selecteer de Linux-installatiekopieën die u wilt bieden gebruikers op uw Azure-Stack.

[Downloaden van de marketplace-items van Azure naar Azure Stack](azure-stack-download-azure-marketplace-item.md).

## <a name="prepare-your-own-image"></a>Uw eigen installatiekopie voorbereiden

U kunt uw eigen Linux-installatiekopie met behulp van een van de volgende instructies voorbereiden:

   * [Op basis van centOS distributies](../virtual-machines/linux/create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [Debian Linux](../virtual-machines/linux/debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [SLES & openSUSE](../virtual-machines/linux/suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [Ubuntu](../virtual-machines/linux/create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

1. Download en installeer de [Azure Linux Agent](https://github.com/Azure/WALinuxAgent/).

    Azure Linux Agent versie 2.2.2 of hoger is vereist voor het inrichten van uw Linux VM op Azure-Stack en sommige versies werkt niet (2.2.12 en 2.2.13 voor voorbeelden). Veel van de vermelde distributies eerder al bevatten een versie van de agent (doorgaans aangeroepen `WALinuxAgent` of `walinuxagent`). Als u een aangepaste installatiekopie maakt, moet u de agent handmatig installeren. De geïnstalleerde versie kan worden bepaald uit naam van het pakket of door te voeren `/usr/sbin/waagent -version` op de virtuele machine.

    Volg de onderstaande instructies voor het installeren van de Azure Linux-agent handmatig:

   a. Eerst, downloaden de nieuwste Azure Linux agent uit [GitHub](https://github.com/Azure/WALinuxAgent/releases), bijvoorbeeld:

            # wget https://github.com/Azure/WALinuxAgent/archive/v2.2.21.tar.gz
   b. Uitpakken van de Azure-agent:

            # tar -vzxf v2.2.21.tar.gz
   c. Python-setuptools installeren

        **Debian / Ubuntu**

            # sudo apt-get update
            # sudo apt-get install python-setuptools

        **Ubuntu 16.04+**

            # sudo apt-get install python3-setuptools

        **RHEL / CentOS / Oracle Linux**

            # sudo yum install python-setuptools
   d. De Azure-agent installeren:

            # cd WALinuxAgent-2.2.21
            # sudo python3 setup.py install --register-service

     Systemen met behulp van Python 2.x en Python 3.x geïnstalleerd side-by-side moet mogelijk de volgende opdracht uitvoeren:

         sudo python3 setup.py install --register-service
     Zie voor meer informatie, de Azure Linux Agent [Leesmij](https://github.com/Azure/WALinuxAgent/blob/master/README.md).
2. [De installatiekopie toevoegen aan de Marketplace](azure-stack-add-vm-image.md). Zorg ervoor dat de `OSType` parameter is ingesteld op `Linux`.
3. Nadat u de installatiekopie aan de Marketplace hebt toegevoegd, een Marketplace-item is gemaakt en gebruikers een virtuele Linux-machine kunnen implementeren.

## <a name="next-steps"></a>Volgende stappen
[Overzicht van services in Azure-Stack van aanbieding](azure-stack-offer-services-overview.md)
