---
title: Copiare e incollare dati (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.pastepreviewdb.f1
ms.assetid: 2f8d8b3d-810b-4c31-98f2-341015e13da8
author: minewiskan
ms.author: owend
ms.openlocfilehash: 30d7e6aafe613e5ca43307aa75540d8fb1cea3ec
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84526837"
---
# <a name="copy-and-paste-data-ssas-tabular"></a>Copiare e incollare dati (SSAS tabulare)
  È possibile copiare i dati delle tabelle da applicazioni esterne e incollarli in una tabella nuova o esistente in Progettazione modelli. I dati incollati dagli Appunti devono essere in formato HTML, come i dati copiati da Excel o Word. Progettazione modelli rileverà e applicherà automaticamente i tipi di dati ai dati incollati. È anche possibile modificare manualmente il tipo di dati o la formattazione di visualizzazione di una colonna.  
  
 A differenza delle tabelle con una connessione all'origine dati, nelle tabelle incollate non è disponibile una proprietà Nome connessione oppure Origine dati. I dati incollati sono persistenti nel file Model.bim. Quando il progetto o il file Model.bim viene salvato, anche i dati incollati vengono salvati.  
  
 Quando viene distribuito un modello, anche i dati incollati saranno distribuiti, indipendentemente dal fatto che il modello venga elaborato con la distribuzione.  
  
 Sezioni dell'argomento:  
  
-   [Prerequisiti](#bkmk_prerequisites)  
  
-   [Incollare i dati](#bkmk_paste_data)  
  
-   [Finestra di dialogo Anteprima Incolla](#bkmk_paste_preview)  
  
##  <a name="prerequisites"></a><a name="bkmk_prerequisites"></a> Prerequisiti  
 Quando si incollano dati si applicano alcune restrizioni:  
  
-   Nelle tabelle incollate non possono essere presenti più di 10.000 righe.  
  
-   Non è possibile partizionare le tabelle incollate.  
  
-   Le tabelle incollate non sono supportate nella modalità DirectQuery.  
  
-   Le opzioni **Accoda il contenuto degli Appunti** e **Incolla e sostituisci** sono disponibili solo quando si usa una tabella inizialmente creata incollando i dati dagli Appunti. Non è possibile usare **Accoda il contenuto degli Appunti** o **Incolla e sostituisci** per aggiungere dati in una tabella di dati importati da un altro tipo di origine dati.  
  
-   Quando si usa l'opzione **Accoda il contenuto degli Appunti** o **Incolla e sostituisci**, nei nuovi dati deve essere contenuto esattamente lo stesso numero di colonne dei dati originali. Preferibilmente, i dati delle colonne che si incollano o si accodano devono essere dello stesso tipo o compatibili con quelli della tabella di destinazione. In alcuni casi è possibile usare un tipo di dati diverso, tuttavia potrebbe venire visualizzato un errore di **tipo non corrispondente** .  
  
##  <a name="paste-data"></a><a name="bkmk_paste_data"></a> Incollare i dati  
  
#### <a name="to-paste-data-into-the-designer"></a>Per incollare dati nella finestra di progettazione  
  
-   In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]fare clic sul menu **Modifica** e quindi scegliere una delle opzioni seguenti:  
  
    -   Fare clic su **Incolla** per incollare il contenuto degli Appunti in una nuova tabella.  
  
    -   Fare clic su **Accoda il contenuto degli Appunti** per incollare il contenuto degli Appunti come righe aggiuntive nella tabella selezionata. Le nuove righe verranno aggiunte alla fine della tabella.  
  
    -   Fare clic su **Incolla e sostituisci** per sostituire la tabella selezionata con il contenuto degli Appunti. Tutti i nomi delle intestazioni di colonna esistenti rimarranno nella tabella e le relazioni vengono mantenute.  
  
##  <a name="paste-preview-dialog-box"></a><a name="bkmk_paste_preview"></a>Finestra di dialogo Anteprima Incolla  
 La finestra di dialogo **Anteprima Incolla** consente di visualizzare un'anteprima dei dati copiati nella finestra di progettazione e di assicurarsi che la copia dei dati sia eseguita correttamente. Per accedere a questa finestra di dialogo, copiare negli Appunti i dati basati su tabelle in formato HTML, quindi nella finestra di progettazione fare clic sul menu **Modifica** e scegliere **Incolla**, **Accoda il contenuto degli Appunti**o **Incolla e sostituisci**. Le opzioni **Accoda il contenuto degli Appunti** e **Incolla e sostituisci** sono disponibili solo quando si aggiungono o si sostituiscono dati in una tabella creata tramite un'operazione di copia e incolla dagli Appunti. Non è possibile usare **Accoda il contenuto degli Appunti** o **Incolla e sostituisci** per aggiungere dati in una tabella con dati importati.  
  
 Le opzioni per questa finestra di dialogo variano a seconda che i dati vengano incollati in una tabella completamente nuova o in una tabella esistente e quindi si sostituiscano i dati esistenti con i nuovi dati o che si aggiungano dati a una tabella esistente.  
  
### <a name="paste-to-new-table"></a>Incolla in nuova tabella  
 **Nome tabella**  
 Specificare il nome della tabella che verrà creata nella finestra di progettazione.  
  
 **Dati da incollare**  
 Consente di visualizzare un esempio del contenuto degli Appunti che verrà aggiunto alla tabella di destinazione.  
  
### <a name="paste-append"></a>Accoda il contenuto degli Appunti  
 **Dati esistenti nella tabella**  
 Consente di visualizzare un esempio di dati esistenti nella tabella in modo da verificare le colonne, i tipi di dati ecc.  
  
 **Dati da incollare**  
 Consente di visualizzare un esempio del contenuto degli Appunti. I dati esistenti saranno accodati da questi dati.  
  
### <a name="paste-replace"></a>Incolla e sostituisci  
 **Dati esistenti nella tabella**  
 Consente di visualizzare un esempio di dati esistenti nella tabella in modo da verificare le colonne, i tipi di dati ecc.  
  
 **Dati da incollare**  
 Consente di visualizzare un esempio del contenuto degli Appunti. I dati esistenti nella tabella di destinazione saranno eliminati e le nuove righe saranno inserite nella tabella.  
  
## <a name="see-also"></a>Vedere anche  
 [Importare dati &#40;SSAS tabulare&#41;](import-data-ssas-tabular.md)   
 [Origini dati supportate &#40;SSAS tabulare&#41;](tabular-models/data-sources-supported-ssas-tabular.md)   
 [Impostare il tipo di dati di una colonna &#40;SSAS tabulare&#41;](tabular-models/set-the-data-type-of-a-column-ssas-tabular.md)  
  
  
