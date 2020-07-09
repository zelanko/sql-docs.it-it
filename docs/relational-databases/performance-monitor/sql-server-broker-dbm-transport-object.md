---
title: Oggetto Trasporto Broker/DBM di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Broker / DBM Transport object
- SQLServer:Broker/DBM Transport
ms.assetid: eddb60b6-20a9-416c-adf3-4bc1687944fa
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: bf22e4f825d29a107f86fb486924b40da5af3752
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85787324"
---
# <a name="sql-server-broker---dbm-transport-object"></a>SQL Server, oggetto Trasporto Broker/DBM
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  L'oggetto prestazione **Trasporto Broker/DBM** include contatori delle prestazioni che contengono informazioni di rete per Service Broker e il mirroring del database. Nella tabella seguente sono elencati i contatori inclusi nell'oggetto.  
  
|Contatore Trasporto Broker/DBM di SQL Server|Descrizione|  
|------------------------------------------------|-----------------|  
|**Byte correnti I/O ricezione**|Questo contatore indica il numero di byte letti dalle operazioni correnti di ricezione del trasporto.|  
|**Byte correnti I/O invio**|Questo contatore indica il numero di byte nei frammenti di messaggi di cui è in corso l'invio in rete.|  
|**Frammenti messaggi correnti per I/O invio**|Questo contatore indica il numero totale di frammenti di messaggi di cui è in corso l'invio in rete.|  
|**Frammenti messaggi P1 inviati/sec**|Questo contatore indica il numero di frammenti di messaggi con priorità 1 inviati in rete al secondo.|  
|**Frammenti messaggi P2 inviati/sec**|Questo contatore indica il numero di frammenti di messaggi con priorità 2 inviati in rete al secondo.|  
|**Frammenti messaggi P3 inviati/sec**|Questo contatore indica il numero di frammenti di messaggi con priorità 3 inviati in rete al secondo.|  
|**Frammenti messaggi P4 inviati/sec**|Questo contatore indica il numero di frammenti di messaggi con priorità 4 inviati in rete al secondo.|  
|**Frammenti messaggi P5 inviati/sec**|Questo contatore indica il numero di frammenti di messaggi con priorità 5 inviati in rete al secondo.|  
|**Frammenti messaggi P6 inviati/sec**|Questo contatore indica il numero di frammenti di messaggi con priorità 6 inviati in rete al secondo.|  
|**Frammenti messaggi P7 inviati/sec**|Questo contatore indica il numero di frammenti di messaggi con priorità 7 inviati in rete al secondo.|  
|**Frammenti messaggi P8 inviati/sec**|Questo contatore indica il numero di frammenti di messaggi con priorità 8 inviati in rete al secondo.|  
|**Frammenti messaggi P9 inviati/sec**|Questo contatore indica il numero di frammenti di messaggi con priorità 9 inviati in rete al secondo.|  
|**Frammenti messaggi P10 inviati/sec**|Questo contatore indica il numero di frammenti di messaggi con priorità 10 inviati in rete al secondo.|  
|**Frammenti messaggi ricevuti/sec**|Questo contatore indica il numero di frammenti di messaggi ricevuti in rete al secondo.|   
|**Frammenti messaggi inviati/sec**|Questo contatore indica il numero di frammenti di messaggi di tutti i livelli di priorità inviati in rete al secondo.|  
|**Dimensioni medie frammenti messaggi ricevuti**|Questo contatore indica le dimensioni medie dei frammenti di messaggi ricevuti in rete.|  
|**Base dimensioni medie frammenti messaggi ricevuti**|Solo per uso interno.| 
|**Dimensioni medie frammenti messaggi inviati**|Questo contatore indica le dimensioni medie dei frammenti di messaggi inviati in rete.|  
|**Base dimensioni medie frammenti messaggi inviati**|Solo per uso interno.|
|**Conteggio connessioni aperte**|Questo contatore indica il numero di connessioni di rete aperte da Service Broker.|  
|**Byte in sospeso I/O ricezione**|Questo contatore indica il numero di byte contenuti nei frammenti di messaggi ricevuti dalla rete ma non ancora inseriti in una coda o scartati.|  
|**Byte in sospeso I/O invio**|Questo contatore indica il numero totale di byte nei frammenti di messaggi pronti per l'invio in rete.|  
|**Frammenti messaggi in sospeso per I/O ricezione**|Questo contatore indica il numero di frammenti di messaggi ricevuti dalla rete ma non ancora inseriti in una coda o scartati.|  
|**Frammenti messaggi in sospeso per I/O invio**|Questo contatore indica il numero totale di frammenti di messaggi pronti per l'invio in rete.|  
|**Byte I/O ricezione/sec**|Questo contatore indica il numero di byte al secondo ricevuti in rete dagli endpoint di Service Broker e dagli endpoint del mirroring del database.|  
|**Totale byte I/O ricezione**|Questo contatore indica il numero totale di byte ricevuti in rete dagli endpoint di Service Broker e dagli endpoint del mirroring del database.|  
|**Lunghezza media I/O ricezione**|Questo contatore indica il numero medio di byte per un'operazione di ricezione del trasporto.|  
|**Base lunghezza media I/O ricezione**|Solo per uso interno.|
|**I/O ricezione/sec**|Questo contatore indica il numero di operazioni di I/O di ricezione del trasporto al secondo completate dal livello di trasporto Service Broker/DBM. Si noti che un'operazione di ricezione del trasporto può includere più frammenti di messaggi.|  
|**Byte copie buffer I/O ricezione/sec**|Frequenza degli spostamenti di frammenti del buffer in memoria richiesti per le operazioni di I/O di ricezione del trasporto.|
|**Conteggio copie buffer I/O ricezione**|Numero di spostamenti di frammenti del buffer in memoria richiesti per le operazioni di I/O di ricezione del trasporto.| 
|**Byte I/O invio/sec**|Questo contatore indica il numero di byte al secondo inviati in rete dagli endpoint di Service Broker e dagli endpoint del mirroring del database.|   
|**Totale byte I/O invio**|Questo contatore indica il numero totale di byte inviati in rete dagli endpoint di Service Broker e dagli endpoint del mirroring del database.| 
|**Lunghezza media I/O invio**|Questo contatore indica le dimensioni medie in byte di ogni operazione di invio del trasporto. Si noti che un'operazione di invio del trasporto può includere più frammenti di messaggi.|  
|**Base lunghezza media I/O invio**|Solo per uso interno.|
|**I/O invio/sec**|Questo contatore indica il numero di operazioni di I/O di invio del trasporto al secondo completate. Si noti che un'operazione di invio del trasporto può includere più frammenti di messaggi.|  
  
## <a name="see-also"></a>Vedere anche  
 [sys.dm_broker_forwarded_messages &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-broker-forwarded-messages-transact-sql.md)   
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [Monitorare l'utilizzo delle risorse &#40;Monitor di sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
