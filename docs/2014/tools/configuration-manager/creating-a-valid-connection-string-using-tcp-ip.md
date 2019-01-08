---
title: Creazione di una stringa di connessione valida con TCP/IP | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connection strings [Database Engine]
- ports [SQL Server], connecting to
- TCP/IP [SQL Server], connection strings
- connection strings [Database Engine], TCP/IP
- aliases [SQL Server], TCP/IP
ms.assetid: ee5dbc2c-1fc6-42bd-bdf5-efa792557934
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6449b073adb406d15f41cfe02d477a05ad8b0b31
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52764253"
---
# <a name="creating-a-valid-connection-string-using-tcp-ip"></a>Creazione di una stringa di connessione valida con TCP/IP
  Per creare una stringa di connessione valida tramite TCP/IP, è necessario:  
  
-   Specificare un **Nome alias**.  
  
-   In **Server** immettere il nome di un server usando l'utilità **PING** o un indirizzo IP a cui sia possibile connettersi usando l'utilità **PING**. Per un'istanza denominata, aggiungere il nome dell'istanza.  
  
-   Specificare **TCP/IP** per il **Protocollo**.  
  
-   Facoltativamente, immettere un numero di porta in **Numero porta**. Il numero di porta predefinito è 1433, ossia il numero di porta dell'istanza predefinita di [!INCLUDE[ssDE](../../includes/ssde-md.md)] in un server. Per connettersi a un'istanza denominata o a un'istanza predefinita non in attesa sulla porta 1433, è necessario fornire il numero di porta o avviare il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser. Per informazioni sulla configurazione del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser, vedere [Servizio SQL Server Browser](../../../2014/tools/configuration-manager/sql-server-browser-service.md).  
  
 Al momento della connessione, tramite il componente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client vengono letti i valori relativi a server, protocollo e porta dal Registro di sistema per il nome alias specificato e viene creata una stringa di connessione nel formato `tcp:<servername>[\<instancename>],<port>` o `tcp:<IPAddress>[\<instancename>],<port>`.  
  
> [!NOTE]  
>  Per impostazione predefinita, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Firewall chiude la porta 1433. Considerato che [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] comunica sulla porta 1433, è necessario aprire nuovamente tale porta se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è configurato per restare in attesa di connessioni client in ingresso che usano TCP/IP. Per informazioni sulla configurazione di un firewall, vedere "Procedura: Configurare un firewall per l'accesso a SQL Server" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oppure vedere la documentazione relativa al firewall.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client supportano completamente sia IPv4 (protocollo IP versione 4) sia IPv6 (protocollo IP versione 6). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gestione configurazione accetta sia il formato IPv4 sia il formato IPv6 per gli indirizzi IP. Per informazioni su IPv6, vedere "Connessioni con IPv6" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="connecting-to-the-local-server"></a>Connessione al server locale  
 Quando si stabilisce una connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in esecuzione nello stesso computer del client, è possibile utilizzare `(local)` come nome del server. Non si tratta di un'operazione consigliabile, in quanto genera ambiguità, ma può risultare utile se si è sicuri che il client viene eseguito nello stesso computer del server. Se, ad esempio, si crea un'applicazione per gli utenti mobili non connessi, ad esempio il personale di vendita, e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verrà eseguito su computer portatili e usato per archiviare dati di progetto, un client che si connette a `(local)` si connetterà sempre a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in esecuzione sul portatile. In sostituzione di `localhost` è possibile usare la parola**o un punto (**. `(local)`).  
  
## <a name="verifying-your-connection-protocol"></a>Verifica del protocollo di connessione  
 La query seguente restituisce il protocollo utilizzato per la connessione corrente.  
  
```  
SELECT net_transport   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
  
```  
  
## <a name="examples"></a>Esempi  
 Connessione tramite il nome del server:  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             <servername>  
  
```  
  
 Connessione tramite il nome del server a un'istanza denominata:  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             <servername>\<instancename>  
  
```  
  
 Connessione tramite il nome del server a una porta specifica:  
  
```  
Alias Name         <serveralias>  
Port No            <port>  
Protocol           TCP/IP  
Server             <servername>  
  
```  
  
 Connessione tramite indirizzo IP:  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             <IPAddress>  
  
```  
  
 Connessione tramite indirizzo IP a un'istanza denominata:  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             <IPAddress>\<instancename>  
  
```  
  
 Connessione tramite indirizzo IP a una porta specificata:  
  
```  
Alias Name         <serveralias>  
Port No            <port number>  
Protocol           TCP/IP  
Server             <IPAddress>  
  
```  
  
 Connessione al computer locale tramite `(local)`:  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             (local)  
  
```  
  
 Connessione al computer locale tramite `localhost`:  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             localhost  
  
```  
  
 Connessione a un'istanza denominata nel computer locale tramite `localhost`:  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             localhost\<instancename>  
  
```  
  
 Connessione al computer locale tramite un punto:  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             .  
  
```  
  
 Connessione a un'istanza denominata nel computer locale tramite un punto:  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             .\<instancename>  
  
```  
  
> [!NOTE]  
>  Per informazioni su come specificare il protocollo di rete come un **sqlcmd** parametro, vedere "procedura: Connettersi al motore di database tramite sqlcmd.exe" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di una stringa di connessione valida mediante il protocollo di memoria condivisa](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)   
 [Creazione di una stringa di connessione valida tramite named pipe](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-named-pipes.md)   
 [Scelta di un protocollo di rete](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)  
  
  
