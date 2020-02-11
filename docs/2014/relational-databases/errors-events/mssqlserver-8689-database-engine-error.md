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
manager: craigg
ms.openlocfilehash: 9f0853d7db0664e75140c0e5478af19c233a2517
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62761718"
---
# <a name="mssqlserver_8689"></a>MSSQLSERVER_8689
    
## <a name="details"></a>Dettagli  
  
|||  
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
 [Hint per la query &#40;&#41;Transact-SQL](/sql/t-sql/queries/hints-transact-sql-query)   
 [Guide di piano](../performance/plan-guides.md)  
  
  
