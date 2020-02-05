---
title: MSSQLSERVER_9002 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9002 (Database Engine error)
ms.assetid: 2e50841f-2b99-45f4-aec5-aa4add70cbeb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3397d8fc1fbf271ab3bd8032ae14c7d9b61b6020
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68118356"
---
# <a name="mssqlserver_9002"></a>MSSQLSERVER_9002
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|9002|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|LOG_IS_FULL|  
|Testo del messaggio|Il log delle transazioni per il database '%.*ls' è pieno. Per sapere perché non è possibile riutilizzare lo spazio nel log, vedere la colonna log_reuse_wait_desc in sys.databases.|  
  
## <a name="explanation"></a>Spiegazione  
Lo spazio nel log del database è esaurito. Nella colonna **log_reuse_wait_desc** in **sys.databases** viene descritto il motivo per cui non è possibile usare di nuovo lo spazio nel log.  
  
## <a name="user-action"></a>Azione dell'utente  
Usare **sys.databases** per determinare perché il log è pieno e quindi correggere tale condizione. Per ulteriori informazioni, vedere l'articolo sulla risoluzione dei problemi relativi a un log delle transazioni pieno (Errore 9002) nella documentazione online di SQL Server.  
  
## <a name="see-also"></a>Vedere anche  
[Risolvere i problemi relativi a un log delle transazioni completo &#40;Errore di SQL Server 9002&#41;](~/relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
[sys.databases &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
