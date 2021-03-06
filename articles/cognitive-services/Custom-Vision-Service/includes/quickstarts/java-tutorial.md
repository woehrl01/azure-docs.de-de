---
author: areddish
ms.author: areddish
ms.service: cognitive-services
ms.date: 04/14/2020
ms.openlocfilehash: efbfed5198620fc07b10354a5b74f6ddaf2cd4ab
ms.sourcegitcommit: 34a6fa5fc66b1cfdfbf8178ef5cdb151c97c721c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/28/2020
ms.locfileid: "82135103"
---
Dieser Artikel enthält Informationen zu den ersten Schritten mit dem Custom Vision Java SDK und unterstützt Sie beim Erstellen eines Bildklassifizierungsmodells. Nach der Erstellung können Sie Tags hinzufügen, Bilder hochladen, das Projekt trainieren, die Standardendpunkt-URL für Vorhersagen des Projekts abrufen und den Endpunkt für die programmgesteuerte Überprüfung eines Bilds verwenden. Verwenden Sie dieses Beispiel als Vorlage für die Erstellung Ihrer eigenen Java-Anwendung. Falls Sie den Prozess zur Erstellung und Verwendung eines Klassifizierungsmodells _ohne_ Code durchlaufen möchten, sehen Sie sich stattdessen die [browserbasierte Anleitung](../../getting-started-build-a-classifier.md) an.

## <a name="prerequisites"></a>Voraussetzungen

- Eine Java-IDE Ihrer Wahl.
- [JDK 7 oder 8](https://aka.ms/azure-jdks) muss installiert sein.
- [Maven](https://maven.apache.org/) muss installiert sein.
- [!INCLUDE [create-resources](../../includes/create-resources.md)]

## <a name="get-the-custom-vision-sdk-and-sample-code"></a>Abrufen von Custom Vision SDK und Beispielcode

Wenn Sie eine Java-App schreiben möchten, die Custom Vision verwendet, benötigen Sie die Maven-Pakete für Custom Vision. Diese Pakete sind in dem Beispielprojekt enthalten, das Sie herunterladen. Sie können hier aber auch einzeln auf sie zugreifen:

Sie finden das Custom Vision SDK im zentralen Maven-Repository:

- [Trainings-SDK](https://mvnrepository.com/artifact/com.microsoft.azure.cognitiveservices/azure-cognitiveservices-customvision-training)
- [Vorhersage-SDK](https://mvnrepository.com/artifact/com.microsoft.azure.cognitiveservices/azure-cognitiveservices-customvision-prediction)

Klonen Sie das Projekt [Cognitive Services Java SDK Samples](https://github.com/Azure-Samples/cognitive-services-java-sdk-samples/tree/master) (Cognitive Services SDK-Beispiele für Java), oder laden Sie es herunter. Navigieren Sie zum Ordner **Vision/CustomVision/** .

Dieses Java-Projekt erstellt ein neues Custom Vision-Bildklassifizierungsprojekt namens __Sample Java Project__, auf das über die [Custom Vision-Website](https://customvision.ai/) zugegriffen werden kann. Anschließend werden Bilder zum Trainieren und Testen einer Klassifizierung hochgeladen. In diesem Projekt soll die Klassifizierung bestimmen, ob es sich bei einem Baum um eine __Hemlocktanne__ oder um eine __japanische Zierkirsche__ handelt.

[!INCLUDE [get-keys](../../includes/get-keys.md)]

Das Programm ist so konfiguriert, dass auf Ihre zentralen Daten als Umgebungsvariablen verwiesen wird. Navigieren Sie zum Ordner **Vision/CustomVision**, und geben Sie die folgenden PowerShell-Befehle ein, um die Umgebungsvariablen festzulegen. 

> [!NOTE]
> Wenn Sie ein anderes Betriebssystem als Windows verwenden, hilft Ihnen die Anleitung unter [Konfigurieren von Umgebungsvariablen](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account?tabs=multiservice%2Cwindows#configure-an-environment-variable-for-authentication) weiter.

```powershell
$env:AZURE_CUSTOMVISION_TRAINING_API_KEY ="<your training api key>"
$env:AZURE_CUSTOMVISION_PREDICTION_API_KEY ="<your prediction api key>"
```

## <a name="understand-the-code"></a>Grundlegendes zum Code

Laden Sie das Projekt `Vision/CustomVision` in Ihre Java-IDE, und öffnen Sie die Datei _CustomVisionSamples.java_. Suchen Sie nach der Methode **runSample**, und kommentieren Sie den Methodenaufruf **ObjectDetection_Sample** aus. (Das dadurch ausgeführte Objekterkennungsszenario wird in dieser Anleitung nicht behandelt.) Die Methode **ImageClassification_Sample** implementiert die Hauptfunktionen dieses Beispiels. Navigieren Sie zur entsprechenden Definition, und sehen Sie sich den Code an.

### <a name="create-a-custom-vision-service-project"></a>Erstellen eines Custom Vision Service-Projekts

Der erste Teil des Codes erstellt ein Bildklassifizierungsprojekt. Das erstellte Projekt wird auf der [Custom Vision-Website](https://customvision.ai/) angezeigt, die Sie zuvor besucht haben. Informationen zur Angabe weiterer Optionen bei der Erstellung Ihres Projekts finden Sie im Artikel zu Überladungen der Methode [CreateProject](https://docs.microsoft.com/java/api/com.microsoft.azure.cognitiveservices.vision.customvision.training.trainings.createproject?view=azure-java-stable#com_microsoft_azure_cognitiveservices_vision_customvision_training_Trainings_createProject_String_CreateProjectOptionalParameter_). Informationen zur Projekterstellung finden Sie unter [Schnellstart: Erstellen einer Klassifizierung mit Custom Vision](../../getting-started-build-a-classifier.md).

[!code-java[](~/cognitive-services-java-sdk-samples/Vision/CustomVision/src/main/java/com/microsoft/azure/cognitiveservices/vision/customvision/samples/CustomVisionSamples.java?name=snippet_create)]

### <a name="create-tags-in-the-project"></a>Erstellen von Tags im Projekt

[!code-java[](~/cognitive-services-java-sdk-samples/Vision/CustomVision/src/main/java/com/microsoft/azure/cognitiveservices/vision/customvision/samples/CustomVisionSamples.java?name=snippet_tags)]

### <a name="upload-and-tag-images"></a>Hochladen und Kennzeichnen von Bildern

Die Beispielbilder befinden sich im Ordner **src/main/resources** des Projekts. Sie werden von dort aus gelesen und mit entsprechenden Tags in den Dienst hochgeladen.

[!code-java[](~/cognitive-services-java-sdk-samples/Vision/CustomVision/src/main/java/com/microsoft/azure/cognitiveservices/vision/customvision/samples/CustomVisionSamples.java?name=snippet_upload)]

Der vorherige Codeausschnitt verwendet zwei Hilfsfunktionen, die die Bilder als Ressourcenstreams abrufen und in den Dienst hochladen. (Sie können bis zu 64 Bilder in einem Batch hochladen.)

[!code-java[](~/cognitive-services-java-sdk-samples/Vision/CustomVision/src/main/java/com/microsoft/azure/cognitiveservices/vision/customvision/samples/CustomVisionSamples.java?name=snippet_helpers)]

### <a name="train-the-classifier-and-publish"></a>Trainieren der Klassifizierung und Veröffentlichen

Dieser Code erstellt die erste Iteration des Vorhersagemodells und veröffentlicht diese anschließend am Vorhersageendpunkt. Der Name der veröffentlichten Iteration kann zum Senden von Vorhersageanforderungen verwendet werden. Eine Iteration ist erst im Vorhersageendpunkt verfügbar, wenn sie veröffentlicht wurde.

[!code-java[](~/cognitive-services-java-sdk-samples/Vision/CustomVision/src/main/java/com/microsoft/azure/cognitiveservices/vision/customvision/samples/CustomVisionSamples.java?name=snippet_train)]

### <a name="use-the-prediction-endpoint"></a>Verwenden des Vorhersageendpunkts

Der Vorhersageendpunkt (hier dargestellt durch das Objekt `predictor`) ist die Referenz, die Sie verwenden, um ein Bild an das aktuelle Modell zu übermitteln und eine Klassifizierungsvorhersage zu erhalten. In diesem Beispiel wird `predictor` an anderer Stelle unter Verwendung der Vorhersageschlüssel-Umgebungsvariablen definiert.

[!code-java[](~/cognitive-services-java-sdk-samples/Vision/CustomVision/src/main/java/com/microsoft/azure/cognitiveservices/vision/customvision/samples/CustomVisionSamples.java?name=snippet_predict)]

## <a name="run-the-application"></a>Ausführen der Anwendung

Navigieren Sie zum Kompilieren und Ausführen der Lösung mit Maven in einer Eingabeaufforderung zum Projektverzeichnis (**Vision/CustomVision**), und führen Sie den run-Befehl aus:

```bash
mvn compile exec:java
```

Die Konsolenausgabe der Anwendung sollte in etwa wie der folgende Text aussehen:

```console
Creating project...
Adding images...
Adding image: hemlock_1.jpg
Adding image: hemlock_2.jpg
Adding image: hemlock_3.jpg
Adding image: hemlock_4.jpg
Adding image: hemlock_5.jpg
Adding image: hemlock_6.jpg
Adding image: hemlock_7.jpg
Adding image: hemlock_8.jpg
Adding image: hemlock_9.jpg
Adding image: hemlock_10.jpg
Adding image: japanese_cherry_1.jpg
Adding image: japanese_cherry_2.jpg
Adding image: japanese_cherry_3.jpg
Adding image: japanese_cherry_4.jpg
Adding image: japanese_cherry_5.jpg
Adding image: japanese_cherry_6.jpg
Adding image: japanese_cherry_7.jpg
Adding image: japanese_cherry_8.jpg
Adding image: japanese_cherry_9.jpg
Adding image: japanese_cherry_10.jpg
Training...
Training status: Training
Training status: Training
Training status: Completed
Done!
        Hemlock: 93.53%
        Japanese Cherry: 0.01%
```

Anhand der letzten Zeilen der Ausgabe können Sie überprüfen, ob die Testbildvorhersage korrekt ist.

[!INCLUDE [clean-ic-project](../../includes/clean-ic-project.md)]

## <a name="next-steps"></a>Nächste Schritte

Sie wissen nun, wie die einzelnen Schritte des Objekterkennungsprozesses im Code ausgeführt werden. In diesem Beispiel wird eine einzelne Trainingsiteration ausgeführt. Zur Verbesserung der Genauigkeit muss ein Modell jedoch häufig mehrmals trainiert und getestet werden.

> [!div class="nextstepaction"]
> [Testen und erneutes Trainieren eines Modells mit Custom Vision Service](../../test-your-model.md)
