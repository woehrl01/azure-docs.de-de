---
title: include file
description: include file
services: storage
author: tamram
ms.service: storage
ms.topic: include
ms.date: 07/30/2019
ms.author: tamram
ms.custom: include file
ms.openlocfilehash: 167d50e5c7f3049f46fd8540630e47044240809f
ms.sourcegitcommit: 31ef5e4d21aa889756fa72b857ca173db727f2c3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2020
ms.locfileid: "81536579"
---
[Azure Files](../articles/storage/files/storage-files-introduction.md) unterstützt die identitätsbasierte Authentifizierung per SMB (Server Message Block) über [lokales Active Directory Domain Services (AD DS)](https://docs.microsoft.com/windows-server/identity/ad-ds/get-started/virtual-dc/active-directory-domain-services-overview) (Vorschauversion) und [Azure Active Directory Domain Services (Azure AD DS)](../articles/active-directory-domain-services/overview.md). In diesem Artikel erfahren Sie, wie Azure-Dateifreigaben Domänendienste lokal oder in Azure nutzen können, um den identitätsbasierten Zugriff auf Azure-Dateifreigaben über SMB zu unterstützen. Durch das Aktivieren des identitätsbasierten Zugriffs für Ihre Azure-Dateifreigaben können Sie vorhandene Dateiserver durch Azure-Dateifreigaben ersetzen, ohne den vorhandenen Verzeichnisdienst zu ersetzen, und so den nahtlosen Benutzerzugriff auf Freigaben aufrechterhalten. 

Azure Files erzwingt die Autorisierung für den Benutzerzugriff sowohl auf Freigabe- als auch auf Verzeichnis-/Dateiebene. Die Berechtigungszuweisung auf Freigabeebene kann für Azure AD-Benutzer (Azure Active Directory) oder -Gruppen erfolgen, die über das Modell der [rollenbasierten Zugriffssteuerung (Role-Based Access Control, RBAC)](../articles/role-based-access-control/overview.md) verwaltet werden. Bei der RBAC müssen die für den Dateizugriff verwendeten Anmeldeinformationen verfügbar sein oder mit Azure AD synchronisiert werden. Sie können Benutzern oder Gruppen in Azure AD integrierte RBAC-Rollen wie „Leser für Speicherdateidaten-SMB-Freigabe“ zuweisen, um Lesezugriff auf eine Azure-Dateifreigabe zu gewähren.

Auf der Verzeichnis-/Dateiebene unterstützt Azure Files die Beibehaltung, Vererbung und Erzwingung von [Windows-DACLs](https://docs.microsoft.com/windows/win32/secauthz/access-control-lists) (genau wie jeder andere Windows-Dateiserver). Sie können Windows-DACLs beim Kopieren von Daten über SMB zwischen Ihrer vorhandenen Dateifreigabe und Ihren Azure-Dateifreigaben beibehalten. Mit Azure-Dateifreigaben können Sie ACLs zusammen mit Ihren Daten sichern, ganz gleich, ob Sie die Autorisierung erzwingen möchten. 
