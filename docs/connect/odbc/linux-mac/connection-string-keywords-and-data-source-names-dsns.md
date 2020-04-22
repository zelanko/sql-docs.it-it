---
title: Connessione con ODBC
description: Informazioni su come creare una connessione a un database da Linux o macOS usando Microsoft ODBC Driver for SQL Server.
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2b99479883fd1cc74008d62a9c322226ed587244
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/17/2020
ms.locfileid: "81632809"
---
# <a name="connecting-to-sql-server"></a>Connessione a SQL Server
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Questo argomento descrive come creare una connessione a un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="connection-properties"></a>Proprietà connessione  

Per tutte le parole chiave e gli attributi delle stringhe di connessione supportati in Linux e macOS, vedere [Parole chiave e attributi per stringhe di connessione e DSN](../dsn-connection-string-attribute.md).

> [!IMPORTANT]  
> Se si stabilisce una connessione a un database che usa il mirroring, ovvero dispone di un partner di failover, non specificare il nome del database nella stringa di connessione. Inviare invece un comando **use** _database_name_ per connettersi al database prima di eseguire le query.  
  
Il valore passato alla parola chiave **Driver** può essere uno dei seguenti:  
  
-   Il nome usato al momento dell'installazione del driver.

-   Il percorso della libreria di driver specificato nel file ini del modello usato per l'installazione del driver.  

Per creare un DSN, creare, se necessario, e modificare il file **~/.ODBC. ini** (`.odbc.ini` nella home directory) per un DSN utente accessibile solo all'utente corrente o `/etc/odbc.ini` per un DSN di sistema (richiede privilegi amministrativi). Di seguito è riportato un file di esempio con le voci minime richieste per un DSN:  

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

È anche possibile specificare il protocollo e la porta per la connessione al server. Ad esempio, **Server=tcp:** _nomeserver_ **, 12345**. Si noti che l'unico protocollo supportato dai driver Linux e macOS è `tcp`.

Per connettersi a un'istanza denominata tramite una porta statica, usare <b>Server=</b>*nomeserver*,**numero_porta**. La connessione a una porta dinamica non è supportata prima della versione 17.4.

In alternativa, è possibile aggiungere le informazioni del DSN in un file di modello ed eseguire il comando seguente per aggiungere tali informazioni a `~/.odbc.ini`:
 - **odbcinst -i -s -f** _template_file_  
 
È possibile verificare che il driver funzioni usando `isql` per testare la connessione oppure usare questo comando:
 - **bcp master.INFORMATION_SCHEMA.TABLES out OutFile.dat -S <server> -U <name> -P <password>**  

## <a name="using-tlsssl"></a>Uso di TLS/SSL  
È possibile usare Transport Layer Security (TLS), noto in precedenza come Secure Sockets Layer (SSL), per crittografare le connessioni a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. TLS protegge i nomi utente e le password di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in rete. TLS verifica anche l'identità del server per la protezione dagli attacchi man-in-the-middle (MITM).  

L'abilitazione della crittografia aumenta la sicurezza a scapito delle prestazioni.

Per altre informazioni, vedere [Crittografia delle connessioni a SQL Server](https://go.microsoft.com/fwlink/?LinkId=220900) e [Utilizzo della crittografia senza convalida](https://docs.microsoft.com/sql/relational-databases/native-client/features/using-encryption-without-validation).

Indipendentemente dalle impostazioni di **Encrypt** e **TrustServerCertificate**, le credenziali di accesso al server (nome utente e password) vengono sempre crittografate. La tabella seguente mostra l'effetto delle impostazioni di **Encrypt** e **TrustServerCertificate** .  

||**TrustServerCertificate=no**|**TrustServerCertificate=yes**|  
|-|-------------------------------------|------------------------------------|  
|**Encrypt=no**|Il certificato del server non viene verificato.<br /><br />I dati inviati dal client al server e viceversa non vengono crittografati.|Il certificato del server non viene verificato.<br /><br />I dati inviati dal client al server e viceversa non vengono crittografati.|  
|**Encrypt=yes**|Il certificato del server viene verificato.<br /><br />I dati inviati dal client al server e viceversa vengono crittografati.<br /><br />Il nome (o l'indirizzo IP) in un nome comune del soggetto (CN, Common Name) o in un nome alternativo del soggetto (SAN, Subject Alternative Name) di un certificato TLS/SSL di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve corrispondere esattamente al nome del server (o all'indirizzo IP) specificato nella stringa di connessione.|Il certificato del server non viene verificato.<br /><br />I dati inviati dal client al server e viceversa vengono crittografati.|  

Per impostazione predefinita, le connessioni crittografate verificano sempre il certificato del server. Tuttavia, se ci si connette a un server che ha un certificato autofirmato, aggiungere anche l'opzione `TrustServerCertificate` per ignorare il controllo del certificato rispetto all'elenco di autorità di certificazione attendibili:  

```  
Driver={ODBC Driver 13 for SQL Server};Server=ServerNameHere;Encrypt=YES;TrustServerCertificate=YES  
```  
  
TLS usa la libreria OpenSSL. La tabella seguente mostra le versioni minime supportate di OpenSSL e i percorsi dei file di archivio di scopi consentiti ai certificati predefiniti per ogni piattaforma:

|Piattaforma|Versione minima OpenSSL|Percorso del file di archivio di scopi consentiti ai certificati|  
|------------|---------------------------|--------------------------------------------|
|Debian 10|1.1.1|/etc/ssl/certs|
|Debian 9|1.1.0|/etc/ssl/certs|
|Debian 8.71|1.0.1|/etc/ssl/certs|
|OS X 10.11, macOS 10.12, 10.13, 10.14|1.0.2|/usr/local/etc/openssl/certs|
|Red Hat Enterprise Linux 8|1.1.1|/etc/pki/tls/cert.pem|
|Red Hat Enterprise Linux 7|1.0.1|/etc/pki/tls/cert.pem|
|Red Hat Enterprise Linux 6|1.0.0-10|/etc/pki/tls/cert.pem|
|SUSE Linux Enterprise 15|1.1.0|/etc/ssl/certs|
|SUSE Linux Enterprise 11, 12|1.0.1|/etc/ssl/certs|
|Ubuntu 18.10, 19.04|1.1.1|/etc/ssl/certs|
|Ubuntu 18.04|1.1.0|/etc/ssl/certs|
|Ubuntu 16.04, 16.10, 17.10|1.0.2|/etc/ssl/certs|
|Ubuntu 14.04|1.0.1|/etc/ssl/certs|

È anche possibile specificare la crittografia nella stringa di connessione usando l'opzione `Encrypt` quando si usa **SQLDriverConnect** per connettersi.

## <a name="adjusting-the-tcp-keep-alive-settings"></a>Regolazione delle impostazioni keep-alive TCP

A partire dalla versione 17.4 del driver ODBC, la frequenza con cui il driver invia pacchetti keep-alive e li ritrasmette quando non viene ricevuta una risposta è configurabile.
Per configurare, aggiungere le impostazioni seguenti alla sezione del driver in `odbcinst.ini` o alla sezione del DSN in `odbc.ini`. Quando ci si connette a un DSN, il driver usa le impostazioni presenti nella sezione del DSN, in caso contrario, o se ci si connette solo con una stringa di connessione, userà le impostazioni presenti nella sezione del driver in `odbcinst.ini`. Se l'impostazione non è presente in nessuna delle due posizioni, il driver usa il valore predefinito.

- `KeepAlive=<integer>` determina la frequenza dei tentativi effettuati da TCP per verificare l'integrità di una connessione inattiva inviando un pacchetto keep-alive. Il valore predefinito è **30** secondi.

- `KeepAliveInterval=<integer>` determina l'intervallo tra le ritrasmissioni keep-alive finché non viene ricevuta una risposta.  Il valore predefinito è **1** secondo.

## <a name="see-also"></a>Vedere anche

- [Installazione di Microsoft ODBC Driver for SQL Server in Linux](installing-the-microsoft-odbc-driver-for-sql-server.md)
- [Installazione di Microsoft ODBC Driver for SQL Server in macOS](install-microsoft-odbc-driver-sql-server-macos.md)
- [Linee guida per la programmazione](programming-guidelines.md)
