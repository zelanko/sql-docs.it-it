---
title: Attività di controllo CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdccontroltask.f1
ms.assetid: 6404dc7f-550c-47cc-b901-c072742f430a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e1ddc919b4658395c6a4268f03131bc92291f1b0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62832883"
---
# <a name="cdc-control-task"></a>Attività di controllo CDC
  L'attività di controllo CDC viene utilizzata per controllare il ciclo di vita di pacchetti Change Data Capture (CDC). Questa attività consente di gestire la sincronizzazione del pacchetto CDC con il pacchetto di caricamento iniziale e la gestione di intervalli di numeri di sequenza del file di log (LSN) elaborati in un'esecuzione di un pacchetto CDC. L'attività di controllo CDC, inoltre, consente di gestire gli scenari di errore e il recupero da errori.  
  
 L'attività di controllo CDC consente di gestire lo stato del pacchetto CDC in una variabile del pacchetto SSIS e di renderlo persistente in una tabella di database, in modo che lo stato venga mantenuto tra attivazioni del pacchetto e tra più pacchetti che eseguono insieme un processo CDC comune. Un'attività, ad esempio, può essere responsabile del caricamento iniziale e l'altra degli aggiornamenti trickle-feed.  
  
 L'attività di controllo CDC supporta due gruppi di operazioni. Mediante un gruppo viene gestita la sincronizzazione del caricamento iniziale e dell'elaborazione delle modifiche; mediante l'altro gruppo viene gestito l'intervallo di elaborazione delle modifiche degli LSN per un'esecuzione di un pacchetto CDC e di tenere traccia degli elementi elaborati correttamente.  
  
 Nelle operazioni seguenti viene gestita la sincronizzazione del caricamento iniziale e dell'elaborazione delle modifiche:  
  
|Operazione|Descrizione|  
|---------------|-----------------|  
|ResetCdcState|Questa operazione viene utilizzata per reimpostare lo stato CDC persistente associato al contesto CDC corrente. Dopo l'esecuzione di questa operazione, l'LSN massimo corrente della tabella LSN-timestamp `sys.fn_cdc_get_max_lsn` diventa l'inizio dell'intervallo di elaborazione successivo. Per questa operazione è necessaria una connessione al database di origine.|  
|MarkInitialLoadStart|Questa operazione viene utilizzata all'inizio di un pacchetto di caricamento iniziale per registrare l'LSN corrente nel database di origine prima che tramite il pacchetto di caricamento iniziale venga avviata la lettura delle tabelle di origine. Per questa operazione è necessaria una connessione al database di origine per chiamare `sys.fn_cdc_get_max_lsn`.<br /><br /> Se si seleziona MarkInitialLoadStart quando si usa CDC di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , ovvero non di Oracle, l'utente specificato nella gestione connessione deve essere db_owner o sysadmin.|  
|MarkInitialLoadEnd|Questa operazione viene utilizzata alla fine di un pacchetto di caricamento iniziale per registrare l'LSN corrente nel database di origine dopo che il pacchetto di caricamento iniziale completa la lettura delle tabelle di origine. Questo LSN viene determinato registrando la data e l'ora correnti in cui si è verificata l'operazione ed eseguendo quindi una query sulla tabella di mapping `cdc.lsn_time_`nel database CDC per trovare una modifica successiva alla data e all'ora.<br /><br /> Se si seleziona MarkInitialLoadEnd quando si usa CDC di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , ovvero non di Oracle, l'utente specificato nella gestione connessione deve essere db_owner o sysadmin.|  
|MarkCdcStart|Questa operazione viene utilizzata quando il caricamento iniziale viene eseguito da un database snapshot. In questo caso, l'elaborazione delle modifiche deve iniziare immediatamente dopo l'LSN dello snapshot. È possibile specificare il nome del database snapshot da utilizzare e l'attività di controllo CDC esegue una query su [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] per trovare l'LSN dello snapshot. È inoltre possibile scegliere di specificare direttamente l'LSN dello snapshot.<br /><br /> Se si seleziona MarkCdcStart quando si usa CDC di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , ovvero non di Oracle, l'utente specificato nella gestione connessione deve essere db_owner o sysadmin.|  
  
 Le operazioni seguenti vengono utilizzate per gestire l'intervallo di elaborazione:  
  
|Operazione|Descrizione|  
|---------------|-----------------|  
|GetProcessingRange|Questa operazione viene utilizzata prima di richiamare il flusso di dati che utilizza il flusso di dati dell'origine CDC. L'operazione consente di stabilire un intervallo di LSN letti dal flusso di dati dell'origine CDC quando il flusso di dati viene richiamato. L'intervallo viene archiviato in una variabile del pacchetto SSIS utilizzata dall'origine CDC durante l'elaborazione del flusso di dati.<br /><br /> Per altre informazioni sugli stati che vengono archiviati, vedere [Definire una variabile di stato](../data-flow/define-a-state-variable.md).|  
|MarkProcessedRange|Questa operazione avviene dopo ogni esecuzione CDC (una volta completato il flusso di dati CDC) per registrare l'ultimo LSN elaborato completamente nell'esecuzione CDC. Alla successiva esecuzione di GetProcessingRange, questa posizione corrisponde all'inizio dell'intervallo di elaborazione.|  
  
## <a name="handling-cdc-state-persistency"></a>Gestione della persistenza dello stato CDC  
 L'attività di controllo CDC consente di gestire uno stato persistente tra attivazioni. Le informazioni archiviate nello stato CDC vengono utilizzate per determinare e gestire l'intervallo di elaborazione per il pacchetto CDC e per il rilevamento di eventuali condizioni di errore. Lo stato persistente viene archiviato come stringa. Per altre informazioni, vedere [Definire una variabile di stato](../data-flow/define-a-state-variable.md).  
  
 L'attività di controllo CDC supporta due tipi di persistenza dello stato  
  
-   Persistenza dello stato manuale: in questo caso, l'attività di controllo CDC gestisce lo stato archiviato in una variabile del pacchetto, ma lo sviluppatore del pacchetto deve leggere la variabile da un archivio persistente prima di chiamare il controllo CDC e quindi riscriverla nell'archivio persistente dopo l'ultima chiamata del controllo CDC e il completamento dell'esecuzione CDC.  
  
-   Persistenza dello stato automatica: lo stato CDC viene archiviato in una tabella di un database. Lo stato viene archiviato con un nome specificato nella proprietà **StateName** in una tabella denominata nella proprietà **Table to Use for Storing State** , inclusa in una gestione connessione selezionata per l'archiviazione dello stato. Il valore predefinito è la gestione connessione di origine, ma secondo la pratica comune è consigliabile impostare il valore sulla gestione connessione di destinazione. Tramite l'attività di controllo CDC viene aggiornato il valore di stato nella tabella di stato e viene eseguito il commit di tale valore come parte della transazione di ambiente.  
  
## <a name="error-handling"></a>Gestione degli errori  
 È possibile che l'attività di controllo CDC restituisca un errore nei casi seguenti:  
  
-   Non è possibile leggere lo stato CDC persistente o l'aggiornamento dello stato persistente non riesce.  
  
-   Non è possibile leggere le informazioni LSN correnti dal database di origine.  
  
-   Lo stato CDC letto non è coerente.  
  
 In tutti questi casi, l'attività di controllo CDC restituisce un errore che può essere gestito tramite la modalità standard di gestione degli errori del flusso di controllo in SSIS.  
  
 L'attività di controllo CDC può inoltre restituire un avviso quando l'operazione GetProcessingRange viene richiamata direttamente dopo un'altra operazione GetProcessingRange senza che venga chiamata l'operazione MarkProcessedRange. Ciò indica che l'esecuzione precedente non è riuscita o che è possibile che un altro pacchetto CDC con lo stesso nome di stato CDC sia in esecuzione.  
  
## <a name="configuring-the-cdc-control-task"></a>Configurazione dell'attività di controllo CDC  
 È possibile impostare le proprietà tramite Progettazione SSIS o a livello di codice.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Editor attività Controllo CDC](../cdc-control-task-editor.md)  
  
-   [Proprietà personalizzate dell'attività di controllo CDC](cdc-control-task-custom-properties.md)  
  
## <a name="related-tasks"></a>Attività correlate  
 [Definire una variabile di stato](../data-flow/define-a-state-variable.md)  
  
## <a name="related-content"></a>Contenuto correlato  
  
-   Articolo tecnico [Installing Microsoft SQL Server 2012 Change Data Capture for Oracle by Attunity](https://go.microsoft.com/fwlink/?LinkId=252958)(Installazione di Microsoft SQL Server 2012 Change Data Capture per Oracle di Attunity) nel sito Web social.technet.microsoft.com.  
  
-   Articolo tecnico [Troubleshoot Configuration Issues in Microsoft Change Data Capture for Oracle by Attunity](https://go.microsoft.com/fwlink/?LinkId=252960)(Risoluzione dei problemi di configurazione in Microsoft Change Data Capture per Oracle di Attunity) nel sito Web social.technet.microsoft.com.  
  
-   Articolo tecnico [Troubleshoot CDC Instance Errors in Microsoft Change Data Capture for Oracle by Attunity](https://go.microsoft.com/fwlink/?LinkId=252961)(Risoluzione degli errori di istanze di CDC in Microsoft Change Data Capture per Oracle di Attunity) nel sito Web social.technet.microsoft.com.  
  
  
