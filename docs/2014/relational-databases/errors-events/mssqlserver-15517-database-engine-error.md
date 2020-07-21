---
title: MSSQLSERVER_15517 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 15517 (Database Engine error)
ms.assetid: f94287f5-129f-4c52-9d34-62b996088001
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9591bc02f07f3bd29c0a2532942851141732d6a2
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553767"
---
# <a name="mssqlserver_15517"></a>MSSQLSERVER_15517
    
## <a name="details"></a>Dettagli  
  
|Attributo|valore|  
|-|-|  
|Nome prodotto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID evento|15517|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|SEC_CANNOTEXECUTEASUSER|  
|Testo del messaggio|Non può essere eseguita come entità di database perché l'entità "*principal*" non esiste; questo tipo di entità non può essere rappresentato oppure non si ha l'autorizzazione.|  
  
## <a name="user-action"></a>Azione dell'utente  
 Utilizzare il nome di un'entità esistente oppure ottenere l'autorizzazione IMPERSONATE per tale entità.  
  
 L'errore 15517 si può verificare anche dopo l'esecuzione di un'operazione di collegamento e ripristino di un database da un utente diverso dal proprietario del database originale. Per risolvere il problema, impostare db_owner su un account di accesso nel server, eseguendo il comando indicato di seguito:  
  
```  
ALTER AUTHORIZATION ON DATABASE:: DBName TO [NewLogin]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [OLTP in memoria &#40;ottimizzazione per la memoria&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
