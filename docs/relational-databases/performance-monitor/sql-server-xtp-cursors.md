---
title: XTP Cursors di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
s.technology: performance
ms.topic: conceptual
ms.assetid: 84bf4654-3ef7-4d7f-a269-c8bb4ed4acad
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 000b1a6815547487635bac28973cb06bf0cb8204
ms.sourcegitcommit: ca038f1ef180e4e1b27910bbc5d87822cd1ed176
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/20/2018
ms.locfileid: "52158529"
---
# <a name="sql-server-xtp-cursors"></a>XTP Cursors di SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  L'oggetto prestazione SQL Server XTP Cursors contiene contatori correlati ai cursori interni del motore OLTP in memoria. I cursori sono i blocchi predefiniti di basso livello usati dal motore OLTP in memoria per elaborare query [!INCLUDE[tsql](../../includes/tsql-md.md)] . Di conseguenza, in genere non si ha controllo diretto su di essi.  
  
 La tabella seguente descrive i contatori di **SQL Server XTP Cursors** .  
  
|Contatore|Descrizione|  
|-------------|-----------------|  
|**Eliminazioni cursori/sec**|Numero medio di eliminazioni di cursori, al secondo.|  
|**Inserimenti cursori/sec**|Numero medio di inserimenti di cursori, al secondo.|  
|**Analisi cursore avviate/sec**|Numero medio di analisi cursore avviate, al secondo.|  
|**Violazioni UNIQUE del cursore/sec**|Numero medio di violazioni di vincolo UNIQUE, al secondo.|  
|**Aggiornamenti cursori/sec**|Numero medio di aggiornamenti di cursori, al secondo.|  
|**Conflitti di scrittura cursore/sec**|Numero medio di conflitti di scrittura sulla stessa versione di riga, al secondo.|  
|**Tentativi di analisi di elementi nascosti/sec (immessi dall'utente)**|Numero medio di tentativi di analisi dovuti a conflitti di scrittura durante le operazioni su elementi nascosti eseguite da un'analisi di tabella completa dell'utente, al secondo. Si tratta di un contatore di livello molto basso, non destinato all'uso da parte del cliente.|  
|**Righe scadute rimosse/sec**|Numero medio di righe scadute rimosse dai cursori, al secondo.|  
|**Righe scadute interessate/sec**|Numero medio di righe scadute interessate dai cursori, al secondo.|  
|**Righe restituite/sec**|Numero medio di righe restituite dai cursori, al secondo.|  
|**Righe interessate/sec**|Numero medio di righe interessate dai cursori, al secondo.|  
|**Righe provvisoriamente eliminate interessate/sec**|Numero medio di righe in scadenza interessate dai cursori, al secondo. Una riga è in scadenza se la transazione che l'ha eliminata è ancora attiva (cioè non ne è stato ancora eseguito il commit o l'interruzione).|  
  
## <a name="see-also"></a>Vedere anche  
 [Contatori delle prestazioni XTP &#40;OLTP in memoria&#41;](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  
