---
title: 'Passaggio 2: Abilitare e configurare le configurazioni di pacchetti | Microsoft Docs'
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 005218ab-8dd5-48e9-a185-6bc60cd43a7a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7706c124160f1f08f39279956d7685085859badd
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "71283134"
---
# <a name="lesson-5-2-enable-and-configure-package-configurations"></a>Lezione 5-2: Abilitare e configurare le configurazioni di pacchetti

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



In questa attività si converte il progetto nel modello di distribuzione del pacchetto e si abilitano le configurazioni di pacchetto usando la Configurazione guidata pacchetto. Questa procedura guidata consente di generare un file di configurazione XML contenente le impostazioni di configurazione per la proprietà **Directory** del contenitore Ciclo Foreach. Il valore della proprietà **Directory** è specificato da una variabile a livello di pacchetto che è possibile aggiornare in fase di esecuzione. È anche possibile popolare una nuova cartella di dati di esempio da usare per i test.  
  
## <a name="create-a-package-level-variable-mapped-to-the-directory-property"></a>Creare una variabile a livello di pacchetto associata alla proprietà Directory  
  
1.  Selezionare lo sfondo della scheda **Flusso di controllo** in Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)]. Con questa selezione viene impostato l'ambito del pacchetto per la variabile che verrà creata.  
  
2.  Scegliere [!INCLUDE[ssIS](../includes/ssis-md.md)] Variabili **dal menu**.  
  
3.  Nella finestra **Variabili** selezionare l'icona **Aggiungi variabile**.  
  
4.  Nella casella **Nome** immettere **varFolderName**.  
  
    > [!IMPORTANT]  
    > Per i nomi delle variabili viene fatta distinzione tra maiuscole e minuscole.  
  
5.  Verificare che nella casella **Ambito** sia visualizzato il nome del pacchetto, **Lesson 5**.  
  
6.  Impostare su **String** il valore della casella `varFolderName` Tipo di dati **della variabile**.  
  
7.  Tornare alla scheda **Flusso di controllo** e fare doppio clic sul contenitore **Foreach File in Folder** .  
  
8.  Nella pagina **Raccolta** di **Editor ciclo Foreach** selezionare **Espressioni** e quindi il pulsante con i puntini di sospensione **(...)** .  
  
9. In **Editor espressioni di proprietà** fare clic nell'elenco **Proprietà** e selezionare **Directory**.  
  
10. Nella casella **Espressione** selezionare il pulsante con i puntini di sospensione **(...)** .  
  
11. In **Generatore di espressioni** espandere la cartella di **variabili e parametri** e trascinare la variabile **User::varFolderName** nella casella **Espressione**.  
  
12. Selezionare **OK** per uscire da **Generatore di espressioni**.  
  
13. Selezionare **OK** per uscire da **Editor espressioni di proprietà**.  
  
14. Selezionare **OK** per uscire da **Editor ciclo Foreach**.  
  
## <a name="enable-package-configurations"></a>Abilita configurazioni pacchetto  
  
1.  Selezionare **Converti nel modello di distribuzione del pacchetto** dal menu **Progetto**.  
  
2.  Selezionare **OK** nel messaggio di avviso e, completata la conversione, selezionare **OK** nella finestra di dialogo **Converti nel modello di distribuzione del pacchetto**.  
  
3.  Selezionare lo sfondo della scheda **Flusso di controllo** in Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)].  
  
4.  Selezionare **Configurazioni di pacchetto** dal menu **SSIS**.  
  
5.  Nella finestra di dialogo **Libreria configurazioni pacchetto** selezionare **Abilita configurazioni pacchetto** e quindi selezionare **Aggiungi**.  
  
6.  Nella pagina iniziale della **Configurazione guidata pacchetto** selezionare **Avanti**.  
  
7.  Nella pagina **Selezione tipo di configurazione** verificare che l'opzione **Tipo configurazione** sia impostata su **File di configurazione XML**.  
  
8.  Nella pagina **Selezione tipo di configurazione** selezionare **Sfoglia**.  
  
9. La finestra di dialogo **Selezionare il percorso del file di configurazione** si apre visualizzando la cartella del progetto.  
  
10. Nella finestra di dialogo **Selezionare il percorso del file di configurazione** digitare **SSISTutorial** nel campo **Nome file** e quindi selezionare **Salva**.  
  
11. Nella pagina **Selezione tipo di configurazione** selezionare **Avanti**.
  
12. Nel riquadro **Oggetti** della pagina **Selezione proprietà da esportare** espandere **Variabili**, **varFolderName**, **Properties** e quindi selezionare **Value**.  
  
13. Nella pagina **Selezione proprietà da esportare** selezionare **Avanti**.  
  
14. Nella pagina **Completamento procedura guidata** immettere un nome per la configurazione, ad esempio **SSIS Tutorial Directory configuration**. Il nome della configurazione viene visualizzato nella finestra di dialogo **Libreria configurazioni pacchetto**.  
  
15. Selezionare **Fine**.  
  
16. Selezionare **Chiudi**.  
  
17. La procedura guidata crea un file di configurazione, denominato **SSISTutorial.dtsConfig**, che contiene le impostazioni di configurazione per il **valore** della variabile che a sua volta imposta la proprietà **Directory** dell'enumeratore.  
  
    > [!NOTE]  
    > Un file di configurazione in genere contiene informazioni complesse sulle proprietà del pacchetto, ma in questa esercitazione le uniche informazioni di configurazione sono le seguenti:

    ```
    <Configuration 
        ConfiguredType="Property"  
        Path="\Package.Variables[User::varFolderName].Properties[Value]" 
        ValueType="String">  
      <ConfiguredValue></ConfiguredValue>  
    </Configuration>
    ```
  
## <a name="create-and-populate-a-new-sample-data-folder"></a>Creare e popolare una nuova cartella di dati di esempio  
  
1.  In Esplora risorse di Windows creare al livello di radice dell'unità disco, ad esempio **C:\\** , una cartella denominata **New Sample Data**.  
  
2.  Individuare i file di esempio nel computer e copiare tre dei file nella cartella.  
  
3.  Incollare i file copiati nella cartella **New Sample Data** .  
  
## <a name="go-to-next-task"></a>Esecuzione del passaggio successivo  
[Passaggio 3: Modificare il valore di configurazione della proprietà Directory](../integration-services/lesson-5-3-modifying-the-directory-property-configuration-value.md)  
  
