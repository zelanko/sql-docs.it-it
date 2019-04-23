---
title: Operazioni di backup e ripristino per Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- databases [Reporting Services], backing up
- databases [Reporting Services], restoring
- databases [Reporting Services], moving
- backing up databases [Reporting Services]
- moving databases
- restoring databases [Reporting Services]
- files [Reporting Services], restoring
- files [Reporting Services], backing up
ms.assetid: 157bc376-ab72-4c99-8bde-7b12db70843a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a11b10ae1403911c7593e9f6cccd21d1fdb8fd16
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59934347"
---
# <a name="backup-and-restore-operations-for-reporting-services"></a>Operazioni di backup e ripristino per Reporting Services
  In questo argomento viene fornita una panoramica di tutti i file di dati utilizzato in un'installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e viene descritto quando e come è necessario eseguire il backup dei file. Lo sviluppo di un piano di backup e ripristino per i file dei database del server di report rappresenta la parte più importante di una strategia di recupero. Una strategia di recupero più completa include tuttavia i backup delle chiavi di crittografia, di estensioni o assembly personalizzati, dei file di configurazione e dei file di origine di report e modelli.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] | Modalità SharePoint di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]   
  
 Le operazioni di backup e ripristino vengono spesso utilizzate per spostare un'installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o parte di essa:  
  
-   Se si stanno spostando solo i database del server di report, è possibile utilizzare il backup e il ripristino oppure eseguire il collegamento e lo scollegamento per spostare i database in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diversa. Per altre informazioni, vedere [Spostamento di database del server di report in un altro computer &#40;modalità nativa SSRS&#41;](../report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md).  
  
-   Lo spostamento di un'installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in un nuovo computer viene definito migrazione. In caso di migrazione di un'installazione, eseguire il programma di installazione per installare una nuova istanza del server di report e quindi copiare i dati dell'istanza in un nuovo computer. Per ulteriori informazioni sulla migrazione di un'installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , vedere gli argomenti seguenti:  
  
    -   [Eseguire l'aggiornamento e la migrazione di Reporting Services](upgrade-and-migrate-reporting-services.md)  
  
    -   [Migrazione di un'installazione di Reporting Services in modalità SharePoint](migrate-a-reporting-services-installation-sharepoint-mode.md)  
  
    -   [Eseguire la migrazione di un'installazione di Reporting Services &#40;modalità nativa&#41;](migrate-a-reporting-services-installation-native-mode.md)  
  
## <a name="backing-up-the-report-server-databases"></a>Backup dei database del server di report  
 Poiché un server di report è un server senza stato, tutti i dati delle applicazioni vengono archiviati nei database **reportserver** e **reportservertempdb** in esecuzione su un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . È possibile eseguire il backup dei database **reportserver** e **reportservertempdb** usando uno dei metodi supportati per il backup dei database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per i database del server di report, tenere presenti le seguenti indicazioni:  
  
-   Per il backup del database **reportserver** , usare il modello di recupero con registrazione completa.  
  
-   Per il backup del database **reportservertempdb** , usare il modello di recupero con registrazione minima.  
  
-   Per ogni database, è possibile utilizzare diverse pianificazioni di backup. È consigliabile eseguire il backup del database **reportservertempdb** solo per non doverlo ricreare nel caso in cui si verifichi un errore hardware. Nel caso di un errore hardware, non è necessario recuperare i dati di **reportservertempdb**, ma è necessaria la struttura della tabella. Se il database **reportservertempdb**viene perso, l'unico modo per recuperarlo consiste nel ricreare il database del server di report. Se si ricrea il database **reportservertempdb**, è importante assegnare lo stesso nome del database del server di report principale.  
  
 Per altre informazioni sul backup e il ripristino dei database relazionali di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vedere [Backup e ripristino di database SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md).  
  
> [!IMPORTANT]  
>  Se il server di report [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] è in modalità SharePoint, è necessario occuparsi di altri database, tra cui i database di configurazione di SharePoint e il database di avvisi di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . In modalità SharePoint vengono creati tre database per ciascuna applicazione di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] : **reportserver**, **reportservertempdb**e **dataalerting** . Per altre informazioni, vedere [Eseguire il backup e il ripristino di applicazioni di servizio SharePoint di Reporting Services](../backup-and-restore-reporting-services-sharepoint-service-applications.md)  
  
## <a name="backing-up-the-encryption-keys"></a>Backup delle chiavi di crittografia  
 Quando si configura un'installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per la prima volta, è consigliabile eseguire il backup delle chiavi di crittografia. È inoltre consigliabile eseguire il backup delle chiavi ogni volta che si modifica l'identità degli account di servizio o si rinomina il computer. Per altre informazioni, vedere [Eseguire il backup e il ripristino delle chiavi di crittografia di Reporting Services](ssrs-encryption-keys-back-up-and-restore-encryption-keys.md). Per i server di report in modalità SharePoint, vedere la sezione "Gestione chiavi" in [Gestire un'applicazione di servizio SharePoint di Reporting Services](../manage-a-reporting-services-sharepoint-service-application.md).  
  
## <a name="backing-up-the-configuration-files"></a>Backup dei file di configurazione  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa i file di configurazione per archiviare le impostazioni dell'applicazione. È consigliabile eseguire il backup dei file quando si configura il server per la prima volta e dopo avere distribuito eventuali estensioni personalizzate. I file di cui eseguire il backup includono:  
  
-   RSReportServer.config  
  
-   Rssvrpolicy.config  
  
-   Rsmgrpolicy.config  
  
-   Reportingservicesservice.exe.config  
  
-   Web.config per entrambe le applicazioni [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] del server di report e Gestione report.  
  
-   Machine.config per [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]  
  
## <a name="backing-up-data-files"></a>Backup dei file di dati  
 Eseguire il backup dei file creati e gestiti in Progettazione report e in Progettazione modelli. Tra questi sono inclusi i file di definizione del report (con estensione rdl), i file modello di report (con estensione smdl), i file delle origini dei dati condivise (con estensione rds), i file di visualizzazione dei dati (con estensione dv), i file dell'origine dati (con estensione ds), i file di progetto del server di report (con estensione rptproj) e i file di soluzione di report (con estensione sln).  
  
 Ricordarsi di eseguire il backup di eventuali file script, con estensione rss, creati per attività di amministrazione o di distribuzione.  
  
 Verificare di avere una copia di backup per tutte le estensioni e gli assembly personalizzati utilizzati.  
  
## <a name="see-also"></a>Vedere anche  
 [Database del server di report &#40;modalità nativa SSRS&#41;](../report-server/report-server-database-ssrs-native-mode.md)   
 [File di configurazione di Reporting Services](../report-server/reporting-services-configuration-files.md)   
 [Utilità rskeymgmt &#40;SSRS&#41;](../tools/rskeymgmt-utility-ssrs.md)   
 [Copiare database tramite backup e ripristino](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)   
 [Amministrare un database del server di report &#40;modalità nativa SSRS&#41;](../report-server/administer-a-report-server-database-ssrs-native-mode.md)   
 [Configurare e gestire chiavi di crittografia &#40;Gestione configurazione SSRS&#41;](ssrs-encryption-keys-manage-encryption-keys.md)  
  
  
