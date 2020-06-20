---
title: Entità a protezione diretta | Microsoft Docs
ms.custom: ''
ms.date: 10/14/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.roleproperties.selectobject.f1
helpviewer_keywords:
- securables [SQL Server]
- schemas [SQL Server], securables
- database securables [SQL Server]
- hierarchies [SQL Server], securables
- server securables [SQL Server]
ms.assetid: bfa748f0-70b0-453c-870a-04b7b205b9ff
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: ff2aaba72e2e5489694d31b35e594622c099acab
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "84997324"
---
# <a name="securables"></a>Entità a protezione diretta
  Le entità a protezione diretta sono le risorse il cui accesso è controllato dal sistema di autorizzazioni del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . Ad esempio, una tabella è un'entità a protezione diretta. Alcune entità a protezione diretta possono essere contenute da altre, creando gerarchie nidificate denominate ambiti, che possono a loro volta essere protetti. Gli ambiti a protezione diretta sono **server**, **database**e **schema**.  
  
## <a name="securable-scope-server"></a>Ambito a protezione diretta: server  
 L'ambito a protezione diretta **server** contiene le entità a protezione diretta seguenti:  
  
-   gruppo di disponibilità  
  
-   Endpoint  
  
-   Login  
  
-   Ruolo server  
  
-   Database  
  
## <a name="securable-scope-database"></a>Ambito a protezione diretta: database  
 L'ambito a protezione diretta **database** contiene le entità a protezione diretta seguenti:  
  
-   Ruolo applicazione  
  
-   Assembly  
  
-   Chiave asimmetrica  
  
-   Certificato  
  
-   Contratto  
  
-   Catalogo full-text  
  
-   Elenco di parole non significative full-text  
  
-   Tipo di messaggio  
  
-   Associazione al servizio remoto  
  
-   Ruolo (database)  
  
-   Route  
  
-   SCHEMA  
  
-   Elenco delle proprietà di ricerca  
  
-   Service  
  
-   Chiave simmetrica  
  
-   Utente  
  
## <a name="securable-scope-schema"></a>Ambito a protezione diretta: schema  
 L'ambito a protezione diretta **schema** contiene le entità a protezione diretta seguenti:  
  
-   Type  
  
-   Raccolta di XML Schema  
  
-   Oggetto - La classe oggetto include i membri seguenti:  
  
    -   Aggregate  
  
    -   Funzione  
  
    -   Procedura  
  
    -   Coda  
  
    -   Sinonimo  
  
    -   Tabella  
  
    -   Visualizza  
  
## <a name="controlling-access-to-a-securable"></a>Controllo di accesso a un'entità a protezione diretta  
 L'entità che riceve autorizzazione per un'entità a protezione diretta viene chiamata entità. Le entità più comuni sono gli account di accesso e gli utenti di database. L'accesso alle entità a protezione diretta viene controllato concedendo o negando autorizzazioni o aggiungendo accessi e utenti a ruoli che dispongono di accesso. Per informazioni sul controllo delle autorizzazioni, vedere [GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql), [REVOKE &#40;Transact-SQL&#41;](/sql/t-sql/statements/revoke-transact-sql), [DENY &#40;Transact-SQL&#41;](/sql/t-sql/statements/deny-transact-sql), [sp_addrolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql) e [sp_droprolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-droprolemember-transact-sql).  
  
> [!CAUTION]  
>  Le autorizzazioni predefinite concesso a oggetti di sistema durante l'installazione vengono valutati attentamente per individuare possibili minacce e non è quindi necessario modificarli per implementare misure di protezione avanzata dell'installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Eventuali modifiche alle autorizzazioni per gli oggetti di sistema possono limitare o compromettere la funzionalità e potrebbero lasciare l'installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in uno stato non supportato.  
  
## <a name="related-content"></a>Contenuto correlato  
 [Sicurezza di SQL Server](securing-sql-server.md)  
  
 [sys.database_principals &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-principals-transact-sql)  
  
 [sys.database_role_members &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-role-members-transact-sql)  
  
 [sys.server_principals &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-principals-transact-sql)  
  
 [sys.server_role_members &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-role-members-transact-sql)  
  
 [sys.sql_logins &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-logins-transact-sql)  
  
  
