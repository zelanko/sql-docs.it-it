---
title: Database del server di report (modalità nativa) | Microsoft Docs
ms.date: 06/06/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- databases [Reporting Services]
- report servers [Reporting Services], databases
- temporary databases [Reporting Services]
- report server database
- reportservertempdb
- reportserver database
ms.assetid: 0fc5c033-3fe1-4cea-86c7-66ea5e424d65
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 71207cc3476374c457ab72aa03e54215b38330ba
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "77078013"
---
# <a name="report-server-database-ssrs-native-mode"></a>Database del server di report (modalità nativa SSRS)
  Un server di report è un server senza stato che usa il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di [!INCLUDE[ssDE](../../includes/ssde-md.md)] per archiviare le definizioni dei metadati e degli oggetti. In un'installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità nativa vengono usati due database per separare i requisiti per l'archiviazione persistente dei dati da quelli per l'archiviazione temporanea. I database vengono creati assieme e associati in base al nome. Per impostazione predefinita, i nomi dei database sono rispettivamente **ReportServer** e **ReportServerTempDB**.  
  
 Un'installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità SharePoint crea anche un database per la funzionalità relativa agli avvisi dei dati. I tre database in modalità SharePoint sono associati alle applicazioni di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Per altre informazioni, vedere [Gestire un'applicazione di servizio SharePoint di Reporting Services](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)  
  
 I database possono essere eseguiti in istanze locali o remote del [!INCLUDE[ssDE](../../includes/ssde-md.md)] . La scelta di un'istanza locale può essere utile se sono disponibili risorse di sistema sufficienti o si desidera utilizzare un numero inferiore di licenze software, ma l'esecuzione dei database in un computer remoto consente di ottenere migliori prestazioni.  
  
 È possibile trasferire o riutilizzare un database del server di report esistente di un'installazione precedente o un'istanza diversa con un'altra istanza del server di report. Lo schema del database del server di report deve essere compatibile con l'istanza del server di report. Se il formato del database è obsoleto, verrà richiesto di eseguire l'aggiornamento al formato corrente. Le versioni più recenti non sono compatibili con una versione precedente. Se è disponibile un database del server di report più recente, non è possibile usarlo con una versione precedente di un'istanza del server di report. Per altre informazioni sulla modalità di aggiornamento dei database del server di report ai formati più recenti, vedere [Aggiornare un database del server di report](../../reporting-services/install-windows/upgrade-a-report-server-database.md).  
  
> [!IMPORTANT]  
> La struttura della tabella per i database è ottimizzata per le operazioni server e non deve essere modificata né regolata. [!INCLUDE[msCoName](../../includes/msconame-md.md)] potrebbe modificare la struttura della tabella da una versione a quella successiva. La modifica o l'estensione del database può impedire o limitare la possibilità di eseguire aggiornamenti o applicare service pack in futuro. Modificando o estendendo il database, inoltre, si potrebbero introdurre modifiche che impediscono il corretto funzionamento del server di report. Ad esempio se si abilita READ_COMMITTED_SNAPSHOT sul database ReportServer, si interromperà la funzionalità dell'ordinamento interattiva.  
  
 Tutti gli accessi a un database del server di report devono essere gestiti tramite il server di report. Per accedere al contenuto di un database del server di report, è possibile usare gli strumenti di gestione del server di report, ad esempio il portale Web e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] oppure interfacce programmatiche, ad esempio l'accesso tramite URL, il servizio Web ReportServer o il provider WMI (Strumentazione gestione Windows).  
  
 La connessione al database del server di report viene in genere definita tramite Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . È tuttavia possibile definire la connessione nel corso dell'installazione se si decide di installare la configurazione predefinita. Per altre informazioni sulla connessione del server di report al database, vedere [Configurare una connessione del database del server di report &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
## <a name="report-server-database"></a>Database del server di report  
 Il database del server di report è un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui è archiviato il contenuto seguente:  
  
-   Gli elementi gestiti da un server di report (report e report collegati, origini dei dati condivise, modelli di report, cartelle e risorse) e tutte le impostazioni di proprietà e sicurezza associate a tali elementi.  
  
-   Definizioni della sottoscrizione e della pianificazione.  
  
-   Snapshot del report (che includono i risultati della query) e la cronologia del report.  
  
-   Proprietà di sistema e impostazioni di sicurezza di sistema.  
  
-   Dati del log di esecuzione del report.  
  
-   Chiavi simmetriche, connessione crittografata e credenziali per le origini dei dati del report.  
  
 Nel database del server di report vengono archiviati lo stato dell'applicazione e dati persistenti, pertanto è consigliabile creare una pianificazione di backup del database per evitare perdite di dati. Per consigli e istruzioni su come eseguire il backup del database, vedere [Spostamento di database del server di report in un altro computer &#40;modalità nativa SSRS&#41;](../../reporting-services/report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md).  
  
## <a name="report-server-temporary-database"></a>Database temporaneo del server di report  
 Ogni database del server di report utilizza un database temporaneo per archiviare i dati delle sessioni e dell'esecuzione, le tabelle di lavoro e i report memorizzati nella cache, generati dal server di report. Tramite i processi server in background vengono periodicamente rimossi gli elementi meno recenti e inutilizzati dalle tabelle nel database temporaneo.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non ricrea il database temporaneo, se assente, né ripristina le tabelle mancanti o modificate. Anche se il database temporaneo non contiene dati persistenti, è necessario eseguire comunque una copia di backup del database per evitare di doverlo ricreare in caso di operazioni di recupero da errori.  
  
 Se si esegue il backup del database temporaneo e successivamente lo si ripristina, è necessario eliminare il contenuto. In genere è opportuno eliminare sempre il contenuto del database temporaneo, ma in questo caso è necessario riavviare il servizio Windows ReportServer dopo l'eliminazione del contenuto.  
  
## <a name="see-also"></a>Vedere anche  
 [Ospitare un database del server di report in un cluster di failover di SQL Server](../../reporting-services/install-windows/host-a-report-server-database-in-a-sql-server-failover-cluster.md)   
 [Archiviare i dati crittografati del server di report &#40;Gestione configurazione SSRS &#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Reporting Services Report Server](../../reporting-services/report-server-sharepoint/reporting-services-report-server.md)   
 [Amministrare un database del server di report &#40;modalità nativa SSRS&#41;](../../reporting-services/report-server/administer-a-report-server-database-ssrs-native-mode.md)   
 [Creare un database del server di report &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md)   
 [Operazioni di backup e ripristino per Reporting Services](../../reporting-services/install-windows/backup-and-restore-operations-for-reporting-services.md)  
  