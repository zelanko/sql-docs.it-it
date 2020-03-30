---
title: Costruzione dell'URL della connessione | Microsoft Docs
ms.custom: ''
ms.date: 01/29/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 44996746-d373-4f59-9863-a8a20bb8024a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2461413e6f41c82404ac11cc5769b74993f13ed8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "77004536"
---
# <a name="building-the-connection-url"></a>Costruzione dell'URL della connessione
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Il formato generale dell'URL della connessione è  
  
 `jdbc:sqlserver://[serverName[\instanceName][:portNumber]][;property=value[;property=value]]`  
  
 dove:  
  
-   **jdbc:sqlserver://** (obbligatorio) è noto come sottoprotocollo ed è costante.  
  
-   **serverName** (facoltativo) indica l'indirizzo del server a cui viene eseguita la connessione. Si tratta del valore DNS o dell'indirizzo IP oppure di localhost o 127.0.0.1 nel caso del computer locale. Se non viene specificato nell'URL della connessione, il nome del server deve essere specificato nella raccolta delle proprietà.  
  
-   **instanceName** (facoltativo) indica l'istanza su serverName a cui viene eseguita la connessione. Se non viene specificata alcuna impostazione, la connessione viene eseguita all'istanza predefinita.  
  
-   **portNumber** (facoltativo) indica la porta su serverName a cui viene eseguita la connessione. Il valore predefinito è 1433. Se si usa tale valore, non è necessario specificare nell'URL né la porta né il carattere ':' che la precede.  
  
    > [!NOTE]  
    >  Per una connessione ottimale a un'istanza denominata, si consiglia di impostare un valore per portNumber. In questo modo si evita un round trip al server per determinare il numero di porta. Se si utilizzano sia portNumber che instanceName, portNumber avrà la precedenza e instanceName verrà ignorato.  
  
-   **property** (facoltativo) indica una o più proprietà della connessione. Per altre informazioni, vedere [Impostazione delle proprietà di connessione](../../connect/jdbc/setting-the-connection-properties.md). È possibile specificare qualsiasi proprietà presente nell'elenco. Le proprietà, tuttavia, possono essere delimitate solo usando il carattere di punto e virgola (';') e non possono essere duplicate.  
  
> [!CAUTION]  
>  Per garantire maggiore sicurezza, si consiglia di evitare di costruire l'URL della connessione sulla base dei dati inseriti dall'utente. Nell'URL dovrebbero essere specificati solo il nome del server e il driver. Per i valori relativi a nome utente e password, utilizzare le raccolte delle proprietà della connessione. Per altre informazioni sulla sicurezza nelle applicazioni JDBC, vedere [Protezione delle applicazioni del driver JDBC](../../connect/jdbc/securing-jdbc-driver-applications.md).  
  
## <a name="connection-examples"></a>Esempi di connessioni  
 Connessione al database predefinito sul computer locale utilizzando un nome utente e la password:  
  
 `jdbc:sqlserver://localhost;user=MyUserName;password=*****;`  
  
> [!NOTE]  
>  Sebbene nell'esempio precedente siano stati utilizzati un nome utente e una password nella stringa di connessione, è consigliabile utilizzare la sicurezza integrata per garantire maggiore protezione. Per altre informazioni, vedere la sezione [Connessione con l'autenticazione integrata](#Connectingintegrated) più avanti in questo argomento.  
  
 La seguente stringa di connessione illustra come connettersi a un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite l'autenticazione integrata e Kerberos da un'applicazione in esecuzione su un sistema operativo supportato da [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]:  
  
```java
jdbc:sqlserver://;servername=server_name;integratedSecurity=true;authenticationScheme=JavaKerberos  
```  
  
 Connessione al database predefinito sul computer locale utilizzando l'autenticazione integrata:  
  
 `jdbc:sqlserver://localhost;integratedSecurity=true;`  
  
 Connessione a un database denominato su un server remoto:  
  
 `jdbc:sqlserver://localhost;databaseName=AdventureWorks;integratedSecurity=true;`  
  
 Connessione alla porta predefinita su un server remoto:  
  
 `jdbc:sqlserver://localhost:1433;databaseName=AdventureWorks;integratedSecurity=true;`  
  
 Connessione specificando un nome di applicazione personalizzato:  
  
 `jdbc:sqlserver://localhost;databaseName=AdventureWorks;integratedSecurity=true;applicationName=MyApp;`  
  
## <a name="named-and-multiple-sql-server-instances"></a>Più istanze denominate di SQL Server  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente l'installazione di più istanze di database per server. Ciascuna istanza è definita in base a un nome specifico. Per eseguire la connessione a un'istanza denominata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile specificare il numero di porta di tale istanza (metodo preferito) oppure specificare il nome dell'istanza come proprietà dell'URL di JDBC o proprietà **datasource**. Se non viene specificato né il nome né il numero della porta, viene creata una connessione all'istanza predefinita. Vedere gli esempi seguenti:  
  
 Per utilizzare un numero di porta, procedere come segue:  
  
 `jdbc:sqlserver://localhost:1433;integratedSecurity=true;<more properties as required>;`  
  
 Per utilizzare una proprietà URL di JDBC, procedere come segue:  
  
 `jdbc:sqlserver://localhost;instanceName=instance1;integratedSecurity=true;<more properties as required>;`  
  
## <a name="escaping-values-in-the-connection-url"></a>Uso della sequenza di escape dei valori nell'URL della connessione  
 Se nell'URL della connessione vengono utilizzati caratteri speciali, quali spazi, punti e virgola, virgolette, è necessario includere alcune parti dell'URL in una sequenza di escape. L'impostazione di una sequenza di escape per tali caratteri è supportata nel driver JDBC se tali caratteri sono racchiusi tra parentesi graffe. Ad esempio con {;} il carattere di punto e virgola è incluso in una sequenza di escape.  
  
 I valori inclusi in una sequenza di escape possono contenere caratteri speciali (in particolare '=', ';', '[]' e lo spazio) ma non parentesi graffe. I valori che contengono parentesi graffe e che devono essere inclusi in una sequenza di escape devono essere aggiunti a una raccolta di proprietà.  
  
> [!NOTE]  
>  Lo spazio all'interno delle parentesi graffe è letterale e non viene eliminato.  
  
##  <a name="connecting-with-integrated-authentication-on-windows"></a><a name="Connectingintegrated"></a> Connessione con autenticazione integrata in Windows  
 Il driver JDBC supporta l'utilizzo dell'autenticazione integrata di tipo 2 nei sistemi operativi Windows tramite la proprietà della stringa di connessione integratedSecurity. Per usare l'autenticazione integrata, copiare il file mssql-jdbc_auth-\<versione>-\<arch>.dll in una directory nel percorso di sistema di Windows nel computer in cui è installato il driver JDBC.  
  
 I file mssql-jdbc_auth-\<versione>-\<arch>.dll sono installati nella posizione seguente:  
  
 \<*directory di installazione*>\<\sqljdbc_*Version*>\\<*Language>* \auth\  
  
 Per i sistemi operativi supportati da [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], vedere [Uso dell'autenticazione integrata Kerberos per la connessione a SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md) per una descrizione di una funzionalità aggiunta in [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] che consente a un'applicazione di connettersi a un database tramite l'autenticazione integrata Kerberos di tipo 4.  
  
> [!NOTE]  
>  Se si esegue Java Virtual Machine (JVM) a 32 bit, usare il file mssql-jdbc_auth-\<versione>-\<arch>.dll nella cartella x86, anche se la versione del sistema operativo è x64. Se si esegue JVM a 64 bit in un processore x64, usare il file mssql-jdbc_auth-\<versione>-\<arch>.dll nella cartella x64.  
  
 In alternativa è possibile impostare la proprietà di sistema java.library.path in modo da specificare la directory di mssql-jdbc_auth-\<versione>-\<arch>.dll. Ad esempio, se il driver JDBC è installato nella directory predefinita, specificare il percorso della DLL utilizzando il seguente argomento della VM (Virtual Machine) quando l'applicazione Java viene avviata:  
  
 `-Djava.library.path=C:\Microsoft JDBC Driver 6.4 for SQL Server\sqljdbc_<version>\enu\auth\x86`  
  
## <a name="connecting-with-ipv6-addresses"></a>Connessione con indirizzi IPv6  
 Il driver JDBC supporta l'utilizzo di indirizzi IPv6 con la raccolta delle proprietà di connessione e con la proprietà della stringa di connessione serverName. Il valore serverName iniziale, quale jdbc:*sqlserver*://*serverName*, non è supportato nelle stringhe di connessione per gli indirizzi IPv6. L'uso di un nome per *serverName* (anziché dell'indirizzo IPv6 non elaborato) nella connessione garantirà il funzionamento corretto in ogni caso. Di seguito sono riportati alcuni esempi.  
  
 **Uso della proprietà serverName**  
  
 `jdbc:sqlserver://;serverName=3ffe:8311:eeee:f70f:0:5eae:10.203.31.9\\instance1;integratedSecurity=true;`  
  
 **Uso della raccolta di proprietà**  
  
 `Properties pro = new Properties();`  
  
 `pro.setProperty("serverName", "serverName=3ffe:8311:eeee:f70f:0:5eae:10.203.31.9\\instance1");`  
  
 `Connection con = DriverManager.getConnection("jdbc:sqlserver://;integratedSecurity=true;", pro);`  
  
## <a name="see-also"></a>Vedere anche  
 [Connessione a SQL Server con il driver JDBC](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
