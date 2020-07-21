---
title: MSSQLSERVER_10502 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10502 (Database Engine error)
ms.assetid: 26d9b64d-4299-4b55-92d0-0a32a3688c0a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ac0209030531f0c56a1a071ba54282f10d4b7db9
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552406"
---
# <a name="mssqlserver_10502"></a>MSSQLSERVER_10502
    
## <a name="details"></a>Dettagli  
  
|Attributo|valore|  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|10502|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|PG_DUP_FOUND|  
|Testo del messaggio|Impossibile creare la guida di piano '%.*ls' perché l'istruzione specificata da @stmt e @module_or_batch o da @plan_handle e @statement_start_offset corrisponde alla guida di piano '%.\*ls' esistente nel database. Eliminare la guida di piano esistente prima di creare quella nuova.|  
  
## <a name="explanation"></a>Spiegazione  
 Per l'istruzione specificata esiste già una guida di piano.  
  
## <a name="user-action"></a>Azione dell'utente  
 Eliminare la guida di piano esistente prima di creare quella nuova.  
  
## <a name="see-also"></a>Vedere anche  
 [Guide di piano](../performance/plan-guides.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
