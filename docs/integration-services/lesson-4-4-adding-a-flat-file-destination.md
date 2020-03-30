---
title: 'Passaggio 4: Aggiungere una destinazione file flat | Microsoft Docs'
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: f4088de3-16d8-419c-96a1-a2cd005d0a5b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ae02b9188ecc9917d26532633e4d5a253d4f326b
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "71295950"
---
# <a name="lesson-4-4-add-a-flat-file-destination"></a>Lezione 4-4: Aggiungere una destinazione file flat

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



L'output degli errori della trasformazione Lookup Currency Key reindirizza tutte le righe di dati in cui la ricerca ha avuto esito negativo all'operazione di trasformazione Script. Per fornire altre informazioni sugli errori, la trasformazione Script esegue uno script che ottiene la descrizione di ciascun errore.  
  
In questa attività, tutte queste informazioni sulle righe con esito negativo vengono salvate in un file di testo delimitato per l'elaborazione in un momento successivo. Per salvare le righe con esito negativo, aggiungere e configurare una gestione connessione file flat per il file di testo che contiene i dati degli errori e una destinazione file flat. Impostando le proprietà della gestione connessione file flat utilizzata dalla destinazione file flat è possibile specificare la modalità con cui la destinazione file flat deve formattare e scrivere il file di testo. Per altre informazioni, vedere [Gestione connessione file flat](../integration-services/connection-manager/flat-file-connection-manager.md) e [Destinazione file flat](../integration-services/data-flow/flat-file-destination.md).  
  
## <a name="add-and-configure-a-flat-file-destination"></a>Aggiungere e configurare una destinazione file flat  
  
1.  Selezionare la scheda **Flusso di dati**.  
  
2.  Nella **Casella degli strumenti SSIS**espandere **Other Destinations** (Altre destinazioni) e trascinare **Destinazione file flat** sull'area di progettazione del flusso di dati. Posizionare la **Destinazione file flat** direttamente sotto la trasformazione **Get Error Description** (Ottieni descrizione errore).  
  
3.  Selezionare la trasformazione **Get Error Description** (Ottieni descrizione errore) e quindi trascinare la freccia blu sulla nuova **Destinazione file flat**.  
  
4.  Nell'area di progettazione **Flusso di dati** selezionare il nome **Destinazione file flat** nella nuova trasformazione **Destinazione file flat** appena aggiunta e impostare tale nome su **Righe con errori**.  
  
5.  Fare clic con il pulsante destro del mouse sulla trasformazione **Righe con errori** , selezionare **Modifica**e quindi in **Editor destinazione file flat** selezionare **Nuovo**.  
  
6.  Nella finestra di dialogo **Formato file flat** verificare che sia stato selezionato **Delimitato** e quindi selezionare **OK**.  
  
7.  In **Editor gestione connessione file flat**immettere **Error Data** nella casella *Nome gestione connessione*.  
  
8.  Nella finestra di dialogo **Editor gestione connessione file flat** selezionare **Sfoglia**e individuare la cartella in cui archiviare il file.  
  
9. Nella finestra di dialogo **Apri** in **Nome file** immettere *ErrorOutput.txt* e quindi selezionare **Apri**.  
  
10. Nella finestra di dialogo **Editor gestione connessione file flat**, verificare che nella casella **Impostazioni locali** sia presente **Inglese (Stati Uniti)** e che nella **Tabella codici** sia presente **1252 (ANSI -Latino I)** .  
  
11. Nel riquadro delle opzioni selezionare **Colonne**.  
  
    Oltre alle colonne dal file di dati di origine, sono presenti tre nuove colonne: ErrorCode, ErrorColumn ed ErrorDescription. Queste colonne rappresentano l'output degli errori della trasformazione Lookup Currency Key e dello script nella trasformazione Get Error Description e possono essere utilizzate per la risoluzione dei problemi relativi alla riga con esito negativo.  
  
12. Selezionare **OK**.  
  
13. In **Editor destinazione file flat**deselezionare la casella di controllo **Sovrascrivi dati nel file** .  
  
    La deselezione di questa casella di controllo mantiene gli errori per più esecuzioni del pacchetto mediante l'aggiunta dell'output degli errori di ogni nuova esecuzione.
  
14. In **Editor destinazione file flat** selezionare **Mapping** per verificare che tutte le colonne siano corrette. Facoltativamente è possibile rinominare le colonne nella destinazione.  
  
15. Selezionare **OK**.  
  
## <a name="go-to-next-task"></a>Esecuzione del passaggio successivo
[Passaggio 5: Testare il pacchetto creato nella lezione 4 dell'esercitazione](../integration-services/lesson-4-5-testing-the-lesson-4-tutorial-package.md)  
  
  
  
