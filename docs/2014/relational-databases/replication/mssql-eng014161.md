---
title: MSSQL_ENG014161 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014161 error
ms.assetid: 4b983e76-bb77-43c5-b44b-19919d3da619
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5624b58f95ca6a5f47af6269a2bd4cbc6a30033b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52758193"
---
# <a name="mssqleng014161"></a>MSSQL_ENG014161
    
## <a name="message-details"></a>Dettagli messaggio  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|14161|  
|Origine evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbolico||  
|Testo del messaggio|È stata impostata la soglia [%s:%s] per la pubblicazione [%s]. Verificare che l'agente di lettura log e l'agente di distribuzione siano in esecuzione e siano in grado di rispettare i requisiti relativi alla latenza.|  
  
## <a name="explanation"></a>Spiegazione  
 La replica consente di attivare avvisi per numerose condizioni, tra cui il superamento di una latenza specificata per sottoscrizioni transazionali. Per latenza si intende l'intervallo di tempo che intercorre tra il commit di una modifica dei dati nel server di pubblicazione e il commit della modifica corrispondente nel Sottoscrittore.  
  
 Quando si attiva un avviso utilizzando Monitoraggio replica o [sp_replmonitorchangepublicationthreshold](/sql/relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql), viene specificata una soglia che determina quando è generato l'avviso. Quando tale soglia viene raggiunta o superata, viene visualizzato un avviso in Monitoraggio replica e viene registrato un evento nel registro eventi di Windows. Il raggiungimento di una soglia può inoltre generare un avviso SQL Server Agent. Per altre informazioni, vedere [Impostare valori di soglia e avvisi in Monitoraggio replica](monitor/set-thresholds-and-warnings-in-replication-monitor.md) e [Monitorare la replica a livello di programmazione](monitor/monitoring-replication-overview.md).  
  
## <a name="user-action"></a>Azione dell'utente  
 Se una sottoscrizione supera una soglia di latenza, è necessario stabilire se il fenomeno dipende da un problema di prestazioni del sistema o se la soglia deve essere regolata. Dopo avere configurato la replica, sviluppare dati di riferimento per le prestazioni in modo da poter stabilire il comportamento della replica in presenza del carico di lavoro tipico delle applicazioni e della topologia in uso. Includere nei dati di riferimento anche la latenza al fine di poter impostare un valore appropriato per la soglia.  
  
 Se il valore soglia è appropriato ma viene superato, è necessario individuare l'area del sistema a cui è dovuto il collo di bottiglia a livello di prestazioni. Per ulteriori informazioni sul monitoraggio e la risoluzione dei problemi delle prestazioni di replica, vedere gli argomenti seguenti:  
  
-   [Misurare la latenza e convalidare le connessioni per la replica transazionale](monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  
-   [Monitorare le prestazioni con Monitoraggio replica](monitor/monitor-performance-with-replication-monitor.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a errori ed eventi &#40;replica&#41;](errors-and-events-reference-replication.md)  
  
  
