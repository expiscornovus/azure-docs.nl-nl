## <a name="deployment-considerations"></a>Overwegingen bij de implementatie

* Zie voor de beschikbaarheid van virtuele machines N-serie, [producten die beschikbaar zijn in elke regio](https://azure.microsoft.com/en-us/regions/services/).

* N-serie VM's kunnen alleen worden geïmplementeerd in het Resource Manager-implementatiemodel.

* N-serie VMs verschillen in het type van Azure Storage ze voor hun schijven ondersteunen. NC en NV virtuele machines alleen ondersteuning voor VM-schijven die worden ondersteund door standaard schijf opslag (HDD). NCv2 ND en NCv3 preview () virtuele machines alleen ondersteuning voor VM schijven die worden ondersteund door Premium schijf opslag (SSD).

* Als u wilt meer dan een paar N-reeks virtuele machines te implementeren, kunt u een abonnement op gebruiksbasis of andere Aankoopopties. Als u een [gratis account van Azure](https://azure.microsoft.com/free/) gebruikt, kunt u slechts een paar Azure Compute-resources van Azure gebruiken.

* Mogelijk moet u het quotum voor kernen (per regio) in uw Azure-abonnement te verhogen en het verhogen van de afzonderlijke quotum voor kernen NC, NCv2, ND of NV. Om aan te vragen een verhoging van het quotum [opent u een ondersteuningsaanvraag online klant](../articles/azure-supportability/how-to-create-azure-support-request.md) zonder kosten. Standaardlimiet kunnen variëren, afhankelijk van de abonnementscategorie van uw.

* Een VM-installatiekopie die u op virtuele machines N-reeks implementeren kunt is de [virtuele Machine van Azure Data wetenschappelijke](../articles/machine-learning/data-science-virtual-machine/overview.md). De virtuele Machine van de gegevens wetenschappelijke vooraf installeert en configureert veel populaire gegevenswetenschap en diepe leren werken met hulpprogramma's. Deze ook vooraf NVIDIA Tesla GPU-stuurprogramma's installeert.





