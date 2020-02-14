---
title: Accedere a SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server, logging in
- services [SQL Server], logging in
- TCP connection string
- connecting to the Database Engine
- logins [SQL Server], about logging in
- named pipe connection string
- log ins [SQL Server]
- shared memory connection string
- logging in [SQL Server]
- logins [SQL Server]
ms.assetid: 77158a9a-d638-4818-90a1-cb2eb57df514
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6b64ac7463e9a1e3ef62d87d5cf9d6096be275cf
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "67998011"
---
# <a name="logging-in-to-sql-server"></a>Accesso a SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  È possibile accedere a un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con uno degli strumenti di amministrazione a interfaccia grafica oppure dal prompt dei comandi.  
  
 Se si accede a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con uno strumento di amministrazione a interfaccia grafica, ad esempio [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], viene richiesto di specificare il nome del server, un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e una password, se necessario. Se si accede a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando l'autenticazione di Windows non è necessario specificare un account di accesso di SQL Server ogni volta che si accede a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizza infatti l'account di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows dell'utente per eseguire automaticamente l'accesso. Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene eseguito in modalità mista (modalità di autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e di Windows) e si sceglie di eseguire l'accesso usando l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario specificare un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e una password. Se possibile, usare l'autenticazione di Windows.  
  
> [!NOTE]  
>  Se al momento dell'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]è stata selezionata una regola di confronto con distinzione tra maiuscole e minuscole, anche l'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporterà la distinzione tra maiuscole e minuscole.  
  
## <a name="format-for-specifying-the-name-of-sql-server"></a>Formattare per specificare il nome di SQL Server  
 Quando si stabilisce una connessione a un'istanza di [!INCLUDE[ssDE](../../includes/ssde-md.md)] è necessario specificare il nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] corrisponde all'istanza predefinita (un'istanza senza nome), specificare il nome del computer in cui è installato [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oppure l'indirizzo IP del computer. Se l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è un'istanza denominata (come ad esempio SQLEXPRESS), specificare il nome del computer in cui è installato [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oppure l'indirizzo IP del computer, quindi aggiungere una barra e il nome dell'istanza.  
  
 Negli esempi riportati di seguito viene effettuata una connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in esecuzione su un computer denominato APPHOST. In caso di specifica di un'istanza denominata, negli esempi viene utilizzato un nome di istanza SQLEXPRESS.  
  
 **Esempi:**  
  
|Tipo di istanza|Voce per il nome del server|  
|----------------------|-------------------------------|  
|Connessione a un'istanza predefinita utilizzando il protocollo predefinito.|APPHOST|  
|Connessione a un'istanza denominata utilizzando il protocollo predefinito. |APPHOST\SQLEXPRESS|  
|Connessione a un'istanza predefinita sullo stesso computer utilizzando un punto per indicare che l'istanza è in esecuzione sul computer locale.|.|  
|Connessione a un'istanza denominata sullo stesso computer utilizzando un punto per indicare che l'istanza è in esecuzione sul computer locale.|.\SQLEXPRESS|  
|Connessione a un'istanza predefinita sullo stesso computer utilizzando localhost per indicare che l'istanza è in esecuzione sul computer locale.|localhost|  
|Connessione a un'istanza denominata sullo stesso computer utilizzando localhost per indicare che l'istanza è in esecuzione sul computer locale.|localhost\SQLEXPRESS|  
|Connessione a un'istanza predefinita sullo stesso computer utilizzando (local) per indicare che l'istanza è in esecuzione sul computer locale.|(local)|  
|Connessione a un'istanza denominata sullo stesso computer utilizzando (local) per indicare che l'istanza è in esecuzione sul computer locale.|(local)\SQLEXPRESS|  
|Connessione a un'istanza predefinita sullo stesso computer che forza una connessione di memoria condivisa.|lpc:APPHOST|  
|Connessione a un'istanza denominata sullo stesso computer che forza una connessione di memoria condivisa.|lpc:APPHOST\SQLEXPRESS|  
|Connessione a un'istanza predefinita che è in ascolto sull'indirizzo TCP 192.168.17.28 utilizzando un indirizzo IP.|192.168.17.28|  
|Connessione a un'istanza denominata che è in ascolto sull'indirizzo TCP 192.168.17.28 utilizzando un indirizzo IP.|192.168.17.28\SQLEXPRESS|  
|Connessione a un'istanza predefinita che non è in ascolto sulla porta TCP predefinita, specificando la porta utilizzata, in questo caso 2828. (La specifica di un numero di porta non è necessaria se [!INCLUDE[ssDE](../../includes/ssde-md.md)] è in ascolto sulla porta predefinita (1433).)|APPHOST,2828|  
|Connessione a un'istanza denominata su una porta TCP designata, in questo caso 2828. (La specifica di un numero di porta è spesso necessaria se il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser non è in esecuzione nel computer host.)|APPHOST,2828|  
|Connessione a un'istanza predefinita che non è in ascolto sulla porta TCP predefinita, specificando sia l'indirizzo IP che la porta TCP utilizzata, in questo caso 2828.|192.168.17.28,2828|  
|Connessione a un'istanza denominata specificando sia l'indirizzo IP che la porta TCP utilizzata, in questo caso 2828.|192.168.17.28\SQLEXPRESS,2828|  
|Connessione a un'stanza predefinita per nome, forzando una connessione TCP.|tcp:APPHOST|  
|Connessione a un'stanza denominata per nome, forzando una connessione TCP.|tcp:APPHOST\SQLEXPRESS|  
|Connessione a un'istanza predefinita specificando un nome di named pipe.|\\\APPHOST\pipe\SQL\query|  
|Connessione a un'istanza denominata specificando un nome di named pipe.|\\\APPHOST\pipe\MSSQL$SQLEXPRESS\SQL\query|  
|Connessione a un'stanza predefinita per nome, forzando una connessione di named pipe.|np:APPHOST|  
|Connessione a un'stanza denominata per nome, forzando una connessione di named pipe.|np:APPHOST\SQLEXPRESS|  
  
## <a name="verifying-your-connection-protocol"></a>Verifica del protocollo di connessione  
 In caso di connessione a [!INCLUDE[ssDE](../../includes/ssde-md.md)], la query seguente restituirà il protocollo utilizzato per la connessione corrente, insieme al metodo di autenticazione (NTLM o Kerberos) e indicherà se la connessione è crittografata.  
  
```sql  
SELECT net_transport, auth_scheme, encrypt_option   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
```  
  
## <a name="related-tasks"></a>Attività correlate  
 [Accedere a un'istanza di SQL Server &#40;prompt dei comandi&#41;](../../database-engine/configure-windows/log-in-to-an-instance-of-sql-server-command-prompt.md)  
  
 Le risorse seguenti possono contribuire alla risoluzione di un problema di connessione.  
  
-   [Risoluzione dei problemi relativi alla connessione al motore di database di SQL Server](https://social.technet.microsoft.com/wiki/contents/articles/how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx)  
  
-   [Passaggi per risolvere i problemi di connettività di SQL](https://blogs.msdn.com/b/sql_protocols/archive/2008/04/30/steps-to-troubleshoot-connectivity-issues.aspx)  
  
## <a name="related-content"></a>Contenuto correlato  
 [Scegliere una modalità di autenticazione](../../relational-databases/security/choose-an-authentication-mode.md)  
  
 [Utilizzo dell'utilità sqlcmd](../../relational-databases/scripting/sqlcmd-use-the-utility.md)  
  
 [Creazione di un account di accesso](../../t-sql/lesson-2-configuring-permissions-on-database-objects.md)
  
  
