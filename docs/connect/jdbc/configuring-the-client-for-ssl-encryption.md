---
title: Configurazione del client per la crittografia | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: vanto
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ae34cd1f-3569-4759-80c7-7c9b33b3e9eb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 123e847e01c07ab04bf5be97593af838abfdc4bd
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "71713281"
---
# <a name="configuring-the-client-for-encryption"></a>Configurazione del client per la crittografia
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] o il client deve convalidare che il server sia quello corretto e che il certificato venga rilasciato da un'autorità di certificazione ritenuta attendibile dal client. Per convalidare il certificato del server, è necessario che in fase di connessione venga fornito il materiale relativo all'attendibilità. L'autorità emittente del certificato del server deve inoltre essere un'Autorità di certificazione considerata attendibile dal client.  
  
 In questo argomento viene innanzitutto descritto come fornire il materiale relativo all'attendibilità nel computer client. Viene quindi descritto come importare un certificato del server nell'archivio di attendibilità del computer client quando l'istanza del certificato TLS (Transport Layer Security) di SQL Server viene emessa da un'Autorità di certificazione privata.  
  
 Per altre informazioni sulla convalida del certificato del server, vedere la sezione Convalida del certificato TLS del server in [Informazioni sul supporto della crittografia](../../connect/jdbc/understanding-ssl-support.md).  
  
## <a name="configuring-the-client-trust-store"></a>Configurazione dell'archivio di attendibilità del client 
 Per la convalida del certificato del server è necessario che il materiale relativo all'attendibilità venga fornito in fase di connessione usando le proprietà di connessione **trustStore** e **trustStorePassword** in modo esplicito o usando l'archivio di attendibilità predefinito di JVM (Java Virtual Machine) sottostante. Per altre informazioni su come impostare le proprietà **trustStore** e **trustStorePassword** in una stringa di connessione, vedere [Connessione tramite la crittografia](../../connect/jdbc/connecting-with-ssl-encryption.md).  
  
 Se la proprietà **trustStore** non è specificata o è impostata su Null, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usa il provider di sicurezza di JVM sottostante, ovvero Java Secure Socket Extension (SunJSSE). Il provider SunJSSE fornisce un oggetto TrustManager predefinito, usato per convalidare i certificati X.509 restituiti da SQL Server rispetto al materiale relativo all'attendibilità fornito in un archivio di attendibilità.  
  
 TrustManager prova a individuare il file trustStore predefinito nell'ordine di ricerca seguente:  
  
-   Se è definita la proprietà di sistema "javax.net.ssl.trustStore", TrustManager prova a individuare il file trustStore predefinito usando il nome file specificato dalla proprietà di sistema.  
  
-   Se la proprietà di sistema "javax.net.ssl.trustStore" non è stata specificata e il file "\<home-java>/lib/security/jssecacerts" è presente, viene usato questo file.  
  
-   Se il file "\<home-java>/lib/security/cacerts" è presente, viene usato questo file.  
  
 Per ulteriori informazioni, vedere la documentazione relativa all'interfaccia TrustManager SUNX509 nel sito Web Sun Microsystems.  
  
 Java Runtime Environment consente di impostare le proprietà di sistema trustStore e trustStorePassword come indicato di seguito:  
  
```  
java -Djavax.net.ssl.trustStore=C:\MyCertificates\storeName  
java -Djavax.net.ssl.trustStorePassword=storePassword  
```  
  
 In questo caso, in qualsiasi applicazione in esecuzione in questo ambiente JVM queste impostazioni vengono utilizzate come predefinite. Per sostituire le impostazioni predefinite nell'applicazione, è necessario impostare le proprietà di connessione **trustStore** e **trustStorePassword** nella stringa di connessione o nel metodo setter appropriato della classe [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md).  
  
 Inoltre, è possibile configurare e gestire i file dell'archivio di attendibilità predefinito, come "\<home-java>/lib/security/jssecacerts" e "\<home-java>/lib/security/cacerts". A tale scopo, utilizzare l'utilità "keytool" JAVA installata con JRE (Java Runtime Environment). Per ulteriori informazioni su tale utilità, vedere la relativa documentazione nel sito Web Sun Microsystems.  
  
### <a name="importing-the-server-certificate-to-trust-store"></a>Importazione del certificato del server nell'archivio di attendibilità  
 Durante l'handshake TLS, il server invia il proprio certificato chiave pubblica al client. L'autorità emittente di un certificato chiave pubblica è nota come Autorità di certificazione (CA). Il client deve verificare che l'Autorità di certificazione sia considerata attendibile dal client stesso. Questa operazione può essere eseguita se la chiave pubblica delle Autorità di certificazione attendibili è conosciuta in anticipo. In genere, con JVM viene fornito un set predefinito di Autorità di certificazione attendibili.  
  
 Se l'istanza del certificato TLS di SQL Server viene emessa da un'Autorità di certificazione privata, è necessario aggiungere il certificato dell'Autorità di certificazione all'elenco di certificati attendibili nell'archivio di attendibilità del computer client.  
  
 A tale scopo, utilizzare l'utilità "keytool" JAVA installata con JRE (Java Runtime Environment). Nel prompt dei comandi seguente viene illustrato come utilizzare l'utilità "keytool" per importare un certificato da un file:  
  
```  
keytool -import -v -trustcacerts -alias myServer -file caCert.cer -keystore truststore.ks  
```  
  
 Nell'esempio viene utilizzato un file denominato "caCert.cer" come file di certificato. È necessario ottenere questo file di certificato dal server. Nei passaggi seguenti viene illustrato come esportare il certificato del server in un file:  
  
1.  Fare clic sul pulsante Start, scegliere Esegui e digitare MMC. MMC è l'acronimo di Microsoft Management Console.  
  
2.  In MMC aprire Certificati.  
  
3.  Espandere Personale, quindi Certificati.  
  
4.  Fare clic con il pulsante destro del mouse sul certificato del server, quindi scegliere Tutte le attività\Esporta.  
  
5.  Scegliere Avanti per passare alla pagina successiva a quella introduttiva dell'Esportazione guidata certificati.  
  
6.  Verificare che l'opzione "Non esportare la chiave privata" sia selezionata, quindi scegliere Avanti.  
  
7.  Verificare che sia selezionata l'opzione X.509 binario codificato DER (.CER) o Codificato Base 64 X.509 (.CER), quindi scegliere Avanti.  
  
8.  Immettere un nome per il file di esportazione.  
  
9. Scegliere Avanti, quindi Fine per esportare il certificato.  
  
## <a name="see-also"></a>Vedere anche  
 [Uso della crittografia](../../connect/jdbc/using-ssl-encryption.md)   
 [Protezione delle applicazioni del driver JDBC](../../connect/jdbc/securing-jdbc-driver-applications.md)