---
title: MSSQL_ENG003165 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG003165 error
ms.assetid: 707d33dd-644e-4cc9-ac51-dddd49031530
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c4c2c6e01fd3e0b862511f71d90baf31d28948ef
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52780983"
---
# <a name="mssqleng003165"></a>MSSQL_ENG003165
    
## <a name="message-details"></a>Dettagli messaggio  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|3165|  
|Origine evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbolico||  
|Testo del messaggio|Il database '%ls' è stato ripristinato ma è stato rilevato un errore durante il ripristino o la rimozione della replica. Il database è stato lasciato offline. Vedere l'argomento MSSQL_ENG003165 della documentazione online di SQL Server.|  
  
## <a name="explanation"></a>Spiegazione  
 Questo errore viene generato se si verifica un problema durante il ripristino di un backup di un database replicato:  
  
-   Se il ripristino del backup avviene nello stesso database e nello stesso server sui quali è stato eseguito, l'errore indica che non è stato possibile ripristinare correttamente le impostazioni della replica.  
  
-   Se invece il backup viene ripristinato in un database o in un server diverso, l'errore indica che non è stato possibile rimuovere correttamente le impostazioni della replica (per impostazione predefinita, queste ultime vengono rimosse se il database o il server è diverso).  
  
 È probabile che l'errore sia il risultato di una mancata corrispondenza tra lo stato del database ripristinato e uno o più database di sistema contenenti metadati di replica, come il database **msdb**, **master**o il database di distribuzione.  
  
## <a name="user-action"></a>Azione dell'utente  
 Per risolvere il problema:  
  
1.  Eseguire l'istruzione ALTER DATABASE per portare il database online. Ad esempio: `ALTER DATABASE AdventureWorks SET ONLINE`. Per altre informazioni, vedere [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql). Per mantenere le impostazioni di replica, andare al passaggio 2. In caso contrario, andare al passaggio 3.  
  
2.  Eseguire [sp_restoredbreplication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-restoredbreplication-transact-sql). Se l'esecuzione di questa stored procedure riesce, il ripristino sarà completo. In caso contrario, andare al passaggio 3.  
  
3.  Eseguire [sp_removedbreplication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) per rimuovere tutte le impostazioni della replica.  
  
     Se necessario, riconfigurare la replica. Se sono stati creati gli script della topologia di replica, come consigliato, utilizzare tali script per riconfigurare la topologia.  
  
## <a name="see-also"></a>Vedere anche  
 [Backup e ripristino di database SQL Server](../backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Backup e ripristino di database replicati](administration/back-up-and-restore-replicated-databases.md)   
 [Guida di riferimento a errori ed eventi &#40;replica&#41;](errors-and-events-reference-replication.md)  
  
  
