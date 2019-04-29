---
title: MSSQLSERVER_1222 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1222 (Database Engine error)
ms.assetid: c5b1c2f4-f591-4cc1-aa17-204636a27f29
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 01325e8d83a5a7d7b65398f4e0cb981b1fca7540
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62915897"
---
# <a name="mssqlserver1222"></a>MSSQLSERVER_1222
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|1222|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|LK_TIMEOUT|  
|Testo del messaggio|Timeout della richiesta di blocco.|  
  
## <a name="explanation"></a>Spiegazione  
Una risorsa necessaria viene mantenuta in blocco da un'altra transazione per un periodo superiore al tempo di attesa ammesso dalla query.  
  
## <a name="user-action"></a>Azione dell'utente  
Per risolvere il problema, eseguire le operazioni seguenti:  
  
1.  Se possibile, individuare la transazione che blocca la risorsa necessaria. Usare le viste a gestione dinamica **sys.dm_os_waiting_tasks** e **sys.dm_tran_locks**.  
  
2.  Se la transazione continua a mantenere il blocco, terminarla se appropriato.  
  
3.  Eseguire nuovamente la query.  
  
Se l'errore si verifica spesso, modificare il periodo di timeout del blocco oppure le transazioni all'origine del problema in modo che mantengano il blocco per un periodo di tempo inferiore.  
  
