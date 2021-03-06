---
title: Untersuchen von Risiken – Azure Active Directory Identity Protection
description: Erfahren Sie, wie Sie riskante Benutzer, Erkennungen und Anmeldungen in Azure Active Directory Identity Protection untersuchen.
services: active-directory
ms.service: active-directory
ms.subservice: identity-protection
ms.topic: conceptual
ms.date: 12/13/2019
ms.author: joflore
author: MicrosoftGuyJFlo
manager: daveba
ms.reviewer: sahandle
ms.collection: M365-identity-device-management
ms.openlocfilehash: c5191f05752c177aa29d121abe9d1aa29fde265a
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2020
ms.locfileid: "79227778"
---
# <a name="how-to-investigate-risk"></a>Anleitung: Untersuchen eines Risikos

Identity Protection stellt Organisationen drei Berichte zur Verfügung, mit denen sie Identitätsrisiken in Ihrer Umgebung untersuchen können. Diese Berichte sind **Riskante Benutzer**, **Riskante Anmeldungen** und **Risikoerkennungen**. Die Untersuchung von Ereignissen ist entscheidend, um alle Schwachpunkte in Ihrer Sicherheitsstrategie besser zu verstehen und zu identifizieren.

Alle drei Berichte ermöglichen das Herunterladen von Ereignissen im CSV-Format für die weitere Analyse außerhalb des Azure-Portals. Die Berichte zu riskanten Benutzern und riskanten Anmeldungen ermöglichen das Herunterladen der letzten 2500 Einträge, während der Bericht „Risikoerkennungen“ das Herunterladen der neuesten 5000-Einträge ermöglicht.

Organisationen können die Microsoft Graph-API-Integrationen nutzen, um Daten mit anderen Quellen zu aggregieren, auf die sie möglicherweise als Organisation zugreifen können.

Die drei Berichte finden Sie unter **Azure-Portal** > **Azure Active Directory** > **Sicherheit**.

## <a name="navigating-the-reports"></a>Navigieren in den Berichten

Jeder Bericht wird mit einer Liste aller Erkennungen für den Zeitraum gestartet, der oben im Bericht angezeigt wird. Jeder Bericht ermöglicht das Hinzufügen oder Entfernen von Spalten auf der Grundlage von Administratoreinstellungen. Administratoren können die Daten im CSV- oder JSON-Format herunterladen. Berichte können über die Filter am oberen Rand des Berichts gefiltert werden.

Durch Auswählen einzelner Einträge können am Anfang des Berichts zusätzliche Einträge aktiviert werden, z.B. die Möglichkeit, eine Anmeldung als gefährdet oder sicher zu bestätigen, einen Benutzer als kompromittiert zu bestätigen oder das Benutzerrisiko zu verwerfen.

Werden einzelne Einträge ausgewählt, wird das Fenster „Details“ unterhalb der Erkennungen erweitert. In der Detailansicht können Administratoren die Erkennungen untersuchen und für jede Erkennung Aktionen ausführen. 

![Beispiel für einen Identity Protection-Bericht mit riskanten Anmeldungen und Details](./media/howto-identity-protection-investigate-risk/identity-protection-risky-sign-ins-report.png)

## <a name="risky-users"></a>Riskante Benutzer

Mit den Informationen im Bericht „Riskante Benutzer“ können Administratoren folgendes ermitteln:

- Welche Benutzer sind gefährdet und für welche Benutzer wurden Risiken behoben oder verworfen?
- Details zu Erkennungen
- Verlauf aller riskanten Anmeldungen
- Risikoverlauf
 
Administratoren können dann Aktionen für diese Ereignisse ausführen. Administratoren haben folgende Möglichkeiten:

- Benutzerkennwort festlegen
- Benutzergefährdung bestätigen
- Benutzerrisiko verwerfen
- Anmeldung eines Benutzers blockieren
- Mit Azure ATP weitere Untersuchungen ausführen

## <a name="risky-sign-ins"></a>Riskante Anmeldungen

Der Bericht „Riskante Anmeldungen“ enthält filterbare Daten der letzten 30 Tage (1 Monat).

Mit den Informationen im Bericht „Riskante Anmeldungen“ können Administratoren Folgendes ermitteln:

- Als Risiko klassifizierte, als gefährdet bzw. sicher bestätigte, verworfene oder behandelte Anmeldungen.
- Echtzeit- und Aggregatrisikostufen in Verbindung mit Anmeldeversuchen.
- Ausgelöste Erkennungstypen
- Angewendete Richtlinien für bedingten Zugriff
- MFA-Details
- Geräteinformationen
- Anwendungsinformationen
- Standortinformationen

Administratoren können dann Aktionen für diese Ereignisse ausführen. Administratoren haben folgende Möglichkeiten:

- Anmeldung als gefährdet bestätigen
- Anmeldung als sicher bestätigen

## <a name="risk-detections"></a>Risikoerkennungen

Der Bericht „Risikoerkennungen“ enthält filterbare Daten der letzten 90 Tage (3 Monate).

Mit den Informationen im Bericht „Risikoerkennungen“ können Administratoren folgendes ermitteln:

- Informationen zu den einzelnen Risikoerkennungen, einschließlich des Typs.
- Andere, gleichzeitig ausgelöste Risiken
- Ort des Anmeldeversuchs
- Links zu weiteren Details von Microsoft Cloud App Security (MCAS).

Administratoren können dann zum Risiko- oder Anmeldebericht des Benutzers zurückkehren, um basierend auf gesammelten Informationen Aktionen auszuführen.

## <a name="next-steps"></a>Nächste Schritte

- [Verfügbare Richtlinien zum Mindern von Risiken](concept-identity-protection-policies.md)

- [Aktivieren von Anmelde- und Benutzerrisikorichtlinien](howto-identity-protection-configure-risk-policies.md)
