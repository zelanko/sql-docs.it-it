---
title: MSSQLSERVER_8689 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 8689 (Database Engine error)
ms.assetid: 99467a32-6576-4272-a076-b16c06933f2a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f66fec380ebd70a4dcbba445f9e0678fb33290eb
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553123"
---
# <a name="mssqlserver_8689"></a>MSSQLSERVER_8689
    
## <a name="details"></a>Dettagli  
  
|Attributo|valore|  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|8689|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|USEPLAN_ERR_NO_DB|  
|Testo del messaggio|Il database '%.*ls' specificato nell'hint USE PLAN non esiste. Specificare un database esistente.|  
  
## <a name="explanation"></a>Spiegazione  
 Un database specificato nell'hint USE PLAN non esiste.  
  
## <a name="user-action"></a>Azione dell'utente  
 Verificare che tutti i database specificati nell'hint USE PLAN esistano.  
  
## <a name="see-also"></a>Vedere anche  
 [Hint di query &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query)   
 [Guide di piano](../performance/plan-guides.md)  
  
  
