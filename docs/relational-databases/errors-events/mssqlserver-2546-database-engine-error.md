---
title: MSSQLSERVER_2546 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2546 (Database Engine error)
ms.assetid: c8f0e1b4-c7c4-45f2-9221-746714172313
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 983c5536d08d9701fd301ace4ca8d2b5d7e76f71
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63046423"
---
# <a name="mssqlserver2546"></a>MSSQLSERVER_2546
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|2546|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|DBCC_INDEX_MARKED_DISABLED|  
|Testo del messaggio|L'indice 'INDEX_NAME' della tabella 'OBJECT_NAME' è contrassegnato come disabilitato. Ricompilare l'indice per riportarlo online.|  
  
## <a name="explanation"></a>Spiegazione  
L'indice specificato è contrassegnato come offline oppure è disabilitato e pertanto non può essere controllato.  
  
## <a name="user-action"></a>Azione dell'utente  
Ricompilare l'indice utilizzando ALTER INDEX.  
  
## <a name="see-also"></a>Vedere anche  
[ALTER INDEX &#40;Transact-SQL&#41;](~/t-sql/statements/alter-index-transact-sql.md)  
[Riorganizzare e ricompilare gli indici](~/relational-databases/indexes/reorganize-and-rebuild-indexes.md)  
  
