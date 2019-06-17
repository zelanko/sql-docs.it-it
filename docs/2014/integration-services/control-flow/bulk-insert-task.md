---
title: Attività Inserimento bulk | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.bulkinserttask.f1
helpviewer_keywords:
- Bulk Insert task
- copying data [Integration Services]
ms.assetid: c5166156-6b4c-4369-81ed-27c4ce7040ae
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9b5da9ff28dc658f870033a02fe88b14ea442c51
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62832873"
---
# <a name="bulk-insert-task"></a>Inserimento bulk - attività
  L'attività Inserimento bulk rappresenta un modo efficiente per copiare grandi quantità di dati in una tabella o in una vista di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si supponga, ad esempio, che nella propria società venga usato un mainframe per archiviare l'elenco prodotti, che include un milione di righe, ma che il sistema e-commerce dell'azienda usi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per popolare le pagine Web. È necessario aggiornare la tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dei prodotti durante la notte utilizzando l'elenco master dei prodotti del mainframe. A tale scopo è possibile salvare l'elenco prodotti in un file delimitato da tabulazione e utilizzare l'attività Inserimento bulk per copiare i dati direttamente nella tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Per garantire la massima velocità di copia, non è consentito eseguire trasformazioni durante lo spostamento dei dati dal file di origine alla tabella o alla vista.  
  
## <a name="usage-considerations"></a>Considerazioni sull'utilizzo  
 Prima di utilizzare l'attività Inserimento bulk, considerare gli aspetti seguenti:  
  
-   Con l'attività Inserimento bulk i dati possono essere trasferiti solo da un file di testo a una tabella o a una vista di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per usare l'attività Inserimento bulk per trasferire dati da altri sistemi di gestione di database (DBMS, Database Management System), è necessario esportare i dati dall'origine a un file di testo e quindi importarli dal file di testo a una tabella o vista di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   La destinazione deve essere una tabella o vista di database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se nella tabella o vista di destinazione sono già presenti dati, durante l'esecuzione dell'attività Inserimento bulk i nuovi dati verranno aggiunti a quelli esistenti. Se si desidera sostituire i dati, prima dell'attività Inserimento bulk avviare un'attività Esegui SQL che esegue un'istruzione DELETE o TRUNCATE. Per altre informazioni, vedere [Attività Esegui SQL](execute-sql-task.md).  
  
-   Nell'oggetto attività Inserimento bulk è possibile utilizzare un file di formato. Se il file di formato è stato creato dall'utilità **bcp** , è possibile specificarne il percorso nell'attività Inserimento bulk. L'attività Inserimento bulk supporta file di formato sia XML che non XML. Per altre informazioni sui file di formato, vedere [File di formato per l'importazione o l'esportazione di dati &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).  
  
-   I pacchetti che contengono attività Inserimento bulk possono essere eseguiti solo dai membri del ruolo predefinito del server sysadmin.  
  
## <a name="bulk-insert-task-with-transactions"></a>Attività Inserimento bulk con le transazioni  
 Se le dimensioni del batch non sono impostate, l'intera operazione di copia bulk verrà considerata come un'unica transazione. Se il valore delle dimensioni del batch è **0** , i dati verranno inseriti in un solo batch. Se le dimensioni del batch sono impostate, ogni batch rappresenterà una transazione di cui verrà eseguito il commit alla fine dell'esecuzione.  
  
 Il comportamento dell'attività Inserimento bulk in relazione alle transazioni varia a seconda che l'attività partecipi o meno alla transazione del pacchetto. Se l'attività Inserimento bulk non partecipa alla transazione del pacchetto, per ogni batch privo di errori verrà eseguito il commit prima di procedere con il batch successivo. Se l'attività Inserimento bulk partecipa alla transazione, al termine dell'attività i batch privi di errori rimarranno nella transazione e saranno soggetti alle operazioni di commit o di rollback del pacchetto.  
  
 In caso di errore nell'attività Inserimento bulk, i batch già caricati non verranno sottoposti automaticamente a rollback. Analogamente l'esito positivo dell'attività non comporta automaticamente l'esecuzione del commit per tali batch. Le operazioni di commit e di rollback vengono eseguite solo se le proprietà del flusso di lavoro o del pacchetto sono state impostate in questo senso.  
  
## <a name="source-and-destination"></a>Origine e destinazione  
 Quando si specifica il percorso del file di testo di origine, prendere in considerazione i fattori seguenti:  
  
-   Il server deve disporre delle autorizzazioni necessarie per accedere sia al file che al database di destinazione.  
  
-   Poiché l'attività Inserimento bulk viene eseguita dal server, tutti i file di formato utilizzati dall'attività devono trovarsi sul server.  
  
-   Il file di origine caricato dall'attività Inserimento bulk può trovarsi sullo stesso server del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui vengono inseriti i dati oppure su un server remoto. Se il file si trova in un server remoto, è necessario specificarne il percorso in formato UNC (Universal Naming Convention).  
  
## <a name="performance-optimization"></a>Ottimizzazione delle prestazioni  
 Per ottimizzare le prestazioni, prendere in considerazione i fattori seguenti:  
  
-   Se il file di testo si trova nello stesso computer del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui vengono inseriti i dati, l'operazione di copia avviene a una velocità superiore, in quanto i dati non devono essere trasferiti in rete.  
  
-   L'attività Inserimento bulk non registra le righe che determinano errori. Se è necessario acquisire tali informazioni, utilizzare gli output degli errori dei componenti flusso di dati per registrare in un file di eccezioni le righe che provocano errori.  
  
## <a name="custom-log-entries-available-on-the-bulk-insert-task"></a>Voci di log personalizzate disponibili nell'attività Inserimento bulk  
 Nella tabella seguente sono elencate le voci di log personalizzate disponibili per l'attività Inserimento bulk. Per altre informazioni, vedere [Registrazione di Integration Services &#40;SSIS&#41;](../performance/integration-services-ssis-logging.md) e [Messaggi personalizzati per la registrazione](../custom-messages-for-logging.md).  
  
|Voce di log|Descrizione|  
|---------------|-----------------|  
|`BulkInsertTaskBegin`|Indica che l'inserimento bulk è iniziato.|  
|`BulkInsertTaskEnd`|Indica che l'inserimento bulk è terminato.|  
|`BulkInsertTaskInfos`|Offre informazioni descrittive sull'attività.|  
  
## <a name="bulk-insert-task-configuration"></a>Configurazione dell'attività Inserimento bulk  
 Per configurare l'attività Inserimento bulk, procedere nel modo seguente:  
  
-   Specificare la gestione connessione OLE DB da usare per la connessione al database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di destinazione e la tabella o la vista in cui inserire i dati. L'attività Inserimento bulk supporta solo le connessioni OLE DB per il database di destinazione.  
  
-   Specificare la gestione connessione file o file flat da utilizzare per accedere al file di origine. L'attività Inserimento bulk utilizza la gestione connessione solo per il percorso del file di origine. L'attività ignora le altre opzioni selezionate nell'editor gestione connessione.  
  
-   Definire il formato utilizzato dall'attività Inserimento bulk, utilizzando un file di formato o definendo i delimitatori di colonna e di riga dei dati di origine. Se si utilizza un file di formato, specificare la gestione connessione file da utilizzare per accedere a tale file.  
  
-   Specificare le azioni da eseguire nella tabella o nella vista di destinazione quando i dati vengono inseriti dall'attività. È possibile specificare se verificare i vincoli, abilitare IDENTITY_INSERT, mantenere i valori Null, attivare trigger o bloccare la tabella.  
  
-   Fornire informazioni sul batch di dati da inserire, ad esempio le dimensioni del batch, la prima e l'ultima riga del file da inserire, il numero massimo di errori oltre il quale arrestare l'inserimento delle righe e i nomi delle colonne che verranno ordinate.  
  
 Se l'attività Inserimento bulk utilizza una gestione connessione file flat per accedere al file di origine, invece del formato specificato nella gestione connessione file flat usa il formato specificato in un file di formato o i valori delle proprietà RowDelimiter e ColumnDelimiter dell'attività.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic su uno degli argomenti seguenti:  
  
-   [Editor attività Inserimento bulk &#40;pagina Generale&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor attività Inserimento bulk &#40;Pagina Connessione&#41;](../bulk-insert-task-editor-connection-page.md)  
  
-   [Editor attività Inserimento bulk &#40;pagina Opzioni&#41;](../bulk-insert-task-editor-options-page.md)  
  
-   [Pagina Espressioni](../expressions/expressions-page.md)  
  
 Per altre informazioni sull'impostazione di queste proprietà in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Impostazione delle proprietà di un'attività o di un contenitore](../set-the-properties-of-a-task-or-container.md)  
  
### <a name="programmatic-configuration-of-the-bulk-insert-task"></a>Configurazione a livello di codice dell'attività Inserimento bulk  
 Per ulteriori informazioni sull'impostazione di queste proprietà a livello di codice, fare clic sull'argomento seguente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask>  
  
## <a name="related-tasks"></a>Attività correlate  
 [Impostazione delle proprietà di un'attività o di un contenitore](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-content"></a>Contenuto correlato  
  
-   Articolo tecnico [You may get "Unable to prepare the SSIS bulk insert for data insertion" error on UAC enabled systems](https://go.microsoft.com/fwlink/?LinkId=233693)(Possibile visualizzazione dell'errore "Impossibile preparare l'attività Inserimento bulk SSIS per l'inserimento dei dati" nei sistemi con Controllo account utente abilitato) nel sito support.microsoft.com.  
  
-   Articolo tecnico relativo alla [guida alle prestazioni del caricamento dati](https://go.microsoft.com/fwlink/?LinkId=233700)sul sito msdn.microsoft.com.  
  
-   Articolo tecnico relativo all' [utilizzo di SQL Server Integration Services per il caricamento bulk dei dati](https://go.microsoft.com/fwlink/?LinkId=233701)sul sito Web simple-talk.com.  
  
  
