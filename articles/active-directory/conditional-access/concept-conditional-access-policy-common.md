---
title: Allgemeine Richtlinien für bedingten Zugriff – Azure Active Directory
description: Häufig verwendete Richtlinien für bedingten Zugriff für Unternehmen
services: active-directory
ms.service: active-directory
ms.subservice: conditional-access
ms.topic: conceptual
ms.date: 03/25/2020
ms.author: joflore
author: MicrosoftGuyJFlo
manager: daveba
ms.reviewer: calebb, rogoya
ms.collection: M365-identity-device-management
ms.openlocfilehash: 20b699f0672b49dd2f947e0cf00d0ffcef7961e6
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2020
ms.locfileid: "80295306"
---
# <a name="common-conditional-access-policies"></a>Allgemeine Richtlinien für bedingten Zugriff

[Sicherheitsstandards](../fundamentals/concept-fundamentals-security-defaults.md) erfüllen die verschiedensten Zwecke, aber viele Organisationen benötigen mehr Flexibilität, als sie bieten. Viele Organisationen benötigen z. B. die Möglichkeit, bestimmte Konten wie ihr Notfallzugriffskonto von den Richtlinien für bedingten Zugriff auszuschließen, die eine mehrstufige Authentifizierung erfordern. Für diese Unternehmen können die in diesem Artikel genannten allgemeinen Richtlinien hilfreich sein.

![Richtlinien für bedingten Zugriff im Azure-Portal](./media/concept-conditional-access-policy-common/conditional-access-policies-azure-ad-listing.png)

## <a name="emergency-access-accounts"></a>Konten für den Notfallzugriff

Weitere Informationen zu Notfallzugriffskonten und warum sie wichtig sind, finden Sie in den folgenden Artikeln: 

* [Verwalten von Konten für den Notfallzugriff in Azure AD](../users-groups-roles/directory-emergency-access.md)
* [Erstellen einer robusten Verwaltungsstrategie für die Zugriffssteuerung in Azure Active Directory](../authentication/concept-resilient-controls.md)

## <a name="typical-policies-deployed-by-organizations"></a>Typische Richtlinien, die von Unternehmen bereitgestellt werden

* [Blockieren älterer Authentifizierungsmethoden](howto-conditional-access-policy-block-legacy.md)\*
* [Vorschreiben der MFA für Administratoren](howto-conditional-access-policy-admin-mfa.md)\*
* [Vorschreiben der MFA für die Azure-Verwaltung](howto-conditional-access-policy-azure-management.md)\*
* [Erzwingen der MFA für alle Benutzer](howto-conditional-access-policy-all-users-mfa.md)\*

\* Bei gemeinsamer Konfiguration imitieren diese vier Richtlinien die Funktionalität, die durch [Sicherheitsstandards](../fundamentals/concept-fundamentals-security-defaults.md) aktiviert wird.

## <a name="additional-policies"></a>Weitere Richtlinien

* [Risikobasierter bedingter Zugriff (erfordert Azure AD Premium P2)](howto-conditional-access-policy-risk.md)
* [Vorschreiben eines vertrauenswürdigen Standorts für die MFA-Registrierung](howto-conditional-access-policy-registration.md)
* [Blockieren des Zugriffs nach Standort](howto-conditional-access-policy-location.md)
* [Erzwingen eines kompatiblen Geräts](howto-conditional-access-policy-compliant-device.md)
* [Blockieren des Zugriffs mit Ausnahme bestimmter Apps](howto-conditional-access-policy-block-access.md)

## <a name="next-steps"></a>Nächste Schritte

- [Simulieren des Anmeldeverhaltens mit dem What If-Tool für bedingten Zugriff](troubleshoot-conditional-access-what-if.md)

- [Verwenden des Modus „Nur Bericht“ für bedingten Zugriff zum Ermitteln der Auswirkungen neuer Richtlinienentscheidungen](concept-conditional-access-report-only.md)
