---
title: Editor attività controllo CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdccontroltask.config.f1
ms.assetid: 4f09d040-9ec8-4aaa-b684-f632d571f0a8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 35d20d475b8f6da9c899c389419233f8e90bf555
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439018"
---
# <a name="cdc-control-task-editor"></a>Editor attività Controllo CDC
  Utilizzare la finestra di dialogo **CDC Control Task Editor** per configurare l'attività di controllo CDC. La configurazione dell'attività di controllo CDC include la definizione di una connessione al database CDC, l'operazione dell'attività CDC e le informazioni sulla gestione dello stato.  
  
 Per ulteriori informazioni sull'attività di controllo CDC, vedere [CDC Control Task](control-flow/cdc-control-task.md).  
  
 **Per aprire CDC Control Task Editor**  
  
1.  In [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]aprire il pacchetto [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] contenente l'attività di controllo CDC.  
  
2.  Nella scheda **Flusso di controllo** fare doppio clic sull'attività di controllo CDC.  
  
## <a name="options"></a>Opzioni  
 **Gestione connessione ADO.NET per database CDC di SQL Server**  
 Selezionare una gestione connessione esistente nell'elenco o creare una nuova connessione facendo clic su **Nuova** . La connessione deve essere stabilita a un database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] abilitato per CDC e in cui si trova la tabella delle modifiche selezionata.  
  
 **Operazione di controllo CDC**  
 Selezionare l'operazione da eseguire per questa attività. Per tutte le operazioni viene utilizzata la variabile di stato archiviata in una variabile del pacchetto SSIS utilizzata per archiviare lo stato e passarlo tra i diversi componenti nel pacchetto.  
  
-   **Contrassegna avvio caricamento iniziale**: questa operazione viene utilizzata durante l'esecuzione di un caricamento iniziale da un database attivo senza uno snapshot. Viene richiamata all'inizio di un pacchetto di caricamento iniziale per registrare il valore LSN corrente nel database di origine prima che venga avviata la lettura delle tabelle di origine. Questa operazione richiede una connessione al database di origine.  
  
     Se si seleziona **Contrassegna avvio caricamento iniziale** quando si usa CDC di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] (ovvero, non Oracle), l'utente specificato nella gestione connessione deve essere  **db_owner** o **sysadmin**.  
  
-   **Contrassegna fine caricamento iniziale**: questa operazione viene utilizzata durante l'esecuzione di un caricamento iniziale da un database attivo senza uno snapshot. Viene richiamata alla fine di un pacchetto di caricamento iniziale per registrare l'LSN corrente nel database di origine al termine della lettura delle tabelle di origine. Questo LSN viene determinato registrando l'ora corrente in cui l'operazione si è verificata ed eseguendo quindi una query sulla tabella `cdc.lsn_time_`mapping nel database CDC per ricercare una modifica successiva a tale ora  
  
     Se si seleziona **Contrassegna fine caricamento iniziale** quando si usa CDC di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] (ovvero, non Oracle), l'utente specificato nella gestione connessione deve essere  **db_owner** o **sysadmin**.  
  
-   **Contrassegna avvio CDC**: questa operazione viene usata quando il caricamento iniziale è costituito da un database snapshot o da un database disattivato. Viene richiamata in qualsiasi punto all'interno del pacchetto di caricamento iniziale. L'operazione accetta un parametro che può essere un LSN snapshot, un nome di un database snapshot (da cui l'LSN snapshot viene automaticamente derivato) o può essere lasciato vuoto, nel qual caso l'LSN del database corrente viene utilizzato come LSN iniziale per il pacchetto di elaborazione delle modifiche.  
  
     Questa operazione viene utilizzata al posto delle operazioni Contrassegna avvio caricamento iniziale/Contrassegna fine caricamento iniziale.  
  
     Se si seleziona **Contrassegna avvio CDC** quando si usa CDC di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] (ovvero, non Oracle), l'utente specificato nella gestione connessione deve essere  **db_owner** o **sysadmin**.  
  
-   **Ottieni intervallo di elaborazione**: questa operazione viene utilizzata in un pacchetto di elaborazione delle modifiche prima di richiamare il flusso di dati che utilizza il flusso di dati dell'origine CDC. L'operazione consente di stabilire un intervallo di LSN letti dal flusso di dati dell'origine CDC quando il flusso di dati viene richiamato. L'intervallo viene archiviato in una variabile del pacchetto SSIS utilizzata dall'origine CDC durante l'elaborazione del flusso di dati.  
  
     Per altre informazioni sui possibili stati CDC che vengono archiviati, vedere [Definire una variabile di stato](data-flow/define-a-state-variable.md).  
  
-   **Contrassegna intervallo elaborato**: questa operazione viene usata in un pacchetto di elaborazione delle modifiche alla fine di un'esecuzione CDC (dopo il corretto completamento del flusso di dati CDC) per registrare l'ultimo LSN elaborato completamente nell'esecuzione CDC. Alla prossima esecuzione di `GetProcessingRange` , questa posizione determina l'inizio dell'intervallo di elaborazione successivo.  
  
-   **Reimposta stato CDC**: questa operazione viene utilizzata per reimpostare lo stato CDC persistente associato al contesto CDC corrente. Dopo l'esecuzione di questa operazione, l'LSN massimo corrente della tabella LSN-timestamp `sys.fn_cdc_get_max_lsn` diventa l'inizio dell'intervallo di elaborazione successivo. Per questa operazione è necessaria una connessione al database di origine.  
  
     Questa operazione viene ad esempio utilizzata quando si desidera elaborare solo i record di modifica appena creati e ignorare tutti i record di modifica obsoleti.  
  
 **Variabile contenente lo stato CDC**  
 Selezionare la variabile del pacchetto SSIS utilizzata per archiviare le informazioni di stato relative all'operazione dell'attività. Prima di iniziare, è necessario definire una variabile. Se si seleziona **AutomaticStatePersistence**, la variabile di stato viene caricata e salvata automaticamente.  
  
 Per altre informazioni sulla definizione della variabile di stato, vedere [Definire una variabile di stato](data-flow/define-a-state-variable.md).  
  
 **LSN SQL Server per avviare il nome snapshot/CDC:**  
 Digitare l'LSN del database di origine corrente o il nome del database snapshot da cui viene eseguito il caricamento iniziale per determinare l'inizio di CDC. Questa opzione è disponibile solo se si imposta **Operazione di controllo CDC** su **Contrassegna avvio CDC**.  
  
 Per ulteriori informazioni su queste operazioni, vedere [CDC Control Task](control-flow/cdc-control-task.md)  
  
 **Archivia automaticamente lo stato in una tabella di database**  
 Selezionare questa casella di controllo se si desidera che tramite l'attività di controllo CDC vengano gestiti automaticamente il caricamento e l'archiviazione dello stato CDC in una tabella di stato contenuta nel database specificato. Se la casella di controllo è deselezionata, lo sviluppatore deve caricare lo stato CDC quando il pacchetto viene avviato e salvarlo ogni volta che lo stato CDC cambia.  
  
 **Gestione connessione per il database in cui è archiviato lo stato**  
 Selezionare una gestione connessione ADO.NET esistente dall'elenco o creare una nuova connessione facendo clic su Nuova. Questa connessione è a un database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] che contiene la tabella Stato. La tabella Stato contiene le informazioni sullo stato.  
  
 È disponibile solo se si seleziona **AutomaticStatePersistence** ed è un parametro obbligatorio.  
  
 **Tabella da utilizzare per l'archiviazione dello stato**  
 Digitare il nome della tabella di stato da utilizzare per l'archiviazione dello stato CDC. La tabella specificata deve disporre di due colonne denominate **name** e **state** , entrambe dello stesso tipo di dati **varchar (256)**.  
  
 Facoltativamente, è possibile selezionare **Nuova** per ottenere uno script SQL che compila una nuova tabella Stato con le colonne obbligatorie. Se **AutomaticStatePersistence** è selezionato, lo sviluppatore deve creare una tabella di stato in base ai requisiti elencati in precedenza.  
  
 È disponibile solo se si seleziona **AutomaticStatePersistence** ed è un parametro obbligatorio.  
  
 **Nome dello stato**  
 Digitare un nome da associare allo stato CDC persistente. Un nome dello stato comune verrà specificato dal caricamento completo e dai pacchetti CDC che utilizzano lo stesso contesto. Questo nome viene utilizzato per cercare la riga di stato nella tabella di stato  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà personalizzate dell'attività di controllo CDC](control-flow/cdc-control-task-custom-properties.md)  
  
  
