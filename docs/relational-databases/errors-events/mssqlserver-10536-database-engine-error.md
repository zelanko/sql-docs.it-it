---
title: MSSQLSERVER_10536 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10536 (Database Engine error)
ms.assetid: 9f97b41f-0ef8-4ad2-aec0-906a5d7522ba
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0ace2712cd53b1b0371bd9deeb4191308a1393de
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060656"
---
# <a name="mssqlserver10536"></a>MSSQLSERVER_10536
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|10536|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|PG_TOO_MANY_STMTS|  
|Testo del messaggio|Impossibile creare la guida di piano '%.\*ls' perché il batch o il modulo corrispondente al valore **@plan_handle** specificato contiene più di 1000 istruzioni idonee. Creare una guida di piano per ogni istruzione nel batch o nel modulo specificando un valore **statement_start_offset** per ogni istruzione.|  
  
## <a name="explanation"></a>Spiegazione  
Il batch o il modulo corrispondente al valore **@plan_handle** specificato contiene più di 1000 istruzioni idonee.  
  
## <a name="user-action"></a>Azione dell'utente  
Creare una guida di piano per ogni istruzione nel batch o nel modulo specificando un valore **statement_start_offset** per ogni istruzione.  
  
## <a name="see-also"></a>Vedere anche  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[Guide di piano](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
