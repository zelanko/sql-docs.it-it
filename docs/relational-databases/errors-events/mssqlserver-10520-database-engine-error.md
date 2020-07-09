---
title: MSSQLSERVER_10520 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10520 (Database Engine error)
ms.assetid: cc8799f1-5b90-4248-b209-e1d5087f9529
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8f83b574d6201d0845f23c9194ea2e873d90daa5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85781489"
---
# <a name="mssqlserver_10520"></a>MSSQLSERVER_10520
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |  
| :-------- | :---- |  
|Nome prodotto|SQL Server|  
|ID evento|10520|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|PG_PARAM_NOT_ALLOWED|  
|Testo del messaggio|Impossibile creare la guida di piano '%.*ls' perché @type è stato specificato come '%ls' ed è stato specificato un valore non NULL per il parametro '%ls'. Questo tipo richiede un valore NULL per il parametro. Specificare NULL per il parametro oppure impostare un tipo che consenta un valore non NULL per il parametro.|  
  
## <a name="explanation"></a>Spiegazione  
Il tipo indicato in @type richiede un valore NULL per il parametro specificato, ma è stato fornito un valore non NULL.  
  
## <a name="user-action"></a>Azione dell'utente  
Specificare NULL per il parametro oppure impostare un tipo che consenta un valore non NULL per il parametro.  
  
## <a name="see-also"></a>Vedere anche  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[Guide di piano](~/relational-databases/performance/plan-guides.md)  
  
