---
title: Avviare SQL Server con la configurazione minima | Microsoft Docs
description: Acquisire familiarità con l'opzione di avvio con la configurazione minima in SQL Server. Scoprire quando e come usarla e come limita le funzionalità.
ms.custom: ''
ms.date: 01/20/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- minimal configuration [SQL Server]
- starting SQL Server, minimal configuration
ms.assetid: 4d733c99-28b3-42d8-b7f6-7b943b548173
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e6e301cd7dc29cc5e2a2cffc34066369ed67d57a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85763998"
---
# <a name="start-sql-server-with-minimal-configuration"></a>Avvio di SQL Server con la configurazione minima
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  In caso di problemi di configurazione che impediscono l'avvio del server, è possibile avviare un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando la configurazione minima. Si tratta dell'opzione di avvio **-f**. L'avvio di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la configurazione minima comporta l'attivazione automatica della modalità utente singolo per il server.  
  
 Quando si avvia un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la configurazione minima, si noti quanto segue:  
  
-   La connessione è consentita a un solo utente e il processo `CHECKPOINT` non viene eseguito.  
  
-   L'accesso remoto e il read-ahead sono disabilitati.  
  
-   Le stored procedure di avvio non vengono eseguite.  

-   `tempdb` viene configurato con la dimensione minima possibile.

-   Il controllo verrà disabilitato ma è comunque possibile eseguire AUDIT DDL. In pratica, l'opzione **-m** dovrebbe essere sufficiente per la maggior parte dei casi che richiedono la riconfigurazione di SQL Server Audit. Per altri dettagli sulla sicurezza nella configurazione di controllo, vedere [Controllo in SQL Server](https://docs.microsoft.com/previous-versions/sql/sql-server-2008/dd392015(v=sql.100)#security).
  
 Dopo aver avviato il server con la configurazione minima, è necessario modificare il valore o i valori delle opzioni del server appropriati e quindi arrestare e riavviare il server.  
  
> [!IMPORTANT]  
>  Usare l'utilità **sqlcmd** e la connessione amministrativa dedicata (DAC) per eseguire la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se si utilizza una connessione normale, arrestare il servizio SQL Server Agent prima di connettersi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modalità configurazione minima. In caso contrario, il servizio SQL Server Agent utilizzerà la connessione, bloccandola.  
  
## <a name="see-also"></a>Vedere anche  
 [Avvio, arresto o sospensione del servizio SQL Server Agent](https://msdn.microsoft.com/library/c95a9759-dd30-4ab6-9ab0-087bb3bfb97c)   
 [Connessione di diagnostica per gli amministratori di database](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)   
 [Utilità sqlcmd](../../tools/sqlcmd-utility.md)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Opzioni di avvio del servizio del motore di database](../../database-engine/configure-windows/database-engine-service-startup-options.md)  
  
  
