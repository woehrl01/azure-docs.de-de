---
title: Azure Blob Storage-Trigger und -Bindungen für Azure Functions
description: Erfahren Sie, wie Sie Azure Blob Storage-Trigger und -Bindungen in Azure Functions verwenden.
author: craigshoemaker
ms.topic: reference
ms.date: 02/13/2020
ms.author: cshoe
ms.openlocfilehash: 6950f1dd81ef2c70f2c45fb4c547ed7676067790
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2020
ms.locfileid: "79235086"
---
# <a name="azure-blob-storage-bindings-for-azure-functions-overview"></a>Übersicht zu Azure Blob Storage-Bindungen für Azure Functions

Azure Functions integriert sich in [Azure Storage](https://docs.microsoft.com/azure/storage/) mittels [Triggern und Bindungen](./functions-triggers-bindings.md). Durch die Integration in Blob Storage können Sie Funktionen erstellen, die auf Änderungen in Blobdaten sowie auf Lese- und Schreib-Werte reagieren.

| Aktion | type |
|---------|---------|
| Ausführen einer Funktion, wenn sich Blob Storage-Daten ändern | [Trigger](./functions-bindings-storage-blob-trigger.md) |
| Lesen von Blob Storage-Daten in eine Funktion | [Eingabebindung](./functions-bindings-storage-blob-input.md) |
| Einer Funktion das Schreiben von Blob Storage-Daten gestatten |[Ausgabebindung](./functions-bindings-storage-blob-output.md) |

## <a name="add-to-your-functions-app"></a>Hinzufügen zu Ihrer Funktions-App

### <a name="functions-2x-and-higher"></a>Functions 2.x und höher

Das Arbeiten mit Triggern und Bindungen erfordert, dass Sie auf das entsprechende Paket verweisen. Das NuGet-Paket wird für .NET-Klassenbibliotheken verwendet, während das Erweiterungspaket für alle anderen Anwendungstypen verwendet wird.

| Sprache                                        | Hinzufügen nach...                                   | Bemerkungen 
|-------------------------------------------------|---------------------------------------------|-------------|
| C#                                              | Installieren des [NuGet-Paket], Version 3.x | |
| C#-Skript, Java, JavaScript, Python, PowerShell | Registrieren des [Erweiterungspaket]          | Die [Erweiterung für Azure-Tools](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack) wird zur Verwendung mit Visual Studio Code empfohlen. |
| C#-Skript (nur online im Azure-Portal)         | Hinzufügen einer Bindung                            | Informationen zum Aktualisieren vorhandener Bindungserweiterungen, ohne Ihre Funktions-App erneut veröffentlichen zu müssen, finden Sie unter [Aktualisieren Ihrer Erweiterungen]. |

[core tools]: ./functions-run-local.md
[Erweiterungspaket]: ./functions-bindings-register.md#extension-bundles
[NuGet-Paket]: https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Storage
[Aktualisieren Ihrer Erweiterungen]: ./install-update-binding-extensions-manual.md
[Azure Tools extension]: https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack

### <a name="functions-1x"></a>Functions 1.x

Functions 1.x-Apps enthalten automatisch einen Verweis auf das NuGet-Paket, Version 2.x, [Microsoft.Azure.WebJobs](https://www.nuget.org/packages/Microsoft.Azure.WebJobs).

[!INCLUDE [functions-storage-sdk-version](../../includes/functions-storage-sdk-version.md)]

## <a name="next-steps"></a>Nächste Schritte

- [Ausführen einer Funktion, wenn sich Blob Storage-Daten ändern](./functions-bindings-storage-blob-trigger.md)
- [Lesen von Blob Storage-Daten, wenn eine Funktion ausgeführt wird](./functions-bindings-storage-blob-input.md)
- [Schreiben von Blob Storage-Daten aus einer Funktion](./functions-bindings-storage-blob-output.md)
