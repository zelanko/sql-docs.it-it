---
title: Funzioni (Transact-SQL) di rilevamento delle modifiche | Documenti di Microsoft
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- functions [SQL Server], change tracking
- change tracking [SQL Server], functions
ms.assetid: 04eb53c4-8b69-414e-9696-185d227fea35
author: rothja
ms.author: jroth
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: dcd12d2495c0be6ec3a643b5c5f0f34d2e50f156
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52544379"
---
# <a name="change-tracking-functions-transact-sql"></a>Funzioni di rilevamento delle modifiche (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  I record di rilevamento delle modifiche inseriscono, aggiornano ed eliminano le attività applicate alle tabelle rilevate, fornendo i dettagli delle modifiche in un formato relazionale facilmente utilizzabile. Per restituire informazioni sulle modifiche, si utilizzano le funzioni seguenti.  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|[CHANGETABLE (CHANGES)](../../relational-databases/system-functions/changetable-transact-sql.md)|Restituisce informazioni di rilevamento per tutte le modifiche a una tabella verificatesi a partire da una versione specificata.|  
|[CHANGETABLE (VERSION)](../../relational-databases/system-functions/changetable-transact-sql.md)|Restituisce le informazioni più recenti sul rilevamento delle modifiche per una riga specificata.|  
|[CHANGE_TRACKING_MIN_VALID_VERSION()](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md)|Restituisce la versione minima valida per l'utilizzo nell'ottenere informazioni rilevamento delle modifiche dalla tabella specificata quando si usa la [CHANGETABLE](../../relational-databases/system-functions/changetable-transact-sql.md) (funzione).|  
|[CHANGE_TRACKING_CURRENT_VERSION](../../relational-databases/system-functions/change-tracking-current-version-transact-sql.md)|Ottiene una versione associata all'ultima transazione completata. È possibile utilizzare questa versione al momento di enumerare le modifiche utilizzando CHANGETABLE.|  
|[CHANGE_TRACKING_IS_COLUMN_IN_MASK](../../relational-databases/system-functions/change-tracking-is-column-in-mask-transact-sql.md)|Interpreta il valore SYS_CHANGE_COLUMNS restituito dalla funzione CHANGETABLE(CHANGES...).|  
|[WITH CHANGE_TRACKING_CONTEXT](../../relational-databases/system-functions/with-change-tracking-context-transact-sql.md)|Abilita la specifica di un contesto di modifica, come ad esempio un ID origine, quando un'applicazione modifica i dati.|  
  
## <a name="see-also"></a>Vedere anche  
 [Rilevare le modifiche ai dati &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  
