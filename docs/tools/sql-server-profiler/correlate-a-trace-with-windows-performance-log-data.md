---
title: Correlare una traccia con i dati del log delle prestazioni di Windows | Microsoft Docs
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- correlating trace with log data
- logs [SQL Server], traces
- Profiler [SQL Server Profiler], correlating trace with log data
- traces [SQL Server], logs
- SQL Server Profiler, correlating trace with log data
ms.assetid: 1e4412c8-d27c-4aae-9b35-214128d1d00a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bdbd634a74c5e7cd48232a28ab4c7709e8febfad
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63033767"
---
# <a name="correlate-a-trace-with-windows-performance-log-data"></a>Correlare una traccia con i dati del log delle prestazioni di Windows
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]consente di aprire un log delle prestazioni di Microsoft Windows, scegliere i contatori da correlare a una traccia e visualizzare i contatori delle prestazioni selezionati insieme alla traccia nell'interfaccia utente grafica di [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] . Quando si seleziona un evento nella finestra della traccia, una barra rossa verticale nel riquadro della finestra dei dati di Monitoraggio di sistema di [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] indica i dati del log delle prestazioni correlati all'evento di traccia selezionato.  
  
 Per correlare una traccia con i contatori delle prestazioni, aprire un file di traccia o una tabella contenente le colonne di dati **StartTime** e **EndTime** data columns, e then click **Importa dati prestazioni** dal menu [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **File** menu. È quindi possibile aprire un log delle prestazioni e selezionare gli oggetti e i contatori di Monitoraggio di sistema da correlare alla traccia.  
  
### <a name="to-correlate-a-trace-with-performance-log-data"></a>Per correlare una traccia ai dati dei registri di prestazioni  
  
1.  In [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]aprire un file o una tabella di traccia salvata. Non è possibile correlare una traccia in esecuzione che sta ancora raccogliendo dati degli eventi. Per assicurare che la correlazione ai dati di monitoraggio di sistema sia corretta, è necessario che la traccia includa le due colonne di dati **StartTime** ed **EndTime** .  
  
2.  Nel menu [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **File** menu, click **Import Performance Data**.  
  
3.  Nella finestra di dialogo **Apri** selezionare un file contenente un registro di prestazioni. I dati del registro di prestazioni devono essere acquisiti quando è in corso l'acquisizione dei dati della traccia.  
  
4.  Nella finestra di dialogo **Limite contatori prestazioni** selezionare le caselle di controllo corrispondenti agli oggetti e ai contatori di monitoraggio di sistema che si desidera visualizzare insieme alla traccia. Scegliere **OK.**  
  
5.  Selezionare un evento nella finestra degli eventi di traccia oppure nella finestra degli eventi di traccia scorrere alcune righe consecutive tramite i tasti di direzione. La barra rossa verticale visualizzata nella finestra dei **dati di monitoraggio di sistema** indica i dati del registro di prestazioni correlati all'evento di traccia selezionato.  
  
6.  Fare clic sul punto desiderato nel grafico di monitoraggio di sistema. Verrà selezionata la riga di traccia corrispondente più prossima in termini di tempo. Per eseguire lo zoom avanti su un intervallo di tempo, premere e trascinare il puntatore del mouse nel grafico di monitoraggio di sistema.  
  
### <a name="to-create-performance-logs-that-can-be-shared-among-different-versions-of-windows"></a>Per creare registri di prestazioni da condividere tra versioni di Windows diverse  
  
1.  Nel Pannello di controllo aprire **Strumenti di amministrazione**e quindi fare doppio clic su **Prestazioni**.  
  
2.  Nella finestra di dialogo **Prestazioni** espandere il nodo **Avvisi e registri di prestazioni**, fare clic con il pulsante destro del mouse su **Registri contatori**e quindi fare clic su **Nuove impostazioni registro**.  
  
3.  Digitare un nome per il registro contatori e quindi fare clic su **OK**.  
  
4.  Nella scheda **Generale** fare clic su **Aggiungi contatori**.  
  
5.  Nell'elenco **Oggetto prestazione** selezionare l'oggetto prestazione che si desidera monitorare. I nomi degli oggetti prestazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per le istanze predefinite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] iniziano con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e le istanze denominate iniziano con MSSQL$*instanceName*.  
  
6.  Aggiungere il numero di contatori necessari per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in uso e altri valori importanti, ad esempio il tempo processore e il tempo disco.  
  
7.  Dopo aver completato questa operazione, fare clic su **Chiudi**.  
  
8.  Impostare i valori desiderati per l'intervallo **Campiona dati ogni** . Iniziare con un intervallo breve, ad esempio 5 minuti, e modificarlo quindi in modo adeguato se necessario.  
  
9. Nella scheda **File di log** scegliere **File di testo (delimitato da virgole)** nell'elenco **Tipo file registro** . I file di log in formato di testo delimitato da virgole possono essere condivisi tra versioni diverse di Windows e visualizzati successivamente in uno strumento per la creazione di report, ad esempio Microsoft Excel.  
  
10. Nella scheda **Pianificazione** specificare una pianificazione per il monitoraggio.  
  
11. Fare clic su **OK** . Verrà creato il registro di prestazioni.  
