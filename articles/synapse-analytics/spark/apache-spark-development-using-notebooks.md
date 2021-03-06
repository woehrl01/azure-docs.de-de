---
title: Erstellen, Entwickeln und Verwalten von Azure Synapse Studio (Vorschau)-Notebooks
description: In diesem Artikel erfahren Sie, wie Sie Azure Synapse Studio (Vorschau)-Notebooks erstellen und entwickeln, um Datenvorbereitung und -visualisierung durchzuführen.
services: synapse analytics
author: ruixinxu
ms.service: synapse-analytics
ms.topic: conceptual
ms.subservice: ''
ms.date: 04/15/2020
ms.author: ruxu
ms.reviewer: ''
ms.openlocfilehash: 506339cefa90fb17bedfc946f70cb4d7d8047cf2
ms.sourcegitcommit: b80aafd2c71d7366838811e92bd234ddbab507b6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2020
ms.locfileid: "81427138"
---
# <a name="create-develop-and-maintain-azure-synapse-studio-preview-notebooks"></a>Erstellen, Entwickeln und Verwalten von Azure Synapse Studio (Vorschau)-Notebooks

Ein Azure Synapse Studio (Vorschau)-Notebook ist eine Webschnittstelle, mit der Sie Dateien erstellen können, die Livecode, Visualisierungen und Text enthalten. Notebooks sind ein guter Ausgangspunkt, um Ideen zu überprüfen und schnelle Experimente zu verwenden, um Erkenntnisse aus Ihren Daten zu gewinnen. Notebooks werden auch häufig bei der Datenvorbereitung, Datenvisualisierung, Machine Learning und andere Big Data-Szenarien verwendet.

Mit einem Azure Synapse Studio-Notebook können Sie:

* Ohne Einrichtungsaufwand sofort loslegen.
* Daten mit integrierten Sicherheitsfeatures auf Unternehmensniveau schützen.
* Daten in Rohformaten (CSV, TXT, JSON usw.), verarbeiteten Dateiformaten (Parquet, Delta Lake, ORC usw.) und tabellarischen SQL-Datendateien gegen Spark und SQL analysieren.
* Produktiv sein mit erweiterten Funktionen zur Dokumenterstellung und integrierter Datenvisualisierung.

In diesem Artikel wird beschrieben, wie Sie Notebooks in Azure Synapse Studio verwenden.

## <a name="create-a-notebook"></a>Erstellen eines Notebooks

Ein Notebook kann auf zwei Arten erstellt werden. Sie können ein neues Notebook erstellen oder ein vorhandenes Notebook aus dem **Objekt-Explorer** in einen Azure Synapse-Arbeitsbereich importieren. Azure Synapse Studio-Notebooks können Jupyter Notebook IPYNB-Standarddateien erkennen.

![Synapse-erstellen-importieren-Notebook](./media/apache-spark-development-using-notebooks/synapse-create-import-notebook.png)

## <a name="develop-notebooks"></a>Entwickeln von Notebooks

Notebooks bestehen aus Zellen, bei denen es sich um einzelne Codeblöcke oder Text handelt, die unabhängig oder als Gruppe ausgeführt werden können.

### <a name="add-a-cell"></a>Hinzufügen einer Zelle

Es gibt mehrere Möglichkeiten, um Ihrem Notebook eine neue Zelle hinzuzufügen.

1. Erweitern Sie die Schaltfläche oben links **+ Zelle**, und wählen Sie **Codezelle hinzufügen** oder **Textzelle hinzufügen** aus.

    ![Hinzufügen-Zelle-mit-Schaltfläche-Zelle](./media/apache-spark-development-using-notebooks/synapse-add-cell-1.png)

2. Zeigen Sie mit dem Mauszeiger auf den Bereich zwischen zwei Zellen, und wählen Sie **Code hinzufügen** oder **Text hinzufügen** aus.

    ![Hinzufügen-Zelle-Zwischenraum](./media/apache-spark-development-using-notebooks/synapse-add-cell-2.png)

3. Verwenden Sie [Tastenkombinationen im Befehlsmodus](#shortcut-keys-under-command-mode). Drücken Sie **A**, um eine Zelle oberhalb der aktuellen Zelle einzufügen. Drücken Sie **B**, um eine Zelle unterhalb der aktuellen Zelle einzufügen.

### <a name="set-a-primary-language"></a>Festlegen einer primären Sprache

Azure Synapse Studio-Notebooks unterstützen vier Spark-Sprachen:

* pyspark (Python)
* spark (Scala)
* sparkSQL
* Spark.NET (C#)

Sie können die primäre Sprache für neu hinzugefügte Zellen in der Dropdownliste in der oberen Befehlsleiste festlegen.

   ![Standard-Synapse-Sprache](./media/apache-spark-development-using-notebooks/synapse-default-language.png)

### <a name="use-multiple-languages"></a>Verwenden mehrerer Sprachen

Sie können in einem Notebook mehrere Sprachen verwenden, indem Sie den richtigen Magic-Befehl für die Sprache am Anfang einer Zelle angeben. In der folgenden Tabelle werden die Magic-Befehle zum Wechseln von Zellensprachen aufgelistet.

|Magic-Befehl |Sprache | BESCHREIBUNG |  
|---|------|-----|
|%%pyspark| Python | Eine **Python**-Abfrage im Spark-Kontext ausführen.  |
|%%spark| Scala | Eine **Scala**-Abfrage im Spark-Kontext ausführen.  |  
|%%sql| SparkSQL | Eine **SparkSQL**-Abfrage im Spark-Kontext ausführen.  |
|%%csharp | Spark.NET C# | Eine **Spark.NET C#** -Abfrage im Spark-Kontext ausführen. |

Die folgende Abbildung zeigt ein Beispiel dafür, wie Sie eine PySpark-Abfrage mit dem Magic-Befehl **%%pyspark** schreiben können oder eine SparkSQL-Abfrage mit dem Magic-Befehl **%%sql** in einem **Spark (Scala)** -Notebook. Beachten Sie, dass die primäre Sprache für das Notebook auf Scala festgelegt ist.

   ![Synapse-Spark-Magic-Befehle](./media/apache-spark-development-using-notebooks/synapse-spark-magics.png)

### <a name="use-temp-tables-to-reference-data-across-languages"></a>Verwenden von temporären Tabellen zum Verweisen auf Daten in verschiedenen Sprachen

Sie können nicht direkt auf Daten oder Variablen in verschiedenen Sprachen einem Synapse Studio-Notebook verweisen. In Spark kann auf eine temporäre Tabelle in verschiedenen Sprachen verwiesen werden. Im Folgenden finden Sie ein Beispiel, wie Sie einen `Scala`-Datenrahmen in `PySpark` und `SparkSQL` mittels einer temporären Spark-Tabelle als Problemumgehung lesen können.

1. In Zelle 1 lesen Sie einen Datenrahmen aus dem SQL-Poolconnector mithilfe von Scala, und erstellen Sie eine temporäre Tabelle.

   ```scala
   %%scala
   val scalaDataFrame = spark.read.option("format", "DW connector predefined type")
   scalaDataFrame.registerTempTable( "mydataframetable" )
   ```

2. In Zelle 2 fragen Sie die Daten mithilfe von Spark SQL ab.
   
   ```sql
   %%sql
   SELECT * FROM mydataframetable
   ```

3. In Zelle 3 verwenden Sie die Daten in PySpark.

   ```python
   %%pyspark
   myNewPythonDataFrame = spark.sql("SELECT * FROM mydataframetable")
   ```

### <a name="ide-style-intellisense"></a>IDE-artiges IntelliSense

Azure Synapse Studio-Notebooks sind in den Monaco-Editor integriert, um den Zellen-Editor mit IDE-artigem IntelliSense auszustatten. Syntaxhervorhebung, Fehlermarkierungen und automatische Codevervollständigungen helfen Ihnen, Code zu schreiben und Probleme schneller zu erkennen.

Die IntelliSense-Funktionen befinden sich in unterschiedlichen Stadien der Entwicklung für verschiedene Sprachen. In der folgenden Tabelle können Sie sehen, was unterstützt wird.

|Languages| Syntaxhervorhebung | Syntaxfehlermarkierungen  | Codevervollständigung für Syntax | Codevervollständigung für Variablen| Codevervollständigung für Systemfunktionen| Codevervollständigung für Benutzerfunktionen| Intelligenter Einzug | Codefaltung|
|--|--|--|--|--|--|--|--|--|
|PySpark (Python)|Ja|Ja|Ja|Ja|Ja|Ja|Ja|Ja|
|Spark (Scala)|Ja|Ja|Ja|Ja|-|-|-|Ja|
|SparkSQL|Ja|Ja|-|-|-|-|-|-|
|Spark.NET (C#)|Ja|-|-|-|-|-|-|-|

### <a name="format-text-cell-with-toolbar-buttons"></a>Textzelle mit Symbolleisten-Schaltflächen formatieren

Sie können die Formatschaltflächen auf der Textzellen-Symbolleiste verwenden, um allgemeine Markdown-Aktionen durchzuführen. Dies umfasst das Formatieren von Text als fett oder kursiv, das Einfügen von Codeausschnitten, das Einfügen einer unsortierten Liste, das Einfügen einer sortierten Liste sowie das Einfügen von Bildern aus URLs.

  ![Synapse-Text-Zelle-Symbolleiste](./media/apache-spark-development-using-notebooks/synapse-text-cell-toolbar.png)

### <a name="undo-cell-operations"></a>Rückgängigmachen von Zellenvorgängen
Klicken Sie auf die Schaltfläche **Rückgängig**, oder drücken Sie **STRG + Z**, um den letzten Zellenvorgang aufzuheben. Sie können jetzt die bis zu letzten 20 zurückliegenden Zellenaktionen rückgängig machen. 

   ![Synapse-Rückgängig-Zellen](./media/apache-spark-development-using-notebooks/synapse-undo-cells.png)

### <a name="move-a-cell"></a>Verschieben einer Zelle

Wählen Sie die Auslassungspunkte (...) aus, um ganz rechts auf das Menü mit zusätzlichen Zellenaktionen zuzugreifen. Wählen Sie dann **Zelle nach oben verschieben** oder **Zelle nach unten verschieben** aus, um die aktuelle Zelle zu verschieben. 

Sie können auch [Tastenkombinationen im Befehlsmodus](#shortcut-keys-under-command-mode) verwenden. Drücken Sie **STRG+ALT+↑**, um die aktuelle Zelle nach oben zu verschieben. Drücken Sie **STRG+ALT+↓**, um die aktuelle Zelle nach unten zu verschieben.

   ![eine-Zelle-verschieben](./media/apache-spark-development-using-notebooks/synapse-move-cells.png)

### <a name="delete-a-cell"></a>Löschen einer Zelle

Um eine Zelle zu löschen, wählen Sie die Auslassungspunkte (...) aus, um ganz rechts auf das Menü mit zusätzlichen Zellenaktionen zuzugreifen, und wählen Sie dann **Zelle löschen** aus. 

Sie können auch [Tastenkombinationen im Befehlsmodus](#shortcut-keys-under-command-mode) verwenden. Drücken Sie **D,D**, um die aktuelle Zelle zu löschen.
  
   ![eine-Zelle-löschen](./media/apache-spark-development-using-notebooks/synapse-delete-cell.png)

### <a name="collapse-a-cell-input"></a>Reduzieren einer Zelleneingabe
Klicken Sie am unteren Rand der aktuellen Zelle auf die Pfeilschaltfläche, um sie zu reduzieren. Um sie zu erweitern, klicken Sie auf die Pfeilschaltfläche, während die Zelle reduziert ist.

   ![Zelleneingabe-reduzieren](./media/apache-spark-development-using-notebooks/synapse-collapse-cell-input.gif)

### <a name="collapse-a-cell-output"></a>Reduzieren einer Zellenausgabe

Klicken Sie links oben in der aktuellen Zellenausgabe auf die Schaltfläche **Ausgabe reduzieren**, um sie zu reduzieren. Um sie zu erweitern, klicken Sie auf **Zellenausgabe anzeigen**, während die Zellenausgabe reduziert ist.

   ![Zellenausgabe-reduzieren](./media/apache-spark-development-using-notebooks/synapse-collapse-cell-output.gif)

## <a name="run-notebooks"></a>Ausführen von Notebooks

Sie können die Codezellen in Ihrem Notebook einzeln oder alle gleichzeitig ausführen. Status und Fortschritt jeder Zelle werden im Notebook dargestellt.

### <a name="run-a-cell"></a>Ausführen einer Zelle

Es gibt mehrere Methoden, um den Code in einer Zelle auszuführen.

1. Zeigen Sie mit dem Mauszeiger auf die Zelle, die Sie ausführen möchten, und wählen Sie die Schaltfläche **Zelle ausführen** aus, oder drücken Sie **STRG+EINGABE**.

   ![Zelle-1-ausführen](./media/apache-spark-development-using-notebooks/synapse-run-cell.png)


2. Um ganz rechts auf das Menü mit zusätzlichen Zellenaktionen zuzugreifen, wählen Sie die Auslassungspunkte ( **...** ) aus. Wählen Sie anschließend **Zelle ausführen** aus.

   ![Zelle-2-ausführen](./media/apache-spark-development-using-notebooks/synapse-run-cell-2.png)
   
3. Verwenden Sie [Tastenkombinationen im Befehlsmodus](#shortcut-keys-under-command-mode). Drücken Sie **UMSCHALT+EINGABE**, um die aktuelle Zelle auszuführen und die Zelle darunter auszuwählen. Drücken Sie **ALT+EINGABE**, um die aktuelle Zelle auszuführen und darunter eine neue Zelle einzufügen.


### <a name="run-all-cells"></a>Ausführen aller Zellen
Klicken Sie auf die Schaltfläche **Alle ausführen**, um alle Zellen im aktuellen Notebook nacheinander auszuführen.

   ![alle-Zellen-ausführen](./media/apache-spark-development-using-notebooks/synapse-run-all.png)

### <a name="run-all-cells-above-or-below"></a>Ausführen aller darüber- oder darunterliegenden Zellen

Um ganz rechts auf das Menü mit zusätzlichen Zellenaktionen zuzugreifen, wählen Sie die Auslassungspunkte ( **...** ) aus. Wählen Sie dann **Zellen oberhalb ausführen** aus, um alle Zellen oberhalb der aktuellen nacheinander auszuführen. Wählen Sie **Zellen unterhalb ausführen** aus, um alle Zellen unterhalb der aktuellen nacheinander auszuführen.

   ![Zellen-oberhalb-oder-unterhalb-ausführen](./media/apache-spark-development-using-notebooks/synapse-run-cells-above-or-below.png)


### <a name="cell-status-indicator"></a>Zellenstatusindikator

Unterhalb der Zelle wird ein schrittweiser Zellenausführungsstatus angezeigt, damit Sie den aktuellen Fortschritt verfolgen können. Nachdem die Ausführung der Zelle abgeschlossen wurde, wird eine Ausführungszusammenfassung mit Gesamtdauer und Endzeit angezeigt, die zur späteren Bezugnahme dort auch aufbewahrt wird.

![Zellenstatus](./media/apache-spark-development-using-notebooks/synapse-cell-status.png)

### <a name="spark-progress-indicator"></a>Spark-Statusanzeige

Ein Azure Synapse Studio-Notebook ist vollständig Spark-basiert. Codezellen werden remote im Spark-Pool ausgeführt. Eine Spark-Auftragsstatusanzeige wird mit einem Statusbalken in Echtzeit angezeigt, um Ihnen den Status der Auftragsausführung zu verdeutlichen.


![Spark-Statusanzeige](./media/apache-spark-development-using-notebooks/synapse-spark-progress-indicator.png)

### <a name="spark-session-config"></a>Spark-Sitzungskonfiguration

Sie können in **Sitzung konfigurieren** die Timeoutdauer sowie die Anzahl und Größe der Executors angeben, die für die aktuelle Spark-Sitzung gelten sollen. Sie müssen die Spark-Sitzung neu starten, damit die Konfigurationsänderungen wirksam werden. Alle zwischengespeicherten Notebook-Variablen werden gelöscht.

![Sitzungsverwaltung](./media/apache-spark-development-using-notebooks/synapse-spark-session-mgmt.png)


## <a name="bring-data-to-a-notebook"></a>Einfügen von Daten in ein Notebook

Sie können Daten aus Azure Blob Storage, Azure Data Lake Store Gen 2 und dem SQL-Pool laden, wie in den folgenden Codebeispielen gezeigt.

### <a name="read-a-csv-from-azure-data-lake-store-gen2-as-a-spark-dataframe"></a>Lesen einer CSV-Datei aus Azure Data Lake Store Gen2 als Spark-Datenrahmen

```python
from pyspark.sql import SparkSession
from pyspark.sql.types import *
account_name = "Your account name"
container_name = "Your container name"
relative_path = "Your path"
adls_path = 'abfss://%s@%s.dfs.core.windows.net/%s' % (blob_container_name, blob_account_name,  blob_relative_path)

spark.conf.set("fs.azure.account.auth.type.%s.dfs.core.windows.net" %account_name, "SharedKey")
spark.conf.set("fs.azure.account.key.%s.dfs.core.windows.net" %account_name ,"Your ADLSg2 Primary Key")

df1 = spark.read.option('header', 'true') \
                .option('delimiter', ',') \
                .csv(adls_path + '/Testfile.csv')

```

#### <a name="read-a-csv-from-azure-blob-storage-as-a-spark-dataframe"></a>Lesen einer CSV-Datei aus Azure Blob Storage als Spark-Datenrahmen

```python

from pyspark.sql import SparkSession
from pyspark.sql.types import *

blob_account_name = "Your blob account name"
blob_container_name = "Your blob container name"
blob_relative_path = "Your blob relative path"
blob_sas_token = "Your blob sas token"

wasbs_path = 'wasbs://%s@%s.blob.core.windows.net/%s' % (blob_container_name, blob_account_name, blob_relative_path)
spark.conf.set('fs.azure.sas.%s.%s.blob.core.windows.net' % (blob_container_name, blob_account_name), blob_sas_token)

df = spark.read.option("header", "true") \
            .option("delimiter","|") \
            .schema(schema) \
            .csv(wasbs_path)

```

### <a name="read-data-from-the-primary-storage-account"></a>Lesen von Daten aus einem primären Speicherkonto

Sie können auf Daten im primären Speicherkonto direkt zugreifen. Es besteht keine Notwendigkeit, die geheimen Schlüssel bereitzustellen. Klicken Sie im Daten-Explorer mit der rechten Maustaste auf eine Datei, und wählen Sie **Neues Notebook** aus, um ein neues Notebook mit einem automatisch generierten Datenextraktor anzuzeigen.

![Daten-in-Zelle](./media/apache-spark-development-using-notebooks/synapse-data-to-cell.png)

## <a name="visualize-data-in-a-notebook"></a>Visualisieren von Daten in einem Notebook

### <a name="display"></a>Display()

Eine tabellarische Ergebnisansicht wird zusammen mit der Möglichkeit zum Erstellen eines Balkendiagramms, eines Liniendiagramms, eines Kreisdiagramms, eines Punktdiagramms und eines Flächendiagramms bereitgestellt. Sie können Ihre Daten visualisieren, ohne Code schreiben zu müssen. Die Diagramme lassen sich in den **Diagrammoptionen** anpassen. 

Die Ausgabe der **%%sql**-Magic-Befehle wird standardmäßig in der gerenderten Tabellenansicht angezeigt. Sie können **display(`<DataFrame name>`)** für Spark-Datenrahmen oder eine RDD-Funktion (resiliente verteilte Datasets) aufrufen, um die gerenderte Tabellenansicht zu erzeugen.

   ![integrierte-Diagramme](./media/apache-spark-development-using-notebooks/synapse-builtin-charts.png)

### <a name="displayhtml"></a>DisplayHTML()

Sie können HTML-oder interaktive Bibliotheken wie **bokeh** mithilfe von **displayHTML()** rendern.

Das folgende Bild ist ein Beispiel für das Zeichnen von Glyphen auf einer Karte mithilfe von **bokeh**.

   ![bokeh-Beispiel](./media/apache-spark-development-using-notebooks/synapse-bokeh-image.png)
   

Führen Sie den folgenden Beispielcode aus, um das obige Bild zu zeichnen.

```python
from bokeh.plotting import figure, output_file
from bokeh.tile_providers import get_provider, Vendors
from bokeh.embed import file_html
from bokeh.resources import CDN
from bokeh.models import ColumnDataSource

tile_provider = get_provider(Vendors.CARTODBPOSITRON)

# range bounds supplied in web mercator coordinates
p = figure(x_range=(-9000000,-8000000), y_range=(4000000,5000000),
           x_axis_type="mercator", y_axis_type="mercator")
p.add_tile(tile_provider)

# plot datapoints on the map
source = ColumnDataSource(
    data=dict(x=[ -8800000, -8500000 , -8800000],
              y=[4200000, 4500000, 4900000])
)

p.circle(x="x", y="y", size=15, fill_color="blue", fill_alpha=0.8, source=source)

# create an html document that embeds the Bokeh plot
html = file_html(p, CDN, "my plot1")

# display this html
displayHTML(html)

```

## <a name="save-notebooks"></a>Speichern von Notebooks

Sie können ein einzelnes Notebook oder alle Notebooks in Ihrem Arbeitsbereich speichern.

1. Um an einem einzelnen Notebook vorgenommene Änderungen zu speichern, wählen Sie auf der Notebook-Befehlsleiste die Schaltfläche**Veröffentlichen** aus.

   ![Notebook-veröffentlichen](./media/apache-spark-development-using-notebooks/synapse-publish-notebook.png)

2. Um alle Notebooks in Ihrem Arbeitsbereich zu speichern, wählen Sie die Schaltfläche **Alle veröffentlichen** auf der Befehlsleiste des Arbeitsbereichs aus. 

   ![alle-veröffentlichen](./media/apache-spark-development-using-notebooks/synapse-publish-all.png)

In den Notebook-Eigenschaften können Sie konfigurieren, ob die Zellenausgabe beim Speichern eingeschlossen werden soll.

   ![Notebook-Eigenschaften](./media/apache-spark-development-using-notebooks/synapse-notebook-properties.png)

## <a name="magic-commands"></a>Magic-Befehle
Sie können Ihre vertrauten Jupyter-Magic-Befehle in Azure Synapse Studio-Notebooks verwenden. Überprüfen Sie die nachstehende Liste mit den aktuellen verfügbaren Magic-Befehlen. Teilen Sie uns Ihre Anwendungsfälle auf GitHub mit, damit wir weitere Magic-Befehle erstellen können, um Ihre Anforderungen zu erfüllen.

Verfügbare Zeilen-Magics: [%lsmagic](https://ipython.readthedocs.io/en/stable/interactive/magics.html#magic-lsmagic), [%time](https://ipython.readthedocs.io/en/stable/interactive/magics.html#magic-time), [%timeit](https://ipython.readthedocs.io/en/stable/interactive/magics.html#magic-timeit)

Verfügbare Zellen-Magics: [%%time](https://ipython.readthedocs.io/en/stable/interactive/magics.html#magic-time), [%%timeit](https://ipython.readthedocs.io/en/stable/interactive/magics.html#magic-timeit), [%%capture](https://ipython.readthedocs.io/en/stable/interactive/magics.html#cellmagic-capture), [%%writefile](https://ipython.readthedocs.io/en/stable/interactive/magics.html#cellmagic-writefile), [%%sql](#use-multiple-languages), [%%pyspark](#use-multiple-languages), [%%spark](#use-multiple-languages), [%%csharp](#use-multiple-languages)

## <a name="shortcut-keys"></a>Tastenkombinationen

Ähnlich wie Jupyter-Notebooks verfügen Azure Synapse Studio-Notebooks über eine modale Benutzeroberfläche. Mit der Tastatur werden unterschiedliche Aktionen ausgeführt, je nachdem, in welchem Modus sich die Notebook-Zelle befindet. Synapse Studio-Notebooks unterstützen die folgenden zwei Modi für eine bestimmte Codezelle: Befehlsmodus und Bearbeitungsmodus.

1. Eine Zelle befindet sich im Befehlsmodus, wenn Sie kein Textcursor zur Eingabe auffordert. Wenn sich eine Zelle im Befehlsmodus befindet, können Sie das Notebook als Ganzes bearbeiten, aber keine Eingaben in einzelne Zellen vornehmen. Sie wechseln in den Befehlsmodus, indem Sie `ESC` drücken oder mit der Maus außerhalb des Editor-Bereichs einer Zelle klicken.

   ![Befehlsmodus](./media/apache-spark-development-using-notebooks/synapse-command-mode2.png)

2. Der Bearbeitungsmodus wird durch einen Textcursor angezeigt, der Sie zur Eingabe im Editor-Bereich auffordert. Wenn sich eine Zelle im Bearbeitungsmodus befindet, können Sie Eingaben in die Zelle vornehmen. Sie wechseln in den Bearbeitungsmodus, indem Sie `Enter` drücken oder mit der Maus auf den Editor-Bereich einer Zelle klicken.
   
   ![Bearbeitungsmodus](./media/apache-spark-development-using-notebooks/synapse-edit-mode2.png)

### <a name="shortcut-keys-under-command-mode"></a>Tastenkombinationen im Befehlsmodus

Mithilfe der folgenden Tastenkombinationen können Sie in Azure Synapse-Notebooks leichter navigieren und Code ausführen.

| Aktion |Tastenkombinationen für Synapse Studio-Notebooks  |
|--|--|
|Aktuelle Zelle ausführen und die darunter auswählen | UMSCHALT+EINGABE |
|Aktuelle Zelle ausführen und darunter einfügen | ALT+EINGABE |
|Zelle darüber auswählen| Nach oben |
|Zelle darunter auswählen| Nach unten |
|Zelle oberhalb einfügen| Ein |
|Zelle unterhalb einfügen| B |
|Ausgewählte Zellen nach oben erweitern| UMSCHALT+NACH-OBEN |
|Ausgewählte Zellen nach unten erweitern| UMSCHALT+NACH-UNTEN|
|Zelle nach oben verschieben| STRG+ALT+↑ |
|Zelle nach unten verschieben| STRG+ALT+↓ |
|Ausgewählte Zellen löschen| D, D |
|In den Bearbeitungsmodus wechseln| EINGABETASTE |

### <a name="shortcut-keys-under-edit-mode"></a>Tastenkombinationen im Bearbeitungsmodus

Mithilfe der folgenden Tastenkombinationen können Sie in Azure Synapse-Notebooks leichter navigieren und Code ausführen, während sie sich im Bearbeitungsmodus befinden.

| Aktion |Tastenkombinationen für Synapse Studio-Notebooks  |
|--|--|
|Cursor nach oben verschieben | Nach oben |
|Cursor nach unten verschieben|Nach unten|
|Rückgängig|STRG+Z|
|Wiederholen|STRG+Y|
|Auskommentieren/Auskommentierung aufheben|STRG+/|
|Wort davor löschen|STRG+RÜCKTASTE|
|Wort danach löschen|STRG+DELETE|
|Zum Anfang der Zelle wechseln|STRG+POS1|
|Zum Ende der Zelle wechseln |STRG+ENDE|
|Ein Wort nach links wechseln|STRG+NACH-LINKS|
|Ein Wort nach rechts wechseln|STRG+NACH-RECHTS|
|Alle auswählen|STRG+A|
|Einziehen| STRG+]|
|Einzug entfernen|STRG+[|
|In den Befehlsmodus wechseln| Esc |

## <a name="next-steps"></a>Nächste Schritte

- [Dokumentation zu .NET für Apache Spark](/dotnet/spark?toc=/azure/synapse-analytics/toc.json&bc=/azure/synapse-analytics/breadcrumb/toc.json)
- [Azure Synapse Analytics](https://docs.microsoft.com/azure/synapse-analytics)
