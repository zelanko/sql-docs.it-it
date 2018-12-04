---
title: Oggetto ExecStatistics di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
s.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:ExecStatistics
- ExecStatistics object
ms.assetid: 4f8557a8-345f-4622-a8a5-763a0388ad94
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 992deb3cf7d976682434d72ffefa046d303dc2ac
ms.sourcegitcommit: ca038f1ef180e4e1b27910bbc5d87822cd1ed176
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/20/2018
ms.locfileid: "52158322"
---
# <a name="sql-server-execstatistics-object"></a>Oggetto ExecStatistics di SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  L'oggetto **SQLServer:ExecStatistics** di Microsoft SQL Server include contatori che consentono di monitorare diversi tipi di esecuzioni.  
  
 Nella tabella seguente vengono descritti i contatori **Exec Statistics** di SQL Server.  
  
|Contatori Exec Statistics di SQL Server|Descrizione|  
|-----------------------------------------|-----------------|  
|**Query distribuite**|Statistiche relative all'esecuzione di query distribuite.|  
|**Chiamate DTC**|Statistiche relative all'esecuzione di chiamate DTC.|  
|**Procedure estese**|Statistiche relative all'esecuzione di procedure estese.|  
|**Chiamate OLEDB**|Statistiche relative all'esecuzione di chiamate OLEDB.|  
  
 Per ogni contatore nell'oggetto sono disponibili le istanze seguenti:  
  
|Elemento|Descrizione|  
|----------|-----------------|  
|**Tempo di esecuzione (ms) medio**|Durata media per il tipo di esecuzione selezionato.|  
|**Tempo di esecuzione (ms) cumulativo al secondo**|Tempo di esecuzione complessivo al secondo per il tipo di esecuzione selezionato.|  
|**Esecuzioni in corso**|Numero di esecuzioni in corso per il tipo di esecuzione selezionato.|  
|**Esecuzioni avviate al secondo**|Numero di esecuzioni avviate al secondo per il tipo di esecuzione selezionato.|  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare l'utilizzo delle risorse &#40;Monitor di sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
