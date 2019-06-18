---
title: Creare una traccia (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], creating
ms.assetid: 0302fa6d-d2b5-43fe-ad70-7a337575b112
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 36f53b9f4daaa25d6276778ed4f38ae641c73c93
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62712418"
---
# <a name="create-a-trace-sql-server-profiler"></a>Creare una traccia (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In questo argomento viene descritto come utilizzare [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] per creare una traccia.  
  
### <a name="to-create-a-trace"></a>Per creare una traccia  
  
1.  Scegliere **Nuova traccia** dal menu **File**e quindi connettersi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Verrà visualizzata la finestra di dialogo **Proprietà traccia** .  
  
    > **NOTA:** se è selezionato **Avvia traccia non appena viene stabilita una connessione** , la finestra di dialogo **Proprietà traccia** non viene visualizzata e viene invece avviata la traccia. Per disattivare questa impostazione, scegliere *Opzioni* dal menu ***Strumenti*** e deselezionare la casella di controllo Avvia traccia non appena viene stabilita una connessione.  
  
2.  Nella casella **Nome traccia** digitare un nome per la traccia.  
  
3.  Nell'elenco **Modello** selezionare un modello di traccia sul quale basare la traccia oppure selezionare **Vuoto** per non utilizzare alcun modello.  
  
4.  Per salvare i risultati della traccia, eseguire una delle operazioni seguenti:  
  
    -   Fare clic su **Salva nel file** per acquisire la traccia in un file. Specificare un valore per l'opzione **Dimensioni massime del file**. Il valore predefinito è 5 megabyte (MB).  
  
         Facoltativamente, selezionare **Consenti rollover dei file** per creare automaticamente nuovi file quando viene raggiunta la dimensione massima consentita per i file. È anche possibile selezionare facoltativamente **Dati di traccia elaborati dal server**per assegnare l'elaborazione dei dati di traccia al servizio che esegue la traccia, invece che all'applicazione client. Quando i dati di traccia vengono elaborati dal server, in condizioni di sovraccarico non verrà ignorato alcun evento, ma è possibile che si verifichi un peggioramento delle prestazioni del server.  
  
    -   Fare clic su **Salva nella tabella** per acquisire la traccia in una tabella del database.  
  
         Facoltativamente fare clic su **Numero massimo di righe**e specificare un valore.  
  
    > **ATTENZIONE!** Se i risultati della traccia non vengono salvati in un file o in una tabella, è possibile visualizzare la traccia quando [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] è aperto. I risultati della traccia andranno tuttavia persi dopo l'arresto della traccia e la chiusura di [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Per evitare tale perdita dei risultati della traccia, scegliere **Salva** dal menu **File** per salvare i risultati prima di chiudere [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
5.  Facoltativamente, selezionare la casella di controllo **Data e ora di arresto della traccia** e specificare una data e un'ora di arresto della traccia.  
  
6.  Per aggiungere o rimuovere eventi, colonne di dati o filtri, fare clic sulla scheda **Selezione eventi**  . Per altre informazioni, vedere [Specificare eventi e colonne di dati per un file di traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)  
  
7.  Fare clic su **Esegui** per avviare la traccia.  
  
## <a name="see-also"></a>Vedere anche  
 [Autorizzazioni necessarie per l'esecuzione di SQL Server Profiler](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md)   
 [Modelli e autorizzazioni di SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)   
 [Correlare una traccia e i dati dei registri di prestazioni di Windows &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/correlate-a-trace-with-windows-performance-log-data-sql-server-profiler.md)  
  
  
