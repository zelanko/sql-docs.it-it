---
title: Salvare tracce e modelli di traccia | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- saving traces
- traces [SQL Server], saving
- templates [SQL Server], SQL Server Profiler
- Profiler [SQL Server Profiler], templates
- trace templates [SQL Server]
- exporting trace templates
- importing trace templates
- SQL Server Profiler, templates
ms.assetid: 957e6bf8-e7a3-4a59-a1cd-0a41538a8158
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d4baca63080a3f67c1f9e54a8a0aa955a27029df
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63267426"
---
# <a name="save-traces-and-trace-templates"></a>Salvare tracce e modelli di traccia
  È importante distinguere il salvataggio di file di traccia dal salvataggio di modelli di traccia. Il salvataggio di un file di traccia comporta il salvataggio dei dati di evento acquisiti in una posizione specificata. Il salvataggio di un modello di traccia comporta invece il salvataggio della definizione di una traccia, ad esempio le colonne di dati, le classi di evento o i filtri specificati.  
  
## <a name="saving-traces"></a>salvataggio di tracce  
 Salvare i dati di evento acquisiti in un file o in una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se è necessario analizzare o riprodurre i dati acquisiti in un momento successivo. Utilizzare un file di traccia nei casi seguenti:  
  
-   Utilizzare un file di traccia o una tabella di traccia per creare un carico di lavoro da utilizzare come input per Ottimizzazione guidata motore di database.  
  
-   Utilizzare un file di traccia per l'acquisizione degli eventi e inviare tale file al supporto tecnico per l'analisi.  
  
-   Utilizzare gli strumenti di elaborazione delle query in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per accedere ai dati o visualizzarli in [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Solo i membri del ruolo predefinito del server **sysadmin** o l'autore della tabella possono accedere direttamente alla tabella di traccia.  
  
> [!NOTE]  
>  L'acquisizione dei dati di traccia in una tabella è un'operazione più lenta rispetto all'acquisizione dei dati di traccia in un file. In alternativa, è possibile acquisire i dati di traccia in un file, aprire il file di traccia e quindi salvarlo come tabella di traccia.  
  
 Se si usa un file di traccia, [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] salva i dati di evento acquisiti (e non le definizioni della traccia) in un file di traccia ( [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] .trc) di\*. L'estensione viene aggiunta al file di traccia automaticamente al momento del salvataggio, indipendentemente da altre estensioni eventualmente specificate. Ad esempio, se si specifica un file di traccia denominato **Trace.dat**, il file creato verrà denominato **Trace.dat.trc**.  
  
> [!IMPORTANT]  
>  Gli utenti che dispongono dell'autorizzazione SHOWPLAN, ALTER TRACE o VIEW SERVER STATE possono visualizzare le query acquisite nell'output di Showplan. Poiché tali query possono contenere informazioni riservate, ad esempio password, è consigliabile concedere tali autorizzazioni solo agli utenti che possono visualizzare le informazioni riservate, ad esempio ai membri del ruolo predefinito del database **db_owner** oppure ai membri del ruolo predefinito del server **sysadmin** . È inoltre consigliabile salvare file Showplan o file di traccia che contengono eventi correlati a Showplan solo in una posizione che utilizza il file system NTFS e limitare l'accesso agli utenti autorizzati a visualizzare le informazioni riservate.  
  
## <a name="saving-templates"></a>Salvataggio dei modelli  
 Nella definizione del modello di una traccia sono incluse le classi di evento, le colonne di dati, i filtri e tutte le altre proprietà, eccetto i dati degli eventi acquisiti, utilizzati per creare una traccia. 
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] fornisce modelli di sistema predefiniti per attività di traccia comuni e per attività specifiche, ad esempio la creazione di un carico di lavoro che Ottimizzazione guidata motore di database può usare per ottimizzare la progettazione fisica del database. È inoltre possibile creare e salvare modelli definiti dall'utente.  
  
### <a name="importing-and-exporting-templates"></a>Importazione ed esportazione di modelli  
 
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] consente di importare ed esportare modelli da un server a un altro. L'esportazione di un modello comporta lo spostamento di una copia di un modello esistente in una directory specificata. L'importazione crea una copia del modello specificato. Visualizzando questi modelli in [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]è possibile distinguerli dai modelli di sistema per il termine "(utente)" che segue il nome del modello. Non è possibile sovrascrivere o modificare direttamente un modello di sistema predefinito.  
  
### <a name="analyzing-performance-with-templates"></a>Analisi delle prestazioni con i modelli  
 Se si esegue spesso il monitoraggio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], utilizzare i modelli per l'analisi delle prestazioni. I modelli consentono di acquisire sempre gli stessi dati di evento e utilizzano la stessa definizione di traccia per il monitoraggio degli stessi eventi. In questo modo non è necessario definire le classi di evento e le colonne di dati ogni volta che si crea una traccia. È inoltre possibile distribuire il modello ad altri utenti per il monitoraggio di eventi specifici di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Ad esempio, il supporto tecnico potrebbe fornire un modello a un cliente in modo che il cliente lo possa utilizzare per acquisire i dati di evento necessari, che potranno poi essere inviati al supporto tecnico per essere analizzati.  
  
 **Per salvare una traccia in un file**  
  
 [Salvare i risultati della traccia in un file &#40;SQL Server Profiler&#41;](save-trace-results-to-a-file-sql-server-profiler.md)  
  
 [sp_trace_create &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-create-transact-sql)  
  
## <a name="see-also"></a>Vedere anche  
 [Salvare i risultati della traccia in una tabella &#40;SQL Server Profiler&#41;](save-trace-results-to-a-table-sql-server-profiler.md)   
 [Creare un modello di traccia &#40;SQL Server Profiler&#41;](create-a-trace-template-sql-server-profiler.md)   
 [Derivare un modello da una traccia in esecuzione &#40;SQL Server Profiler&#41;](derive-a-template-from-a-running-trace-sql-server-profiler.md)   
 [Derivare un modello da un file di traccia o da una tabella di traccia &#40;SQL Server Profiler&#41;](derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)   
 [Esportare un modello di traccia &#40;SQL Server Profiler&#41;](export-a-trace-template-sql-server-profiler.md)   
 [Importare un modello di traccia &#40;SQL Server Profiler&#41;](import-a-trace-template-sql-server-profiler.md)  
  
  
