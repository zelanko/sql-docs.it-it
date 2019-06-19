---
title: MSSQLSERVER_1406 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1406 (Database Engine error)
ms.assetid: 915f97de-9b74-41f8-8bd5-b2d061416718
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 23d09ae4eaefb7228e0eb0f7593b8d844ef66a65
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62859981"
---
# <a name="mssqlserver1406"></a>MSSQLSERVER_1406
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|1406|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|DBM_BADSTATEFORFORCESERVICE|  
|Testo del messaggio|Impossibile forzare il servizio senza rischi. Per ottenere l'accesso, rimuovere il mirroring del database e recuperare il database "%.*ls".|  
  
## <a name="explanation"></a>Spiegazione  
Il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] non può forzare il servizio perché lo stato del mirroring non è in grado di garantire che il servizio venga forzato correttamente.  
  
## <a name="user-action"></a>Azione dell'utente  
Rimuovere il mirroring del database. Sarà quindi possibile recuperare il database mirror per potervi accedere.  
  
## <a name="see-also"></a>Vedere anche  
[Utilizzo forzato del servizio in una sessione di mirroring del database &#40;Transact-SQL&#41;](~/database-engine/database-mirroring/force-service-in-a-database-mirroring-session-transact-sql.md)  
[Rimozione del mirroring del database &#40;SQL Server&#41;](~/database-engine/database-mirroring/removing-database-mirroring-sql-server.md)  
  
