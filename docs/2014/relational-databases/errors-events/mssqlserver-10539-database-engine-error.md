---
title: MSSQLSERVER_10539 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10539 (Database Engine error)
ms.assetid: 49c26ff7-18b8-4f07-a087-f45f63463b3b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5fd1f190b8f5d3ab9755409bdd034fa374ea5314
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84969771"
---
# <a name="mssqlserver_10539"></a>MSSQLSERVER_10539
    
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
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
