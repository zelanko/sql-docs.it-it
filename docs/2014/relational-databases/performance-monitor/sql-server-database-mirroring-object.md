---
title: Oggetto Database Mirroring di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Database Mirroring
- database mirroring [SQL Server], performance counters
- performance counters [SQL Server], database mirroring
- Database Mirroring object
ms.assetid: a27b51ee-7637-4525-9424-bcc16947dc13
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 95d7bb5d1d071cab0c791a958a5e2f61fea41af5
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85038665"
---
# <a name="sql-server-database-mirroring-object"></a>Oggetto Database Mirroring di SQL Server
  L'oggetto prestazioni **SQLServer:Database Mirroring** include contatori delle prestazioni con informazioni sul mirroring del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Nella tabella seguente sono elencati i contatori inclusi nell'oggetto.  
  
|Nome|Descrizione|  
|----------|-----------------|  
|**Byte ricevuti/sec**|Numero di byte ricevuti al secondo.|  
|**Byte inviati/sec**|Numero di byte inviati al secondo.|  
|**Byte log ricevuti/sec**|Numero di byte di log ricevuti al secondo.|  
|**Byte log rollforward da cache/sec**|Numero di byte del log di cui è stato eseguito il rollforward ottenuti dalla cache del log di mirroring nell'ultimo secondo.<br /><br /> Questo contatore è utilizzato solo sul server mirror. Sul server principale il valore è sempre 0.|  
|**Byte log inviati da cache/sec**|Numero di byte del log inviati ottenuti dalla cache del log di mirroring nell'ultimo secondo.<br /><br /> Questo contatore è utilizzato solo sul server principale. Sul server mirror il valore è sempre 0.|  
|**Byte log inviati/sec**|Numero di byte di log inviati al secondo.|  
|**Byte log compressi ricev/sec**|Numero di byte di log compressi ricevuti nell'ultimo secondo.|  
|**Byte log compressi inviati/sec**|Numero di byte di log compressi inviati nell'ultimo secondo.|  
|**Tempo salvataggio log (ms)**|Millisecondi di attesa prima che i blocchi di log vengano salvati su disco nell'ultimo secondo.|  
|**KB log residui per rollback**|Kilobyte totali di log che devono ancora essere analizzati dal nuovo server mirror dopo il failover.<br /><br /> Questo contatore è utilizzato solo sul server mirror durante la fase di rollback. Al termine della fase di rollback il contatore viene reimpostato su 0. Sul server principale il valore è sempre 0.|  
|**KB log analizzati per rollback**|Kilobyte totali di log che sono stati analizzati dal nuovo server mirror dopo il failover.<br /><br /> Questo contatore è utilizzato solo sul server mirror durante la fase di rollback. Al termine della fase di rollback il contatore viene reimpostato su 0. Sul server principale il valore è sempre 0.|  
|**Tempo controllo flusso di invio log (ms)**|Millisecondi di attesa prima che i messaggi del flusso di log siano sottoposti a controllo del flusso di invio nell'ultimo secondo.<br /><br /> L'invio di dati e metadati del log al partner per il  mirroring è l'operazione che fa l'utilizzo di dati più intensivo. Utilizzare tale contatore per monitorare l'utilizzo di questo buffer da parte della sessione di mirroring del database.|  
|**KB coda invii log**|Numero totale di kilobyte di log non ancora inviati al server mirror.|  
|**Scrittura transazioni con mirroring/sec**|Numero di transazioni che hanno scritto nel database con mirroring e che vengono eseguite prima che il log venga inviato al mirror per eseguire il commit nell'ultimo secondo.<br /><br /> Questo contatore viene incrementato solo quando il server principale sta inviando attivamente record di log al server mirror.|  
|**Pagine inviate/sec**|Numero di pagine inviate al secondo.|  
|**Ricezioni/sec**|Numero di messaggi di mirroring ricevuti al secondo.|  
|**Byte rollforward/sec**|Numero di byte di log di cui viene eseguito il rollforward sul database mirror al secondo.|  
|**KB coda rollforward**|Numero totale di kilobyte di log salvato ancora da applicare al database mirror per eseguirne il rollforward. Viene inviato al principale dal mirror.|  
|**Tempo ACK invio/ricezione**|Millisecondi di attesa prima che i messaggi vengano riconosciuti dal partner nell'ultimo secondo.<br /><br /> Questo contatore è utile per diagnosticare un problema che potrebbe essere causato da un collo di bottiglia della rete, ad esempio failover inspiegabili, una lunga coda di invio o un'elevata latenza della transazione. In questi casi è possibile analizzare il valore di tale contatore per determinare se la causa del problema risiede nella rete.|  
|**Invii/sec**|Numero di messaggi di mirroring inviati al secondo.|  
|**Ritardo transazioni**|Periodo di attesa dell'acknowledgement per un commit senza terminazione.|  
  
> [!NOTE]  
>  Su ogni partner, alcuni dei contatori mostrano un valore zero in base al ruolo attualmente svolto dal partner.  
  
## <a name="remarks"></a>Osservazioni  
 I contatori delle prestazioni consentono di monitorare le prestazioni del mirroring del database. Ad esempio, è possibile esaminare il contatore **Ritardo transazioni** per verificare se il mirroring del database sta influenzando le prestazioni sul server principale. È possibile esaminare i contatori **Coda rollforward** e **Coda invii log** per verificare se il database mirror è in grado di mantenersi aggiornato rispetto al database principale. Il contatore **Byte log inviati/sec** consente di monitorare il numero di eventi di log inviati al secondo.  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare l'utilizzo delle risorse &#40;Monitor di sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  
