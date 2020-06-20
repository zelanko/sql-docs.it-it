---
title: MSSQLSERVER_10538 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10538 (Database Engine error)
ms.assetid: 284d19b4-4979-4cbe-a9be-ac1104433c69
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: edc6abf192a3341f9b84c99e99071343cc882c3d
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84968111"
---
# <a name="mssqlserver_10538"></a>MSSQLSERVER_10538
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|10538|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|PG_INVALID_PLANGUIDE_HANDLE|  
|Testo del messaggio|Impossibile trovare la guida di piano. L'ID della guida di piano specificato è NULL o non valido oppure l'utente non dispone dell'autorizzazione per l'oggetto a cui fa riferimento la guida di piano. Verificare che l'ID della guida di piano sia valido, che la sessione corrente sia impostata sul contesto di database corretto e di disporre dell'autorizzazione ALTER per l'oggetto a cui fa riferimento la guida di piano o dell'autorizzazione ALTER DATABASE.|  
  
## <a name="explanation"></a>Spiegazione  
 L'ID della guida di piano specificato è NULL o non valido oppure l'utente non dispone dell'autorizzazione per l'oggetto a cui fa riferimento la guida di piano.  
  
## <a name="user-action"></a>Azione dell'utente  
 Verificare che l'ID della guida di piano sia valido, che la sessione corrente sia impostata sul contesto di database corretto e di disporre dell'autorizzazione ALTER per l'oggetto a cui fa riferimento la guida di piano o dell'autorizzazione ALTER DATABASE.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [Guide di piano](../performance/plan-guides.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
