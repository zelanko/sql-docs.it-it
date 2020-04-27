---
title: MSSQLSERVER_41365 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 41365 (Database Engine error)
ms.assetid: 4fc7ec15-b722-4e3d-b7f9-3d39d171e96e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dbf921e280b7b01685bb2d4817975149864614a0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62867942"
---
# <a name="mssqlserver_41365"></a>MSSQLSERVER_41365
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID evento|41365|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|HK_MERGE_SCHEDULE_ERROR|  
|Testo del messaggio|La richiesta di unione per l'intervallo della transazioni [%ld, %ld) sul database %.*ls non è stata pianificata. I file del checkpoint che rappresentano l'intervallo non sono disponibili per unione o parte di un'unione in corso.|  
  
## <a name="explanation"></a>Spiegazione  
 I file del checkpoint che rappresentano l'intervallo non sono disponibili per unione o parte di un'unione in corso.  
  
## <a name="user-action"></a>Azione dell'utente  
 Fornire un migliore intervallo di transazioni per merge/attesa prima di eseguire la stessa richiesta. Per altre informazioni, vedere [OLTP in memoria &#40;ottimizzazione in memoria&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Vedere anche  
 [OLTP in memoria &#40;ottimizzazione per la memoria&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
