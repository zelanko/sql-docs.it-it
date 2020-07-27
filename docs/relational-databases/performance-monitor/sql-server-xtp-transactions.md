---
title: XTP Transactions di SQL Server | Microsoft Docs
description: Informazioni sull'oggetto prestazione XTP Transactions di SQL Server, che contiene i contatori correlati alle transazioni che includono OLTP in memoria in SQL Server.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 443d67e4-1c7f-41d7-b18d-2d657f58c22a
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 384e2feb7d638a7ff8cad4e22346ba58369cc6aa
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/17/2020
ms.locfileid: "86458068"
---
# <a name="sql-server-xtp-transactions"></a>Transazioni XTP di SQL Server
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  L'oggetto prestazione XTP Transactions di SQL Server contiene i contatori correlati alle transazioni che includono OLTP in memoria in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Nella tabella seguente sono descritti i contatori di **XTP Transactions di SQL Server** .  
  
|Contatore|Descrizione|  
|-------------|-----------------|  
|**Interruzioni a catena/sec**|Numero medio di transazioni di cui è stato eseguito il rollback a causa di un rollback di dipendenza di commit, al secondo.|  
|**Dipendenze di commit acquisite/sec**|Numero medio delle dipendenze di commit acquisite dalle transazioni, al secondo.|  
|**Transazioni di sola lettura preparate/sec**|Numero di transazioni di sola lettura che sono state preparate per l'elaborazione del commit, al secondo.|  
|**Aggiornamenti del punto di salvataggio/sec**|Numero medio di volte in cui un punto di salvataggio "è stato aggiornato", al secondo. L'aggiornamento di un punto di salvataggio avviene quando un punto di salvataggio esistente viene reimpostato sul punto corrente della durata della transazione.|  
|**Rollback del punto di salvataggio/sec**|Numero medio di volte che è stato eseguito il rollback di una transazione a un punto di salvataggio, al secondo.|  
|**Punti di salvataggio creati/sec**|Numero medio di punti di salvataggio creati, al secondo.|  
|**Errori di convalida delle transazioni/sec**|Numero medio di transazioni per cui l'elaborazione di convalida ha avito esito negativo, al secondo.|  
|**Transazioni interrotte dall'utente/sec**|Numero medio di transazioni che sono state interrotte dall'utente, al secondo.|  
|**Transazioni interrotte/sec**|Numero medio di transazioni che sono state interrotte (sia dall'utente che dal sistema), al secondo.|  
|**Transazioni create/sec**|Numero medio di transazioni create nel sistema, al secondo.<br /><br /> Le transazioni XTP sono calcolate in modo diverso rispetto alle transazioni basate su disco (come indicato in Database:Transazioni/sec). Ad esempio, Transazioni create/sec conteggia le transazioni di sola lettura, a differenza di Database:Transazioni/sec.|  
  
## <a name="see-also"></a>Vedere anche  
 [Contatori delle prestazioni XTP &#40;OLTP in memoria&#41;](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  
