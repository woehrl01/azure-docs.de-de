---
title: Zuordnen der Peer-ASN zum Azure-Abonnement mithilfe von PowerShell
titleSuffix: Azure
description: Zuordnen der Peer-ASN zum Azure-Abonnement mithilfe von PowerShell
services: internet-peering
author: prmitiki
ms.service: internet-peering
ms.topic: article
ms.date: 11/27/2019
ms.author: prmitiki
ms.openlocfilehash: 77cc4732e017d95cbae19578cf26b1111b08fdde
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/27/2020
ms.locfileid: "75908985"
---
# <a name="associate-peer-asn-to-azure-subscription-using-powershell"></a>Zuordnen der Peer-ASN zum Azure-Abonnement mithilfe von PowerShell

Vor dem Einreichen einer Peeringanforderung sollten Sie zunächst mithilfe der unten dargestellten Schritte Ihre ASN dem Azure-Abonnement zuordnen.

Falls Sie es vorziehen, können Sie diese Anleitung auch mithilfe des [Portals](howto-subscription-association-portal.md) ausführen.

### <a name="working-with-azure-powershell"></a>Arbeiten mit Azure PowerShell
[!INCLUDE [CloudShell](./includes/cloudshell-powershell-about.md)]

## <a name="create-peerasn-to-associate-your-asn-with-azure-subscription"></a>Erstellen einer PeerASN zum Zuordnen Ihrer ASN zum Azure-Abonnement

### <a name="sign-in-to-your-azure-account-and-select-your-subscription"></a>Melden Sie sich bei Ihrem Azure-Konto an, und wählen Sie Ihr Abonnement aus.
[!INCLUDE [Account](./includes/account-powershell.md)]

### <a name="register-for-peering-resource-provider"></a>Für Peeringressourcenanbieter registrieren
Registrieren Sie sich mithilfe des Befehls unten in Ihrem Abonnement für den Peeringressourcenanbieter. Wenn Sie diese Schritte nicht ausführen, sind die zum Einrichten des Peerings erforderlichen Azure-Ressourcen nicht verfügbar.

```powershell
Register-AzResourceProvider -ProviderNamespace Microsoft.Peering
```

Sie können den Registrierungsstatus mithilfe der Befehle unten überprüfen:
```powershell
Get-AzResourceProvider -ProviderNamespace Microsoft.Peering
```

> [!IMPORTANT]
> Warten Sie, bis *RegistrationState* zu „Registriert“ wechselt, bevor Sie fortfahren. Dies kann 5 bis 30 Minuten dauern, nachdem Sie den Befehl ausgeführt haben.

### <a name="update-the-peer-information-associated-with-this-subscription"></a>Aktualisieren der diesem Abonnement zugeordneten Peerinformationen

Unten finden Sie ein Beispiel für die Aktualisierung von Peerinformationen.

```powershell
New-AzPeerAsn `
    -Name "Contoso_1234" `
    -PeerName "Contoso" `
    -PeerAsn 1234 `
    -Email noc@contoso.com, support@contoso.com `
    -Phone "+1 (555) 555-5555"
```

> [!NOTE]
> -Name entspricht dem Ressourcennamen und ist frei wählbar. -peerName entspricht jedoch dem Namen Ihres Unternehmens und muss so nah wie möglich an Ihrem PeeringDB-Profil sein. Beachten Sie, dass der Wert für -peerName nur die Zeichen a–z, A–Z und Leerzeichen unterstützt.

Ein Abonnement kann über mehrere ASNs verfügen. Aktualisieren Sie die Peeringinformationen für jede ASN. Achten Sie darauf, dass „name“ für jede ASN eindeutig ist.

Von Peers wird erwartet, dass sie über ein umfassendes und aktuelles Profil auf [PeeringDB](https://www.peeringdb.com) verfügen. Wir verwenden diese Informationen während der Registrierung, um die Detailangaben des Peers zu überprüfen, wie etwa die NOC-Informationen, Informationen zum technischen Kontakt, die Anwesenheit in den Peeringeinrichtungen usw.

Beachten Sie, dass anstelle von **{subscriptionId}** in der obigen Ausgabe die tatsächliche Abonnement-ID angezeigt wird.

## <a name="view-status-of-a-peerasn"></a>Anzeigestatus einer PeerASN

Überprüfen Sie den ASN-Überprüfungsstatus mit dem folgenden Befehl:

```powershell
Get-AzPeerAsn
```

Unten finden Sie eine Beispielantwort:
```powershell
PeerContactInfo : Microsoft.Azure.PowerShell.Cmdlets.Peering.Models.PSContactInfo
PeerName        : Contoso
ValidationState : Approved
PeerAsnProperty : 1234
Name            : Contoso_1234
Id              : /subscriptions/{subscriptionId}/providers/Microsoft.Peering/peerAsns/Contoso_1234
Type            : Microsoft.Peering/peerAsns
```

> [!IMPORTANT]
> Warten Sie, bis der ValidationState sich in „Genehmigt“ geändert hat, bevor Sie eine Peeringanforderung einreichen. Diese Genehmigung kann bis zu 12 Stunden dauern.

## <a name="modify-peerasn"></a>PeerAsn ändern
Sie können die NOC-Kontaktinformationen jederzeit ändern.

Unten ist ein Beispiel aufgeführt:

```powershell
Set-PeerAsn -Name Contoso_1234 -Email "newemail@test.com" -Phone "1800-000-0000"
```

## <a name="delete-peerasn"></a>PeerAsn löschen
Das Löschen einer PeerASN wird zurzeit nicht unterstützt. Wenn Sie die PeerASN löschen müssen, wenden Sie sich an [Microsoft Peering](mailto:peering@microsoft.com).

## <a name="next-steps"></a>Nächste Schritte

* [Erstellen oder Ändern einer Instanz für Direct Peering](howto-direct-powershell.md)
* [Konvertieren einer älteren Instanz für Direct Peering in eine Azure-Ressource](howto-legacy-direct-powershell.md)
* [Erstellen oder Ändern von Exchange Peering](howto-exchange-powershell.md)
* [Konvertieren einer älteren Instanz für Exchange Peering in eine Azure-Ressource](howto-legacy-exchange-powershell.md)

## <a name="additional-resources"></a>Zusätzliche Ressourcen

Weitere Informationen finden Sie unter [Internetpeering: häufig gestellte Fragen](faqs.md).
