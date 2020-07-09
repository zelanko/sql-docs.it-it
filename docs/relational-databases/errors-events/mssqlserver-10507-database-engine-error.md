---
title: MSSQLSERVER_10507 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10507 (Database Engine error)
ms.assetid: cd83fa81-ac37-4eda-a3c3-17610b051de2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 82d21d961f623ee20625f0fefd9fc4403f000e96
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85781501"
---
# <a name="mssqlserver_10507"></a>MSSQLSERVER_10507
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |  
| :-------- | :---- |  
|Nome prodotto|SQL Server|  
|ID evento|10507|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|PG_STMT_DOES_NOT_MATCH|  
|Testo del messaggio|Impossibile creare la guida di piano '%.\*ls' perché l'istruzione specificata da **\@stmt** e **\@module_or_batch** o da **\@plan_handle** e **\@statement_start_offset** non corrisponde ad alcuna istruzione nel modulo o nel batch specificato. Modificare i valori in modo da corrispondere a un'istruzione nel modulo o nel batch.|  
  
## <a name="explanation"></a>Spiegazione  
Un'istruzione nel modulo o nel batch non corrisponde a quella specificata o al valore dell'offset dell'istruzione.  
  
## <a name="user-action"></a>Azione dell'utente  
Modificare i valori del parametro specificato in modo da corrispondere a un'istruzione nel modulo o nel batch.  
  
## <a name="see-also"></a>Vedere anche  
[Guide di piano](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
