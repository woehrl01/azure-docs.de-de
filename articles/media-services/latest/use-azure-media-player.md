---
title: Wiedergabe mit Azure Media Player – Azure | Microsoft-Dokumentation
description: Azure Media Player ist ein Webvideoplayer für die Wiedergabe von Medieninhalten aus Microsoft Azure Media Services über eine Vielzahl von Browsern und Geräten.
services: media-services
documentationcenter: ''
author: Juliako
manager: femila
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: article
ms.date: 07/17/2019
ms.author: juliako
ms.openlocfilehash: d9e42e809443a2dd6cdeb989f692b96d63269f79
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2020
ms.locfileid: "78673580"
---
# <a name="azure-media-player-overview"></a>Übersicht über Azure Media Player

Azure Media Player ist ein Webvideoplayer für die Wiedergabe von Medieninhalten aus Microsoft Azure Media Services über eine Vielzahl von Browsern und Geräten. Der Azure Media Player nutzt Industriestandards wie HTML5, MSE (Media Source Extensions) und EME (Encrypted Media Extensions) für ein funktionsreiches adaptives Streaming. Wenn diese Standards auf einem Gerät oder in einem Browser nicht verfügbar sind, verwendet Azure Media Player Flash und Silverlight als Fallback-Technologien. Unabhängig von der verwendeten Wiedergabetechnologie müssen Entwickler eine einheitliche Schnittstelle für JavaScript für den Zugriff auf APIs verwenden. Dies ermöglicht die Inhaltswiedergabe von Azure Media Services über eine breite Palette von Geräten und Browsern ohne jeglichen Zusatzaufwand.

Mit Microsoft Azure Media Services können Inhalte in den Streamingformaten HLS, DASH und Smooth Streaming wiedergegeben werden. Der Azure Media Player erkennt diese unterschiedlichen Formate und übernimmt automatisch die beste Verknüpfung basierend auf den Funktionen von Plattform und Browser. Media Services ermöglicht auch die dynamische Verschlüsselung von Medienobjekten mit PlayReady-Verschlüsselung oder AES-128-Bit-Umschlagverschlüsselung. Der Azure Media Player ermöglicht bei entsprechender Konfiguration die Entschlüsselung von PlayReady- und AES-128-Bit-verschlüsselten Inhalten. 

> [!NOTE]
> Für Inhalte mit Widevine-Verschlüsselung ist die HTTPS-Wiedergabe erforderlich.

## <a name="use-azure-media-player-demo-page"></a>Verwenden der Azure Media Player-Demoseite

### <a name="start-using"></a>Jetzt beginnen

Sie können die [Azure Media Player-Demoseite](https://aka.ms/azuremediaplayer) verwenden, um Azure Media Services-Beispiele oder Ihren eigenen Stream wiederzugeben.  

Fügen Sie zum Wiedergeben eines neuen Videos eine andere URL ein, und wählen Sie die Option **Aktualisieren**.

Wählen Sie **Erweiterte Optionen**, um die Wiedergabeoptionen zu konfigurieren (z.B. Technologie, Sprache oder Verschlüsselung).

![Azure Media Player](./media/azure-media-player/home-page.png)

### <a name="monitor-diagnostics-of-a-video-stream"></a>Überwachen der Diagnosedaten eines Videostreams

Sie können mithilfe der [Azure Media Player-Demoseite](https://aka.ms/azuremediaplayer) die Diagnosedaten eines Videostreams überwachen. 

![Azure Media Player-Diagnose](./media/azure-media-player/diagnostics.png)

## <a name="set-up-azure-media-player-in-your-html"></a>Einrichten von Azure Media Player in Ihrem HTML-Code

Die Einrichtung von Azure Media Player ist einfach. Es dauert nur einige Augenblicke, bis die einfache Wiedergabe von Medieninhalten über Ihr Media Services-Konto möglich ist. Ausführliche Informationen zur Einrichtung und Konfiguration von Azure Media Player finden Sie in der [Azure Media Player-Dokumentation](https://aka.ms/ampdocs). 

## <a name="additional-notes"></a>Zusätzliche Hinweise

* Widevine ist ein von Google Inc. bereitgestellter Dienst, der den Vertragsbedingungen und der Datenschutzrichtlinie von Google, Inc. unterliegt.

## <a name="next-steps"></a>Nächste Schritte

- [Azure Media Player-Dokumentation](https://aka.ms/ampdocs)
- [Azure Media Player-Beispiele](https://aka.ms/ampsamples)
