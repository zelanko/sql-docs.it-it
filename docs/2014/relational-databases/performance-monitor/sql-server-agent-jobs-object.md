---
title: Oggetto Processi di SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLAgent:Jobs
- Jobs object
ms.assetid: 225b5e2d-4a78-4178-b2b6-b419df83c4aa
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 927e5b199d983a1a850f069408dba2156f67a408
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85017101"
---
# <a name="sql-server-agent-jobs-object"></a>Oggetto Processi di SQL Server Agent
  L'oggetto prestazioni **Processi** di SQL Server Agent include contatori delle prestazioni che forniscono informazioni relative ai processi di SQL Server Agent. Nella tabella seguente sono elencati i contatori inclusi nell'oggetto.  
  
 Nella tabella seguente sono illustrati i contatori di **SQLAgent:Processi** .  
  
|Nome|Descrizione|  
|----------|-----------------|  
|**Processi attivi**|Questo contatore indica il numero di processi attualmente in esecuzione.|  
|**Processi non riusciti**|Questo contatore indica il numero di processi chiusi con un errore.|  
|**Percentuale processi completati**|Questo contatore indica la percentuale di processi eseguiti completati correttamente.|  
|**Processi attivati/minuto**|Questo contatore indica il numero di processi avviati nell'ultimo minuto.|  
|**Processi in coda**|Questo contatore indica il numero di processi pronti per l'esecuzione in SQL Server Agent, ma la cui esecuzione non è ancora stata avviata.|  
|**Processi completati**|Questo contatore indica il numero di processi chiusi correttamente.|  
  
 Per ogni contatore nell'oggetto sono disponibili le istanze seguenti:  
  
|Istanza|Descrizione|  
|--------------|-----------------|  
|**_Total**|Informazioni relative a tutti i processi.|  
|**Avvisi**|Informazioni relative ai processi avviati da avvisi.|  
|**Altro**|Informazioni relative a processi non avviati da avvisi o pianificazioni. In genere, si tratta di processi avviati manualmente tramite **sp_start_job**.|  
|**Pianificazioni**|Informazioni relative ai processi avviati da pianificazioni.|  
  
## <a name="see-also"></a>Vedere anche  
 [Implementazione di processi](../../ssms/agent/implement-jobs.md)   
 [Utilizzo degli oggetti prestazioni](../../ssms/agent/use-performance-objects.md)   
 [Monitorare l'utilizzo delle risorse &#40;Monitor di sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  
