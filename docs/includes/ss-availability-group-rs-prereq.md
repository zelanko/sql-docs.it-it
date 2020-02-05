## <a name="prerequisites"></a>Prerequisites

Prima di creare il gruppo di disponibilità, è necessario:

- Impostare l'ambiente in modo che tutti i server che ospitano le repliche di disponibilità possano comunicare.
- Installare SQL Server. Per informazioni dettagliate, vedere [Installare SQL Server](../database-engine/install-windows/install-sql-server.md).

## <a name="enable-always-on-availability-groups-and-restart-mssql-server"></a>Abilitare la funzionalità Gruppi di disponibilità Always On e riavviare mssql-server

>[!NOTE]
>Il comando seguente usa cmdlet del modulo sqlserver pubblicato in PowerShell Gallery. È possibile installare questo modulo usando il comando Install-Module.

Abilitare Gruppi di disponibilità Always On per ogni replica che ospita un'istanza di SQL Server. Quindi riavviare il servizio SQL Server. Eseguire il comando seguente per abilitare e quindi riavviare i servizi SQL Server:

```powershell
Enable-SqlAlwaysOn -ServerInstance <server\instance> -Force
```

## <a name="enable-an-alwayson_health-event-session"></a>Abilitare una sessione eventi AlwaysOn_health

 Per diagnosticare più facilmente la causa radice durante la risoluzione dei problemi che interessano un gruppo di disponibilità, è possibile abilitare facoltativamente una sessione di eventi estesi dei gruppi di disponibilità Always On (XEvents). A tale scopo, eseguire il comando seguente in ogni istanza di SQL Server:

```sql
ALTER EVENT SESSION  AlwaysOn_health ON SERVER WITH (STARTUP_STATE=ON);
GO
```

Per altre informazioni su questa sessione XEvents, vedere [Eventi estesi dei gruppi di disponibilità Always On](../database-engine/availability-groups/windows/always-on-extended-events.md).

## <a name="database-mirroring-endpoint-authentication"></a>Autenticazione endpoint del mirroring del database

Per il funzionamento corretto della sincronizzazione, le repliche incluse nel gruppo di disponibilità per scalabilità in lettura devono eseguire l'autenticazione attraverso l'endpoint. I due scenari principali che è possibile usare per l'autenticazione di questo tipo sono illustrati nelle sezioni successive.

### <a name="service-account"></a>Account servizio

In un ambiente Active Directory in cui tutte le repliche secondarie sono aggiunte allo stesso dominio, SQL Server può eseguire l'autenticazione usando l'account del servizio. È necessario creare in modo esplicito un account di accesso per l'account di servizio in ogni istanza di SQL Server:

```sql
CREATE LOGIN [<domain>\service account] FROM WINDOWS;
```

### <a name="sql-login-authentication"></a>Autenticazione dell'account di accesso SQL

Negli ambienti in cui le repliche secondarie non possono essere aggiunte a un dominio di Active Directory, è necessario usare l'autenticazione SQL. Lo script Transact-SQL seguente crea un account di accesso con nome `dbm_login` e un utente con nome `dbm_user`. Aggiornare lo script con una password complessa. Per creare l'utente dell'endpoint di mirroring del database, eseguire il comando seguente in tutte le istanze di SQL Server:

```sql
CREATE LOGIN dbm_login WITH PASSWORD = '**<1Sample_Strong_Password!@#>**';
CREATE USER dbm_user FOR LOGIN dbm_login;
```

#### <a name="certificate-authentication"></a>Autenticazione del certificato

Se si usa una replica secondaria che richiede l'autenticazione con l'autenticazione SQL, usare un certificato per l'autenticazione tra gli endpoint di mirroring.

Lo script Transact-SQL seguente crea una chiave master e un certificato. Quindi esegue il backup del certificato e protegge il file con una chiave privata. Aggiornare lo script con password complesse. Eseguire lo script nell'istanza di SQL Server primaria per creare il certificato:

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate WITH SUBJECT = 'dbm';
BACKUP CERTIFICATE dbm_certificate
   TO FILE = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.cer'
   WITH PRIVATE KEY (
           FILE = 'c:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.pvk',
           ENCRYPTION BY PASSWORD = '**<Private_Key_Password>**'
       );
```

A questo punto la replica di SQL Server primaria dispone di un certificato in `c:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.cer` e di una chiave privata in `c:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.pvk`. Copiare questi due file nello stesso percorso in tutti i server che ospiteranno le repliche di disponibilità.

In ogni replica secondaria verificare che l'account del servizio per l'istanza di SQL Server abbia le autorizzazioni per l'accesso al certificato.

#### <a name="create-the-certificate-on-secondary-servers"></a>Creare il certificato nei server secondari

Lo script Transact-SQL seguente crea una chiave master e un certificato dal backup creato nella replica primaria di SQL Server. Inoltre, il comando autorizza gli utenti ad accedere al certificato. Aggiornare lo script con password complesse. La password di decrittografia è la stessa password usata per creare il file *.pvk* in un passaggio precedente. Per creare il certificato eseguire lo script seguente in tutte le repliche secondarie:

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate
    AUTHORIZATION dbm_user
    FROM FILE = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.cer'
    WITH PRIVATE KEY (
    FILE = 'c:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.pvk',
    DECRYPTION BY PASSWORD = '**<Private_Key_Password>**'
            );
```

## <a name="create-database-mirroring-endpoints-on-all-replicas"></a>Creare endpoint di mirroring del database in tutte le repliche

Gli endpoint del mirroring del database usano il protocollo TCP (Transmission Control Protocol) per inviare e ricevere messaggi tra istanze del server che partecipano a sessioni di mirroring del database o ospitano repliche di disponibilità. L'endpoint del mirroring del database è in attesa su un numero di porta TCP univoco.

Lo script Transact-SQL seguente crea un endpoint di ascolto denominato `Hadr_endpoint` per il gruppo di disponibilità. Avvia l'endpoint e concede l'autorizzazione di connessione all'account del servizio o all'account di accesso SQL creato in un passaggio precedente. Prima di eseguire lo script, sostituire i valori compresi tra `**< ... >**`. Facoltativamente è possibile includere un indirizzo IP `LISTENER_IP = (0.0.0.0)`. L'indirizzo IP del listener deve essere un indirizzo IPv4. È anche possibile usare `0.0.0.0`.

Aggiornare lo script Transact-SQL seguente per il proprio ambiente in tutte le istanze di SQL Server:

```SQL
CREATE ENDPOINT [Hadr_endpoint]
    AS TCP (LISTENER_PORT = **<5022>**)
    FOR DATA_MIRRORING (
        ROLE = ALL,
        AUTHENTICATION = CERTIFICATE dbm_certificate,
        ENCRYPTION = REQUIRED ALGORITHM AES
        );
ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
GRANT CONNECT ON ENDPOINT::[Hadr_endpoint] TO [<service account or user>];
```

La porta TCP sul firewall deve essere aperta per la porta del listener.

Per altre informazioni, vedere [Endpoint del mirroring del database (SQL Server)](https://docs.microsoft.com/sql/database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server?view=sql-server-2017).
