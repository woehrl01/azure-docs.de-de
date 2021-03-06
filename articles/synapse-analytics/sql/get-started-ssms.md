---
title: 'SSMS: Herstellen einer Verbindung mit und Abfragen von Synapse SQL'
description: Verwenden Sie SQL Server Management Studio (SSMS), um eine Verbindung mit Synapse SQL in Azure Synapse Analytics herzustellen und Abfragen auszuführen.
services: synapse-analytics
author: azaricstefan
ms.service: synapse-analytics
ms.topic: overview
ms.subservice: ''
ms.date: 04/15/2020
ms.author: v-stazar
ms.reviewer: jrasnick
ms.openlocfilehash: 704da86fd1d816dbf5d6cd9cf67dfee53fce2622
ms.sourcegitcommit: b80aafd2c71d7366838811e92bd234ddbab507b6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2020
ms.locfileid: "81419634"
---
# <a name="connect-to-synapse-sql-with-sql-server-management-studio-ssms"></a>Herstellen einer Verbindung mit Synapse SQL mithilfe von SQL Server Management Studio (SSMS)
> [!div class="op_single_selector"]
> * [Azure Data Studio](get-started-azure-data-studio.md)
> * [Power BI](get-started-power-bi-professional.md)
> * [Visual Studio](../sql-data-warehouse/sql-data-warehouse-query-visual-studio.md?toc=/azure/synapse-analytics/toc.json&bc=/azure/synapse-analytics/breadcrumb/toc.json)
> * [sqlcmd](../sql/get-started-connect-sqlcmd.md)
> * [SSMS](get-started-ssms.md)
> 
> 

Sie können mithilfe von [SQL Server Management Studio (SSMS)](/sql/ssms/download-sql-server-management-studio-ssms) entweder über SQL On-Demand (Vorschauversion) oder SQL-Poolressourcen eine Verbindung mit Synapse SQL in Azure Synapse Analytics herstellen und Abfragen durchführen. 

### <a name="supported-tools-for-sql-on-demand-preview"></a>Unterstützte Tools für SQL On-Demand (Vorschauversion)

SSMS wird ab Version 18.5 teilweise unterstützt und bietet eingeschränkte Funktionen (etwa Verbinden und Abfragen). [Azure Data Studio](/sql/azure-data-studio/download-azure-data-studio) wird vollständig unterstützt.

## <a name="prerequisites"></a>Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:  

* [SQL Server Management Studio (SSMS)](/sql/ssms/download-sql-server-management-studio-ssms). 
* Für den SQL-Pool benötigen Sie ein vorhandenes Data Warehouse. Informationen zur Erstellung finden Sie unter [Erstellen eines SQL-Pools](../quickstart-create-sql-pool.md). Bei SQL On-Demand wird bereits bei der Erstellung ein Data Warehouse in Ihrem Arbeitsbereich bereitgestellt. 
* Den vollqualifizierten SQL Server-Namen. Informationen zur Ermittlung finden Sie unter [Herstellen einer Verbindung mit Synapse SQL](connect-overview.md).

## <a name="connect"></a>Verbinden

### <a name="sql-pool"></a>SQL-Pool

Führen Sie die folgenden Schritte aus, um mithilfe des SQL-Pools eine Verbindung mit Synapse SQL herzustellen: 

1. Öffnen Sie SQL Server Management Studio (SSMS). 
1. Füllen Sie im Dialogfeld **Mit Server verbinden** die Felder aus, und wählen Sie dann **Verbinden** aus: 
  
    ![Verbindung mit Server herstellen](../sql-data-warehouse/media/sql-data-warehouse-query-ssms/connect-object-explorer1.png)
   
   * **Servername**: Geben Sie den zuvor ermittelten **Servernamen** ein.
   * **Authentifizierung:**  Wählen Sie einen Authentifizierungstyp aus, etwa **SQL Server-Authentifizierung** oder **Integrierte Active Directory-Authentifizierung**.
   * **Benutzername** und **Kennwort**: Geben Sie Benutzername und Kennwort ein, wenn Sie oben „SQL Server-Authentifizierung“ ausgewählt haben.

1. Erweitern Sie Ihre Azure SQL Server-Instanz im **Objekt-Explorer**. Sie können die dem Server zugeordneten Datenbanken anzeigen, etwa die Beispieldatenbank „AdventureWorksDW“. Sie können die Datenbank erweitern, um die Tabellen anzuzeigen:
   
    ![AdventureWorksDW erkunden](../sql-data-warehouse/media/sql-data-warehouse-query-ssms/explore-tables.png)


### <a name="sql-on-demand-preview"></a>SQL On-Demand (Vorschauversion)

Führen Sie die folgenden Schritte aus, um mithilfe von SQL On-Demand eine Verbindung mit Synapse SQL herzustellen: 

1. Öffnen Sie SQL Server Management Studio (SSMS).
1. Füllen Sie im Dialogfeld **Mit Server verbinden** die Felder aus, und wählen Sie dann **Verbinden** aus: 
   
    ![Verbindung mit Server herstellen](./media/get-started-ssms/connect-object-explorer1.png)
   
   * **Servername**: Geben Sie den zuvor ermittelten **Servernamen** ein.
   * **Authentifizierung:** Wählen Sie einen Authentifizierungstyp aus, etwa **SQL Server-Authentifizierung** oder **Integrierte Active Directory-Authentifizierung**.
   * **Benutzername** und **Kennwort**: Geben Sie Benutzername und Kennwort ein, wenn Sie oben „SQL Server-Authentifizierung“ ausgewählt haben.
   * Klicken Sie auf **Verbinden**.

4. Erweitern Sie den Azure SQL-Server. Sie können die dem Server zugeordneten Datenbanken anzeigen. Erweitern Sie *Demo*, um den Inhalt in der Beispieldatenbank anzuzeigen.
   
    ![AdventureWorksDW erkunden](./media/get-started-ssms/explore-tables.png)


## <a name="run-a-sample-query"></a>Ausführen einer Beispielabfrage

### <a name="sql-pool"></a>SQL-Pool

Nachdem eine Datenbankverbindung hergestellt wurde, können Sie die Daten nun abfragen.

1. Klicken Sie mit der rechten Maustaste im SQL Server-Objekt-Explorer auf Ihre Datenbank.
2. Wählen Sie **Neue Abfrage** aus. Ein neues Abfragefenster wird geöffnet.
   
    ![Neue Abfrage](../sql-data-warehouse/media/sql-data-warehouse-query-ssms/new-query.png)
3. Kopieren Sie die folgende T-SQL-Abfrage in das Abfragefenster:
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. Führen Sie die Abfrage aus. Zu diesem Zweck klicken Sie auf `Execute` oder drücken auf `F5`.
   
    ![Abfrage ausführen](../sql-data-warehouse/media/sql-data-warehouse-query-ssms/execute-query.png)
5. Sehen Sie sich die Abfrageergebnisse an. In diesem Beispiel weist die Tabelle „FactInternetSales“ 60398 Zeilen auf.
   
    ![Abfrageergebnisse](../sql-data-warehouse/media/sql-data-warehouse-query-ssms/results.png)

### <a name="sql-on-demand"></a>SQL On-Demand

Nachdem eine Datenbankverbindung hergestellt wurde, können Sie die Daten nun abfragen.

1. Klicken Sie mit der rechten Maustaste im SQL Server-Objekt-Explorer auf Ihre Datenbank.
2. Wählen Sie **Neue Abfrage** aus. Ein neues Abfragefenster wird geöffnet.
   
    ![Neue Abfrage](./media/get-started-ssms/new-query.png)
3. Kopieren Sie die folgende TSQL-Abfrage in das Abfragefenster:
   
    ```sql
    SELECT COUNT(*) FROM demo.dbo.usPopulationView
    ```
4. Führen Sie die Abfrage aus. Zu diesem Zweck klicken Sie auf `Execute` oder drücken auf `F5`.
   
    ![Abfrage ausführen](./media/get-started-ssms/execute-query.png)
5. Sehen Sie sich die Abfrageergebnisse an. In diesem Beispiel enthält die Ansicht „usPopulationView“ 3.664.512 Zeilen.
   
    ![Abfrageergebnisse](./media/get-started-ssms/results.png)

## <a name="next-steps"></a>Nächste Schritte
Nun da Sie eine Verbindung hergestellt haben und Abfragen senden können, versuchen Sie, [die Daten mit Power BI zu visualisieren](get-started-power-bi-professional.md).

Informationen zum Konfigurieren der Umgebung für die Azure Active Directory-Authentifizierung finden Sie unter [Authentifizieren bei Azure Synapse Analytics](../sql-data-warehouse/sql-data-warehouse-authentication.md?toc=/azure/synapse-analytics/toc.json&bc=/azure/synapse-analytics/breadcrumb/toc.json).

