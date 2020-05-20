---
title: Creazione di una stringa di connessione valida tramite named pipe | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connection strings [Database Engine], named pipes
- pipes [SQL Server]
- pipes [SQL Server], connecting to
- aliases [SQL Server], named pipes
- Named Pipes [SQL Server], connection strings
ms.assetid: 90930ff2-143b-4651-8ae3-297103600e4f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1c22ee167318fb6e37194a3558637d9afc642111
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2020
ms.locfileid: "83001031"
---
# <a name="creating-a-valid-connection-string-using-named-pipes"></a>Creazione di una stringa di connessione valida tramite named pipe
  A meno che non venga modificato dall'utente, quando l'istanza predefinita di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in attesa sul protocollo Named Pipes, utilizza `\\.\pipe\sql\query` come nome della pipe. Il periodo indica che il computer è il computer locale, `pipe` indica che la connessione è una named pipe e `sql\query` è il nome della pipe. Per connettersi alla pipe predefinita, è necessario che il nome della pipe dell'alias sia `\\<computer_name>\pipe\sql\query`. Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è stato configurato per essere in attesa su una pipe diversa, è necessario che il nome della pipe utilizzi tale pipe. Se ad esempio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizza `\\.\pipe\unit\app` come pipe, è necessario che l'alias utilizzi `\\<computer_name>\pipe\unit\app` come nome della pipe.  
  
 Per creare un nome di pipe valido, è necessario:  
  
-   Specificare un **Nome alias**.  
  
-   Selezionare **Named Pipes** come **protocollo**.  
  
-   Immettere il **nome della pipe**. In alternativa, è possibile lasciare vuoto il **nome della pipe** e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager completerà il nome della pipe appropriato dopo aver specificato il **protocollo** e il **Server**  
  
-   Specificare un **Server**. Per un'istanza denominata è possibile specificare un nome di server e un nome di istanza.  
  
 Al momento della connessione, tramite il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] componente native client vengono letti i valori del nome del server, del protocollo e della pipe dal registro di sistema per il nome alias specificato e viene creato un nome di pipe nel formato `np:\\<computer_name>\pipe\<pipename>` o `np:\\<IPAddress>\pipe\<pipename>` . Per un'istanza denominata, il nome della pipe predefinita è `\\<computer_name>\pipe\MSSQL$<instance_name>\sql\query` .  
  
> [!NOTE]  
>  Per impostazione predefinita, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Firewall chiude la porta 445. Poiché [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] comunica sulla porta 445, è necessario aprire nuovamente tale porta se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è configurato per restare in attesa di connessioni client in arrivo mediante Named Pipes. Per informazioni sulla configurazione di un firewall, vedere "Procedura: Configurazione di un firewall per l’accesso a SQL Server" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oppure vedere la documentazione relativa al firewall.  
  
## <a name="connecting-to-the-local-server"></a>Connessione al server locale  
 Quando si stabilisce una connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in esecuzione nello stesso computer del client, è possibile utilizzare `(local)` come nome del server. L'utilizzo di `(local)` non è consigliabile in quanto genera ambiguità, ma può risultare utile se si è sicuri che il client venga eseguito nel computer desiderato. Se, ad esempio, si crea un'applicazione per gli utenti mobili non connessi, ad esempio il personale di vendita, e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verrà eseguito su computer portatili e utilizzato per archiviare dati di progetto, un client che si connette al server (local) si connetterà sempre all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in esecuzione sul portatile. In sostituzione di `localhost` è possibile utilizzare la parola `(local)` o un punto (.).  
  
## <a name="verifying-your-connection-protocol"></a>Verifica del protocollo di connessione  
 La query seguente restituisce il protocollo utilizzato per la connessione corrente.  
  
```  
SELECT net_transport   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
  
```  
  
## <a name="examples"></a>Esempio  
 Connessione tramite il nome del server alla pipe predefinita:  
  
```  
Alias Name         <serveralias>  
Pipe Name          <blank>  
Protocol           Named Pipes  
Server             <servername>  
  
```  
  
 Connessione tramite indirizzo IP alla pipe predefinita:  
  
```  
Alias Name         <serveralias>  
Pipe Name          <leave blank>  
Protocol           Named Pipes  
Server             <IPAddress>  
  
```  
  
 Connessione tramite il nome del server a una pipe non predefinita:  
  
```  
Alias Name         <serveralias>  
Pipe Name          \\<servername>\pipe\unit\app  
Protocol           Named Pipes  
Server             <servername>  
  
```  
  
 Connessione tramite il nome del server a un'istanza denominata:  
  
```  
Alias Name         <serveralias>  
Pipe Name          \\<servername>\pipe\MSSQL$<instancename>\SQL\query  
Protocol           Named Pipes  
Server             <servername>  
  
```  
  
 Connessione al computer locale tramite `localhost`:  
  
```  
Alias Name         <serveralias>  
Pipe Name          <blank>  
Protocol           Named Pipes  
Server             localhost  
  
```  
  
 Connessione al computer locale tramite un punto:  
  
```  
Alias Name         <serveralias>  
Pipe Name          <left blank>  
Protocol           Named Pipes  
Server             .  
  
```  
  
> [!NOTE]  
>  Per specificare il protocollo di rete come parametro **SQLCMD** , vedere "procedura: connessione al motore di database tramite sqlcmd. exe" nella documentazione in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] linea.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di una stringa di connessione valida tramite il protocollo Shared Memory](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)   
 [Creazione di una stringa di connessione valida tramite TCP IP](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)   
 [Scelta di un protocollo di rete](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)  
  
  
