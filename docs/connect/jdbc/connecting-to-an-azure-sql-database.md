---
title: Connessione a un database SQL di Azure | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 49645b1f-39b1-4757-bda1-c51ebc375c34
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 58a0b6f11fa28dca0e8aae98cb1794b12e3fc227
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "70155105"
---
# <a name="connecting-to-an-azure-sql-database"></a>Connessione a un database SQL di Azure

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

In questo argomento vengono illustrati i problemi dell'uso di [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] per la connessione a [!INCLUDE[ssAzure](../../includes/ssazure_md.md)]. Per altre informazioni sulla connessione a [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], vedere:  
  
- [Database SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview)  
  
- [Procedura: Connettersi a SQL Azure mediante JDBC](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java)  

- [Connessione tramite autenticazione di Azure Active Directory](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md)  
  
## <a name="details"></a>Dettagli

Per la connessione a [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] è necessario connettersi al database master per chiamare **SQLServerDatabaseMetaData.getCatalogs**.  
[!INCLUDE[ssAzure](../../includes/ssazure_md.md)] non supporta la restituzione dell'intero set di cataloghi da un database utente. **SQLServerDatabaseMetaData.getCatalogs** usa la vista sys.databases per ottenere i cataloghi. Vedere la discussione relativa alle autorizzazioni in [sys.databases (Transact-SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) per comprendere il comportamento di **SQLServerDatabaseMetaData.getCatalogs** in un [!INCLUDE[ssAzure](../../includes/ssazure_md.md)].  
  
## <a name="connections-dropped"></a>Connessioni eliminate

Durante la connessione a [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], è possibile che le connessioni inattive siano terminate da un componente di rete, ad esempio un firewall, dopo un periodo di inattività. In questo contesto esistono due tipi di inattività:  

- Inattività a livello TCP, in cui le connessioni possono essere eliminate da un certo numero di dispositivi di rete.  

- Inattività in SQL Azure Gateway, in cui potrebbero verificarsi messaggi TCP **keepalive** (rendendo la connessione non inattiva da una prospettiva TCP), ma in cui non è stata rilevata una query attiva da 30 minuti. In questo scenario il gateway determinerà che la connessione TDS è inattiva da 30 minuti e la terminerà.  
  
Per evitare l'eliminazione di connessioni inattive da un componente di rete, è consigliabile impostare le seguenti impostazioni del Registro di sistema, o le relative equivalenti non Windows, nel sistema operativo in cui viene caricato il driver:  
  
|Impostazione del Registro di sistema|Valore consigliato|  
|----------------------|-----------------------|  
|HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\KeepAliveTime|30000|  
|HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\KeepAliveInterval|1000|  
|HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\TcpMaxDataRetransmissions|10|  
  
Riavviare il computer per attivare le impostazioni del Registro di sistema.  

A tale scopo, durante l'esecuzione di Azure creare un'attività di avvio per aggiungere le chiavi del Registro di sistema.  Ad esempio, aggiungere l'attività di avvio al file di definizione del servizio:  

```xml
<Startup>  
    <Task commandLine="AddKeepAlive.cmd" executionContext="elevated" taskType="simple">  
    </Task>  
</Startup>  
```

Successivamente, aggiungere il file AddKeepAlive.cmd al progetto in uso. Impostare l'impostazione "Copia nella directory di output" su Copia sempre. Di seguito è riportato un esempio di file AddKeepAlive.cmd:  

```bat
if exist keepalive.txt goto done  
time /t > keepalive.txt  
REM Workaround for JDBC keep alive on SQL Azure  
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v KeepAliveTime /t REG_DWORD /d 30000 >> keepalive.txt  
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v KeepAliveInterval /t REG_DWORD /d 1000 >> keepalive.txt  
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v TcpMaxDataRetransmissions /t REG_DWORD /d 10 >> keepalive.txt  
shutdown /r /t 1  
:done  
```

## <a name="appending-the-server-name-to-the-userid-in-the-connection-string"></a>Accodamento del nome del server all'ID utente nella stringa di connessione  

Prima della versione 4.0 di [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], durante la connessione a [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] veniva richiesto l'accodamento del nome del server all'ID utente nella stringa di connessione. Ad esempio: user@servername. A partire dalla versione 4.0 di [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] l'accodamento di @servername all'ID utente nella stringa di connessione non è più necessario.  

## <a name="using-encryption-requires-setting-hostnameincertificate"></a>Impostazione di hostNameInCertificate obbligatoria per l'uso della crittografia

Nelle versioni di [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] precedenti alla 7.2, quando ci si connette a un [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] è necessario specificare **hostNameInCertificate** se si specifica **encrypt=true** (se il nome server nella stringa di connessione è *shortName*.*domainName*, impostare la proprietà **hostNameInCertificate** su \*.*domainName*). Questa proprietà è facoltativa a partire dalla versione 7.2 del driver.

Ad esempio:

```java
jdbc:sqlserver://abcd.int.mscds.com;databaseName=myDatabase;user=myName;password=myPassword;encrypt=true;hostNameInCertificate=*.int.mscds.com;
```

## <a name="see-also"></a>Vedere anche

[Connessione a SQL Server con il driver JDBC](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
