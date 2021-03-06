---
title: Application Insights-Abhängigkeitsdatenmodell von Azure Monitor
description: Application Insights-Datenmodell für Abhängigkeitstelemetrie
ms.topic: conceptual
ms.date: 04/17/2017
ms.reviewer: sergkanz
ms.openlocfilehash: ba0d848904d1ba885dc53e2941953d8dfb4864cf
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2020
ms.locfileid: "77671918"
---
# <a name="dependency-telemetry-application-insights-data-model"></a>Abhängigkeitstelemetrie: Application Insights-Datenmodell

Abhängigkeitstelemetrie (in [Application Insights](../../azure-monitor/app/app-insights-overview.md)) stellt eine Interaktion der überwachten Komponente mit einer Remotekomponente wie SQL oder einem HTTP-Endpunkt dar.

## <a name="name"></a>Name

Name des Befehls, der mit diesem Abhängigkeitsaufruf ausgelöst wird. Niedriger Kardinalitätswert. Beispiele sind der Name einer gespeicherten Prozedur und eine URL-Pfadvorlage.

## <a name="id"></a>id

Bezeichner einer Instanz eines Aufrufs einer Abhängigkeit. Dient zur Korrelation mit dem Anforderungstelemetrieelement, das diesem Aufruf einer Abhängigkeit entspricht. Weitere Informationen hierzu finden Sie auf der Seite [Korrelation](../../azure-monitor/app/correlation.md).

## <a name="data"></a>Data

Der durch diesen Aufruf einer Abhängigkeit ausgelöste Befehl. Beispiele sind eine SQL-Anweisung und HTTP-URL mit allen Abfrageparametern.

## <a name="type"></a>type

Name des Abhängigkeitstyps. Niedriger Kardinalitätswert für die logische Gruppierung von Abhängigkeiten und Interpretation der anderen Felder wie „commandName“ und „resultCode“. Beispiele sind die SQL, Azure-Tabelle und HTTP.

## <a name="target"></a>Ziel

Zielstandort eines Aufrufs einer Abhängigkeit. Beispiele sind Servername und Hostadresse. Weitere Informationen hierzu finden Sie auf der Seite [Korrelation](../../azure-monitor/app/correlation.md).

## <a name="duration"></a>Duration

Dauer der Anforderung im Format `DD.HH:MM:SS.MMMMMM`. Muss kleiner als `1000` Tage sein.

## <a name="result-code"></a>Ergebniscode

Ergebniscode eines Aufrufs einer Abhängigkeit. Beispiele sind SQL-Fehlercode und HTTP-Statuscode.

## <a name="success"></a>Erfolg

Angabe eines erfolgreichen oder fehlgeschlagenen Aufrufs.

## <a name="custom-properties"></a>Benutzerdefinierte Eigenschaften

[!INCLUDE [application-insights-data-model-properties](../../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>Benutzerdefinierte Messungen

[!INCLUDE [application-insights-data-model-measurements](../../../includes/application-insights-data-model-measurements.md)]


## <a name="next-steps"></a>Nächste Schritte

- Einrichten der Abhängigkeitsnachverfolgung für [.NET](../../azure-monitor/app/asp-net-dependencies.md).
- Einrichten der Abhängigkeitsnachverfolgung für [Java](../../azure-monitor/app/java-agent.md).
- [Schreiben benutzerdefinierter Telemetriedaten zu Abhängigkeiten](../../azure-monitor/app/api-custom-events-metrics.md#trackdependency)
- Lesen Sie die Informationen zu den Application Insights-Typen und zum Datenmodell unter [Datenmodell](data-model.md).
- Lesen Sie die Informationen zu den von Application Insights unterstützten [Plattformen](../../azure-monitor/app/platforms.md).
