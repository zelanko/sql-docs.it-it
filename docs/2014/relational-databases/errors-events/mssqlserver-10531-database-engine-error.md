---
title: MSSQLSERVER_10531 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10531 (Database Engine error)
ms.assetid: bb40e994-231c-44ce-933f-8d767fb2f450
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7324979238eda7f3ee63a709c199878350edb82d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62916198"
---
# <a name="mssqlserver_10531"></a>MSSQLSERVER_10531
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|10531|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|PG_NO_ELIGIBLE_STMT|  
|Testo del messaggio|Impossibile creare la guida di piano '%.*ls' dalla cache perché l'utente non dispone delle autorizzazioni necessarie. Per creare la guida di piano, concedere all'utente l'autorizzazione VIEW SERVER STATE.|  
  
## <a name="explanation"></a>Spiegazione  
 L'utente non dispone delle autorizzazioni necessarie per creare la guida di piano dalla cache dei piani.  
  
## <a name="user-action"></a>Azione dell'utente  
 Concedere l'autorizzazione VIEW SERVER STATE all'utente che crea la guida di piano.  
  
## <a name="see-also"></a>Vedere anche  
 [Guide di piano](../performance/plan-guides.md)   
 [sp_create_plan_guide &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
