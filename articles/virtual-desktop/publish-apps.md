---
title: Veröffentlichen von integrierten Apps in Windows Virtual Desktop – Azure
description: Hier erfahren Sie, wie Sie integrierte Apps in Windows Virtual Desktop veröffentlichen.
services: virtual-desktop
author: Heidilohr
ms.service: virtual-desktop
ms.topic: conceptual
ms.date: 04/30/2020
ms.author: helohr
manager: lizross
ms.openlocfilehash: 3a238a5ae282d5059eee23b4bcaa86a3e84b6656
ms.sourcegitcommit: 602e6db62069d568a91981a1117244ffd757f1c2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/06/2020
ms.locfileid: "82863296"
---
# <a name="publish-built-in-apps-in-windows-virtual-desktop"></a>Veröffentlichen von integrierten Apps in Windows Virtual Desktop

>[!IMPORTANT]
>Dieser Inhalt gilt für das Update vom Frühjahr 2020 mit Windows Virtual Desktop-Objekten für Azure Resource Manager. Wenn Sie das Windows Virtual Desktop-Release vom Herbst 2019 ohne Azure Resource Manager-Objekte verwenden, finden Sie weitere Informationen in [diesem Artikel](./virtual-desktop-fall-2019/publish-apps-2019.md).
>
> Das Windows Virtual Desktop-Update vom Frühjahr 2020 befindet sich derzeit in der öffentlichen Vorschauphase. Diese Vorschauversion wird ohne Vereinbarung zum Servicelevel bereitgestellt und ist nicht für Produktionsworkloads vorgesehen. Manche Features werden möglicherweise nicht unterstützt oder sind nur eingeschränkt verwendbar. 
> Weitere Informationen finden Sie unter [Zusätzliche Nutzungsbestimmungen für Microsoft Azure-Vorschauen](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

In diesem Artikel erfahren Sie, wie Sie Apps in Ihrer Windows Virtual Desktop-Umgebung veröffentlichen.

## <a name="publish-built-in-apps"></a>Veröffentlichen von integrierten Apps

So veröffentlichen Sie eine integrierte App:

1. Stellen Sie eine Verbindung mit einem der virtuellen Computer in Ihrem Hostpool her.
2. Rufen Sie den **PackageFamilyName** der zu veröffentlichenden App ab. Befolgen Sie dazu die Anweisungen in [diesem Artikel](/powershell/module/appx/get-appxpackage?view=win10-ps/).
3. Führen Sie schließlich das folgende Cmdlet aus; ersetzen Sie dabei `<PackageFamilyName>` durch den **PackageFamilyName** aus dem vorherigen Schritt:
   
   ```powershell
   New-AzWvdApplication -Name <applicationname> -ResourceGroupName <resourcegroupname> -ApplicationGroupName <appgroupname> -FilePath "shell:appsFolder\<PackageFamilyName>!App" -CommandLineSetting <Allow|Require|DoNotAllow> -IconIndex 0 -IconPath <iconpath> -ShowInPortal:$true
   ```

>[!NOTE]
> Windows Virtual Desktop unterstützt nur das Veröffentlichen von Apps mit Installationsspeicherorten, die mit `C:\Program Files\WindowsApps`beginnen.

## <a name="update-app-icons"></a>Aktualisieren von App-Symbolen

Nach dem Veröffentlichen einer App weist diese das Windows-Standardsymbol für Apps und nicht ihr normales App-Symbolbild auf. Wenn Sie das Symbol in das normale Symbol ändern möchten, legen Sie das Bild für das gewünschte Symbol auf einer Netzwerkfreigabe ab. Unterstützte Bildformate sind PNG, BMP, GIF, JPG, JPEG und ICO.

## <a name="publish-microsoft-edge"></a>Veröffentlichen von Microsoft Edge

Der Vorgang zum Veröffentlichen von Microsoft Edge unterscheidet sich etwas von dem Vorgang beim Veröffentlichen anderer Apps. Führen Sie dieses Cmdlet aus, um Microsoft Edge mit der standardmäßigen Startseite zu veröffentlichen:

```powershell
New-AzWvdApplication -Name -ResourceGroupName -ApplicationGroupName -FilePath "shell:Appsfolder\Microsoft.MicrosoftEdge_8wekyb3d8bbwe!MicrosoftEdge" -CommandLineSetting <Allow|Require|DoNotAllow> -iconPath "C:\Windows\SystemApps\Microsoft.MicrosoftEdge_8wekyb3d8bbwe\microsoftedge.exe" -iconIndex 0 -ShowInPortal:$true 
```

## <a name="next-steps"></a>Nächste Schritte

- Informieren Sie sich unter [Anpassen von Feeds für Windows Virtual Desktop-Benutzer](customize-feed-for-virtual-desktop-users.md), wie Sie Feeds konfigurieren, um festzulegen, wie Apps für Benutzer angezeigt werden.
- Machen Sie sich unter [Einrichten des MSIX-Features zum Anfügen von Apps](app-attach.md) mit dem MSIX-Feature zum Anfügen von Apps vertraut.

