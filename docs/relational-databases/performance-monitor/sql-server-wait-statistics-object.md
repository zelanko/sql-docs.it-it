---
title: Oggetto Wait Statistics di SQL Server | Microsoft Docs
description: Informazioni sull'oggetto prestazione SQLServer:Wait Statistics, che contiene contatori delle prestazioni che forniscono informazioni sullo stato di attesa.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Wait Statistics object
- SQLServer:Wait Statistics
ms.assetid: cb7f917d-4291-4115-9b78-ee7692ebbb2d
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: df97bc68487d6113857fa0d9c6a56bdc7a2871b9
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505557"
---
# <a name="sql-server-wait-statistics-object"></a>Oggetto Statistiche attesa di SQL Server
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  L'oggetto prestazioni **SQLServer:Statistiche attesa** contiene contatori delle prestazioni che forniscono informazioni sullo stato di attesa.  
  
 Nella tabella seguente sono elencati i contatori inclusi nell'oggetto Statistiche attesa.  
  
|Contatori dell'oggetto Statistiche attesa di SQL Server|Descrizione|  
|-----------------------------------------|-----------------|  
|**Attese di blocco**|Statistiche relative ai processi in attesa di un blocco.|  
|**Attese buffer log**|Statistiche relative ai processi in attesa che il buffer del log diventi disponibile.|  
|**Attese scrittura log**|Statistiche relative ai processi in attesa di scrittura nel buffer del log.|  
|**Attese coda concessione memoria**|Statistiche relative ai processi in attesa di una concessione di memoria.|  
|**Attese I/O di rete**|Statistiche relative alle attese per operazioni di I/O di rete.|  
|**Attese latch non di pagina**|Statistiche relative ai latch non di pagina.|  
|**Attese latch I/O di pagina**|Statistiche relative ai latch di I/O di pagina.|  
|**Attese latch pagina**|Statistiche relative ai latch di pagina, esclusi i latch di I/O.|  
|**Attesa oggetti memoria affidabili**|Statistiche relative ai processi in attesa di allocatori di memoria affidabili.|  
|**Attese proprietà transazione**|Statistiche relative alla sincronizzazione dell'accesso dei processi alla transazione.|  
|**Attesa thread di lavoro**|Statistiche relative ai processi in attesa che il thread di lavoro diventi disponibile.|  
|**Attese sincronizzazione area di lavoro**|Statistiche relative alla sincronizzazione dell'accesso dei processi all'area di lavoro.|  
  
 Per ogni contatore nell'oggetto sono disponibili le istanze seguenti:  
  
|Elemento|Descrizione|  
|----------|-----------------|  
|**Tempo medio di attesa (ms)**|Tempo medio per il tipo di attesa selezionato.|  
|**Tempo di attesa (ms) cumulativo al secondo**|Tempo di attesa aggregato al secondo per il tipo di attesa selezionato|  
|**Attese in corso**|Numero di processi attualmente in attesa del tipo seguente.|  
|**Attese avviate al secondo**|Numero di attese avviate al secondo del tipo di attesa selezionato.|  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare l'utilizzo delle risorse &#40;Monitor di sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
