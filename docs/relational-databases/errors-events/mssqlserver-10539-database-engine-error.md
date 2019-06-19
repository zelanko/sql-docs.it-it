---
title: MSSQLSERVER_10539 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10539 (Database Engine error)
ms.assetid: 49c26ff7-18b8-4f07-a087-f45f63463b3b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e44899e6b586610dc9b18e3ab2e4ec31d4451c1e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63048379"
---
# <a name="mssqlserver10539"></a>MSSQLSERVER_10539
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|10539|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|PG_NO_PLAN_FOR_STMT|  
|Testo del messaggio|Impossibile creare la guida di piano '%.*ls' dalla cache perché non è disponibile un piano di query per l'istruzione con offset iniziale %d. Questo problema può verificarsi se l'istruzione dipende da oggetti di database non ancora creati. Verificare che esistano tutti gli oggetti di database necessari ed eseguire l'istruzione prima di creare la guida di piano.|  
  
## <a name="explanation"></a>Spiegazione  
Un piano di query non è disponibile nella cache dei piani per l'istruzione con l'offset iniziale specificato.  
  
## <a name="user-action"></a>Azione dell'utente  
Verificare che esistano tutti gli oggetti di database necessari ed eseguire l'istruzione prima di creare la guida di piano.  
  
## <a name="see-also"></a>Vedere anche  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
