---
title: Estrarre dati delle modifiche tramite l'origine CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 604fbafb-15fa-4d11-8487-77d7b626eed8
author: janinezhang
ms.author: janinez
ms.openlocfilehash: e0e4fe1f3c7920f034103a4fca6df3460ff4aea7
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84915795"
---
# <a name="extract-change-data-using-the-cdc-source"></a>Estrarre dati delle modifiche tramite l'origine CDC
  Per aggiungere e configurare un'origine CDC, è necessario che il pacchetto includa già almeno un'attività Flusso di dati e un'attività di controllo CDC.  
  
 Per altre informazioni sull'attività di controllo CDC, vedere [Attività di controllo CDC](../control-flow/cdc-control-task.md).  
  
 Per altre informazioni sull'origine CDC, vedere [Origine CDC](cdc-source.md).  
  
### <a name="to-extract-change-data-using-a-cdc-source"></a>Per estrarre dati delle modifiche tramite un'origine CDC  
  
1.  In [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]aprire il progetto di [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di dati** e quindi, dalla **casella degli strumenti**, trascinare l'origine CDC sull'area di progettazione.  
  
4.  Fare doppio clic sull'origine CDC.  
  
5.  Nella pagina **Gestione connessione** della finestra di dialogo **Editor origine CDC** selezionare nell'elenco una gestione connessione ADO.NET esistente oppure fare clic su **Nuova** per creare una nuova connessione. La connessione deve essere stabilita a un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contenente le tabelle delle modifiche da leggere.  
  
6.  Selezionare la **tabella CDC** in cui si vuole elaborare le modifiche.  
  
7.  Selezionare o digitare il nome dell' **istanza di acquisizione CDC** con la tabella CDC da leggere.  
  
     Una tabella di origine acquisita può contenere una o due istanze acquisite per gestire la transizione senza problemi della definizione di tabella mediante modifiche dello schema. Se per la tabella di origine in corso di acquisizione sono definite più istanze di acquisizione, selezionare l'istanza di acquisizione che si desidera utilizzare a questo punto. Nome dell'istanza di acquisizione predefinita per una tabella [schema]. [Table] è \<schema> _ \<table> , ma i nomi delle istanze di acquisizione effettivi in uso possono essere diversi. La tabella effettiva da cui viene letta è la tabella CDC **CDC. \<capture-instance> _CT**.  
  
8.  Selezionare la modalità di elaborazione più adatta per le esigenze di elaborazione correnti. Di seguito sono elencate le opzioni possibili:  
  
    -   **All**: restituisce le modifiche nell'intervallo CDC corrente senza i valori **Before Update** .  
  
    -   **All with old values**: restituisce le modifiche nell'intervallo di elaborazione CDC corrente inclusi i valori precedenti (**Before Update**). Ogni operazione di aggiornamento prevede due righe: una con i valori prima dell'aggiornamento e una con i valori dopo l'aggiornamento.  
  
    -   **Net**: restituisce una sola riga delle modifiche per ogni riga di origine modificata nell'intervallo di elaborazione CDC corrente. Se una riga di origine è stata aggiornata più volte, viene restituita la modifica combinata (ad esempio, inserimento+aggiornamento viene prodotto come un singolo aggiornamento e aggiornamento+eliminazione viene prodotto come una singola eliminazione). Quando si utilizza la modalità di elaborazione delle modifiche Net, è possibile suddividere le modifiche negli output Delete, Insert e Update e gestirli in parallelo, perché la singola riga di origine viene visualizzata in più output.  
  
    -   **Net with update mask**: questa modalità è simile alla modalità NET standard, ma aggiunge anche colonne booleane con il modello di nome **_ _ $ \<column-name> \_ _Changed** che indica le colonne modificate nella riga delle modifiche corrente.  
  
    -   **Net with merge**: questa modalità è simile alla modalità Net standard, ma con le operazioni Insert e Update unite in una singola operazione Merge (UPSERT).  
  
9. Selezionare la variabile del pacchetto di stringhe SSIS che gestisce lo stato CDC per il contesto CDC corrente. Per altre informazioni sulla variabile di stato CDC, vedere [Definire una variabile di stato](define-a-state-variable.md).  
  
10. Selezionare la casella di controllo **Include reprocessing indicator column** per creare una speciale colonna di output denominata **__$reprocessing**. Questa colonna contiene un valore **true** quando l'intervallo di elaborazione CDC si sovrappone all'intervallo di elaborazione iniziale (l'intervallo di LSN che corrisponde al periodo di caricamento iniziale) o quando un intervallo di elaborazione CDC viene rielaborato a causa di un errore in un'esecuzione precedente. Questa colonna indicatore consente agli sviluppatori di SSIS di gestire gli errori in modo diverso durante la rielaborazione delle modifiche. Azioni quali l'eliminazione di una riga non esistente e l'inserimento non riuscito su una chiave duplicata, ad esempio, possono essere ignorate.  
  
     Per altre informazioni, vedere [Proprietà personalizzate dell'origine CDC](cdc-source-custom-properties.md).  
  
11. Per aggiornare il mapping tra colonne esterne e colonne di output, fare clic su **Colonne** e selezionare colonne diverse nell'elenco **Colonna esterna** .  
  
12. Facoltativamente, aggiornare i valori delle colonne di output eliminando i valori nell'elenco **Colonna di output** .  
  
13. Per configurare l'output degli errori, fare clic su **Output errori**.  
  
14. Facendo clic su **Anteprima** è possibile visualizzare fino a 200 righe di dati estratti dall'origine CDC.  
  
15. Fare clic su **OK**.  
  
## <a name="see-also"></a>Vedere anche  
 [Editor origine CDC &#40;pagina Gestione connessione&#41;](../cdc-source-editor-connection-manager-page.md)   
 [Editor origine CDC &#40;pagina Colonne&#41;](../cdc-source-editor-columns-page.md)   
 [Editor origine CDC &#40;pagina Output degli errori&#41;](../cdc-source-editor-error-output-page.md)  
  
  
