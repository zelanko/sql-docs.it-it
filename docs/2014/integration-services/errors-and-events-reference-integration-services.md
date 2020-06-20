---
title: Guida di riferimento a errori ed eventi (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, events
- events [Integration Services]
- errors [Integration Services]
- Integration Services, errors
ms.assetid: cf4f0f14-8087-42d7-9b67-e4929228abd6
author: janinezhang
ms.author: janinez
ms.openlocfilehash: f26689dde5f840eb0e23d9506272056574969003
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84966936"
---
# <a name="errors-and-events-reference-integration-services"></a>Guida di riferimento a errori ed eventi (Integration Services)
  In questa sezione della documentazione vengono fornite informazioni su diversi errori ed eventi correlati a [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Sono inoltre incluse le informazioni sulle cause e la risoluzione dei messaggi di errore.  
  
 Per altre informazioni sui messaggi di errore di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , incluso un elenco della maggior parte degli errori di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e le rispettive descrizioni, vedere [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md). Nell'elenco, tuttavia, non sono incluse informazioni per la risoluzione dei problemi.  
  
> [!IMPORTANT]  
>  Molti dei messaggi di errore visualizzati quando si usa [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] provengono da altri componenti, tra cui provider OLE DB, altri componenti di database come [!INCLUDE[ssDE](../includes/ssde-md.md)] e [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o altri servizi o componenti, come il file system, il server SMTP o Microsoft Message Queuing. Per informazioni su questi messaggi di errore esterni, vedere la documentazione specifica del componente.  
  
## <a name="error-messages"></a>messaggi di errore  
  
|Nome simbolico dell'errore|Descrizione|  
|----------------------------|-----------------|  
|DTS_E_CACHELOADEDFROMFILE|Indica che non è possibile eseguire il pacchetto perché una trasformazione cache sta tentando di scrivere dati nella cache in memoria. Tuttavia, un file di cache è già stato caricato nella cache in memoria tramite una gestione connessione della cache.|  
|DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER|Indica che il pacchetto non può essere eseguito perché non è stato possibile stabilire una connessione specificata.|  
|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMN|Indica che un componente flusso di dati sta tentando di passare dati stringa Unicode a un altro componente per cui sono previsti dati non Unicode nella colonna corrispondente, o viceversa.|  
|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMNS|Indica che un componente flusso di dati sta tentando di passare dati stringa Unicode a un altro componente per cui sono previsti dati non Unicode nella colonna corrispondente, o viceversa.|  
|DTS_E_CANTINSERTCOLUMNTYPE|Indica che non è possibile aggiungere la colonna alla tabella di database perché la conversione tra il tipo di dati della colonna di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e il tipo di dati della colonna del database non è supportata.|  
|DTS_E_CONNECTIONNOTFOUND|Indica che il pacchetto non può essere eseguito perché non è possibile trovare la gestione connessione specificata.|  
|DTS_E_CONNECTIONREQUIREDFORMETADATA|Indica che per recuperare metadati nuovi o aggiornati per un'origine o una destinazione, è necessaria una connessione tra Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] e un'origine dati, ma questa connessione non può essere eseguita correttamente.|  
|DTS_E_MULTIPLECACHEWRITES|Indica che non è possibile eseguire il pacchetto perché una trasformazione cache sta tentando di scrivere dati nella cache in memoria. È tuttavia possibile che con un'altra trasformazione cache sia già stata effettuata una scrittura nella cache in memoria.|  
|DTS_E_PRODUCTLEVELTOLOW|Indica che non è possibile eseguire il pacchetto perché non è installata la versione corretta di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].|  
|DTS_E_READNOTFILLEDCACHE|Indica che una trasformazione Ricerca sta tentando di leggere dati dalla cache in memoria contemporaneamente al tentativo di scrittura dei dati nella cache da parte di una trasformazione cache.|  
|DTS_E_UNPROTECTXMLFAILED|Indica che il sistema non ha decrittografato un nodo XML protetto.|  
|DTS_E_WRITEWHILECACHEINUSE|Indica che una trasformazione cache sta tentando di scrivere dati nella cache in memoria contemporaneamente al tentativo di lettura dei dati da tale cache da parte di una trasformazione Ricerca.|  
|DTS_W_EXTERNALMETADATACOLUMNSOUTOFSYNC|Indica che i metadati della colonna nell'origine dati non corrispondono a quelli del componente di origine o di destinazione connesso all'origine dati.|  
  
## <a name="events-sqlispackage"></a>Eventi (SQLISPackage)  
 Per altre informazioni, vedere [Eventi registrati da un pacchetto di Integration Services](performance/events-logged-by-an-integration-services-package.md).  
  
|Event|Descrizione|  
|-----------|-----------------|  
|SQLISPackage_12288|Indica che un pacchetto è stato avviato.|  
|SQLISPackage_12289|Indica che l'esecuzione di un pacchetto è stata completata correttamente.|  
|SQLISPACKAGE_12291|Indica che l'esecuzione di un pacchetto è stata arrestata e non è stata completata.|  
|SQLISPackage_12546|Indica che l'esecuzione di un'attività o di un altro file eseguibile in un pacchetto è stata completata.|  
|SQLISPackage_12549|Indica che è stato generato un messaggio di avviso in un pacchetto.|  
|SQLISPackage_12550|Indica che è stato generato un messaggio di errore in un pacchetto.|  
|SQLISPackage_12551|Indica che un pacchetto è stato arrestato e non ha eseguito le operazioni previste.|  
|SQLISPackage_12557|Indica il completamento dell'esecuzione di un pacchetto.|  
  
## <a name="events-sqlisservice"></a>Eventi (SQLISService)  
 Per altre informazioni, vedere [Eventi registrati dal servizio Integration Services](service/events-logged-by-the-integration-services-service.md).  
  
|Event|Descrizione|  
|-----------|-----------------|  
|SQLISService_256|Indica che il servizio sta per essere avviato.|  
|SQLISService_257|Indica che il servizio è stato avviato.|  
|SQLISService_258|Indica che il servizio sta per essere arrestato.|  
|SQLISService_259|Indica che il servizio è stato arrestato.|  
|SQLISService_260|Indica un tentativo non riuscito di avviare il servizio.|  
|SQLISService_272|Indica che il file di configurazione non esiste nel percorso specificato.|  
|SQLISService_273|Indica che non è stato possibile leggere il file di configurazione o che tale file non è valido.|  
|SQLISService_274|Indica che la voce del Registro di sistema che contiene il percorso del file di configurazione non esiste o è vuota.|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
