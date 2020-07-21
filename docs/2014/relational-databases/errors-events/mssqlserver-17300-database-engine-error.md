---
title: MSSQLSERVER_17300 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17300 (Database Engine error)
ms.assetid: c1d6bfb6-28af-4df6-8087-25807602d282
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 193c07ee815aedb555528b1cdec3956e09bb2ce9
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553586"
---
# <a name="mssqlserver_17300"></a>MSSQLSERVER_17300
    
## <a name="details"></a>Dettagli  
  
|Attributo|valore|  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|17300|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|PROC_OUT_OF_SYSTASK_SESSIONS|  
|Testo del messaggio|Impossibile eseguire una nuova attività di sistema. Memoria insufficiente o numero di sessioni configurate maggiore del numero massimo consentito nel server. Verificare che la memoria del server sia adeguata. Per controllare il numero massimo di connessioni utente consentite, eseguire sp_configure con l'opzione 'user connections'. Per controllare il numero di sessioni, inclusi i processi utente, eseguire sys.dm_exec_sessions.|  
  
## <a name="explanation"></a>Spiegazione  
 Il tentativo di eseguire una nuova attività di sistema non è riuscito a causa di un problema di memoria insufficiente o perché è stato superato il numero di sessioni configurate nel server.  
  
## <a name="user-action"></a>Azione dell'utente  
 Verificare che la memoria del server sia sufficiente. Verificare il numero corrente di attività di sistema che utilizzano sys.dm_exec_sessions e il valore configurato di connessioni utente massime mediante sp_configure.  
  
 Eseguire le attività seguenti in modo appropriato:  
  
-   Aggiungere una quantità maggiore di memoria al server.  
  
-   Terminare uno o più sessioni.  
  
-   Aumentare il numero massimo di connessioni utente consentite sul server.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sys.dm_exec_sessions &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql)   
 [Configurare l'opzione di configurazione del server user connections](../../database-engine/configure-windows/configure-the-user-connections-server-configuration-option.md)   
 [KILL &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/kill-transact-sql)  
  
  
