---
title: MSSQLSERVER_17083 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17083 (Database Engine error)
ms.assetid: 6c83737d-0531-4fd9-88f6-2da5a150532d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c04d010a690d99d90ea3a18ae7f70d33ed39f24b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62915498"
---
# <a name="mssqlserver17083"></a>MSSQLSERVER_17083
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID evento|17083|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|P3_HEKATON_NOT_ATOMIC|  
|Testo del messaggio|Il corpo di una stored procedure compilata in modo nativo deve essere un blocco ATOMIC.|  
  
## <a name="explanation"></a>Spiegazione  
 Il corpo di una stored procedure compilata in modo nativo non disponeva di un blocco ATOMIC.  
  
## <a name="user-action"></a>Azione dell'utente  
 Una stored procedure compilata in modo nativo deve essere un blocco ATOMIC. Ad esempio:  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE= N'us_english')  
```  
  
 Per altre informazioni, vedere [OLTP in memoria &#40;ottimizzazione in memoria&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Vedere anche  
 [OLTP in memoria &#40;ottimizzazione per la memoria&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
