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
ms.openlocfilehash: 4419796b75fbd10ab866cbf78b67fcab0c1e2ca5
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68023159"
---
# <a name="mssqlserver_1406"></a>MSSQLSERVER_1406
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
  
