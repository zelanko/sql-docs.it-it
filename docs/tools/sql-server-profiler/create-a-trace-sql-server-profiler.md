---
title: Creare una traccia
titleSuffix: SQL Server Profiler
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: 0302fa6d-d2b5-43fe-ad70-7a337575b112
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 08/01/2016
ms.openlocfilehash: 5a5c004bbc7e93720f18df998b989c46ced0188e
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "75307336"
---
# <a name="create-a-trace-sql-server-profiler"></a>Creare una traccia (SQL Server Profiler)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In questo argomento viene descritto come utilizzare [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] per creare una traccia.  
  
### <a name="to-create-a-trace"></a>Per creare una traccia  
  
1.  Scegliere **Nuova traccia** dal menu **File**e quindi connettersi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Verrà visualizzata la finestra di dialogo **Proprietà traccia** .  
  
    > **NOTA** Se la casella di controllo **Avvia traccia non appena viene stabilita una connessione** è selezionata, la finestra di dialogo **Proprietà traccia** non verrà visualizzata e verrà invece avviata la traccia. Per disattivare questa impostazione, scegliere *Opzioni* dal menu ***Strumenti*** e deselezionare la casella di controllo Avvia traccia non appena viene stabilita una connessione.  
  
2.  Nella casella **Nome traccia** digitare un nome per la traccia.  
  
3.  Nell'elenco **Modello** selezionare un modello di traccia sul quale basare la traccia oppure selezionare **Vuoto** per non utilizzare alcun modello.  
  
4.  Per salvare i risultati della traccia, eseguire una delle operazioni seguenti:  
  
    -   Fare clic su **Salva nel file** per acquisire la traccia in un file. Specificare un valore per l'opzione **Dimensioni massime del file**. Il valore predefinito è 5 megabyte (MB).  
  
         Facoltativamente, selezionare **Consenti rollover dei file** per creare automaticamente nuovi file quando viene raggiunta la dimensione massima consentita per i file. È anche possibile selezionare facoltativamente **Dati di traccia elaborati dal server**per assegnare l'elaborazione dei dati di traccia al servizio che esegue la traccia, invece che all'applicazione client. Quando i dati di traccia vengono elaborati dal server, in condizioni di sovraccarico non verrà ignorato alcun evento, ma è possibile che si verifichi un peggioramento delle prestazioni del server.  
  
    -   Fare clic su **Salva nella tabella** per acquisire la traccia in una tabella del database.  
  
         Facoltativamente fare clic su **Numero massimo di righe**e specificare un valore.  
  
    > **ATTENZIONE!** Se i risultati della traccia non vengono salvati in un file o in una tabella, è possibile visualizzare la traccia quando [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] è aperto. I risultati della traccia andranno tuttavia persi dopo l'arresto della traccia e la chiusura di [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Per evitare tale perdita dei risultati della traccia, scegliere **Salva** dal menu **File** per salvare i risultati prima di chiudere [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
5.  Facoltativamente, selezionare la casella di controllo **Data e ora di arresto della traccia** e specificare una data e un'ora di arresto della traccia.  
  
6.  Per aggiungere o rimuovere eventi, colonne di dati o filtri, fare clic sulla scheda **Selezione eventi**  . Per altre informazioni, vedere: [Specificare eventi e colonne di dati per un file di traccia &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)  
  
7.  Fare clic su **Esegui** per avviare la traccia.  
  
## <a name="see-also"></a>Vedere anche  
 [Autorizzazioni necessarie per l'esecuzione di SQL Server Profiler](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md)   
 [Modelli e autorizzazioni di SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)   
 [Correlare una traccia e i dati dei registri di prestazioni di Windows &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/correlate-a-trace-with-windows-performance-log-data-sql-server-profiler.md)  
  
  
