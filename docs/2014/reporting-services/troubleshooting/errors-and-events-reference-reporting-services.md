---
title: Guida di riferimento a errori ed eventi (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- messages [Reporting Services]
- errors [Reporting Services]
- Reporting Services, errors and events
- troubleshooting [Reporting Services], errors
- events [Reporting Services]
ms.assetid: 818b4cc1-e65d-4f1a-bf7d-fe269e6dd739
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2708c2609d23c6094cd69bddd08d958a85262d88
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66099322"
---
# <a name="errors-and-events-reference-reporting-services"></a>Guida di riferimento a errori ed eventi (Reporting Services)
  In questo argomento vengono fornite informazioni sugli errori e sugli eventi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Anche i file di log di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] contengono informazioni sugli errori. Per altre informazioni sui tipi di file di log disponibili e sulla modalità di visualizzazione di tali file, vedere [File di log e origini di Reporting Services](../report-server/reporting-services-log-files-and-sources.md).  
  
## <a name="cause-and-resolution-for-reporting-services-error-messages"></a>Causa e risoluzione dei messaggi di errore di Reporting Services  
 Sono disponibili informazioni sulla causa e sulla risoluzione degli errori per i quali vengono eseguite con maggiore frequenza ricerche nei siti Web [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Per altre informazioni, vedere [Causa e risoluzione degli errori di Reporting Services](cause-and-resolution-of-reporting-services-errors.md).  
  
## <a name="report-server-events"></a>Eventi del server di report  
 Gli eventi del server di report riportati di seguito vengono registrati nel registro applicazioni di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
|ID evento|Type|Category|`Source`|Descrizione|  
|--------------|----------|--------------|------------|-----------------|  
|106|Errore|Pianificazione|Server di report|Quando si definisce un'operazione pianificata, ad esempio la sottoscrizione e il recapito di report, deve essere in esecuzione SQL Server Agent.|  
|[107](../../relational-databases/errors-events/mssqlserver-107-database-engine-error.md)|Errore|Avvio/Chiusura|Server di report<br /><br /> Elaborazione pianificazione e recapito|*\<Origine>* non è in grado di connettersi al database del server di report. Per altre informazioni, vedere [Servizio Windows ReportServer &#40;MSSQLServer&#41; 107](../../relational-databases/errors-events/mssqlserver-107-database-engine-error.md).|  
|108|Errore|Estensione|Server di report<br /><br /> Gestione report|*\<Origine>* non è in grado di caricare un'estensione per il recapito, l'elaborazione dati o il rendering.<br /><br /> L'errore è probabilmente dovuto al mancato completamento della distribuzione o alla rimozione di un'estensione. Per altre informazioni, vedere [Distribuzione di un’estensione per l’elaborazione dati](../extensions/data-processing/deploying-a-data-processing-extension.md) e [Distribuzione di un’estensione per il recapito](../extensions/delivery-extension/deploying-a-delivery-extension.md).|  
|109|Informazioni|Gestione|Server di report<br /><br /> Gestione report|Un file di configurazione è stato modificato. Per altre informazioni, vedere [File di configurazione di Reporting Services](../report-server/reporting-services-configuration-files.md).|  
|110|Avviso|Gestione|Server di report<br /><br /> Gestione report|Un'impostazione in uno dei file di configurazione è stata modificata in modo da non risultare più valida. Verrà utilizzato un valore predefinito. Per altre informazioni, vedere [File di configurazione di Reporting Services](../report-server/reporting-services-configuration-files.md).|  
|111|Errore|Registrazione|Server di report<br /><br /> Gestione report|*\<Source>* non è in grado di creare il log di traccia. Per altre informazioni, vedere [Report Server Service Trace Log](../report-server/report-server-service-trace-log.md).|  
|112|Avviso|Sicurezza|Server di report|Nel server di report è stato rilevato un possibile attacco Denial of Service. Per altre informazioni, vedere [Sicurezza e protezione di Reporting Services](../security/reporting-services-security-and-protection.md).|  
|113|Errore|Registrazione|Server di report|Il server di report non è in grado di creare un contatore delle prestazioni.|  
|114|Errore|Avvio/Chiusura|Gestione report|Gestione report non è in grado di connettersi al servizio del server di report.|  
|115|Avviso|Pianificazione|Elaborazione pianificazione e recapito|Un'attività pianificata nella coda di SQL Server Agent è stata modificata o eliminata.|  
|116|Errore|Interno|Server di report<br /><br /> Gestione report<br /><br /> Elaborazione pianificazione e recapito|Si è verificato un errore interno.|  
|117|Errore|Avvio/Chiusura|Server di report|La versione del database del server di report non è valida.|  
|118|Avviso|Registrazione|Server di report<br /><br /> Gestione report|Il log di traccia non è disponibile nel percorso di directory previsto. Verrà creato un nuovo log di traccia nella directory predefinita. Per altre informazioni, vedere [Report Server Service Trace Log](../report-server/report-server-service-trace-log.md).|  
|119|Errore|Attivazione|Server di report<br /><br /> Elaborazione pianificazione e recapito|*\<Source>* non ha l'autorizzazione per l'accesso al contenuto del database del server di report.|  
|120|Errore|Attivazione|Server di report|Impossibile decrittografare la chiave simmetrica. È stato probabilmente modificato l'account con cui viene eseguito il servizio. Per altre informazioni, vedere [Configurare e gestire chiavi di crittografia &#40;Gestione configurazione SSRS&#41;](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md).|  
|121|Errore|Avvio/Chiusura|Server di report|Impossibile avviare il servizio RPC (Remote Procedure Call).|  
|122|Avviso|Recapito|Elaborazione pianificazione e recapito|Elaborazione pianificazione e recapito non è in grado di connettersi al server SMTP utilizzato per il recapito della posta elettronica. Per altre informazioni sulle connessioni server SMTP, vedere [configurare un Server di Report per il recapito tramite posta elettronica &#40;Gestione configurazione SSRS&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md).|  
|123|Avviso|Registrazione|Server di report<br /><br /> Gestione report|Il server di report non è stato in grado di scrivere nel log di traccia. Per altre informazioni sui log di traccia, vedere [Log di traccia del servizio del server di report](../report-server/report-server-service-trace-log.md).|  
|124|Informazioni|Attivazione|Server di report|Il servizio del server di report è stato inizializzato. Per altre informazioni, vedere [Inizializzare un server di report &#40;Gestione configurazione SSRS&#41;](../install-windows/ssrs-encryption-keys-initialize-a-report-server.md).|  
|125|Informazioni|Attivazione|Server di report|La chiave utilizzata per la crittografia dei dati è stata estratta. Per altre informazioni sulle chiavi, vedere [Configurare e gestire chiavi di crittografia &#40;Gestione configurazione SSRS&#41;](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md).|  
|126|Informazioni|Attivazione|Server di report|La chiave utilizzata per la crittografia dei dati è stata applicata. Per altre informazioni sulle chiavi, vedere [Configurare e gestire chiavi di crittografia &#40;Gestione configurazione SSRS&#41;](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md).|  
|127|Informazioni|Attivazione|Server di report|Il contenuto crittografato è stato rimosso dal database del server di report. Per altre informazioni sull'eliminazione di dati crittografati non recuperabili, vedere [Configurare e gestire chiavi di crittografia &#40;Gestione configurazione SSRS&#41;](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md).|  
|128|Errore|Attivazione|Server di report|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Impossibile utilizzare contemporaneamente componenti appartenenti a edizioni diverse di|  
|129|Errore|Gestione|Server di report<br /><br /> Elaborazione pianificazione e recapito|Impossibile decrittografare un'impostazione crittografata nel file di configurazione.|  
|130|Errore|Gestione|Server di report<br /><br /> Elaborazione pianificazione e recapito|*\<Origine>* non è in grado di trovare il file di configurazione. I file di configurazione sono necessari per il server di report.|  
|131|Errore|Sicurezza|Server di report<br /><br /> Elaborazione pianificazione e recapito|Impossibile decrittografare un valore di dati utente crittografato.|  
|132|Errore|Sicurezza|Server di report|Errore durante l'operazione di crittografia dei dati utente. Impossibile salvare il valore.|  
|133|Errore|Gestione|Server di report<br /><br /> Gestione report<br /><br /> Elaborazione pianificazione e recapito|Impossibile caricare un file di configurazione. Questo errore potrebbe essere dovuto a codice XML non valido.|  
|134|Errore|Gestione|Server di report|Il server di report non è stato in grado di crittografare i valori per un'impostazione in un file di configurazione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare le sottoscrizioni di Reporting Services](../subscriptions/monitor-reporting-services-subscriptions.md)   
 [File di log e origini di Reporting Services](../report-server/reporting-services-log-files-and-sources.md)  
  
  
