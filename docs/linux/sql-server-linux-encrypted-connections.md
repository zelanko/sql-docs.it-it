---
title: Crittografia delle connessioni a SQL Server in Linux
description: Questo articolo descrive la crittografia delle connessioni a SQL Server in Linux.
ms.date: 01/30/2018
author: vin-yu
ms.author: vinsonyu
ms.reviewer: vanto
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
helpviewer_keywords:
- Linux, encrypted connections
ms.openlocfilehash: 3f658ba8723b142f37763ea8b4f0c8f7b0c5d0e1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077294"
---
# <a name="encrypting-connections-to-sql-server-on-linux"></a>Crittografia delle connessioni a SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in Linux possono usare Transport Layer Security (TLS) per crittografare i dati trasmessi attraverso una rete tra un'applicazione client e un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] supporta gli stessi protocolli TLS in Windows e Linux: TLS 1.2, 1.1 e 1.0. Tuttavia, è specifica per il sistema operativo in cui la procedura per configurare TLS [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] è in esecuzione.  

## <a name="requirements-for-certificates"></a>Requisiti per i certificati 
Prima di iniziare, è necessario assicurarsi che i certificati di rispettano i requisiti seguenti:
- Dopo la valido dalla proprietà del certificato e prima la valido alla proprietà del certificato deve essere l'ora di sistema corrente.
- Il certificato deve essere destinato all'autenticazione del server. Ciò richiede che la proprietà Enhanced Key Usage del certificato per specificare l'autenticazione Server (1.3.6.1.5.5.7.3.1).
- Il certificato deve essere creato usando l'opzione KeySpec di AT_KEYEXCHANGE. Proprietà di utilizzo della chiave del certificato (KEY_USAGE) include in genere, anche la crittografia chiave (CERT_KEY_ENCIPHERMENT_KEY_USAGE).
- La proprietà Subject del certificato deve indicare che il nome comune (CN) sia lo stesso come il nome host o nome di dominio completo (FQDN) del computer del server. Nota: I certificati con caratteri jolly sono supportati.

## <a name="configuring-the-openssl-libraries-for-use-optional"></a>Configurare le librerie OpenSSL per l'utilizzo (facoltativo)
È possibile creare collegamenti simbolici nel `/opt/mssql/lib/` directory che fanno riferimento a cui `libcrypto.so` e `libssl.so` librerie devono essere utilizzate per la crittografia. Ciò è utile se si vuole forzare il Server SQL da utilizzare una specifica versione di OpenSSL diverso da quello predefinito fornito dal sistema. Se questi collegamenti simbolici non sono presenti, SQL Server caricherà le librerie OpenSSL predefinito configurato nel sistema.

Devono essere denominati questi collegamenti simbolici `libcrypto.so` e `libssl.so` e inserito nel `/opt/mssql/lib/` directory.

## <a name="overview"></a>Panoramica
TLS è usato per crittografare le connessioni da un'applicazione client per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Quando è configurato correttamente, TLS fornisce privacy e integrità dei dati per le comunicazioni tra client e server.  Le connessioni TLS possono essere inizializzata sul lato client o server avviate. 

## <a name="client-initiated-encryption"></a>Client ha avviato la crittografia 
- **Genera certificato** (/CN deve corrispondere il nome di dominio completo di host di SQL Server)

> [!NOTE]
> Per questo esempio viene usato un certificato autofirmato, questo non usare per gli scenari di produzione. È consigliabile usare i certificati della CA. 

        openssl req -x509 -nodes -newkey rsa:2048 -subj '/CN=mssql.contoso.com' -keyout mssql.key -out mssql.pem -days 365 
        sudo chown mssql:mssql mssql.pem mssql.key 
        sudo chmod 600 mssql.pem mssql.key   
        sudo mv mssql.pem /etc/ssl/certs/ 
        sudo mv mssql.key /etc/ssl/private/ 

- **Configurare SQL Server**

        systemctl stop mssql-server 
        cat /var/opt/mssql/mssql.conf 
        sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssql.pem 
        sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssql.key 
        sudo /opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2 
        sudo /opt/mssql/bin/mssql-conf set network.forceencryption 0 

- **Registrare il certificato nel computer client (Windows, Linux o macOS)**

    -   Se si usa certificato CA firmato, è necessario copiare il certificato di autorità di certificazione (CA) anziché il certificato utente al computer client. 
    -   Se si usa il certificato autofirmato, è sufficiente copiare il file con estensione PEM nelle cartelle seguenti corrispondente alla distribuzione ed eseguire i comandi per consentire loro 
        - **Ubuntu**: Certificato di copia al ```/usr/share/ca-certificates/``` rename estensione CRT usare i certificati della ca dpkg reconfigure per abilitarlo come certificato di sistema CA. 
        - **RHEL**: Certificato di copia al ```/etc/pki/ca-trust/source/anchors/``` usare ```update-ca-trust``` per abilitarlo come certificato di sistema CA.
        - **SUSE**: Certificato di copia al ```/usr/share/pki/trust/anchors/``` usare ```update-ca-certificates``` per abilitarlo come certificato di sistema CA.
        - **Windows**:  Importa il file con estensione PEM in un certificato in utente corrente -> attendibile l'autorità di certificazione radice -> certificati
        - **macOS**: 
           - Copiare il certificato al ```/usr/local/etc/openssl/certs```
           - Eseguire il comando seguente per ottenere il valore hash: ```/usr/local/Cellar/openssql/1.0.2l/openssql x509 -hash -in mssql.pem -noout```
           - Rinominare il certificato come valore. Ad esempio: ```mv mssql.pem dc2dd900.0```. Verificare che sia dc2dd900.0 in ```/usr/local/etc/openssl/certs```
    
-   **Esempi di stringhe di connessione** 

    - **[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)]**   
  ![Finestra di dialogo connessione SQL Server Management Studio](media/sql-server-linux-encrypted-connections/ssms-encrypt-connection.png "finestra di dialogo connessione SQL Server Management Studio")  
  
    - **SQLCMD** 

            sqlcmd  -S <sqlhostname> -N -U sa -P '<YourPassword>' 
    - **ADO.NET** 

            "Encrypt=True; TrustServerCertificate=False;" 
    - **ODBC** 

            "Encrypt=Yes; TrustServerCertificate=no;" 
    - **JDBC** 
    
            "encrypt=true; trustServerCertificate=false;" 

## <a name="server-initiated-encryption"></a>Server ha avviato la crittografia 

- **Genera certificato** (/CN deve corrispondere il nome di dominio completo di host di SQL Server)
        
        openssl req -x509 -nodes -newkey rsa:2048 -subj '/CN=mssql.contoso.com' -keyout mssql.key -out mssql.pem -days 365 
        sudo chown mssql:mssql mssql.pem mssql.key 
        sudo chmod 600 mssql.pem mssql.key   
        sudo mv mssql.pem /etc/ssl/certs/ 
        sudo mv mssql.key /etc/ssl/private/ 

- **Configurare SQL Server**

        systemctl stop mssql-server 
        cat /var/opt/mssql/mssql.conf 
        sudo /opt/mssql/bin/mssql-conf set network.tlscert /etc/ssl/certs/mssql.pem 
        sudo /opt/mssql/bin/mssql-conf set network.tlskey /etc/ssl/private/mssql.key 
        sudo /opt/mssql/bin/mssql-conf set network.tlsprotocols 1.2 
        sudo /opt/mssql/bin/mssql-conf set network.forceencryption 1 
        
-   **Esempi di stringhe di connessione** 

    - **SQLCMD**

            sqlcmd  -S <sqlhostname> -U sa -P '<YourPassword>' 
    - **ADO.NET** 

            "Encrypt=False; TrustServerCertificate=False;" 
    - **ODBC** 

            "Encrypt=no; TrustServerCertificate=no;"  
    - **JDBC** 
    
            "encrypt=false; trustServerCertificate=false;" 
            
> [!NOTE]
> Impostare **TrustServerCertificate** su True se il client non è possibile connettersi all'autorità di certificazione per convalidare l'autenticità del certificato

## <a name="common-connection-errors"></a>Errori comuni durante la connessione  

|Messaggio di errore |Fix |
|--- |--- |
|La catena di certificati è stato emesso da un'autorità non attendibile.  |Questo errore si verifica quando i client sono in grado di verificare la firma sul certificato presentato da SQL Server durante l'handshake TLS. Assicurarsi che il client considera attendibile uno il [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] certificato direttamente oppure l'autorità di certificazione che ha firmato il certificato di SQL Server. |
|Il nome dell'entità di destinazione non è corretto.  |Assicurarsi che il campo nome comune nel certificato del Server SQL corrisponde al nome di server specificato nella stringa di connessione del client. |  
|Connessione in corso interrotta forzatamente dall'host remoto. |Questo errore può verificarsi quando il client non supporta la versione del protocollo TLS richiesta da SQL Server. Ad esempio, se [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] è configurato per richiedere di TLS 1.2, assicurarsi che i client supportano anche il protocollo TLS 1.2. |
| | |   
