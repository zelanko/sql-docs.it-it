---
title: Oggetto Broker Statistics di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Broker Statistics
- Broker Statistics object
ms.assetid: e9e36f01-93f6-4e6e-90c6-c7f3fd121737
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 77a6174931924c30b8d482c0bd5d3f4a358f4a10
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67987018"
---
# <a name="sql-server-broker-statistics-object"></a>Oggetto Statistiche Broker di SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Nell'oggetto prestazione SQLServer:Statistiche Broker sono inclusi contatori delle prestazioni che contengono informazioni generali su [!INCLUDE[ssSB](../../includes/sssb-md.md)] per un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Nella tabella seguente sono elencati i contatori inclusi nell'oggetto:  
  
|Contatori dell'oggetto Statistiche Broker di SQL Server|Descrizione|  
|-------------------------------------------|-----------------|  
|**Totale errori di attivazione**|Numero di volte in cui una stored procedure di attivazione di [!INCLUDE[ssSB](../../includes/sssb-md.md)] termina con un errore.|  
|**Rollback transazioni Broker**|Numero di transazioni di cui è stato eseguito il rollback contenenti istruzioni DML correlate a [!INCLUDE[ssSB](../../includes/sssb-md.md)], ad esempio SEND e RECEIVE.|  
|**Totale messaggi danneggiati**|Numero di messaggi danneggiati ricevuti dall'istanza.|  
|**Messaggi rimossi da coda di trasmissione/sec**|Numero di messaggi rimossi dalla coda di trasmissione di [!INCLUDE[ssSB](../../includes/sssb-md.md)] al secondo.|  
|**Conteggio eventi timer dialogo**|Numero di timer attivi nel livello del protocollo di dialogo. Tale numero corrisponde al numero di dialoghi attivi.|  
|**Totale messaggi rimossi**|Numero di messaggi ricevuti dall'istanza, ma recapitato a una coda.|  
|**Totale messaggi locali accodati**|Numero di messaggi inseriti nelle code dell'istanza, conteggiando solo quelli che non sono stati recapitati attraverso la rete.|  
|**Messaggi locali accodati/sec**|Numero di messaggi al secondo inseriti nelle code dell'istanza, conteggiando solo quelli che non sono stati recapitati attraverso la rete.|  
|**Totale messaggi accodati**|Numero totale di messaggi inseriti nelle code dell'istanza.|  
|**Messaggi accodati/sec**|Numero di messaggi al secondo inseriti nelle code dell'istanza. Sono inclusi i messaggi di tutti i livelli di priorità.|  
|**Messaggi P1 accodati/sec**|Numero di messaggi con priorità 1 inseriti nelle code dell'istanza al secondo.|  
|**Messaggi P2 accodati/sec**|Numero di messaggi con priorità 2 inseriti nelle code dell'istanza al secondo.|  
|**Messaggi P2 accodati/sec**|Numero di messaggi con priorità 3 inseriti nelle code dell'istanza al secondo.|  
|**Messaggi P4 accodati/sec**|Numero di messaggi con priorità 4 inseriti nelle code dell'istanza al secondo.|  
|**Messaggi P5 accodati/sec**|Numero di messaggi con priorità 5 inseriti nelle code dell'istanza al secondo.|  
|**Messaggi P6 accodati/sec**|Numero di messaggi con priorità 6 inseriti nelle code dell'istanza al secondo.|  
|**Messaggi P7 accodati/sec**|Numero di messaggi con priorità 7 inseriti nelle code dell'istanza al secondo.|  
|**Messaggi P8 accodati/sec**|Numero di messaggi con priorità 8 inseriti nelle code dell'istanza al secondo.|  
|**Messaggi P9 accodati/sec**|Numero di messaggi con priorità 9 inseriti nelle code dell'istanza al secondo.|  
|**Messaggi P10 accodati/sec**|Numero di messaggi con priorità 10 inseriti nelle code dell'istanza al secondo.|  
|**Messaggi inseriti in coda di trasmissione/sec**|Numero di messaggi inseriti nella coda di trasmissione di [!INCLUDE[ssSB](../../includes/sssb-md.md)] al secondo.|  
|**Totale frammenti messaggi trasporto accodati**|Numero di frammenti di messaggi inseriti nelle code dell'istanza, conteggiando solo i messaggi recapitati correttamente attraverso la rete.|  
|**Frammenti messaggi trasporto accodati/sec**|Numero di frammenti di messaggi al secondo inseriti nelle code dell'istanza.|  
|**Totale messaggi trasporto accodati**|Numero di messaggi inseriti nelle code dell'istanza, conteggiando solo quelli recapitati correttamente attraverso la rete.|  
|**Messaggi trasporto accodati/sec**|Numero di messaggi al secondo inseriti nelle code dell'istanza, conteggiando solo quelli recapitati correttamente attraverso la rete.|  
|**Totale messaggi inoltrati**|Numero totale di messaggi di [!INCLUDE[ssSB](../../includes/sssb-md.md)] inoltrati dal computer.|  
|**Messaggi inoltrati/sec**|Numero di messaggi al secondo inoltrati dal computer.|  
|**Totale byte messaggi inoltrati**|Dimensioni totali, in byte, dei messaggi inoltrati dal computer.|  
|**Byte messaggi inoltrati/sec**|Dimensioni, in byte, dei messaggi al secondo inoltrati dal computer.|  
|**Totale messaggi inoltrati scartati**|Numero di messaggi ricevuti dal computer per l'inoltro, che tuttavia non è stato eseguito correttamente.|  
|**Messaggi inoltrati scartati/sec**|Numero di messaggi al secondo ricevuti dal computer per l'inoltro, che tuttavia non è stato eseguito correttamente.|  
|**Byte messaggi inoltrati in sospeso**|Dimensioni totali dei messaggi attualmente in attesa di inoltro.|  
|**Conteggio messaggi inoltrati in sospeso**|Numero totale di messaggi attualmente in attesa di inoltro.|  
|**Totale SQL RECEIVE**|Numero totale di istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] RECEIVE elaborate.|  
|**SQL RECEIVE/sec**|Numero di istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] RECEIVE elaborate al secondo.|  
|**Totale SQL SEND**|Numero totale di istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] SEND eseguite.|  
|**SQL SEND/sec**|Numero di istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] SEND eseguite al secondo.|  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [Monitorare l'utilizzo delle risorse &#40;Monitor di sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
