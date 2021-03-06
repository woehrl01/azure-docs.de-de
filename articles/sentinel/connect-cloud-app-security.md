---
title: Verknüpfen von Cloud App Security-Daten mit Azure Sentinel | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie Cloud App Security-Daten mit Azure Sentinel verknüpfen.
services: sentinel
documentationcenter: na
author: yelevin
manager: rkarlin
editor: ''
ms.service: azure-sentinel
ms.subservice: azure-sentinel
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2020
ms.author: yelevin
ms.openlocfilehash: 266d97e834247088d40837cbec1436e00d0f4be2
ms.sourcegitcommit: 7581df526837b1484de136cf6ae1560c21bf7e73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80422140"
---
# <a name="connect-data-from-microsoft-cloud-app-security"></a>Verknüpfen von Microsoft Cloud App Security-Daten 



Mit dem [Microsoft Cloud App Security](https://docs.microsoft.com/cloud-app-security/what-is-cloud-app-security) (MCAS)-Connector können Sie Warnungen und [Cloud Discovery-Protokolle](https://docs.microsoft.com/cloud-app-security/tutorial-shadow-it) von MCAS in Azure Sentinel streamen. So erhalten Sie Einblicke in Ihre Cloud-Apps, erweiterte Analysen zur Erkennung und Abwehr von Cyberbedrohungen und Kontrolle darüber, wie Ihre Daten übertragen werden.

## <a name="prerequisites"></a>Voraussetzungen

- Ihr Benutzer muss über Lese- und Schreibberechtigungen für den Arbeitsbereich verfügen.
- Der Benutzer muss für den Mandanten des Arbeitsbereichs über Berechtigungen für globale Administratoren oder Sicherheitsadministratoren verfügen.
- Um Cloud Discovery-Protokolle in Azure Sentinel zu streamen, [aktivieren Sie Azure Sentinel als SIEM in Microsoft Cloud App Security](https://aka.ms/AzureSentinelMCAS).

> [!IMPORTANT]
> Die Erfassung von Cloud Discovery-Protokollen befindet sich derzeit in der öffentlichen Vorschauversion.
> Dieses Feature wird ohne Vereinbarung zum Servicelevel bereitgestellt und ist nicht für Produktionsworkloads vorgesehen.
> Weitere Informationen finden Sie unter [Zusätzliche Nutzungsbestimmungen für Microsoft Azure-Vorschauen](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).
 
## <a name="connect-to-cloud-app-security"></a>Herstellen einer Verbindung mit Cloud App Security

Wenn Sie Cloud App Security bereits haben, vergewissern Sie sich, dass es [in Ihrem Netzwerk aktiviert ist](https://docs.microsoft.com/cloud-app-security/getting-started-with-cloud-app-security).
Wenn Cloud App Security bereitgestellt ist und Daten erhält, können die Warnungsdaten problemlos an Azure Sentinel gestreamt werden.


1. Klicken Sie im Azure Sentinel-Navigationsmenü auf **Datenconnectors**. Klicken Sie in der Liste der Connectors auf die Kachel **Microsoft Cloud App Security** und dann unten rechts auf die Schaltfläche **Connectorseite öffnen**.

1. Wählen Sie aus, welche Protokolle in Azure Sentinel gestreamt werden sollen. Sie können **Warnungen** und **Cloud Discovery-Protokolle** (Vorschau) auswählen. 

1. Klicken Sie auf **Apply Changes**.

1. Geben Sie im Abfragefenster `SecurityAlert` ein, um das entsprechende Schema in Log Analytics für Cloud App Security-Warnungen zu verwenden. Geben Sie für das Cloud Discovery-Protokollschema `McasShadowItReporting` ein.

> [!NOTE]
> Die Cloud Discovery hilft, Trends zu erkennen, indem die Daten aggregiert werden, die den Verbindungen der Benutzer mit Cloud-Apps zugrunde liegen.
>
> Da Cloud Discovery-Daten täglich aggregiert werden, sollten Sie beachten, dass die neuesten Daten der letzten 24 Stunden (maximal) nicht in Azure Sentinel berücksichtigt werden. Falls eine eingehendere Untersuchung aktuellere Daten erfordert, sollte sie direkt in der Quellappliance oder dem Quelldienst durchgeführt werden, wo sich die Rohdaten befinden.

## <a name="next-steps"></a>Nächste Schritte
In diesem Dokument wurde erläutert, wie Sie Microsoft Cloud App Security mit Azure Sentinel verbinden. Weitere Informationen zu Azure Sentinel finden Sie in den folgenden Artikeln:
- Erfahren Sie, wie Sie [Einblick in Ihre Daten und potenzielle Bedrohungen erhalten](quickstart-get-visibility.md).
- Beginnen Sie mit dem Erkennen von Bedrohungen mit Azure Sentinel mithilfe von [integrierten](tutorial-detect-threats.md) oder [benutzerdefinierten](tutorial-detect-threats-custom.md) Regeln.
