---
title: Correlare una traccia con i dati del log delle prestazioni di Windows (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], logs
ms.assetid: e1b3072c-8daf-49a7-9895-c8cccd2adb95
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 2d1b66cbbed716a4ce7b2d5cf9611e161141f162
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934582"
---
# <a name="correlate-a-trace-with-windows-performance-log-data-sql-server-profiler"></a>Correlare una traccia e i dati dei registri di prestazioni di Windows (SQL Server Profiler)
  [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]consente di correlare i contatori di monitoraggio di sistema di Microsoft Windows con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] gli eventi o. Con monitoraggio di sistema di Windows viene registrata l'attività del sistema per i contatori specificati nei registri di prestazioni.  
  
> [!NOTE]  
>  Per informazioni sulla condivisione di log tra versioni di Windows diverse, vedere la procedura descritta alla fine di questo argomento.  
  
### <a name="to-correlate-a-trace-with-performance-log-data"></a>Per correlare una traccia ai dati dei registri di prestazioni  
  
1.  In [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]aprire un file o una tabella di traccia salvata. Non è possibile correlare una traccia in esecuzione che sta ancora raccogliendo dati degli eventi. Per assicurare che la correlazione ai dati di monitoraggio di sistema sia corretta, è necessario che la traccia includa le due colonne di dati **StartTime** ed **EndTime** .  
  
2.  Scegliere **Importa dati prestazioni** dal menu  **File** di [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)].  
  
3.  Nella finestra di dialogo **Apri** selezionare un file contenente un registro di prestazioni. I dati del registro di prestazioni devono essere acquisiti quando è in corso l'acquisizione dei dati della traccia.  
  
4.  Nella finestra di dialogo **Limite contatori prestazioni** selezionare le caselle di controllo corrispondenti agli oggetti e ai contatori di monitoraggio di sistema che si desidera visualizzare insieme alla traccia. Fare clic su **OK**.  
  
5.  Selezionare un evento nella finestra degli eventi di traccia oppure nella finestra degli eventi di traccia scorrere alcune righe consecutive tramite i tasti di direzione. La barra rossa verticale visualizzata nella finestra dei **dati di monitoraggio di sistema** indica i dati del registro di prestazioni correlati all'evento di traccia selezionato.  
  
6.  Fare clic sul punto desiderato nel grafico di monitoraggio di sistema. Verrà selezionata la riga di traccia corrispondente più prossima in termini di tempo. Per eseguire lo zoom avanti su un intervallo di tempo, premere e trascinare il puntatore del mouse nel grafico di monitoraggio di sistema.  
  
### <a name="to-create-performance-logs-that-can-be-shared-among-different-versions-of-windows"></a>Per creare registri di prestazioni da condividere tra versioni di Windows diverse  
  
1.  Nel Pannello di controllo aprire **Strumenti di amministrazione**e quindi fare doppio clic su **Prestazioni**.  
  
2.  Nella finestra di dialogo **Prestazioni** espandere il nodo **Avvisi e registri di prestazioni**, fare clic con il pulsante destro del mouse su **Registri contatori**e quindi fare clic su **Nuove impostazioni registro**.  
  
3.  Digitare un nome per il registro contatori e quindi fare clic su **OK**.  
  
4.  Nella scheda **Generale** fare clic su **Aggiungi contatori**.  
  
5.  Nell'elenco **Oggetto prestazione** selezionare l'oggetto prestazione che si desidera monitorare. I nomi degli oggetti prestazioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per le istanze predefinite di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] iniziano con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e le istanze denominate iniziano con MSSQL$*instanceName*.  
  
6.  Aggiungere il numero di contatori necessari per l'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in uso e altri valori importanti, ad esempio il tempo processore e il tempo disco.  
  
7.  Dopo aver completato questa operazione, fare clic su **Chiudi**.  
  
8.  Impostare i valori desiderati per l'intervallo **Campiona dati ogni** . Iniziare con un intervallo breve, ad esempio 5 minuti, e modificarlo quindi in modo adeguato se necessario.  
  
9. Nella scheda **File di log** scegliere **File di testo (delimitato da virgole)** nell'elenco **Tipo file registro** . I file di log in formato di testo delimitato da virgole possono essere condivisi tra versioni diverse di Windows e visualizzati successivamente in uno strumento per la creazione di report, ad esempio Microsoft Excel.  
  
10. Nella scheda **Pianificazione** specificare una pianificazione per il monitoraggio.  
  
11. Fare clic su **OK** . Verrà creato il registro di prestazioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Modelli e autorizzazioni di SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [Avviare SQL Server Profiler](../tools/sql-server-profiler/start-sql-server-profiler.md)  
  
  
