---
title: Creazione di una stringa di connessione valida tramite Named pipe | Microsoft Docs
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
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 12d5cb30217a0580d4da101d614b4930cfd8184b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63065549"
---
# <a name="creating-a-valid-connection-string-using-named-pipes"></a>Creazione di una stringa di connessione valida tramite named pipe
  Se non è stato modificato dall'utente, quando l'istanza predefinita di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in ascolto sul protocollo named pipes, Usa `\\.\pipe\sql\query` come nome della pipe. Il periodo di indica che il computer sia sul computer locale `pipe` indica che la connessione è una named pipe e `sql\query` è il nome della pipe. Per connettersi alla pipe predefinita, è necessario che il nome della pipe dell'alias sia `\\<computer_name>\pipe\sql\query`. Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è stato configurato per essere in attesa su una pipe diversa, è necessario che il nome della pipe utilizzi tale pipe. Se ad esempio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizza `\\.\pipe\unit\app` come pipe, è necessario che l'alias utilizzi `\\<computer_name>\pipe\unit\app` come nome della pipe.  
  
 Per creare un nome di pipe valido, è necessario:  
  
-   Specificare un **Nome alias**.  
  
-   Selezionare **Named pipe** come la **protocollo**.  
  
-   Immettere il **inviare tramite Pipe nome**. In alternativa, è possibile lasciare **nome della Pipe** vuoto e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager verrà completata il nome appropriato dopo aver specificato la **protocollo** e **Server**  
  
-   Specificare una **Server**. Per un'istanza denominata è possibile specificare un nome di server e un nome di istanza.  
  
 Al momento della connessione, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] componente Native Client legge il server, protocollo e nome della pipe i valori dal Registro di sistema per il nome alias specificato e crea un nome di pipe nel formato `np:\\<computer_name>\pipe\<pipename>` o `np:\\<IPAddress>\pipe\<pipename>`. Per un'istanza denominata, è il nome della pipe predefinita `\\<computer_name>\pipe\MSSQL$<instance_name>\sql\query`.  
  
> [!NOTE]  
>  Per impostazione predefinita, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Firewall chiude la porta 445. Poiché [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] comunica sulla porta 445, è necessario aprire nuovamente tale porta se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è configurato per restare in attesa di connessioni client in arrivo mediante Named Pipes. Per informazioni su come configurare un firewall, vedere "procedura: Configurare un Firewall per l'accesso di SQL Server"in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione in linea oppure consultare la documentazione del firewall.  
  
## <a name="connecting-to-the-local-server"></a>Connessione al server locale  
 Quando si stabilisce una connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in esecuzione nello stesso computer del client, è possibile utilizzare `(local)` come nome del server. L'utilizzo di `(local)` non è consigliabile in quanto genera ambiguità, ma può risultare utile se si è sicuri che il client venga eseguito nel computer desiderato. Se, ad esempio, si crea un'applicazione per gli utenti mobili non connessi, ad esempio il personale di vendita, e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verrà eseguito su computer portatili e utilizzato per archiviare dati di progetto, un client che si connette al server (local) si connetterà sempre all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in esecuzione sul portatile. In sostituzione di `localhost` è possibile utilizzare la parola `(local)` o un punto (.).  
  
## <a name="verifying-your-connection-protocol"></a>Verifica del protocollo di connessione  
 La query seguente restituisce il protocollo utilizzato per la connessione corrente.  
  
```  
SELECT net_transport   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
  
```  
  
## <a name="examples"></a>Esempi  
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
>  Per specificare il protocollo di rete come un **sqlcmd** parametro, vedere "procedura: Connettersi al motore di Database mediante sqlcmd.exe"in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione Online.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di una stringa di connessione valida mediante il protocollo di memoria condivisa](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)   
 [Creazione di una stringa di connessione valida con TCP/IP](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)   
 [Scelta di un protocollo di rete](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)  
  
  
