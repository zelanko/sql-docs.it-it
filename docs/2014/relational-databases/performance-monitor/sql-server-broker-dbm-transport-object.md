---
title: Oggetto di trasporto di SQL Server, Service Broker e mirroring del database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Broker / DBM Transport object
- SQLServer:Broker/DBM Transport
ms.assetid: eddb60b6-20a9-416c-adf3-4bc1687944fa
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b0347c7f7e19ae5500f8c5be100ef2d0dc663784
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63250726"
---
# <a name="sql-server-broker-and-dbm-transport-object"></a>Oggetto Trasporto Broker/mirroring del database di SQL Server
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
|**Dimensioni medie invio frammenti di messaggi**|Questo contatore indica le dimensioni medie dei frammenti di messaggi inviati in rete.|  
|**Frammenti messaggi inviati/sec**|Questo contatore indica il numero di frammenti di messaggi di tutti i livelli di priorità inviati in rete al secondo.|  
|**Frammenti messaggi ricevuti/sec**|Questo contatore indica il numero di frammenti di messaggi ricevuti in rete al secondo.|  
|**Dimensioni medie frammenti messaggi ricevuti**|Questo contatore indica le dimensioni medie dei frammenti di messaggi ricevuti in rete.|  
|**Conteggio connessioni aperte**|Questo contatore indica il numero di connessioni di rete aperte da Service Broker.|  
|**Byte in sospeso I/O ricezione**|Questo contatore indica il numero di byte contenuti nei frammenti di messaggi ricevuti dalla rete ma non ancora inseriti in una coda o scartati.|  
|**Byte in sospeso I/O invio**|Questo contatore indica il numero totale di byte nei frammenti di messaggi pronti per l'invio in rete.|  
|**Frammenti messaggi in sospeso per I/O ricezione**|Questo contatore indica il numero di frammenti di messaggi ricevuti dalla rete ma non ancora inseriti in una coda o scartati.|  
|**Frammenti messaggi in sospeso per I/O invio**|Questo contatore indica il numero totale di frammenti di messaggi pronti per l'invio in rete.|  
|**Totale byte I/O ricezione**|Questo contatore indica il numero totale di byte ricevuti in rete dagli endpoint di Service Broker e dagli endpoint del mirroring del database.|  
|**Byte I/O ricezione/sec**|Questo contatore indica il numero di byte al secondo ricevuti in rete dagli endpoint di Service Broker e dagli endpoint del mirroring del database.|  
|**Lunghezza media I/O ricezione**|Questo contatore indica il numero medio di byte per un'operazione di ricezione del trasporto.|  
|**Ricevere i/o al secondo**|Questo contatore indica il numero di operazioni di I/O di ricezione del trasporto al secondo completate dal livello di trasporto Service Broker/DBM. Si noti che un'operazione di ricezione del trasporto può includere più frammenti di messaggi.|  
|**Totale byte I/O invio**|Questo contatore indica il numero totale di byte inviati in rete dagli endpoint di Service Broker e dagli endpoint del mirroring del database.|  
|**Byte I/O invio/sec**|Questo contatore indica il numero di byte al secondo inviati in rete dagli endpoint di Service Broker e dagli endpoint del mirroring del database.|  
|**Lunghezza media I/O invio**|Questo contatore indica le dimensioni medie in byte di ogni operazione di invio del trasporto. Si noti che un'operazione di invio del trasporto può includere più frammenti di messaggi.|  
|**I/O invio/sec**|Questo contatore indica il numero di operazioni di I/O di invio del trasporto al secondo completate. Si noti che un'operazione di invio del trasporto può includere più frammenti di messaggi.|  
  
## <a name="see-also"></a>Vedere anche  
 [sys.dm_broker_forwarded_messages &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-broker-forwarded-messages-transact-sql)   
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [Monitorare l'utilizzo delle risorse &#40;Monitor di sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  
