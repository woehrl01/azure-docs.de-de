---
title: Debugging und Problembehandlung von ParallelRunStep
titleSuffix: Azure Machine Learning
description: Debuggen und Problembehandlung für ParallelRunStep in Machine Learning-Pipelines im Azure Machine Learning SDK für Python. Lernen Sie häufige Fallstricke bei der Entwicklung mit Pipelines kennen, und erhalten Sie Tipps, die Ihnen helfen, Ihre Skripts vor und während der Remoteausführung zu debuggen.
services: machine-learning
ms.service: machine-learning
ms.subservice: core
ms.topic: conceptual
ms.reviewer: trbye, jmartens, larryfr, vaidyas
ms.author: trmccorm
author: tmccrmck
ms.date: 01/15/2020
ms.openlocfilehash: ca50d70965d5edc4e31606e542ddf163fe3b0741
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/27/2020
ms.locfileid: "76122927"
---
# <a name="debug-and-troubleshoot-parallelrunstep"></a>Debugging und Problembehandlung von ParallelRunStep
[!INCLUDE [applies-to-skus](../../includes/aml-applies-to-basic-enterprise-sku.md)]

In diesem Artikel erfahren Sie, wie Sie Debugging und Problembehandlung für die [ParallelRunStep](https://docs.microsoft.com/python/api/azureml-contrib-pipeline-steps/azureml.contrib.pipeline.steps.parallel_run_step.parallelrunstep?view=azure-ml-py)-Klasse im [Azure Machine Learning SDK](https://docs.microsoft.com/python/api/overview/azure/ml/intro?view=azure-ml-py) durchführen.

## <a name="testing-scripts-locally"></a>Lokales Testen von Skripts

Weitere Informationen finden Sie im Abschnitt [Lokales Testen von Skripts](how-to-debug-pipelines.md#testing-scripts-locally) für Pipelines des maschinellen Lernens. Ihre ParallelRunStep-Instanz wird als Schritt in ML-Pipelines ausgeführt, sodass die gleiche Antwort für beide gilt.

## <a name="debugging-scripts-from-remote-context"></a>Debuggen von Skripts aus Remotekontext

Der Übergang vom lokalen Debuggen eines Bewertungsskripts zum Debuggen eines Bewertungsskripts in einer echten Pipeline kann einen schwierigen Schritt darstellen. Informationen zum Suchen Ihrer Protokolle im Portal finden Sie im [Abschnitt zu Pipelines des maschinellen Lernens über das Debuggen von Skripts aus einem Remotekontext](how-to-debug-pipelines.md#debugging-scripts-from-remote-context). Die Informationen in diesem Abschnitt gelten auch für eine parallele Schrittausführung.

Die Protokolldatei `70_driver_log.txt` enthält z. B. Informationen vom Controller, der den Code für die parallele Schrittausführung startet.

Aufgrund der verteilten Struktur von parallel ausgeführten Aufträgen gibt es Protokolle aus mehreren verschiedenen Quellen. Es werden jedoch zwei konsolidierte Dateien erstellt, die allgemeine Informationen bieten:

- `~/logs/overview.txt`: Diese Datei enthält allgemeine Informationen zur Anzahl der bisher erstellten Minibatches (auch als Aufgaben bezeichnet) und der Anzahl der bisher verarbeiteten Minibatches. Am Ende wird das Ergebnis des Auftrags aufgeführt. Wenn bei dem Auftrag ein Fehler aufgetreten ist, wird die Fehlermeldung angezeigt, und es wird beschrieben, wo mit der Problembehandlung begonnen werden sollte.

- `~/logs/sys/master.txt`: Diese Datei stellt die Masterknotenansicht (auch als Orchestrator bezeichnet) des laufenden Auftrags bereit. Dies umfasst die Aufgabenerstellung, die Fortschrittsüberwachung und das Ergebnis der Ausführung.

Protokolle, die mit „EntryScript.logger“ aus dem Eingabeskript generiert wurden, sowie Druckanweisungen finden Sie in den folgenden Dateien:

- `~/logs/user/<ip_address>/Process-*.txt`: Diese Datei enthält Protokolle, die von „entry_script“ mit „EntryScript.logger“ geschrieben wurden. Sie enthält auch eine Druckanweisung (stdout) von „entry_script“.

Wenn Sie detailliert erfahren möchten, wie die einzelnen Knoten das Bewertungsskript ausgeführt haben, sehen Sie sich die jeweiligen Prozessprotokolle für jeden Knoten an. Die Prozessprotokolle befinden sich im Ordner `sys/worker`, gruppiert nach Workerknoten:

- `~/logs/sys/worker/<ip_address>/Process-*.txt`: Diese Datei enthält ausführliche Informationen zu den einzelnen Minibatches, die von einem Worker abgerufen oder abgeschlossen werden. Für jeden Minibatch umfasst diese Datei Folgendes:

    - Die IP-Adresse und die PID des Workerprozesses. 
    - Die Gesamtzahl der Elemente, die Anzahl der erfolgreich verarbeiteten Elemente und die Anzahl der nicht erfolgreichen Elemente.
    - Die Startzeit, die Dauer, die Verarbeitungszeit und die Laufzeit der Methode.

Sie finden auch Informationen zur Ressourcennutzung der Prozesse für jeden Worker. Diese Informationen liegen im CSV-Format vor und befinden sich unter `~/logs/sys/perf/<ip_address>/`. Für einen einzelnen Knoten sind die Auftragsdateien unter `~logs/sys/perf` verfügbar. Wenn Sie z. B. die Ressourcennutzung überprüfen, sehen Sie sich die folgenden Dateien an:

- `Process-*.csv`: Ressourcennutzung pro Workerprozess. 
- `sys.csv`: Protokoll pro Knoten.

### <a name="how-do-i-log-from-my-user-script-from-a-remote-context"></a>Wie protokolliere ich mein Benutzerskript aus einem Remotekontext?
Sie können eine Protokollierung von EntryScript abrufen, wie im folgenden Beispielcode gezeigt, damit die Protokolle im Ordner **logs/user** im Portal angezeigt werden.

**Ein Beispiel für Eingabeskript mit der Protokollierung:**
```python
from entry_script import EntryScript

def init():
    """ Initialize the node."""
    entry_script = EntryScript()
    logger = entry_script.logger
    logger.debug("This will show up in files under logs/user on the Azure portal.")


def run(mini_batch):
    """ Accept and return the list back."""
    # This class is in singleton pattern and will return same instance as the one in init()
    entry_script = EntryScript()
    logger = entry_script.logger
    logger.debug(f"{__file__}: {mini_batch}.")
    ...

    return mini_batch
```

### <a name="how-could-i-pass-a-side-input-such-as-a-file-or-files-containing-a-lookup-table-to-all-my-workers"></a>Wie könnte ich eine seitliche Eingabe, z. B. eine oder mehrere Dateien mit einer Nachschlagetabelle, an alle meine Mitarbeiter weitergeben?

Konstruieren Sie ein [Dataset](https://docs.microsoft.com/python/api/azureml-core/azureml.core.dataset.dataset?view=azure-ml-py)-Objekt, das die seitliche Eingabe enthält, und registrieren Sie es in Ihrem Arbeitsbereich. Danach können Sie in Ihrem Rückschlussskript (z. B. in Ihrer init()-Methode) wie folgt darauf zugreifen:

```python
from azureml.core.run import Run
from azureml.core.dataset import Dataset

ws = Run.get_context().experiment.workspace
lookup_ds = Dataset.get_by_name(ws, "<registered-name>")
lookup_ds.download(target_path='.', overwrite=True)
```

## <a name="next-steps"></a>Nächste Schritte

* In der SDK-Referenz finden Sie Hilfe zum Paket [azureml-contrib-pipeline-step](https://docs.microsoft.com/python/api/azureml-contrib-pipeline-steps/azureml.contrib.pipeline.steps?view=azure-ml-py) und die [Dokumentation](https://docs.microsoft.com/python/api/azureml-contrib-pipeline-steps/azureml.contrib.pipeline.steps.parallelrunstep?view=azure-ml-py) für die ParallelRunStep-Klasse.

* Folgen Sie dem [erweiterten Tutorial](tutorial-pipeline-batch-scoring-classification.md) zur Verwendung von Pipelines mit parallel ausgeführtem Schritt.
