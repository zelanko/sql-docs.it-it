---
title: XTP Cursors di SQL Server | Microsoft Docs
description: Informazioni sull'oggetto prestazione XTP Cursors di SQL Server, che contiene contatori correlati ai cursori interni del motore OLTP in memoria.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 84bf4654-3ef7-4d7f-a269-c8bb4ed4acad
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 39c491efc7b0001b7f6b44bda127e7b128c31851
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505527"
---
# <a name="sql-server-xtp-cursors"></a>XTP Cursors di SQL Server
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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
  
  
