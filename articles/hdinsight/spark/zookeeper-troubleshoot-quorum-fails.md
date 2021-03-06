---
title: Fehler beim Bilden eines Quorums durch den Apache ZooKeeper-Server in Azure HDInsight
description: Fehler beim Bilden eines Quorums durch den Apache ZooKeeper-Server in Azure HDInsight
ms.service: hdinsight
ms.topic: troubleshooting
author: hrasheed-msft
ms.author: hrasheed
ms.reviewer: jasonh
ms.date: 08/20/2019
ms.openlocfilehash: 41ac109e5c5379e6085dd57a3fcd8119915558fb
ms.sourcegitcommit: 849bb1729b89d075eed579aa36395bf4d29f3bd9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/28/2020
ms.locfileid: "82133274"
---
# <a name="apache-zookeeper-server-fails-to-form-a-quorum-in-azure-hdinsight"></a>Fehler beim Bilden eines Quorums durch den Apache ZooKeeper-Server in Azure HDInsight

In diesem Artikel werden Schritte zur Problembehandlung und mögliche Lösungen für Probleme bei der Interaktion mit Azure HDInsight-Clustern beschrieben.

## <a name="issue"></a>Problem

Die Integrität des Apache ZooKeeper-Servers ist beeinträchtigt; mögliche Symptome: Resource Manager-Knoten/Namensknoten befinden sich im Standbymodus, einfache HDFS-Vorgänge (Hadoop Distributed File System) schlagen fehl, `zkFailoverController` wird beendet und kann nicht gestartet werden, Yarn/Spark/Livy-Aufträge schlagen aufgrund von ZooKeeper-Fehlern fehl. Auch LLAP-Daemons können möglicherweise nicht in Secure Spark- oder Interactive Hive-Clustern gestartet werden. Unter Umständen wird in etwa folgende Fehlermeldung angezeigt:

```
19/06/19 08:27:08 ERROR ZooKeeperStateStore: Fatal Zookeeper error. Shutting down Livy server.
19/06/19 08:27:08 INFO LivyServer: Shutting down Livy server.
```

In den Zookeeper-Serverprotokollen auf einem Zookeeper-Host unter „/var/log/zookeeper/zookeeper-zookeeper-server-\*.out“ wird möglicherweise auch der folgende Fehler angezeigt:

```
2020-02-12 00:31:52,513 - ERROR [CommitProcessor:1:NIOServerCnxn@178] - Unexpected Exception:
java.nio.channels.CancelledKeyException
```

## <a name="cause"></a>Ursache

Wenn das Volume mit den Momentaufnahmedateien groß oder beschädigt ist, kann der ZooKeeper-Server kein Quorum bilden, und dies führt zu Fehlern in den ZooKeeper-Diensten. Der ZooKeeper-Server entfernt keine alten Momentaufnahmedateien aus seinem Datenverzeichnis. Dies ist stattdessen ein Vorgang, der von Benutzern regelmäßig auszuführen ist, um die Integrität von ZooKeeper zu erhalten. Weitere Informationen finden Sie unter [ZooKeeper Strengths and Limitations](https://zookeeper.apache.org/doc/r3.3.5/zookeeperAdmin.html#sc_strengthsAndLimitations) (Vorteile und Einschränkungen von ZooKeeper).

## <a name="resolution"></a>Lösung

Überprüfen Sie das ZooKeeper `/hadoop/hdinsight-zookeeper/version-2`-Datenverzeichnis `/hadoop/zookeeper/version-2`, und stellen Sie fest, ob die Momentaufnahmendatei groß ist. Wenn große Momentaufnahmen vorhanden sind, führen Sie folgende Schritte aus:

1. Überprüfen Sie den Status anderer ZooKeeper-Server im selben Quorum, um sicherzustellen, dass sie mit dem Befehl „`echo stat | nc {zk_host_ip} 2181 (or 2182)`“ einwandfrei funktionieren.  

1. Melden Sie sich bei dem problematischen ZooKeeper-Host an, sichern Sie Momentaufnahmen und Transaktionsprotokolle in `/hadoop/zookeeper/version-2` und `/hadoop/hdinsight-zookeeper/version-2`, und bereinigen Sie dann diese Dateien in den beiden Verzeichnissen. 

1. Starten Sie den problematischen ZooKeeper-Server in Ambari oder den ZooKeeper-Host neu. Starten Sie dann den Dienst neu, bei dem Probleme auftreten.

## <a name="next-steps"></a>Nächste Schritte

Wenn Ihr Problem nicht aufgeführt ist oder Sie es nicht lösen können, besuchen Sie einen der folgenden Kanäle, um weitere Unterstützung zu erhalten:

- Nutzen Sie den [Azure-Communitysupport](https://azure.microsoft.com/support/community/), um Antworten von Azure-Experten zu erhalten.

- Herstellen einer Verbindung mit [@AzureSupport](https://twitter.com/azuresupport), dem offiziellen Microsoft Azure-Konto zum Verbessern der Kundenfreundlichkeit. Verbinden der Azure-Community mit den richtigen Ressourcen: Antworten, Support und Experten.

- Sollten Sie weitere Unterstützung benötigen, senden Sie eine Supportanfrage über das [Azure-Portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade/). Wählen Sie dazu auf der Menüleiste die Option **Support** aus, oder öffnen Sie den Hub **Hilfe und Support**. Ausführlichere Informationen hierzu finden Sie unter [Erstellen einer Azure-Supportanfrage](https://docs.microsoft.com/azure/azure-portal/supportability/how-to-create-azure-support-request). Zugang zu Abonnementverwaltung und Abrechnungssupport ist in Ihrem Microsoft Azure-Abonnement enthalten. Technischer Support wird über einen [Azure-Supportplan](https://azure.microsoft.com/support/plans/) bereitgestellt.
