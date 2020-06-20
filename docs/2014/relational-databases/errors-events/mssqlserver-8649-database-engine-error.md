---
title: MSSQLSERVER_8649 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 8649 (Database Engine error)
ms.assetid: 992dbc74-7c3a-498b-9f1b-b28387640677
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b39ed0d8ffe5f7f601b6cb1393596d0d6546e557
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85031776"
---
# <a name="mssqlserver_8649"></a>MSSQLSERVER_8649
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|8649|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|COST_TOO_HIGH|  
|Testo del messaggio|La query è stata annullata perché il suo costo stimato (%d) è maggiore della soglia configurata, pari a %d. Contattare l'amministratore del sistema.|  
  
## <a name="explanation"></a>Spiegazione  
 La query è stata annullata perché il suo costo stimato supera la soglia configurata impostata per QUERY_GOVERNOR_COST_LIMIT.  
  
## <a name="user-action"></a>Azione dell'utente  
 Impostare l'opzione QUERY_GOVERNOR_COST_LIMIT su un valore più elevato.  
  
## <a name="see-also"></a>Vedere anche  
 [SET QUERY_GOVERNOR_COST_LIMIT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-query-governor-cost-limit-transact-sql)  
  
  
