---
title: Oggetto Batch Resp Statistics di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Batch Resp Statistics
ms.assetid: a58e8733-6a8d-4b47-b5cb-042e813d808a
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 87045f104bdf183c91c3b60b0d85c4a64929359e
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "67987198"
---
# <a name="sql-server-batch-resp-statistics-object"></a>SQL Server, Oggetto Batch Resp Statistics
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
L'oggetto prestazioni **SQLServer:Batch Resp Statistics** fornisce i contatori per tenere traccia dei tempi di risposta dei batch di SQL Server.

La tabella seguente descrive gli oggetti prestazioni **Batch Resp Statistics** di SQL Server.


|**Contatori di SQL Server Batch Resp Statistics**|Descrizione|  
|-------------|-----------------|  
|**Batch >=000000ms e \<000001ms**|Numero di batch SQL con tempi di risposta maggiori o uguali a 0 ms ma minori di 1 ms|
|**Batch >=000001ms e \<000002ms**|Numero di batch SQL con tempi di risposta maggiori o uguali a 1 ms ma minori di 2 ms|
|**Batch >=000002ms e \<000005ms**|Numero di batch SQL con tempi di risposta maggiori o uguali a 2 ms ma minori di 5 ms|
|**Batch >=000005ms e \<000010ms**|Numero di batch SQL con tempi di risposta maggiori o uguali a 5 ms ma minori di 10 ms|
|**Batch >=000010ms e \<000020ms**|Numero di batch SQL con tempi di risposta maggiori o uguali a 10 ms ma minori di 20 ms|
|**Batch >=000020ms e \<000050ms**|Numero di batch SQL con tempi di risposta maggiori o uguali a 20 ms ma minori di 50 ms|
|**Batch >=000050ms e \<000100ms**|Numero di batch SQL con tempi di risposta maggiori o uguali a 50 ms ma minori di 100 ms|
|**Batch >=000100ms e \<000200ms**|Numero di batch SQL con tempi di risposta maggiori o uguali a 100 ms ma minori di 200 ms|
|**Batch >=000200ms e \<000500ms**|Numero di batch SQL con tempi di risposta maggiori o uguali a 200 ms ma minori di 500 ms|
|**Batch >=000500ms e \<001000ms**|Numero di batch SQL con tempi di risposta maggiori o uguali a 500 ms ma minori di 1.000 ms|
|**Batch >=001000ms e \<002000ms**|Numero di batch SQL con tempi di risposta maggiori o uguali a 1.000 ms ma minori di 2.000 ms|
|**Batch >=002000ms e \<005000ms**|Numero di batch SQL con tempi di risposta maggiori o uguali a 2.000 ms ma minori di 5.000 ms|
|**Batch >=005000ms e \<010000ms**|Numero di batch SQL con tempi di risposta maggiori o uguali a 5000 ms ma minori di 10.000 ms|
|**Batch >=010000ms e \<020000ms**|Numero di batch SQL con tempi di risposta maggiori o uguali a 10.000 ms ma minori di 20.000 ms|
|**Batch >=020000ms e \<050000ms**|Numero di batch SQL con tempi di risposta maggiori o uguali a 20.000 ms ma minori di 50.000 ms|
|**Batch >=050000ms e \<100000ms**|Numero di batch SQL con tempi di risposta maggiori o uguali a 50.000 ms ma minori di 100.000 ms| 
|**Batch >= 100000 ms**|Numero di batch SQL con tempi di risposta maggiori o uguali a 100.000 ms| 

Per ogni contatore nell'oggetto sono disponibili le istanze seguenti:  
  
|Elemento|Descrizione|  
|----------|-----------------|  
|**CPU Time:Requests**|Tempo CPU impiegato per la richiesta.|  
|**CPU Time:Total(ms)**|Tempo CPU totale impiegato per il batch.|  
|**Elapsed Time:Requests**|Tempo trascorso della richiesta.|  
|**Elapsed Time:Total(ms)**|Tempo trascorso del batch.|  

## <a name="see-also"></a>Vedere anche
[Oggetto Plan Cache di SQL Server](../../relational-databases/performance-monitor/sql-server-plan-cache-object.md)  
[Monitoraggio dell'utilizzo delle risorse (Monitor di sistema)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
