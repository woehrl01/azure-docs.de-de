---
title: Azure Confidential Computing-Lösungen auf virtuellen Computern
description: Erfahren Sie mehr über Azure Confidential Computing-Lösungen auf virtuellen Computern.
author: JBCook
ms.service: virtual-machines
ms.subservice: workloads
ms.workload: infrastructure
ms.topic: conceptual
ms.date: 04/06/2020
ms.author: JenCook
ms.openlocfilehash: e574ac33e5f7da814c4bd813fc1c083c7cb4c2c9
ms.sourcegitcommit: 849bb1729b89d075eed579aa36395bf4d29f3bd9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/28/2020
ms.locfileid: "82187884"
---
# <a name="solutions-on-azure-virtual-machines"></a>Lösungen auf virtuellen Azure-Computern

In diesem Artikel werden Informationen über die Bereitstellung von Azure Confidential Computing-VMs mit Intel-Prozessoren behandelt, die von [Intel Software Guard Extension](https://software.intel.com/sgx) (Intel SGX) unterstützt werden. 

## <a name="azure-confidential-computing-vm-sizes"></a>VM-Größen für Azure Confidential Computing

Die Azure Confidential Computing-VMs wurden entwickelt, um die Vertraulichkeit und Integrität Ihrer Daten und Ihres Codes zu schützen, während die Verarbeitung in der Cloud erfolgt. 

VMs der [DCsv2-Serie](../virtual-machines/dcv2-series.md) sind die neueste Größenfamilie für Confidential Computing. Diese VMs unterstützen eine größere Palette an Bereitstellungsmöglichkeiten, verfügen über einen doppelt so großen Enclave Page Cache (EPC) und bieten im Vergleich zu unseren VMs der DC-Serie eine umfangreichere Auswahl an Größen. Die VMs der [DC-Serie](../virtual-machines/sizes-previous-gen.md#preview-dc-series) befinden sich derzeit in der Vorschauphase, gelten allerdings als veraltet und gelangen nicht in die Phase der allgemeinen Verfügbarkeit.

Beginnen Sie mit der Bereitstellung einer VM der DCsv2-Serie über den kommerziellen Marketplace von Microsoft, indem Sie dem [Tutorial für den Schnellstart](quick-create-marketplace.md) folgen.

### <a name="current-available-sizes-and-regions"></a>Aktuelle verfügbare Größen und Regionen

Um eine Liste aller allgemein verfügbaren Größen für Confidential Computing-VMs in verfügbaren Regionen und Verfügbarkeitszonen zu erhalten, führen Sie in der [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli-windows?view=azure-cli-latest) den folgenden Befehl aus:

```azurecli-interactive
az vm list-skus 
    --size dc 
    --query "[?family=='standardDCSv2Family'].{name:name,locations:locationInfo[0].location,AZ_a:locationInfo[0].zones[0],AZ_b:locationInfo[0].zones[1],AZ_c:locationInfo[0].zones[2]}" 
    --all 
    --output table
```

Ab April 2020 sind diese SKUs in den folgenden Regionen und Verfügbarkeitszonen verfügbar:

```output
Name              Locations      AZ_a
----------------  -------------  ------
Standard_DC8_v2   eastus         2
Standard_DC1s_v2  eastus         2
Standard_DC2s_v2  eastus         2
Standard_DC4s_v2  eastus         2
Standard_DC8_v2   CanadaCentral
Standard_DC1s_v2  CanadaCentral
Standard_DC2s_v2  CanadaCentral
Standard_DC4s_v2  CanadaCentral
Standard_DC8_v2   uksouth        3
Standard_DC1s_v2  uksouth        3
Standard_DC2s_v2  uksouth        3
Standard_DC4s_v2  uksouth        3
Standard_DC8_v2   CentralUSEUAP
Standard_DC1s_v2  CentralUSEUAP
Standard_DC2s_v2  CentralUSEUAP
Standard_DC4s_v2  CentralUSEUAP
```

Um eine detailliertere Ansicht der oben genannten Größen zu erhalten, führen Sie den folgenden Befehl aus:

```azurecli-interactive
az vm list-skus 
    --size dc 
    --query "[?family=='standardDCSv2Family']"
```

## <a name="deployment-considerations"></a>Überlegungen zur Bereitstellung

Folgen Sie einem Tutorial zum Schnellstart, um eine VM der DCsv2-Serie in weniger als 10 Minuten bereitzustellen. 

- **Azure-Abonnement:** Um eine größere Anzahl von Confidential Computing-VM-Instanzen bereitzustellen, sollten Sie ein Abonnement mit nutzungsbasierter Bezahlung oder eine andere Kaufoption in Erwägung ziehen. Wenn Sie ein [kostenloses Azure-Konto](https://azure.microsoft.com/free/) verwenden, verfügen Sie nicht über ein Kontingent für die entsprechende Menge von Azure-Computekernen.

- **Preise und regionale Verfügbarkeit**: Die Preise für VMs der DCsv2-Serie finden Sie auf der [Seite mit der Preisübersicht für virtuelle Computer](https://azure.microsoft.com/pricing/details/virtual-machines/linux/). Informationen zur Verfügbarkeit in den Azure-Regionen finden Sie unter [Verfügbare Produkte nach Region](https://azure.microsoft.com/global-infrastructure/services/?products=virtual-machines) .


- **Kontingent Speicherkerne:** Es kann sein, dass Sie das Kontingent für die Speicherkerne in Ihrem Azure-Abonnement anpassen müssen, indem Sie den Standardwert erhöhen. Möglicherweise ist bei Ihrem Abonnement auch die Anzahl von Kernen beschränkt, die in bestimmten VM-Größenkategorien, einschließlich der DCsv2-Serie, bereitgestellt werden können. In diesem Fall können Sie kostenlos [eine Anfrage an den Onlinekundensupport richten](https://docs.microsoft.com/azure/azure-portal/supportability/per-vm-quota-requests) und eine Erhöhung des Kontingents anfordern. Beachten Sie, dass Standardgrenzwerte unter Umständen je nach Abonnementkategorie variieren.

  > [!NOTE]
  > Wenn Sie einen umfangreichen Kapazitätsbedarf haben, wenden Sie sich an den Azure-Support. Azure-Kontingente sind Angebotsbeschränkungen, keine Kapazitätsgarantien. Unabhängig von Ihrem Kontingent werden nur die tatsächlich verwendeten Kerne in Rechnung gestellt.
  
- **Größenänderung:** Aufgrund ihrer speziellen Hardware können Sie die Größe von Confidential Computing-Instanzen nur innerhalb der gleichen Größenfamilie anpassen. So können Sie beispielsweise die Größe einer VM der DCsv2-Serie nur in eine andere Größe der DCsv2-Serie ändern. Eine Änderung von einer Nicht-Confidential Computing-Größe in eine Confidential Computing-Größe wird nicht unterstützt.  

- **Image**: Um Unterstützung für Intel Software Guard Extension (Intel SGX) auf Confidential Computing-Instanzen zu bieten, müssen alle Bereitstellungen auf Images der Generation 2 erfolgen. Azure Confidential Computing unterstützt Workloads, die unter Ubuntu 18.04 Gen 2, Ubuntu 16.04 Gen 2 und Windows Server 2016 Gen 2 ausgeführt werden. Weitere Informationen zu unterstützten und nicht unterstützten Szenarien finden Sie unter [Unterstützung für VMs der Generation 2 in Azure](../virtual-machines/linux/generation-2.md). 

- **Speicher**: Datenträger für Azure Confidential Computing-VMs und kurzlebige Betriebssystemdatenträger befinden sich auf NVMe-Datenträgern. Instanzen unterstützen ausschließlich SSD Premium- und SSD Standard- und keine SSD Ultra- oder HDD Standard-Datenträger. Die VM-Größe **DC8_v2** unterstützt nicht Storage Premium. 

- **Datenträgerverschlüsselung**: Confidential Computing-Instanzen unterstützen zurzeit keine Datenträgerverschlüsselung. 

## <a name="high-availability-and-disaster-recovery-considerations"></a>Überlegungen zu Hochverfügbarkeit und Notfallwiederherstellung

Wenn Sie VMs in Azure nutzen, müssen Sie eine Lösung für Hochverfügbarkeit und Notfallwiederherstellung implementieren, um Ausfallzeiten zu vermeiden. 

Azure Confidential Computing unterstützt derzeit keine Zonenredundanz über Verfügbarkeitszonen. Um für Confidential Computing maximale Verfügbarkeit und Redundanz zu erreichen, verwenden Sie [Verfügbarkeitsgruppen](../virtual-machines/windows/manage-availability.md#configure-multiple-virtual-machines-in-an-availability-set-for-redundancy). Aufgrund von Hardwarebeschränkungen können Verfügbarkeitsgruppen für Confidential Computing-Instanzen nur maximal 10 Updatedomänen haben. 

## <a name="deploying-via-an-azure-resource-manager-template"></a>Bereitstellen über eine Azure Resource Manager-Vorlage 

Azure Resource Manager ist der Bereitstellungs- und Verwaltungsdienst für Azure. Er bietet eine Verwaltungsebene, die das Erstellen, Aktualisieren und Löschen von Ressourcen in Ihrem Azure-Abonnement ermöglicht. Mithilfe von Verwaltungsfeatures wie Zugriffssteuerung, Sperren und Tags können Sie Ihre Ressourcen nach der Bereitstellung schützen und organisieren.

Informationen zu Azure Resource Manager-Vorlagen finden Sie in der [Übersicht über die Vorlagenbereitstellung](../azure-resource-manager/templates/overview.md).

Um eine VM der DCsv2-Serie mithilfe einer Resource Manager-Vorlage bereitzustellen, verwenden Sie die Ressource [Virtual Machine](../virtual-machines/windows/template-description.md). Vergewissern Sie sich, dass Sie die richtigen Eigenschaften für **vmSize** und **imageReference** angeben.

### <a name="vm-size"></a>VM-Größe

Geben Sie in der Resource Manager-Vorlage in der Ressource „Virtual Machine“ die folgenden Größen an. Diese Zeichenfolge wird in **properties** als **vmSize** eingegeben.

```json
  [
        "Standard_DC1s_v2",
        "Standard_DC2s_v2",
        "Standard_DC4s_v2",
        "Standard_DC8_v2"
      ],
```

### <a name="gen2-os-image"></a>Gen2-Betriebssystemimage

Unter **properties** müssen Sie zudem unter **storageProfile** auf ein Image verweisen. Verwenden Sie *nur eines* der folgenden Images für **imageReference**.

```json
      "2016-datacenter-gensecond": {
        "offer": "WindowsServer",
        "publisher": "MicrosoftWindowsServer",
        "sku": "2016-datacenter-gensecond",
        "version": "latest"
      },
        "18_04-lts-gen2": {
        "offer": "UbuntuServer",
        "publisher": "Canonical",
        "sku": "18_04-lts-gen2",
        "version": "latest"
      },
      "16_04-lts-gen2": {
        "offer": "UbuntuServer",
        "publisher": "Canonical",
        "sku": "16_04-lts-gen2",
        "version": "latest"
      }
```

## <a name="next-steps"></a>Nächste Schritte 

In diesem Artikel haben Sie sich über die Qualifikationen und Konfigurationen informiert, die zum Erstellen einer Confidential Computing-VM erforderlich sind. Sie können nun zum Azure Marketplace wechseln, um eine VM der DCsv2-Serie bereitzustellen.

> [!div class="nextstepaction"]
> [Bereitstellen einer VM der DCsv2-Serie in Azure Marketplace](quick-create-marketplace.md)