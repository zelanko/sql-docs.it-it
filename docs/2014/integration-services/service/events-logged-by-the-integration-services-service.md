---
title: Eventi registrati dal servizio Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- service [Integration Services], events
- events [Integration Services], service
- Integration Services service, events
ms.assetid: d4122dcf-f16f-47a0-93a2-ffa3d0d4f9cf
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: dedffe0f30c62399e4d694f7ee1bf5247222e87d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62889273"
---
# <a name="events-logged-by-the-integration-services-service"></a>Eventi registrati dal servizio Integration Services
  Quando l'esecuzione del servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] viene avviata, arrestata o quando si verificano determinati problemi, vengono registrati vari messaggi di evento nel registro eventi applicazioni di Windows.  
  
 In questo argomento vengono fornite informazioni sui messaggi di evento comuni registrati dal servizio nel registro eventi applicazioni. Il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] registra tutti i messaggi descritti in questo argomento con un'origine evento di SQLISService.  
  
 Per informazioni generali sul servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vedere [Servizio Integration Services &#40;servizio SSIS&#41;](integration-services-service-ssis-service.md).  
  
## <a name="messages-about-the-status-of-the-service"></a>Messaggi relativi allo stato del servizio  
 Quando si seleziona [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per l'installazione, viene installato e avviato il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e l'opzione Tipo di avvio è impostata su Automatico.  
  
|ID evento|Nome simbolico|Text|Note|  
|--------------|-------------------|----------|-----------|  
|256|DTS_MSG_SERVER_STARTING|È in corso l'avvio del servizio [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)].|Il servizio sta per essere avviato.|  
|257|DTS_MSG_SERVER_STARTED|Servizio [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] avviato.|Il servizio è stato avviato.|  
|260|DTS_MSG_SERVER_START_FAILED|Impossibile avviare il servizio [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)].%nErrore: %1|Non è stato possibile avviare il servizio. L'impossibilità di avviare il servizio potrebbe dipendere da un'installazione danneggiata o da un account del servizio non corretto.|  
|258|DTS_MSG_SERVER_STOPPING|È in corso l'arresto del servizio [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)].%n%nArresta tutti i pacchetti in esecuzione all'uscita: %1|Il servizio sta per essere arrestato e, se la configurazione lo prevede, verranno arrestati tutti i pacchetti in esecuzione. È possibile impostare un valore True o False nel file di configurazione per specificare se arrestare i pacchetti in esecuzione quando viene arrestato il servizio. Nel messaggio relativo a questo evento è incluso il valore di questa impostazione.|  
|259|DTS_MSG_SERVER_STOPPED|Servizio [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] arrestato.%nVersione server %1|Il servizio è stato arrestato.|  
  
## <a name="messages-about-the-configuration-file"></a>Messaggi relativi al file di configurazione  
 Le impostazioni per il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] vengono archiviate in un file XML che è possibile modificare. Per altre informazioni, vedere [Configurazione del servizio Integration Services &#40;servizio SSIS&#41;](../configuring-the-integration-services-service-ssis-service.md).  
  
|ID evento|Nome simbolico|Text|Note|  
|--------------|-------------------|----------|-----------|  
|274|DTS_MSG_SERVER_MISSING_CONFIG_REG|Servizio [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)]: %nL'impostazione del Registro di sistema che specifica il file di configurazione non esiste. %nVerrà eseguito un tentativo di caricamento del file di configurazione predefinito.|La voce del Registro di sistema che contiene il percorso del file di configurazione non esiste o è vuota.|  
|272|DTS_MSG_SERVER_MISSING_CONFIG|Il file di configurazione del servizio [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] non esiste.%nIl servizio verrà caricato con le impostazioni predefinite.|Il file di configurazione non esiste nel percorso specificato.|  
|273|DTS_MSG_SERVER_BAD_CONFIG|Il file di configurazione del servizio [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] non è corretto.%nErrore durante la lettura del file di configurazione:%1%n%nIl servizio verrà caricato con le impostazioni predefinite.|Non è possibile leggere il file di configurazione o il file non è valido. Questo errore potrebbe essere determinato da un errore di sintassi di XML nel file.|  
  
## <a name="other-messages"></a>Altri messaggi  
  
|ID evento|Nome simbolico|Text|Note|  
|--------------|-------------------|----------|-----------|  
|336|DTS_MSG_SERVER_STOPPING_PACKAGE|Servizio [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)]: è in corso l'arresto del pacchetto in esecuzione.%nID istanza pacchetto: %1%nID pacchetto: %2%nNome pacchetto: %3%nDescrizione pacchetto: %4%nPacchetto|Il servizio sta tentando di arrestare l'esecuzione di un pacchetto. È possibile monitorare e arrestare i pacchetti in esecuzione in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Per altre informazioni su come gestire i pacchetti in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], vedere [Gestione dei pacchetti &#40;servizio SSIS&#41;](package-management-ssis-service.md).|  
  
## <a name="related-tasks"></a>Attività correlate  
 Per informazioni su come visualizzare le voci di log, vedere [Visualizzazione delle voci di log nella finestra Registra eventi](../view-log-entries-in-the-log-events-window.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Eventi registrati da un pacchetto di Integration Services](../performance/events-logged-by-an-integration-services-package.md)  
  
  
