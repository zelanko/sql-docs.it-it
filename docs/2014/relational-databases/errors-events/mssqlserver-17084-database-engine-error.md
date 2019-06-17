---
title: MSSQLSERVER_17084 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17084 (Database Engine error)
ms.assetid: e579d104-3307-4edd-8587-b14ecbc02ed9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 95d0da610a8030c68bcf25d650e68aef4ae83128
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62915461"
---
# <a name="mssqlserver17084"></a>MSSQLSERVER_17084
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID evento|17084|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|P3_ATOMIC_WITH_MISSING_OPTION|  
|Testo del messaggio|La clausola WITH dell'istruzione BEGIN ATOMIC deve specificare un valore per l'opzione "%ls".|  
  
## <a name="explanation"></a>Spiegazione  
 La clausola WITH dell'istruzione BEGIN ATOMIC non specificava un valore per un'opzione.  
  
## <a name="user-action"></a>Azione dell'utente  
 I blocchi`ATOMIC` richiedono valori per le opzioni `WITH` `TRANSACTION ISOLATION LEVEL` e `LANGUAGE`. Ad esempio:  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE= N'us_english')  
```  
  
 Per altre informazioni, vedere [OLTP in memoria &#40;ottimizzazione in memoria&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Vedere anche  
 [OLTP in memoria &#40;ottimizzazione per la memoria&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
