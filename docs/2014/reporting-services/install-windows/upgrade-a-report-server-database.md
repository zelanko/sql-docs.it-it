---
title: Aggiornare un database del server di report | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- upgrading databases
- report server database
- upgrading Reporting Services
ms.assetid: 4091cf87-9d97-4048-a393-67f1f9207401
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e3ba4d9ee2e0b92617c2d2bcadae3bf87c8b5414
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108634"
---
# <a name="upgrade-a-report-server-database"></a>Aggiornare un database del server di report
  Il database del server di report fornisce archiviazione per una o più istanze del server di report. Poiché lo schema del database del server di report può essere modificato con ogni nuova versione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], è necessario che la versione del database corrisponda alla versione dell'istanza del server di report in uso. Nella maggior parte dei casi, un database del server di report può essere aggiornato automaticamente senza alcun intervento dell'utente.  
  
 **Modalità nativa:** In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] modalità nativa, il database del server di report è costituito in realtà da due database i cui nomi predefiniti sono "ReportServer e ReportServerTempDB".  
  
 **Modalità SharePoint:** In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] modalità SharePoint il database del server di report è in realtà una raccolta di database creata per ogni istanza dell' [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] applicazione di servizio.  
  
## <a name="ways-to-upgrade-a-native-mode-report-server-database"></a>Modalità di aggiornamento di un database del server di report in modalità nativa  
 Nell'elenco seguente sono incluse le condizioni necessarie per l'aggiornamento di un database del server di report:  
  
-   
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Il programma di installazione aggiorna una singola istanza di un server di report. Lo schema del database del server di report viene quindi aggiornato automaticamente dopo l'avvio del servizio e il server di report determina che la versione dello schema del database non corrisponde alla versione del server.  
  
     All'avvio del servizio, il server di report verifica che la versione dello schema del database corrisponda alla versione del server. Se la versione dello schema del database è precedente, il database viene aggiornato automaticamente alla versione dello schema richiesta dal server di report. La funzionalità di aggiornamento automatico è particolarmente utile se è stato ripristinato o collegato un database del server di report meno recente. Nel file del log di traccia del server di report viene immesso un messaggio indicante che è stato eseguito l'aggiornamento della versione dello schema del database.  
  
-   Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aggiorna un database del server di report locale o remoto quando si seleziona una versione precedente da usare con un'istanza del server di report più recente. In questo caso, è necessario confermare l'azione di aggiornamento prima che si verifichi.  
  
     In Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non è più disponibile un pulsante Aggiorna separato o uno script di aggiornamento. Queste funzionalità sono obsolete a partire da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a causa della funzionalità di aggiornamento automatico del servizio del server di report.  
  
 Al termine dell'aggiornamento dello schema, non sarà possibile eseguire il rollback dell'aggiornamento a una versione precedente. Eseguire sempre il backup del database del server di report qualora sia necessario ricreare un'installazione precedente.  
  
## <a name="how-the-schema-metadata-and-report-server-content-is-updated"></a>Modalità di aggiornamento di schema, metadati e contenuto del server di report  
 Il database del server di report viene aggiornato in tre fasi:  
  
1.  Lo schema viene aggiornato automaticamente dopo l'installazione e l'avvio del servizio o quando si seleziona un database del server di report della modalità nativa di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , che è una versione precedente. Il servizio del server di report, inoltre, verifica la versione del database all'avvio. Se il server di report è connesso a un database di una versione precedente, il server di report aggiornerà il database durante l'avvio.  
  
2.  I descrittori di sicurezza vengono aggiornati al primo utilizzo del database del server di report dopo l'aggiornamento dello schema.  
  
3.  I report pubblicati e gli snapshot dei report compilati vengono aggiornati al primo utilizzo. Per altre informazioni, vedere [Upgrade Reports](upgrade-reports.md).  
  
 Oltre al database del server di report, un server di report utilizza anche un database temporaneo. Il database temporaneo viene aggiornato automaticamente durante l'aggiornamento del database del server di report.  
  
## <a name="permissions-required-to-upgrade-a-report-server-database"></a>Autorizzazioni richieste per aggiornare un database del server di report  
 Se si sta aggiornando un'installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] che include un database del server di report, potrebbe essere visualizzato un messaggio di errore se l'aggiornamento del database viene eseguito con autorizzazioni insufficienti. Per impostazione predefinita, nel programma di installazione viene utilizzato il token di sicurezza dell'utente che sta eseguendo il programma di installazione per connettersi all'istanza remota di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e aggiornare lo schema. Se si hanno le autorizzazioni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **sysadmin** permissions on the database server that hosts the report server databases, the database upgrade will succeed. Allo stesso modo, se si esegue il programma di installazione dal prompt dei comandi e si specificano gli argomenti RSUPGRADEDATABASEACCOUNT e RSUPGRADEPASSWORD per un account che ha l'autorizzazione **sysadmin** per modificare lo schema nel computer remoto, l'aggiornamento del database avrà esito positivo.  
  
 Se invece non si ha l'autorizzazione **sysadmin** per il database nel computer remoto, la connessione verrà rifiutata con l'errore seguente:  
  
 `"Setup was not able to upgrade the report server database schema. You must update the database schema manually after setup is finished. To update the schema, run the Reporting Services Configuration Manager, open the Database Setup page, re-select the database, and click Apply. The database will be upgraded automatically."`  
  
 A questo punto verranno aggiornati i file di programma del server di report, ma il database del server di report manterrà il formato della versione precedente. Il server di report non sarà disponibile finché non si completa il processo di aggiornamento aggiornando manualmente il database.  
  
#### <a name="to-upgrade-a-native-mode-database-with-scripts"></a>Per aggiornare un database in modalità nativa con gli script  
 È possibile utilizzare script WMI per aggiornare un database del server di report. Per altre informazioni, vedere [Metodo GenerateDatabaseUpgradeScript &#40;WMI MSReportServer_ConfigurationSetting&#41;](../wmi-provider-library-reference/configurationsetting-method-generatedatabaseupgradescript.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [Creare un database del server di report &#40;Gestione configurazione SSRS&#41;](../../sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md)   
 [Procedura guidata Cambia database &#40;modalità nativa SSRS&#41;](../../sql-server/install/change-database-wizard-ssrs-native-mode.md)   
 [Aggiornare ed eseguire la migrazione Reporting Services](upgrade-and-migrate-reporting-services.md)   
 [Eseguire la migrazione di un'installazione di Reporting Services &#40;modalità nativa&#41;](migrate-a-reporting-services-installation-native-mode.md)  
  
  
