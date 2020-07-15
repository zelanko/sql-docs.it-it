---
title: Server remoti | Microsoft Docs
description: Informazioni sui server remoti che sono stati sostituiti con i server collegati in SQL Server. Visualizzare informazioni su funzionalità, configurazione e sicurezza.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- server management [SQL Server], remote servers
- remote servers [SQL Server], configuring
- remote servers [SQL Server]
- servers [SQL Server], remote
- remote access option
ms.assetid: abf0fa24-f199-4273-9a1a-e8787ac9bee1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 393688d3ecb5d0e29a1b05aa6f00d7eec7ca7e22
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85651575"
---
# <a name="remote-servers"></a>Server remoti
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  I server remoti sono supportati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esclusivamente per compatibilità con le versioni precedenti. È opportuno impostare le nuove applicazioni in modo che utilizzino i server collegati. Per altre informazioni, vedere [Server collegati &#40;Motore di database&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md).  
  
 Tramite la configurazione con server remoto, un client connesso a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può eseguire una stored procedure su un'altra istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] senza stabilire un'ulteriore connessione. Il server al quale il client è connesso accetta la richiesta e la inoltra al server remoto per conto del client. Il server remoto elabora la richiesta e restituisce i risultati al server di origine, che a sua volta li passa al client. Quando si imposta la configurazione con server remoto è bene prestare attenzione alla modalità di impostazione della sicurezza.  
  
 Se si desidera impostare una configurazione server per l'esecuzione di stored procedure su un altro server e non sono attive configurazioni con server remoti, utilizzare i server collegati anziché i server remoti. I server collegati supportano sia le stored procedure che le query distribuite, mentre i server remoti supportano soltanto le stored procedure.  
  
## <a name="remote-server-details"></a>Informazioni sui server remoti  
 I server remoti vengono configurati a coppie. È necessario configurare i due server della coppia in modo che si riconoscano a vicenda come server remoti.  
  
 Nella maggior parte dei casi non è necessario impostare opzioni di configurazione per i server remoti. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] I valori predefiniti impostati sul computer locale e sul computer remoto consentono le connessioni ai server remoti.  
  
 Per ottenere il corretto funzionamento dell'accesso ai server remoti, è necessario che l'opzione di configurazione **remote access** sia impostata su 1 sia nel computer locale che nel computer remoto Questa è l'impostazione predefinita.  **remote access** controlla gli accessi dai server remoti. È possibile reimpostare questa opzione di configurazione usando la stored procedure **sp_configure** di [!INCLUDE[tsql](../../includes/tsql-md.md)] oppure [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Per impostare l'opzione in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], nella pagina **Connessioni** della pagina Proprietà server selezionare l'opzione **Consenti connessioni remote al server**. Per accedere alla pagina **Connessioni** della finestra di dialogo Proprietà server, in Esplora oggetti fare clic con il pulsante destro del mouse sul nome del server e quindi scegliere **Proprietà**. Nella pagina **Proprietà server** fare clic sulla pagina **Connessioni** .  
  
 Dal server locale è possibile disabilitare una configurazione con server remoto, impedendo l'accesso a tale server locale da parte degli utenti del server remoto a cui è abbinato.  
  
## <a name="security-for-remote-servers"></a>Sicurezza per server remoti  
 Per abilitare le chiamate di procedura remota (RPC, Remote Procedure Call) verso un server remoto, è necessario impostare mapping di account di accesso nel server remoto e, in alcuni casi, nel server locale in cui è in esecuzione un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per impostazione predefinita, le chiamate RPC sono disabilitate in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa configurazione migliora la sicurezza del server riducendone i punti vulnerabili. Prima di utilizzare le chiamate RPC è necessario abilitare questa caratteristica. Per altre informazioni, vedere [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
### <a name="setting-up-the-remote-server"></a>Configurazione del server remoto  
 Nel server remoto è necessario impostare mapping di account di accesso remoto. Tali mapping consentono al server remoto di eseguire il mapping dell'accesso in entrata relativo a una connessione RPC da un server specifico a un account di accesso locale. I mapping di accesso remoto possono essere configurati usando la stored procedure **sp_addremotelogin** nel server remoto.  
  
> [!NOTE]  
>  L'opzione **trusted** di  **sp_remoteoption** non è supportata in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="setting-up-the-local-server"></a>Configurazione del server locale  
 Per gli accessi locali autenticati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , non è necessario configurare un mapping di accesso nel server locale. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa l'account di accesso locale e la password per la connessione al server remoto. Per gli account di accesso di Windows, configurare un mapping di account di accesso locali in un server locale per definire l'account e la password utilizzati da un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la connessione RPC a un server remoto.  
  
 Per gli account di accesso creati dall'autenticazione di Windows, è necessario creare un mapping a un nome di account di accesso e una password usando la stored procedure **sp_addlinkedservlogin** . Il nome dell'account di accesso e la password devono corrispondere all'account di accesso e alla password in ingresso previsti dal server remoto, in base a ciò che è stato creato dalla stored procedure **sp_addremotelogin**.  
  
> [!NOTE]  
>  Se possibile, usare l'autenticazione di Windows.  
  
### <a name="remote-server-security-example"></a>Esempio di sicurezza del server remoto  
 Considerare queste installazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] : **serverSend** e **serverReceive**. **serverReceive** viene configurata per eseguire il mapping di un account di accesso in ingresso da **serverSend**, denominato **Sales_Mary**, a un account di accesso autenticato di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in **serverReceive**, denominato **Alice**. Viene eseguito il mapping di un altro account di accesso in ingresso da **serverSend**, denominato **Joe**, a un account di accesso autenticato di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in **serverReceive** _,_ denominato **Joe**.  
  
 Il codice di esempio di Transact-SQL seguente configura `serverSend` per l'esecuzione di RPC su `serverReceive`.  
  
```  
--Create remote server entry for RPCs   
--from serverSend in serverReceive.  
EXEC sp_addserver 'serverSend';  
GO  
  
--Create remote login mapping for login 'Sales_Mary' from serverSend  
--to Alice.  
EXEC sp_addremotelogin 'serverSend', 'Alice', 'Sales_Mary';  
GO  
--Create remote login mapping for login Joe from serverReceive   
--to same login.  
--Assumes same password for Joe in both servers.  
EXEC sp_addremotelogin 'serverSend', 'Joe', 'Joe';  
GO  
```  
  
 In `serverSend`viene creato un mapping di account di accesso locale autenticato `Sales\Mary` di Windows a un account di accesso `Sales_Mary`. Per l'account `Joe`non è necessario alcun mapping locale, in quanto per impostazione predefinita vengono utilizzati lo stesso nome di account di accesso e la stessa password e `serverReceive` dispone già di un mapping per `Joe`.  
  
```  
--Create a remote server entry for RPCs from serverReceive.  
EXEC sp_addserver 'serverReceive';  
GO  
--Create a local login mapping for the Windows authenticated login.  
--Sales\Mary to Sales_Mary. The password should match the  
--password for the login Sales_Mary in serverReceive.  
EXEC sp_addlinkedsrvlogin 'serverReceive', false, 'Sales\Mary',  
   'Sales_Mary', '430[fj%dk';  
GO  
```  
  
## <a name="viewing-local-or-remote-server-properties"></a>Visualizzazione delle proprietà dei server locali o remoti  
 Per esaminare gli attributi per i server locali o remoti, è possibile usare la stored procedure estesa **xp_msver** . Tali attributi includono il numero di versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il tipo e il numero di processori nel computer e la versione del sistema operativo. Dal server locale è possibile visualizzare database, file, account di accesso e strumenti di un server remoto. Per altre informazioni, vedere [xp_msver &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/xp-msver-transact-sql.md).  
  
## <a name="related-tasks"></a>Attività correlate  
 [Server collegati &#40;Motore di database&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)  
  
## <a name="related-content"></a>Contenuto correlato  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
 [Configurare l'opzione di configurazione del server remote access](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)  
  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)  
  
  
