---
title: MSSQL_ENG014120 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014120 error
ms.assetid: 6b169a3b-30da-4981-b998-b52d61811572
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1cb395edd4d0c8cd9b9745967e210713bdb49388
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100244"
---
# <a name="mssqleng014120"></a>MSSQL_ENG014120
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Dettagli messaggio  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|14120|  
|Origine evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbolico||  
|Testo del messaggio|Il database di distribuzione '%s' è associato a un server di pubblicazione. Impossibile eliminarlo.|  
  
## <a name="explanation"></a>Spiegazione  
 Nel database di distribuzione vengono memorizzati metadati e dati di cronologia relativi a tutti i tipi di replica e alle transazioni per la replica transazionale. Questo errore si verifica se si tenta di eliminare un database di distribuzione associato a uno o più server di pubblicazione.  
  
## <a name="user-action"></a>Azione dell'utente  
 Per eliminare un database di distribuzione, è innanzitutto necessario eliminare l'associazione tra il server di distribuzione e il server di pubblicazione. Per altre informazioni, vedere [sp_dropdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a errori ed eventi &#40;replica&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Configurare la distribuzione](../../relational-databases/replication/configure-distribution.md)  
  
  
