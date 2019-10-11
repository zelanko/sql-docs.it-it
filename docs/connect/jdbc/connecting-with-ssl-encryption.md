---
title: Connessione con crittografia | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: vanto
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ec91fa8a-ab7e-4c1e-a05a-d7951ddf33b1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cff4228404690147d97a44f6f5dd43b1a180153c
ms.sourcegitcommit: fd3e81c55745da5497858abccf8e1f26e3a7ea7d
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2019
ms.locfileid: "71713288"
---
# <a name="connecting-with-encryption"></a>Connessione tramite la crittografia
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Gli esempi in questo articolo descrivono come usare le proprietà della stringa di connessione che consentono alle applicazioni di usare la crittografia TLS (Transport Layer Security) in un'applicazione Java. Per altre informazioni sulle nuove proprietà della stringa di connessione, ad esempio **encrypt**, **trustServerCertificate**, **trustStore**, **trustStorePassword** e **hostNameInCertificate**, vedere [Impostazione delle proprietà delle connessioni](../../connect/jdbc/setting-the-connection-properties.md).  
  
 Se la proprietà **encrypt** è impostata su **true** e la proprietà **trustServerCertificate** è impostata su **true**, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] non convalida il certificato TLS di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ciò è in genere necessario per consentire le connessioni in ambienti di test, ad esempio nel caso in cui l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] abbia solo un certificato autofirmato.  
  
 L'esempio di codice seguente illustra come impostare la proprietà **trustServerCertificate** in una stringa di connessione:  
  
```java
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true;trustServerCertificate=true";  
```  
  
 Se la proprietà **encrypt** è impostata su **true** e la proprietà **trustServerCertificate** è impostata su **false**, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] convaliderà il certificato TLS di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La convalida del certificato del server fa parte dell'handshake TLS e assicura che il server a cui si esegue la connessione sia quello corretto. Per la convalida del certificato del server è necessario che in fase di connessione venga fornito il materiale relativo all'attendibilità usando in modo esplicito le proprietà di connessione **trustStore** e **trustStorePassword** oppure usando in modo implicito l'archivio di scopi predefinito di JVM (Java Virtual Machine) sottostante.  
  
 La proprietà **trustStore** specifica il percorso (incluso il nome file) del file trustStore, che contiene l'elenco di certificati considerati attendibili dal client. La proprietà **trustStorePassword** specifica la password usata per verificare l'integrità dei dati del file trustStore. Per ulteriori informazioni sull'utilizzo dell'archivio di attendibilità predefinito di JVM, vedere la pagina relativa alla [configurazione del client per la crittografia](../../connect/jdbc/configuring-the-client-for-ssl-encryption.md).  
  
 L'esempio di codice seguente illustra come impostare le proprietà **trustStore** e **trustStorePassword** in una stringa di connessione:  
  
```java
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true; trustServerCertificate=false;" +  
     "trustStore=storeName;trustStorePassword=storePassword";  
```  
  
 Il driver JDBC è dotato di una proprietà aggiuntiva, **hostNameInCertificate**, che specifica il nome host del server. Il valore di questa proprietà deve corrispondere alla proprietà relativa al soggetto del certificato.  
  
 L'esempio di codice seguente illustra come usare la proprietà **hostNameInCertificate** in una stringa di connessione:  
  
```java
String connectionUrl =   
    "jdbc:sqlserver://localhost:1433;" +  
     "databaseName=AdventureWorks;integratedSecurity=true;" +  
     "encrypt=true; trustServerCertificate=false;" +  
     "trustStore=storeName;trustStorePassword=storePassword" +  
     "hostNameInCertificate=hostName";  
```  
  
> [!NOTE]  
>  In alternativa, è possibile impostare il valore delle proprietà di connessione usando i metodi **setter** appropriati offerti dalla classe [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md).  
  
 Se la proprietà **Encrypt** è impostata su **true** e la proprietà **TrustServerCertificate** è impostata su **false** e il nome del server nella stringa di connessione non corrisponde al nome del server nel certificato TLS, l'errore seguente sarà Rilasciato: `The driver couldn't establish a secure connection to SQL Server by using Secure Sockets Layer (SSL) encryption. Error: "java.security.cert.CertificateException: Failed to validate the server name in a certificate during Secure Sockets Layer (SSL) initialization."`. A partire dalla versione 7,2, il driver supporta la corrispondenza dei criteri di ricerca con caratteri jolly nell'etichetta a sinistra del nome del server nel certificato TLS.

## <a name="see-also"></a>Vedere anche

 [Uso della crittografia](../../connect/jdbc/using-ssl-encryption.md) per la [protezione delle applicazioni del driver JDBC](../../connect/jdbc/securing-jdbc-driver-applications.md)