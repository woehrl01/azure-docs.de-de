---
title: Häufig gestellte Fragen zu IoT-Solution Accelerators (Azure) | Microsoft-Dokumentation
description: In diesem Artikel werden die häufig gestellten Fragen zu IoT-Solution Accelerators beantwortet. Er enthält Links zu den GitHub-Repositorys.
author: dominicbetts
manager: timlt
ms.service: iot-accelerators
services: iot-accelerators
ms.topic: conceptual
ms.date: 02/15/2018
ms.author: dobett
ms.openlocfilehash: 7a2b167f90b4ec79f5fa515ded1c676ca7085e72
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/27/2020
ms.locfileid: "75647712"
---
# <a name="frequently-asked-questions-for-iot-solution-accelerators"></a>Häufig gestellte Fragen zu IoT-Solution Accelerators

Sehen Sie sich auch die [häufig gestellten Fragen zu verbundenen Factorys](iot-accelerators-faq-cf.md) und die [häufig gestellten Fragen zur Remoteüberwachung](iot-accelerators-faq-rm-v2.md) an.

### <a name="where-can-i-find-the-source-code-for-the-solution-accelerators"></a>Wo finde ich den Quellcode für die Solution Accelerators?

Der Quellcode wird in den folgenden GitHub-Repositorys gespeichert:

* [Solution Accelerator für die Remoteüberwachung (.NET)](https://github.com/Azure/azure-iot-pcs-remote-monitoring-dotnet)
* [Solution Accelerator für die Remoteüberwachung (Java)](https://github.com/Azure/azure-iot-pcs-remote-monitoring-java)
* [Solution Accelerator für Predictive Maintenance](https://github.com/Azure/azure-iot-predictive-maintenance)
* [Solution Accelerator für verbundene Factorys](https://github.com/Azure/azure-iot-connected-factory)

### <a name="what-sdks-can-i-use-to-develop-device-clients-for-the-solution-accelerators"></a>Welche SDKs kann ich zum Entwickeln von Geräteclients für die Solution Accelerators verwenden?

Links zu den IoT-Geräte-SDKs in verschiedenen Sprachen (C, .NET, Java, Node.js, Python) finden Sie im GitHub-Repository [Microsoft Azure IoT SDKs](https://github.com/Azure/azure-iot-sdks).

Wenn Sie das DevKit-Gerät verwenden, finden Sie Ressourcen und Beispiele im GitHub-Repository [IoT DevKit SDK](https://github.com/Microsoft/devkit-sdk).

### <a name="is-the-new-microservices-architecture-available-for-all-the-three-solution-accelerators"></a>Ist die neue Microservicearchitektur für alle drei Solution Accelerators verfügbar?

Derzeit wird die Microservices-Architektur nur in der Remoteüberwachungslösung verwendet, da sie das umfangreichste Szenario abdeckt.

### <a name="what-advantages-does-the-new-open-sourced-microservices-based-architecture-provide-in-the-new-update"></a>Welche Vorteile bietet die neue auf Microservices basierende Open-Source-Architektur im neuen Update?

In den letzten beiden Jahren hat sich die Cloudarchitektur stark weiterentwickelt. Microservices haben sich als hervorragendes Muster für mehr Skalierbarkeit und Flexibilität ohne Einbußen bei der Entwicklungsgeschwindigkeit erwiesen. Mehrere Microsoft-Dienste nutzen dieses Architekturmuster intern mit hervorragenden Ergebnissen bei Zuverlässigkeit und Skalierbarkeit. Microsoft hat diese Erfahrungen mit dem Solution Accelerator umgesetzt, sodass auch die Kunden von diesen profitieren können.

### <a name="im-a-service-administrator-and-id-like-to-change-the-directory-mapping-between-my-subscription-and-a-specific-azure-ad-tenant-how-do-i-complete-this-task"></a>Ich bin Dienstadministrator und möchte die Verzeichniszuordnung zwischen meinem Abonnement und einen bestimmten Azure AD-Mandanten ändern. Wie führe ich diese Aufgabe aus?

Informationen dazu finden Sie unter [Hinzufügen eines vorhandenen Abonnements zu Ihrem Azure AD-Verzeichnis](../active-directory/fundamentals/active-directory-how-subscriptions-associated-directory.md#to-associate-an-existing-subscription-to-your-azure-ad-directory).

### <a name="i-want-to-change-a-service-administrator-or-co-administrator-when-logged-in-with-an-organizational-account"></a>Ich möchte bei der Anmeldung über ein Organisationskonto einen Dienstadministrator oder Co-Administrator ändern.

Lesen Sie den Supportartikel [Ändern des Dienstadministrators und des Co-Administrators bei Anmeldung über ein Organisationskonto](https://azure.microsoft.com/support/changing-service-admin-and-co-admin).

### <a name="why-am-i-seeing-this-error-your-account-does-not-have-the-proper-permissions-to-create-a-solution-please-check-with-your-account-administrator-or-try-with-a-different-account"></a>Warum wird dieser Fehler angezeigt? „Ihr Konto hat nicht die erforderlichen Berechtigungen zum Erstellen einer Lösung. Wenden Sie sich an den Administrator Ihres Kontos, oder versuchen Sie es mit einem anderen Konto.“

Orientieren Sie sich an folgendem Diagramm:

![Flussdiagramm für Berechtigungen](media/iot-accelerators-faq/flowchart.png)

> [!NOTE]
> Wenn der Fehler auch nach der Überprüfung noch angezeigt wird und Sie globaler Administrator des Azure AD-Mandanten und Co-Administrator des Abonnements sind, können Sie Ihren Kontoadministrator bitten, den Benutzer zu entfernen und die erforderlichen Berechtigungen in dieser Reihenfolge neu zuzuweisen. Fügen Sie zuerst den Benutzer als globalen Administrator hinzu, und fügen Sie den Benutzer dann als Co-Administrator für das Azure-Abonnement hinzu. Falls die Probleme weiterhin bestehen, nutzen Sie die Option [Hilfe und Support](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

### <a name="why-am-i-seeing-this-error-when-i-have-an-azure-subscription-an-azure-subscription-is-required-to-create-pre-configured-solutions-you-can-create-a-free-trial-account-in-just-a-couple-of-minutes"></a>Weshalb wird dieser Fehler angezeigt, wenn ich ein Azure-Abonnement habe? „Zum Erstellen vorkonfigurierter Lösungen ist ein Azure-Abonnement erforderlich. In nur wenigen Minuten können Sie ein kostenloses Testkonto erstellen.“

Wenn Sie sicher sind, dass Sie über ein Azure-Abonnement verfügen, überprüfen Sie die Mandantenzuordnung für Ihr Abonnement, und prüfen Sie, ob der richtige Mandant in der Dropdownliste ausgewählt wurde. Überprüfen Sie anschließend anhand des obigen Diagramms die Zuordnung Ihres Abonnements und dieses Azure AD-Mandanten.

### <a name="where-can-i-find-information-about-the-previous-version-of-the-remote-monitoring-solution"></a>Wo finde ich Informationen über die Vorgängerversion der Remoteüberwachungslösung?

Die Vorversion des Solution Accelerators für die Remoteüberwachung war als vorkonfigurierte IoT Suite-Lösung für die Remoteüberwachung bekannt. Sie finden die archivierte Dokumentation unter [https://docs.microsoft.com/previous-versions/azure/iot-suite/](https://docs.microsoft.com/previous-versions/azure/iot-suite/).

### <a name="is-the-new-solution-accelerator-available-in-the-same-geographic-region-as-the-existing-solution"></a>Ist der neue Solution Accelerator in derselben geografischen Region wie die vorhandene Lösung verfügbar?

Ja, die neue Remoteüberwachung ist in den gleichen geografischen Regionen verfügbar.

### <a name="whats-the-difference-between-deleting-a-resource-group-in-the-azure-portal-and-clicking-delete-on-a-solution-accelerator-in-azureiotsolutionscom"></a>Was ist der Unterschied zwischen dem Löschen einer Ressourcengruppe im Azure-Portal und dem Klicken auf „Löschen“ für einen Solution Accelerator unter azureiotsolutions.com?

* Wenn Sie den Solution Accelerator unter [azureiotsolutions.com](https://www.azureiotsolutions.com/) löschen, werden alle Ressourcen gelöscht, die beim Erstellen des Solution Accelerators bereitgestellt wurden. Wenn Sie dieser Ressourcengruppe weitere Ressourcen hinzugefügt haben, werden diese ebenfalls gelöscht.
* Wenn Sie die Ressourcengruppe im [Azure-Portal](https://portal.azure.com) löschen, werden nur die Ressourcen in dieser Ressourcengruppe gelöscht. Sie müssen auch die Azure Active Directory-Anwendung löschen, die dem Solution Accelerator zugeordnet ist.

### <a name="can-i-continue-to-leverage-my-existing-investments-in-azure-iot-solution-accelerators"></a>Kann ich meine bestehenden Investitionen in Azure IoT-Solution Accelerators weiterhin nutzen?

Ja. Jede aktuell vorhandene Lösung wird in Ihrem Azure-Abonnement weiterhin ausgeführt, und der Quellcode bleibt in GitHub verfügbar.

### <a name="how-many-iot-hub-instances-can-i-provision-in-a-subscription"></a>Wie viele IoT Hub-Instanzen kann ich in einem Abonnement bereitstellen?

Standardmäßig können Sie [10 IoT Hubs pro Abonnement](../azure-resource-manager/management/azure-subscription-service-limits.md#iot-hub-limits) bereitstellen. Sie können ein [Azure-Supportticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade) erstellen, um dieses Limit zu erhöhen. Da jeder Solution Accelerator einen neuen IoT Hub bereitstellt, können Sie somit in einem Abonnement nur bis zu zehn Solution Accelerators bereitstellen.

### <a name="how-many-azure-cosmos-db-instances-can-i-provision-in-a-subscription"></a>Wie viele Instanzen von Cosmos DB kann ich in einem Abonnement bereitstellen?

50. Sie können ein [Azure-Supportticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade) erstellen, um dieses Limit zu erhöhen. Standardmäßig können Sie jedoch nur 50 Cosmos DB-Instanzen pro Abonnement bereitstellen.

### <a name="how-many-free-bing-maps-apis-can-i-provision-in-a-subscription"></a>Wie viele Bing Maps-APIs im Tarif „Free“ kann ich in einem Abonnement bereitstellen?

Zwei. In einem Azure-Abonnement können für Bing Karten für Unternehmen nur zwei Tarife für die erste interne Transaktionsebene erstellt werden. Die Remoteüberwachungslösung wird standardmäßig mit dem Tarif für die erste interne Transaktionsebene bereitgestellt. Daher können Sie in einem Abonnement nur bis zu zwei vorkonfigurierte Remoteüberwachungslösungen ohne Modifikationen bereitstellen.

### <a name="can-i-create-a-solution-accelerator-if-i-have-microsoft-azure-for-dreamspark"></a>Kann ich einen Solution Accelerator erstellen, wenn ich Microsoft Azure für DreamSpark besitze?

> [!NOTE]
> Microsoft Azure für DreamSpark wird jetzt als Microsoft Imagine für Schüler und Studenten bezeichnet.

Derzeit können Sie mit einem Konto für [Microsoft Azure für DreamSpark](https://azure.microsoft.com/pricing/member-offers/imagine/) keinen Solution Accelerator erstellen. Sie können jedoch in wenigen Minuten ein [kostenloses Testkonto für Azure](https://azure.microsoft.com/free/) einrichten, mit dem Sie einen Solution Accelerator erstellen können.

### <a name="how-do-i-delete-an-azure-ad-tenant"></a>Gewusst wie: Löschen eines Azure AD-Mandanten

Informationen hierzu finden Sie im Blogbeitrag von Eric Golpe: [Walkthrough of Deleting an Azure AD Tenant](https://blogs.msdn.com/b/ericgolpe/archive/2015/04/30/walkthrough-of-deleting-an-azure-ad-tenant.aspx) (Exemplarische Vorgehensweise zum Löschen eines Azure AD-Mandanten).

### <a name="next-steps"></a>Nächste Schritte

Sie können auch einige andere Features und Funktionen der IoT-Solution Accelerators ausprobieren:

* [Erkunden der Funktionen des Solution Accelerators für die Remoteüberwachung](quickstart-remote-monitoring-deploy.md)
* [Übersicht über den Solution Accelerator für Predictive Maintenance](iot-accelerators-predictive-overview.md)
* [Bereitstellen des Solution Accelerators für Connected Factory](quickstart-connected-factory-deploy.md)
* [Sicherheit im Internet der Dinge von Anfang an](/azure/iot-fundamentals/iot-security-ground-up)
