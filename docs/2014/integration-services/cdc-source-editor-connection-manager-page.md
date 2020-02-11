---
title: Editor origine CDC (pagina Gestione connessione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdcsource.connection.f1
ms.assetid: 304e6717-e160-4a7b-a06f-32182449fef8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7e33946220b10f35596a6496637c8572f5b97403
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66061058"
---
# <a name="cdc-source-editor-connection-manager-page"></a>Editor origine CDC (pagina Gestione connessione)
  Usare la pagina **Gestione connessione** della finestra di dialogo **Editor origine CDC** per selezionare la gestione connessione ADO.NET per il database di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] da cui l'origine CDC legge le righe delle modifiche (database CDC). Dopo aver selezionato il database CDC è necessario selezionare una tabella acquisita nel database.  
  
 Per altre informazioni sull'origine CDC, vedere [Origine CDC](data-flow/cdc-source.md).  
  
## <a name="task-list"></a>Elenco attività  
 **Per aprire CDC Source Editor (pagina Gestione connessione)**  
  
1.  In [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], aprire il pacchetto [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] che contiene l'origine CDC.  
  
2.  Nella scheda **Flusso di dati** fare doppio clic sull'origine CDC.  
  
3.  Nell' **Editor origine CDC**fare clic su **Gestione connessione**.  
  
## <a name="options"></a>Opzioni  
 **Gestione connessione ADO.NET**  
 Selezionare una gestione connessione esistente nell'elenco o creare una nuova connessione facendo clic su **Nuova** . La connessione deve essere stabilita a un database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] abilitato per CDC e in cui si trova la tabella delle modifiche selezionata.  
  
 **Nuovo**  
 Fare clic su **Nuovo**. Verrà visualizzata la finestra di dialogo **Editor della gestione connessione ADO.NET** in cui è possibile creare una nuova gestione connessione  
  
 **Tabella CDC**  
 Selezionare la tabella di origine CDC contenente le modifiche acquisite che si desidera leggere e inviare ai componenti SSIS a valle per l'elaborazione.  
  
 **Istanza di acquisizione**  
 Selezionare o digitare il nome dell'istanza di acquisizione CDC con la tabella CDC da leggere.  
  
 Una tabella di origine acquisita può contenere una o due istanze acquisite per gestire la transizione senza problemi della definizione di tabella mediante modifiche dello schema. Se per la tabella di origine in corso di acquisizione sono definite più istanze di acquisizione, selezionare l'istanza di acquisizione che si desidera utilizzare a questo punto. Il nome dell'istanza di acquisizione predefinito per una tabella [schema].[tabella] è \<schema_\<tabella, ma i nomi delle istanze di acquisizione effettivi in uso possono essere diversi. La tabella effettiva da cui viene eseguita la lettura è la tabella CDC **cdc .\<istanza-acquisizione>_CT**.  
  
 **Modalità di elaborazione CDC**  
 Selezionare la modalità di elaborazione più adatta per le esigenze di elaborazione correnti. Di seguito sono elencate le opzioni possibili:  
  
-   **All**: restituisce le modifiche nell'intervallo CDC corrente senza i valori **Before Update** .  
  
-   **All with old values**: restituisce le modifiche nell'intervallo di elaborazione CDC corrente inclusi i valori precedenti (**Before Update**). Ogni operazione di aggiornamento prevede due righe: una con i valori prima dell'aggiornamento e una con i valori dopo l'aggiornamento.  
  
-   **Net**: restituisce una sola riga delle modifiche per ogni riga di origine modificata nell'intervallo di elaborazione CDC corrente. Se una riga di origine è stata aggiornata più volte, viene restituita la modifica combinata (ad esempio, inserimento+aggiornamento viene prodotto come un singolo aggiornamento e aggiornamento+eliminazione viene prodotto come una singola eliminazione). Quando si utilizza la modalità di elaborazione delle modifiche Net, è possibile suddividere le modifiche negli output Delete, Insert e Update e gestirli in parallelo, perché la singola riga di origine viene visualizzata in più output.  
  
-   **Net with update mask**: questa modalità è simile alla modalità Net standard, ma aggiunge anche colonne booleane con il modello di nome **__$\<<nome-colonna>\___Changed**, che indica la presenza di colonne modificate nella riga delle modifiche corrente.  
  
-   **Net with merge**: questa modalità è simile alla modalità Net standard, ma con le operazioni Insert e Update unite in una singola operazione Merge (UPSERT).  
  
> [!NOTE]  
>  Per tutte le opzioni di modifica Net, è necessario che la tabella di origine disponga di una chiave primaria o di un indice univoco. Per tabelle senza una chiave primaria o indici univoci, usare l'opzione **All** .  
  
 **Variabile contenente lo stato CDC**  
 Selezionare la variabile del pacchetto di stringhe SSIS che gestisce lo stato CDC per il contesto CDC corrente. Per altre informazioni sulla variabile di stato CDC, vedere [Definire una variabile di stato](data-flow/define-a-state-variable.md).  
  
 **Includi colonna indicatore di rielaborazione**  
 Selezionare questa casella di controllo per creare una colonna di output speciale denominata **__$reprocessing**.  
  
 Questa colonna contiene un valore **true** quando l'intervallo di elaborazione CDC si sovrappone all'intervallo di elaborazione iniziale (l'intervallo di LSN che corrisponde al periodo di caricamento iniziale) o quando un intervallo di elaborazione CDC viene rielaborato a causa di un errore in un'esecuzione precedente. Questa colonna indicatore consente agli sviluppatori di SSIS di gestire gli errori in modo diverso durante la rielaborazione delle modifiche. Azioni quali l'eliminazione di una riga non esistente e l'inserimento non riuscito su una chiave duplicata, ad esempio, possono essere ignorate.  
  
 Per altre informazioni, vedere [Proprietà personalizzate dell'origine CDC](data-flow/cdc-source-custom-properties.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Editor origine CDC &#40;pagina Colonne&#41;](../../2014/integration-services/cdc-source-editor-columns-page.md)   
 [Editor origine CDC &#40;pagina Output degli errori&#41;](../../2014/integration-services/cdc-source-editor-error-output-page.md)  
  
  
