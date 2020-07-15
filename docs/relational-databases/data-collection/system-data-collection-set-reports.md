---
title: Report per i set di raccolta dati di sistema | Microsoft Docs
description: L'agente di raccolta dati fornisce un report per ogni set di raccolta dati di sistema per il monitoraggio della capacità e delle prestazioni del sistema in SQL Server.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- data collector [SQL Server], server activity
- server activity [SQL Server]
- reports [SQL Server], data collection
- reports [SQL Server], disk usage
- collection sets [SQL Server], reports
- data collector [SQL Server], reports
- reports [SQL Server], query statistics
- query statistics reports [SQL Server]
- disk usage reports [SQL Server]
ms.assetid: 0b126b8d-4fe7-443d-8a9a-c266350181e5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 34992877bd226fd62df290e5d196fdf1a667f031
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85715542"
---
# <a name="system-data-collection-set-reports"></a>Report per i set di raccolta dati di sistema
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  L'agente di raccolta dati fornisce un report cronologico per ognuno dei set di raccolta dati di sistema. Ognuno dei report seguenti utilizza i dati archiviati nel data warehouse di gestione:  
  
-   [Riepilogo utilizzo disco](#Disk)  
  
-   [Cronologia statistiche query](#Query)  
  
-   [Cronologia attività server](#Server)  
  
 È possibile utilizzare questi report per ottenere informazioni per il monitoraggio della capacità del sistema e la risoluzione dei problemi relativi alle prestazioni.  
  
##  <a name="disk-usage-summary-report"></a><a name="Disk"></a> Report Riepilogo utilizzo disco  
 Il report Riepilogo utilizzo disco contiene dati sull'utilizzo dello spazio su disco per tutti i database nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. I dati forniti nei report vengono ottenuti usando il set di raccolta Utilizzo disco, che usa il tipo di agente di raccolta Query T-SQL generico.  
  
 È possibile accedere al report Riepilogo utilizzo disco da Esplora oggetti. Per visualizzare il report, espandere la cartella **Gestione** , fare clic con il pulsante destro del mouse su **Raccolta dati**, scegliere **Report**, **Data warehouse di gestione**, quindi fare clic su **Riepilogo utilizzo disco**. Per altre informazioni, vedere [Visualizzare un report sui set di raccolta &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-a-collection-set-report-sql-server-management-studio.md).  
  
### <a name="disk-usage-collection-set-report"></a>Report del set di raccolta Utilizzo disco  
 Il report del set di raccolta Utilizzo disco fornisce una panoramica dello spazio su disco utilizzato per tutti i database nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e le tendenze di incremento per i file di dati e di log di ognuno di questi database.  
  
-   Nella tabella di riepilogo vengono visualizzate le dimensioni iniziali (in megabyte) e le dimensioni correnti per tutti i database installati nel server monitorato dall'agente di raccolta dati.  
  
-   Le informazioni sulle tendenze e l'incremento medio vengono visualizzate sia in formato grafico che numerico per i file di dati e di log.  
  
#### <a name="disk-usage-collection-set---database-database_name-subreport"></a>Sottoreport del set di raccolta Utilizzo disco - Database: <database_name>  
 Il sottoreport del set di raccolta Utilizzo disco - Database: *<nome_database>* viene visualizzato quando si fa clic su una linea di tendenza per un database o un file di log specifico nella tabella di riepilogo del report del set di raccolta Utilizzo disco. Il report include una rappresentazione grafica delle tendenze di incremento relative all'utilizzo dello spazio su disco per il periodo del report. Le informazioni sull'utilizzo del disco sono organizzate e riportate in base a spazio utilizzato, spazio dati, spazio non allocato e spazio degli indici per i file di dati, nonché in base a spazio utilizzato e spazio inutilizzato per i file di log.  
  
 Nella tabella al di sotto del grafico sono indicati gli orari di raccolta dati e i corrispondenti dati di utilizzo.  
  
#### <a name="disk-usage-for-database-database_name-subreport"></a>Sottoreport Utilizzo disco per database: <database_name>  
 Il sottoreport **Utilizzo disco per database:** _<nome_database>_ viene visualizzato quando si fa clic sul nome di un database nella tabella di riepilogo del report del set di raccolta Utilizzo disco. In questo report viene fornita una suddivisione grafica e numerica dello spazio utilizzato dai file di dati e dai file di log delle transazioni del database. Lo spazio utilizzato per i file di dati è suddiviso in categorie relative a percentuale di spazio allocato alle pagine di indice, spazio non allocato, spazio allocato alle pagine di dati e spazio inutilizzato. Queste categorie sono definite come segue:  
  
|Category|Definizione|  
|--------------|----------------|  
|Indice|Quantità di spazio su disco utilizzato per contenere le pagine di indice.|  
|Non allocato|Quantità di spazio su disco disponibile per il database ma non ancora allocato a un oggetto.|  
|Data|Quantità di spazio su disco utilizzato dalle pagine di dati.|  
|Non utilizzato|Quantità di spazio su disco allocato a uno o più oggetti ma non ancora utilizzato.|  
  
 Lo spazio utilizzato per il file di log delle transazioni è suddiviso in categorie relative a spazio utilizzato e spazio inutilizzato.  
  
 Se nel database si verificano eventi di aumento automatico e compattazione automatica, tali eventi verranno riportati sia per i file di dati che per i file di log. Nel report vengono visualizzate l'ora di inizio e la durata di ogni evento e la modifica risultante nelle dimensioni dei file.  
  
 Viene riportato lo spazio su disco utilizzato da ogni file di dati nel database. Lo spazio riportato come Spazio riservato è la quantità di spazio utilizzato più lo spazio allocato al file ma non ancora utilizzato. Lo spazio indicato da Spazio utilizzato corrisponde allo spazio effettivo utilizzato dal file, ad esclusione dello spazio allocato.  
  
##  <a name="query-statistics-history-report"></a><a name="Query"></a> Report Cronologia statistiche query  
 Il report Cronologia statistiche query contiene le statistiche di esecuzione della query. I dati utilizzati in questo report vengono ottenuti tramite il set di raccolta Statistiche query, che utilizza il tipo di agente di raccolta Attività query.  
  
 È possibile accedere al report Cronologia statistiche query da Esplora oggetti. Per visualizzare il report, espandere la cartella **Gestione** , fare clic con il pulsante destro del mouse su **Raccolta dati**, scegliere **Report**, **Data warehouse di gestione**, quindi fare clic su **Cronologia statistiche query**. Per altre informazioni, vedere [Visualizzare un report sui set di raccolta &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-a-collection-set-report-sql-server-management-studio.md).  
  
### <a name="selecting-data-to-include-in-the-report"></a>Selezione dei dati da includere nel report  
 Il report include le statistiche di esecuzione della query per tutto il periodo di raccolta dei dati. Sono disponibili due modi per spostarsi nella cronologia della raccolta dati per selezionare un segmento dei dati da visualizzare.  
  
 **Pulsanti di controllo e navigazione della sequenza temporale**  
  
 Utilizzare i pulsanti di controllo e navigazione della sequenza temporale per spostarsi all'intero della sequenza temporale o per selezionare un intervallo di date. I pulsanti freccia consentono lo scorrimento a sinistra e a destra per spostarsi avanti e indietro nella sequenza temporale. Per impostazione predefinita, le frecce consentono di spostarsi nella sequenza temporale con incrementi di 4 ore. Usando i pulsanti di ingrandimento e riduzione è possibile espandere o ridurre l'incremento del tempo impostando uno dei valori seguenti: 15 minuti, 1 ora, 4 ore, 12 ore o 24 ore. L'intervallo di tempo attualmente selezionato è indicato dalla parte evidenziata della sequenza temporale e viene visualizzato nel testo al di sotto della sequenza temporale. I valori e i dati del report vengono aggiornati quando si fa clic sulla sequenza temporale o si utilizzano i pulsanti di navigazione.  
  
 **Pulsante calendario**  
  
 Utilizzare il pulsante calendario per specificare la data e l'ora di inizio nonché la durata dei dati per cui si desidera creare il report.  
  
#### <a name="query-statistics-history-report"></a>Report Cronologia statistiche query  
 Nel grafico Prime query per tempo CPU totale viene indicato il costo relativo di ciascuna query per l'intervallo di tempo selezionato in base all'utilizzo totale della CPU. Per visualizzare una vista diversa del costo relativo della query, fare clic su uno dei collegamenti ipertestuali disponibili sotto il grafico: **Durata**, **Totale I/O**, **Letture fisiche** o **Scritture logiche**.  
  
 Nella tabella al di sotto del grafico vengono forniti ulteriori dati sulle query. Viene riportato il testo per ogni query per cui è stato creato un grafico, insieme alle informazioni statistiche dettagliate. Si noti che le barre del grafico sono collegamenti attivi, come ciascuna delle query incluse nella tabella. Facendo clic su un collegamento attivo si apre il sottoreport Dettagli query per la query.  
  
#### <a name="query-details-subreport"></a>Sottoreport Dettagli query  
 Nel sottoreport Dettagli query viene fornito il testo completo della query. Accanto alla query è disponibile un collegamento ipertestuale **Modifica testo query** . È possibile fare clic su questo collegamento per aprire la query nell'editor di query. Nella tabella al di sotto della query sono incluse le statistiche di esecuzione della query, ad esempio la durata media per ogni esecuzione della query.  
  
 Vengono visualizzati un grafico dei piani di query e la durata media per ogni esecuzione. Per visualizzare una vista diversa del costo relativo del piano di query, fare clic su uno dei collegamenti ipertestuali disponibili sotto il grafico: **Durata**, **Letture fisiche** o **Scritture logiche**. La linea del grafico è attiva ed è possibile fare clic su un punto qualsiasi per aprire il sottoreport Dettagli piano query.  
  
 Nella tabella al di sotto del grafico vengono visualizzati i primi 10 piani di query in base all'utilizzo della CPU per esecuzione. Ogni numero nella colonna **N. piano** è un collegamento attivo su cui è possibile fare clic per aprire il sottoreport Dettagli piano query.  
  
#### <a name="query-plan-details-subreport"></a>Sottoreport Dettagli piano query  
 In questo report vengono visualizzate le informazioni per un piano di query. Oltre a consentire di modificare la query e di visualizzare le statistiche di esecuzione, il report fornisce informazioni dettagliate sul piano di query. Il collegamento ipertestuale **Visualizza piano di esecuzione query in formato grafico** consente di aprire una rappresentazione grafica del piano di esecuzione per la query corrente.  
  
## <a name="server-activity-history-report"></a>Report Cronologia attività server  
 Il report Cronologia attività server contiene i dati relativi all'utilizzo delle risorse e alle attività del server per il server e per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. I dati forniti in questo report vengono raccolti dal set di raccolta Attività server che usa il tipo di agente di raccolta Query T-SQL generico e il tipo di agente di raccolta Contatori delle prestazioni.  
  
 È possibile accedere al report Cronologia attività server da Esplora oggetti. Per visualizzare il report, espandere la cartella **Gestione** , fare clic con il pulsante destro del mouse su **Raccolta dati**, scegliere **Report**, **Data warehouse di gestione**, quindi fare clic su **Cronologia attività server**. Per altre informazioni, vedere [Visualizzare un report sui set di raccolta &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-a-collection-set-report-sql-server-management-studio.md).  
  
### <a name="selecting-data-to-include-in-the-report"></a>Selezione dei dati da includere nel report  
 Il report include le attività del server per tutto il periodo di raccolta dei dati. Sono disponibili due modi per spostarsi nella cronologia della raccolta dati per selezionare un segmento dei dati da visualizzare.  
  
 **Pulsanti di controllo e navigazione della sequenza temporale**  
  
 Utilizzare i pulsanti di controllo e navigazione della sequenza temporale per spostarsi all'intero della sequenza temporale o per selezionare un intervallo di date. I pulsanti freccia consentono lo scorrimento a sinistra e a destra per spostarsi avanti e indietro nella sequenza temporale. Per impostazione predefinita, le frecce consentono di spostarsi nella sequenza temporale con incrementi di 4 ore. Usando i pulsanti di ingrandimento e riduzione è possibile espandere o ridurre l'incremento del tempo impostando uno dei valori seguenti: 15 minuti, 1 ora, 4 ore, 12 ore o 24 ore. L'intervallo di tempo attualmente selezionato è indicato dalla parte evidenziata della sequenza temporale e viene visualizzato nel testo al di sotto della sequenza temporale. I valori e i dati del report vengono aggiornati quando si fa clic sulla sequenza temporale o si utilizzano i pulsanti di navigazione.  
  
 **Pulsante calendario**  
  
 Utilizzare il pulsante calendario per specificare la data e l'ora di inizio nonché la durata dei dati per cui si desidera creare il report.  
  
###  <a name="server-activity-history-report"></a><a name="Server"></a> Report Cronologia attività server  
 Nel report Cronologia attività server viene illustrata la vista iniziale dell'attività del server per un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e per il sistema operativo host.  
  
 Nella tabella seguente vengono descritti i grafici che tracciano l'attività di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e del sistema nel report e i sottoreport dettagliati a cui è possibile accedere tramite i grafici.  
  
|Grafico|Descrizione del report|  
|-----------|------------------------|  
|% CPU|È possibile accedere a questi sottoreport facendo clic su qualsiasi punto delle linee del grafico di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o del sistema nel grafico % CPU.<br /><br /> **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** : Il report Cronologia statistiche query fornisce un grafico delle query che richiedono il maggior numero di risorse nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nella tabella al di sotto del grafico sono indicate le query e vengono inclusi i dati statistici per ogni query. È possibile fare clic su una query per ottenere ulteriori dettagli.<br /><br /> **Sistema**: Il report Utilizzo CPU sistema fornisce un grafico della percentuale di tempo della CPU per processore e i dati statistici per ogni processo in formato tabulare.|  
|Utilizzo della memoria|È possibile accedere a questi sottoreport facendo clic su qualsiasi punto delle linee del grafico di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o del sistema nel grafico Utilizzo memoria.<br /><br /> **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** : Il report Utilizzo memoria [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornisce i grafici relativi all'utilizzo di memoria dei processi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ai contatori di memoria e al consumo di memoria interno per tipo, nonché una tabella contenente i dati sulla quantità di memoria utilizzata in media per tipo di componente.<br /><br /> **Sistema**: Il report Utilizzo memoria sistema fornisce i grafici relativi alle percentuali di utilizzo di memoria, di riscontri nella cache e di accessi alle pagine, nonché una tabella contenente informazioni sul working set e i byte privati per ogni processo.|  
|Utilizzo I/O disco|È possibile accedere a questi sottoreport facendo clic su qualsiasi punto delle linee del grafico di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o del sistema nel grafico Utilizzo I/O disco.<br /><br /> **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** : Il report Utilizzo I/O disco [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornisce i grafici relativi al tempo di risposta del disco e alla velocità di trasferimento del disco. In un'altra tabella vengono fornite le statistiche dei file virtuali per disco, database e file.<br /><br /> **Sistema**: Il report Utilizzo dischi sistema fornisce i grafici relativi al tempo di risposta del disco, alla lunghezza media della coda dei dischi e alla velocità di trasferimento del disco, nonché una tabella contenente le informazioni sulle operazioni di lettura e scrittura I/O per ogni processo.|  
|Utilizzo rete|Non sono disponibili report aggiuntivi.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Attese|Nel grafico Attese [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono visualizzate le attese rilevate dai thread eseguiti per categoria di attesa. È possibile accedere a un report dettagliato facendo clic su qualsiasi segmento del grafico. Oltre a fornire statistiche di attesa per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in formato grafico in un intervallo di tempo più ridotto, questo report include informazioni sulle categorie di attesa in formato tabella. Per ogni categoria, ad esempio la CPU e le relative sottocategorie, la tabella include il numero di attese, il tempo di attesa e la percentuale di tempo di attesa totale.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Attività|È possibile accedere ai diversi aspetti dell'attività di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dal grafico Attività di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Di seguito vengono indicati i report che è possibile ottenere facendo clic su un punto della linea del grafico Compilazioni SQL/sec:<br /><br /> <br /><br /> Connessioni e sessioni<br /><br /> Requests<br /><br /> Percentuale riscontri cache piano<br /><br /> Caratteristiche TempDb|  
  
## <a name="see-also"></a>Vedere anche  
 [Raccolta dati](../../relational-databases/data-collection/data-collection.md)   
 [Visualizzare un report sui set di raccolta &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-a-collection-set-report-sql-server-management-studio.md)  
  
  
