---
title: Sicurezza dell'applicazione | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 940879b4-aa0f-41ce-a369-6cfc0e78e01d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 81c57e5ab7ca88267693690992106b5f39e2af82
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "69028508"
---
# <a name="application-security"></a>Sicurezza dell'applicazione
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Quando si usa [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], è importante adottare tutte le misure necessarie per garantire la sicurezza delle applicazioni. Nelle sezioni seguenti vengono fornite informazioni relative alle procedure da implementare a questo scopo.  
  
## <a name="using-java-policy-permissions"></a>Uso di autorizzazioni basate sui criteri Java  
 Quando si usa [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], è importante specificare le autorizzazioni basate sui criteri Java necessarie richieste dal driver JDBC. Java Runtime Environment (JRE) offre un modello di sicurezza completo utilizzabile in fase di esecuzione per determinare se un thread dispone dei diritti di accesso a una risorsa. L'accesso può essere gestito grazie ai file dei criteri di sicurezza, i quali, a loro volta, sono gestiti dal distributore e dal ruolo sysadmin del contenitore. Le autorizzazioni elencate in questo argomento sono quelle che influiscono sul driver JDBC.  
  
 Di seguito è riportato un esempio di autorizzazione tipica disponibile nel file dei criteri:  
  
```  
// Example policy file entry.  
grant [signedBy <signer>,] [codeBase <code source>] {  
   permission  <class>  [<name> [, <action list>]];  
};  
```  
  
 La base di codice seguente deve essere limitata alla base del codice del driver JDBC in modo da concedere il livello minore possibile di privilegi.  
  
```  
grant codeBase "file:/install_dir/lib/-" {  
  
// Grant access to data source.  
permission java.util.PropertyPermission "java.naming.*", "read,write";  
  
// Specify which hosts can be connected to.  
permission java.net.socketPermission "host:port", "connect";  
  
// Logger permission to take advantage of logging.  
permission java.util.logging.LoggingPermission;  
  
// Grant listen/connect/accept permissions to the driver if   
// connecting to a named instance as the client driver.   
// This connects to a udp service and listens for a response.  
permission java.net.SocketPermission "*", "listen, connect, accept";   
};   
```  
  
> [!NOTE]  
>  Il codice "file:/install_dir/lib/-" fa riferimento alla directory di installazione del driver JDBC.  
  
## <a name="protecting-server-communication"></a>Protezione delle comunicazioni con il server  
 Quando si usa il driver JDBC per comunicare con un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile proteggere il canale di comunicazione usando il protocollo IPSec (Internet Protocol Security) o SSL (Secure Sockets Layer) oppure entrambi.  
  
 Il supporto SSL può essere utilizzato per fornire un livello aggiuntivo di protezione oltre a IPsec. Per altre informazioni sull'uso di SSL, vedere [Uso della crittografia SSL](../../connect/jdbc/using-ssl-encryption.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Protezione delle applicazioni del driver JDBC](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
