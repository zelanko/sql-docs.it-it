---
title: Connessione a SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data source names
- connection string keywords
- DSNs
ms.assetid: f95cdbce-e7c2-4e56-a9f7-8fa3a920a125
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1f3e311b0f7d27b6a0ca2d12ae510960859ae80d
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66797508"
---
# <a name="connecting-to-sql-server"></a>Connessione a SQL Server
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Questo argomento descrive come creare una connessione a un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="connection-properties"></a>Proprietà delle connessioni  

Visualizzare [DSN e parole chiave delle stringhe di connessione e gli attributi](../../../connect/odbc/dsn-connection-string-attribute.md) per tutte le parole chiave delle stringhe di connessione e gli attributi supportati in Linux e Mac

> [!IMPORTANT]  
> Se si stabilisce una connessione a un database che usa il mirroring, ovvero dispone di un partner di failover, non specificare il nome del database nella stringa di connessione. Inviare invece un comando **use**_nome_database_ per connettersi al database prima di eseguire le query.  
  
Il valore passato per il **Driver** parola chiave può essere uno dei seguenti:  
  
-   Il nome usato al momento dell'installazione del driver.

-   Il percorso della libreria di driver specificato nel file ini del modello usato per l'installazione del driver.  

Per creare un DSN, creare (se necessario) e modificare il file **~/.odbc.ini** (`.odbc.ini` nella home directory) per un DSN utente accessibile solo all'utente corrente, o `/etc/odbc.ini` per un DSN di sistema (sono necessari privilegi amministrativi.) Di seguito è riportato un file di esempio che mostra le voci necessarie per un DSN:  

```  
[MSSQLTest]  
Driver = ODBC Driver 13 for SQL Server  
Server = [protocol:]server[,port]  
#   
# Note:  
# Port is not a valid keyword in the odbc.ini file  
# for the Microsoft ODBC driver on Linux or macOS
#  
```  

È anche possibile specificare il protocollo e la porta per la connessione al server. Ad esempio, **Server = tcp:** _servername_ **, 12345**. Si noti che è l'unico protocollo supportato dai driver di Linux e macOS `tcp`.

Per connettersi a un'istanza denominata tramite una porta statica, usare <b>Server=</b>*nomeserver*,**numero_porta**. La connessione a una porta dinamica non è supportata.  

In alternativa, è possibile aggiungere le informazioni del DSN in un file di modello ed eseguire il comando seguente per aggiungere tali informazioni a `~/.odbc.ini`:
 - **odbcinst -i -s -f** _template_file_  
 
È possibile verificare che il driver funzioni usando `isql` per testare la connessione, oppure è possibile usare questo comando:
 - **master.INFORMATION_SCHEMA.TABLES BCP out -S OUTFILE <server> - U <name> - P <password>**  

## <a name="using-secure-sockets-layer-ssl"></a>Uso di Secure Sockets Layer (SSL)  
Secure Sockets Layer (SSL) consente di crittografare le connessioni a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. SSL protegge i nomi utente e le password di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in rete. SSL verifica inoltre l'identità del server per la protezione dagli attacchi man-in-the-middle (MITM).  

L'abilitazione della crittografia aumenta la sicurezza a scapito delle prestazioni.

Per altre informazioni, vedere [crittografia delle connessioni a SQL Server](https://go.microsoft.com/fwlink/?LinkId=220900) e [Using Encryption Without Validation](https://docs.microsoft.com/sql/relational-databases/native-client/features/using-encryption-without-validation).

Indipendentemente dalle impostazioni di **Encrypt** e **TrustServerCertificate**, le credenziali di accesso al server (nome utente e password) vengono sempre crittografate. La tabella seguente mostra l'effetto delle impostazioni di **Encrypt** e **TrustServerCertificate** .  

||**TrustServerCertificate=no**|**TrustServerCertificate=yes**|  
|-|-------------------------------------|------------------------------------|  
|**Encrypt=no**|Il certificato del server non viene verificato.<br /><br />I dati inviati dal client al server e viceversa non vengono crittografati.|Il certificato del server non viene verificato.<br /><br />I dati inviati dal client al server e viceversa non vengono crittografati.|  
|**Encrypt=yes**|Il certificato del server viene verificato.<br /><br />I dati inviati dal client al server e viceversa vengono crittografati.<br /><br />Il nome (o indirizzo IP) in un nome comune del soggetto (CN) o nome alternativo del soggetto (SAN) di un certificato SSL di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve corrispondere esattamente al nome server (o indirizzo IP) specificato nella stringa di connessione.|Il certificato del server non viene verificato.<br /><br />I dati inviati dal client al server e viceversa vengono crittografati.|  

Per impostazione predefinita, le connessioni crittografate verificano sempre il certificato del server. Tuttavia, se ci si connette a un server che dispone di un certificato autofirmato, aggiungere anche il `TrustServerCertificate` opzione per ignorare il controllo del certificato nell'elenco delle autorità di certificazione attendibili:  

```  
Driver={ODBC Driver 13 for SQL Server};Server=ServerNameHere;Encrypt=YES;TrustServerCertificate=YES  
```  
  
SSL usa la libreria OpenSSL. La tabella seguente mostra le versioni minime supportate di OpenSSL e i percorsi dei file di archivio di scopi consentiti ai certificati predefiniti per ogni piattaforma:

|Piattaforma|Versione minima OpenSSL|Percorso del file di archivio di scopi consentiti ai certificati|  
|------------|---------------------------|--------------------------------------------|
|Debian 9|1.1.0|/etc/ssl/certs|
|Debian 8.71 |1.0.1|/etc/ssl/certs|
|macOS 10.13|1.0.2|/usr/local/etc/OpenSSL/certs|
|macOS 10.12|1.0.2|/usr/local/etc/OpenSSL/certs|
|OS X 10.11|1.0.2|/usr/local/etc/OpenSSL/certs|
|Red Hat Enterprise Linux 7|1.0.1|/etc/pki/tls/cert.pem|
|Red Hat Enterprise Linux 6|1.0.0-10|/etc/pki/tls/cert.pem|
|SuSE Linux Enterprise 12 |1.0.1|/etc/ssl/certs|
|SuSE Linux Enterprise 11 |0.9.8|/etc/ssl/certs|
|Ubuntu 17.10 |1.0.2|/etc/ssl/certs|
|Ubuntu 16.10 |1.0.2|/etc/ssl/certs|
|Ubuntu 16.04 |1.0.2|/etc/ssl/certs|
  
È anche possibile specificare la crittografia nella stringa di connessione utilizzando il `Encrypt` opzione quando si usa **SQLDriverConnect** per la connessione.

## <a name="see-also"></a>Vedere anche  
[Installazione di Microsoft ODBC Driver for SQL Server in Linux e macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)  
[Linee guida per la programmazione](../../../connect/odbc/linux-mac/programming-guidelines.md)
