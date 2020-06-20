---
title: MSSQLSERVER_10536 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10536 (Database Engine error)
ms.assetid: 9f97b41f-0ef8-4ad2-aec0-906a5d7522ba
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 00d08f4555f38b61661a917ba94c023f9dd6c4a8
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84968121"
---
# <a name="mssqlserver_10536"></a>MSSQLSERVER_10536
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|10536|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|PG_TOO_MANY_STMTS|  
|Testo del messaggio|Impossibile creare la guida di piano '%.\*ls' perché il batch o il modulo corrispondente al valore `@plan_handle` specificato contiene più di 1000 istruzioni idonee. Creare una guida di piano per ciascuna istruzione nel batch o nel modulo specificando un valore `statement_start_offset` per ciascuna istruzione.|  
  
## <a name="explanation"></a>Spiegazione  
 Il batch o il modulo corrispondente al valore `@plan_handle` contiene più di 1000 istruzioni idonee.  
  
## <a name="user-action"></a>Azione dell'utente  
 Creare una guida di piano per ciascuna istruzione nel batch o nel modulo specificando un valore `statement_start_offset` per ciascuna istruzione.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [Guide di piano](../performance/plan-guides.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
