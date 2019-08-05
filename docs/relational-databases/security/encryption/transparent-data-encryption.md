---
title: Transparent Data Encryption (TDE) | Microsoft Docs
ms.custom: ''
ms.date: 05/09/2019
ms.prod: sql
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Transparent Data Encryption
- database encryption key, about
- TDE
- database encryption key
- TDE, about
- Transparent Data Encryption, about
- encryption [SQL Server], transparent data encryption
ms.assetid: c75d0d4b-4008-4e71-9a9d-cee2a566bd3b
author: aliceku
ms.author: aliceku
ms.reviewer: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ef9e0378d3a7ca0b5749788471b4ef97832d179d
ms.sourcegitcommit: c70a0e2c053c2583311fcfede6ab5f25df364de0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/31/2019
ms.locfileid: "68670592"
---
# <a name="transparent-data-encryption-tde"></a>Transparent Data Encryption (TDE)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  *Transparent Data Encryption* (TDE) consente di crittografare file di dati di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)]e [!INCLUDE[ssSDWfull](../../../includes/sssdwfull-md.md)] con un'operazione nota come crittografia dei dati inattivi. Per proteggere il database è possibile adottare alcune accortezze, tra cui la progettazione di un sistema sicuro, la crittografia dei dati riservati e la compilazione di un firewall attorno ai server di database. Tuttavia, nel caso in cui i supporti fisici (ad esempio unità o nastri di backup) venissero rubati, un malintenzionato potrebbe ripristinare o collegare il database e accedere ai dati. Una soluzione per ovviare al problema consiste nel crittografare i dati sensibili nel database e proteggere con un certificato le chiavi usate per la crittografia. In questo modo si impedisce a chi è sprovvisto delle chiavi di usare i dati; tuttavia, questo tipo di protezione deve essere pianificato in anticipo.  
  
 TDE consente di eseguire la crittografia e la decrittografia I/O in tempo reale dei file di dati e di log. Per la crittografia viene usata una chiave di crittografia del database (DEK), archiviata nel record di avvio del database affinché sia disponibile durante le operazioni di recupero. La chiave di crittografia del database è una chiave simmetrica protetta tramite un certificato archiviato nel database master del server o una chiave asimmetrica protetta da un modulo EKM. TDE consente di proteggere i dati "non operativi", ovvero i file di dati e di log, e assicura la conformità a numerose leggi, normative e linee guida stabilite in vari settori. Gli sviluppatori software possono ora crittografare i dati usando gli algoritmi di crittografia AES e 3DES senza modificare applicazioni esistenti.  
  
> [!IMPORTANT]
>  TDE non fornisce funzionalità di crittografia tramite canali di comunicazione. Per altre informazioni su come crittografare i dati su diversi canali di comunicazione, vedere [Abilitare connessioni crittografate al Motore di database &#40;Gestione configurazione SQL Server&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
> 
>  **Argomenti correlati:**  
> 
>  -   [Transparent Data Encryption con il database SQL di Azure](../../../relational-databases/security/encryption/transparent-data-encryption-azure-sql.md)  
> -   [Introduzione a Transparent Data Encryption (TDE) in SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-encryption-tde-tsql/)  
> -   [Spostare un database protetto da TDE in un'altra istanza di SQL Server](../../../relational-databases/security/encryption/move-a-tde-protected-database-to-another-sql-server.md)  
> -   [Abilitare TDE in SQL Server con EKM](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)   
> -   [Usare Connettore SQL Server con le funzionalità di crittografia SQL](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)
> - [Blog sulla sicurezza di SQL Server in TDE con domande frequenti](https://blogs.msdn.microsoft.com/sqlsecurity/2016/10/05/feature-spotlight-transparent-data-encryption-tde/)
 
  
## <a name="about-tde"></a>Informazioni su TDE  
 La crittografia del file di database viene eseguita a livello di pagina. Le pagine di un database crittografato sono crittografate prima di essere scritte sul disco e decrittografate quando vengono lette in memoria. L'uso di TDE non comporta un aumento delle dimensioni del database crittografato.  
  
 **Informazioni applicabili a [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]**  
  
 Quando si usa TDE con [!INCLUDE[sqldbesa](../../../includes/sqldbesa-md.md)] V12 il certificato a livello di server archiviato nel database master viene creato automaticamente da [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]. Per spostare un database TDE nel [!INCLUDE[ssSDS](../../../includes/sssds-md.md)], non è necessario decrittografare il database per l'operazione di spostamento. Per altre informazioni sull'utilizzo di TDE con [!INCLUDE[ssSDS](../../../includes/sssds-md.md)], vedere [Transparent Data Encryption per il database SQL e Data Warehouse](../../../relational-databases/security/encryption/transparent-data-encryption-azure-sql.md).  
  
 **Informazioni applicabili a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**  
  
 Una volta protetto, il database può essere ripristinato usando il certificato corretto. Per altre informazioni sui certificati, vedere [SQL Server Certificates and Asymmetric Keys](../../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  
  
 Quando si abilita TDE, è consigliabile eseguire immediatamente il backup del certificato e della chiave privata associata al certificato. Se il certificato non è più disponibile o se è necessario ripristinare o collegare il database a un altro server, è necessario disporre di copie di backup del certificato e della chiave privata, altrimenti non sarà possibile aprire il database. Il certificato di crittografia deve essere mantenuto anche se la funzionalità TDE non è più abilitata nel database. Anche se il database non è crittografato, è possibile che parti del log delle transazioni restino comunque protette e che il certificato sia necessario per alcune operazioni per l'esecuzione del backup completo del database. Un certificato che ha superato la data di scadenza può ancora essere usato per crittografare e decrittografare dati con TDE.  
  
 **Gerarchia di crittografia**  
  
 La figura seguente illustra l'architettura della crittografia TDE: Solo gli elementi a livello di database, la chiave di crittografia del database e le parti ALTER DATABASE sono configurabili dall'utente quando si usa TDE nel [!INCLUDE[ssSDS](../../../includes/sssds-md.md)].  
  
 ![Visualizza la gerarchia descritta nell'argomento.](../../../relational-databases/security/encryption/media/tde-architecture.png "Visualizza la gerarchia descritta nell'argomento.")  
  
## <a name="using-transparent-data-encryption"></a>Uso della crittografia trasparente dei dati  
 Per usare TDE, eseguire le operazioni seguenti:  
  
**Si applica a**: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Creare una chiave master  
  
-   Creare o ottenere un certificato protetto dalla chiave master  
  
-   Creare una chiave di crittografia del database e proteggerla mediante il certificato  
  
-   Impostare il database per l'uso della crittografia  
  
 L'esempio seguente illustra come crittografare e decrittografare il database `AdventureWorks2012` usando un certificato installato nel server denominato `MyServerCert`.  
  
```sql  
USE master;  
GO  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<UseStrongPasswordHere>';  
go  
CREATE CERTIFICATE MyServerCert WITH SUBJECT = 'My DEK Certificate';  
go  
USE AdventureWorks2012;  
GO  
CREATE DATABASE ENCRYPTION KEY  
WITH ALGORITHM = AES_128  
ENCRYPTION BY SERVER CERTIFICATE MyServerCert;  
GO  
ALTER DATABASE AdventureWorks2012  
SET ENCRYPTION ON;  
GO  
```  
  
 Le operazioni di crittografia e decrittografia sono pianificate sui thread di background da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Per visualizzare lo stato di queste operazioni, è possibile usare le viste del catalogo e le viste a gestione dinamica nell'elenco illustrato di seguito in questo argomento.  
  
> [!CAUTION]  
>  I file di backup dei database in cui è abilitata la funzionalità TDE vengono crittografati anche tramite la chiave di crittografia del database. Di conseguenza, quando questi backup vengono ripristinati, è necessario disporre del certificato che protegge la chiave di crittografia del database. Pertanto, oltre ad eseguire il backup del database, è necessario assicurarsi di conservare un backup dei certificati server per impedire la perdita di dati. Se il certificato non è più disponibile, si verificherà la perdita di dati. Per altre informazioni, vedere [SQL Server Certificates and Asymmetric Keys](../../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  
  
## <a name="commands-and-functions"></a>Comandi e funzioni  
 Affinché vengano accettati dalle istruzioni indicate di seguito, è necessario che i certificati TDE siano crittografati mediante la chiave master del database. Se sono crittografati solo tramite password, verranno rifiutati dalle istruzioni come componenti di crittografia.  
  
> [!IMPORTANT]  
>  Se si modificano i certificati per abilitarne la protezione tramite password quando vengono usati da TDE, il database diventerà inaccessibile dopo un riavvio.  
  
 Nella tabella seguente sono inclusi collegamenti e spiegazioni delle funzioni e dei comandi correlati a TDE.  
  
|Comando o funzione|Scopo|  
|-------------------------|-------------|  
|[CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-encryption-key-transact-sql.md)|Consente di creare una chiave usata per crittografare un database.|  
|[ALTER DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-encryption-key-transact-sql.md)|Consente di modificare la chiave usata per crittografare un database.|  
|[DROP DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-database-encryption-key-transact-sql.md)|Consente di rimuovere la chiave usata per crittografare un database.|  
|[Opzioni ALTER DATABASE SET &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-transact-sql-set-options.md)|Descrive l'opzione **ALTER DATABASE** , usata per abilitare TDE.|  
  
## <a name="catalog-views-and-dynamic-management-views"></a>Viste del catalogo e viste a gestione dinamica  
 Nella tabella seguente vengono illustrate le viste del catalogo e le viste a gestione dinamica di TDE.  
  
|Vista del catalogo e vista a gestione dinamica|Scopo|  
|---------------------------------------------|-------------|  
|[sys.databases &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)|Vista del catalogo che consente di visualizzare le informazioni del database.|  
|[sys.certificates &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)|Vista del catalogo che consente di visualizzare i certificati di un database.|  
|[sys.dm_database_encryption_keys &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md)|Tramite la vista a gestione dinamica vengono fornite informazioni relative alle chiavi di crittografia usate in un database e allo stato di crittografia di un database.|  
  
## <a name="permissions"></a>Autorizzazioni  
 Ogni funzionalità e comando di TDE ha requisiti specifici relativi alle autorizzazioni, descritti nelle tabelle precedenti.  
  
 La visualizzazione dei metadati interessati da TDE richiede l'autorizzazione VIEW DEFINITION per il certificato.  
  
## <a name="considerations"></a>Considerazioni  
 Durante un'analisi di una nuova crittografia di un database, le operazioni di manutenzione per il database sono disabilitate. È possibile usare l'impostazione modalità utente singolo per il database per eseguire operazioni di manutenzione. Per altre informazioni, vedere [Impostare un database in modalità utente singolo](../../../relational-databases/databases/set-a-database-to-single-user-mode.md).  
  
 È possibile determinare lo stato della crittografia del database utilizzando la vista a gestione dinamica sys.dm_database_encryption_keys. Per altre informazioni, vedere la sezione "Viste del catalogo e viste a gestione dinamica" più indietro in questo argomento.  
  
 In TDE vengono crittografati tutti i file e i filegroup del database. Se un database include filegroup contrassegnati come READ ONLY, l'operazione di crittografia del database avrà esito negativo.  
  
 Se un database viene usato per il mirroring del database o il log shipping, entrambi i database saranno crittografati. Le transazioni del log verranno crittografate quando vengono inviate tra i database.  
  
> [!IMPORTANT]  
>  Gli indici full-text vengono crittografati quando un database viene impostato per la crittografia. Gli indici full-text creati prima di SQL Server 2008 verranno importati nel database durante l'aggiornamento a SQL Server 2008 o versione successiva e verranno crittografati con TDE.  

> [!TIP]  
> Per monitorare le modifiche nello stato TDE di un database, usare SQL Server Audit o il servizio di controllo del database SQL. Per SQL Server, lo stato TDE è registrato nel gruppo di azioni di controllo DATABASE_CHANGE_GROUP, disponibile in [Azioni e gruppi di azioni di SQL Server Audit](../../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md).
  
### <a name="restrictions"></a>Restrictions  
 Durante le operazioni di crittografia del database iniziale, modifica della chiave o decrittografia del database, non sono consentite le azioni seguenti:  
  
-   Eliminazione di un file da un filegroup del database  
  
-   Eliminazione del database  
  
-   Attivazione della modalità offline per il database  
  
-   Scollegamento di un database  
  
-   Transizione di un database o filegroup in un stato READ ONLY  
  
 Le operazioni indicate di seguito non sono consentite durante l'esecuzione delle istruzioni CREATE DATABASE ENCRYPTION KEY, ALTER DATABASE ENCRYPTION KEY, DROP DATABASE ENCRYPTION KEY e ALTER DATABASE...SET ENCRYPTION.  
  
-   Eliminazione di un file da un filegroup del database.  
  
-   Eliminazione del database.  
  
-   Attivazione della modalità offline per il database.  
  
-   Scollegamento di un database.  
  
-   Transizione di un database o filegroup in un stato READ ONLY.  
  
-   Uso di un comando ALTER DATABASE.  
  
-   Avvio del backup di un database o di un file di database.  
  
-   Avvio del ripristino di un database o di un file di database.  
  
-   Creazione di uno snapshot  
  
 Le operazioni o condizioni indicate di seguito impediscono l'esecuzione delle istruzioni CREATE DATABASE ENCRYPTION KEY, ALTER DATABASE ENCRYPTION KEY, DROP DATABASE ENCRYPTION KEY e ALTER DATABASE...SET ENCRYPTION.  
  
-   Il database è di sola lettura o ha gruppi di file di sola lettura.  
  
-   È in corso l'esecuzione di un comando ALTER DATABASE.  
  
-   Un backup dei dati è in corso di esecuzione.  
  
-   Il database è offline o è in corso di ripristino.  
  
-   Uno snapshot è in corso.  
  
-   Attività di manutenzione del database.  
  
 Durante la creazione dei file di database, l'inizializzazione immediata dei file non è disponibile se è abilitata la crittografia TDE.  
  
 Per crittografare la chiave di crittografia del database con una chiave asimmetrica, è necessario che quest'ultima risieda in un provider EKM (Extensible Key Management).  
  
### <a name="transparent-data-encryption-and-transaction-logs"></a>Crittografia trasparente dei dati e log delle transazioni  
 Se si abilita TDE per un database, la parte rimanente del log delle transazioni virtuale viene "azzerata" in modo da forzare l'uso del log delle transazioni virtuale successivo. Ciò garantisce che non rimanga alcun testo non crittografato nei log delle transazioni dopo che il database viene impostato per la crittografia. È possibile determinare lo stato di crittografia dei file di log visualizzando la colonna `encryption_state` nella vista `sys.dm_database_encryption_keys`, come illustrato nell'esempio seguente:  
  
```  
USE AdventureWorks2012;  
GO  
/* The value 3 represents an encrypted state   
   on the database and transaction logs. */  
SELECT *  
FROM sys.dm_database_encryption_keys  
WHERE encryption_state = 3;  
GO  
```  
  
 Per altre informazioni sull'architettura del file di log di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], vedere [Log delle transazioni &#40;SQL Server&#41;](../../../relational-databases/logs/the-transaction-log-sql-server.md).  
  
 Tutti i dati scritti nel log delle transazioni prima di una modifica della chiave di crittografia del database saranno crittografati usando la chiave di crittografia del database precedente.  
  
 Dopo che una chiave di crittografia del database è stata modificata due volte, è necessario eseguire un backup del log prima che sia possibile modificare nuovamente la chiave di crittografia del database.  
  
### <a name="transparent-data-encryption-and-the-tempdb-system-database"></a>Transparent Data Encryption e database di sistema tempdb  
 Il database di sistema tempdb verrà crittografato se altri database nell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vengono crittografati tramite Transparent Data Encryption. Ciò potrebbe influire sulla prestazione dei database non crittografati presenti nella stessa istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Per altre informazioni sul database di sistema tempdb, vedere [Database tempdb](../../../relational-databases/databases/tempdb-database.md).  
  
### <a name="transparent-data-encryption-and-replication"></a>Transparent Data Encryption e replica  
 La replica non consente di replicare automaticamente dati da un database abilitato per TDE in un formato crittografato. Per proteggere i database di distribuzione e del Sottoscrittore, è necessario abilitare separatamente TDE. La replica snapshot, nonché la distribuzione iniziale dei dati per la replica transazionale e di tipo merge, può archiviare dati in file intermedi non crittografati, ad esempio i file con estensione bcp.  Durante la replica transazionale o di tipo merge è possibile abilitare la crittografia per proteggere il canale di comunicazione. Per altre informazioni, vedere [Abilitare le connessioni crittografate al motore di database &#40;Gestione configurazione SQL Server&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
### <a name="transparent-data-encryption-and-filestream-data"></a>Transparent Data Encryption e dati FILESTREAM  
 Anche se si abilita TDE, i dati FILESTREAM non vengono crittografati.  

<a name="scan-suspend-resume"></a>

## <a name="transparent-data-encryption-tde-scan"></a>Analisi Transparent Data Encryption (TDE)

Per abilitare Transparent Data Encryption (TDE) in un database, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve eseguire un'analisi della crittografia che legge ogni pagina dei file di dati nel pool di buffer e quindi riscrive le pagine crittografate su disco. Per offrire all'utente maggior controllo sull'analisi della crittografia, [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] include la sintassi per sospendere l'analisi TDE quando il carico di lavoro nel sistema è pesante o durante gli orari strategici per l'azienda e di riprenderla in un momento successivo.

Per sospendere l'analisi della crittografia TDE, usare la sintassi seguente:

```sql
ALTER DATABASE <db_name> SET ENCRYPTION SUSPEND;
```

Per riprendere l'analisi della crittografia TDE, usare la sintassi seguente:

```sql
ALTER DATABASE <db_name> SET ENCRYPTION RESUME;
```

Per visualizzare lo stato corrente dell'analisi della crittografia, `encryption_scan_state` è stato aggiunta alla DMV `sys.dm_database_encryption_keys`. È anche disponibile una nuova colonna denominata `encryption_scan_modify_date` che conterrà la data e l'ora dell'ultima modifica dello stato dell'analisi della crittografia. Si noti anche che se l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] viene riavviata mentre l'analisi della crittografia è sospesa, verrà registrato un messaggio nel log degli errori all'avvio che indica la presenza di un'analisi esistente sospesa.
  
## <a name="transparent-data-encryption-and-buffer-pool-extension"></a>Transparent Data Encryption ed estensione del pool di buffer  
 I file correlati all'estensione del pool di buffer non vengono crittografati quando il database viene crittografato con TDE. Per tali file è necessario usare strumenti di crittografia a livello di file system, come BitLocker o EFS.  
  
## <a name="transparent-data-encryption-and-in-memory-oltp"></a>Transparent Data Encryption e OLTP in memoria  
 È possibile abilitare TDE in un database contenente oggetti di OLTP in memoria. In [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] e [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] , se la funzionalità TDE è abilitata, i dati e i record del log di OLTP in memoria vengono crittografati. In [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] i record di log OLTP in memoria vengono crittografati se è abilitata la crittografia TDE, ma non vengono crittografati i file del filegroup MEMORY_OPTIMIZED_DATA.  
  
## <a name="related-tasks"></a>Attività correlate  
 [Spostare un database protetto da TDE in un'altra istanza di SQL Server](../../../relational-databases/security/encryption/move-a-tde-protected-database-to-another-sql-server.md)  
 [Abilitare TDE in SQL Server con EKM](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
 [Extensible Key Management con l'insieme di credenziali delle chiavi di Azure &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
## <a name="related-content"></a>Contenuto correlato  
 [Transparent Data Encryption con il database SQL di Azure](../../../relational-databases/security/encryption/transparent-data-encryption-azure-sql.md)  
 [Introduzione a Transparent Data Encryption (TDE) in SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-encryption-tde-tsql/)  
 [Crittografia di SQL Server](../../../relational-databases/security/encryption/sql-server-encryption.md)  
 [Chiavi di crittografia del database e di SQL Server &#40;Motore di database&#41;](../../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)  
   
## <a name="see-also"></a>Vedere anche  
 [Centro di sicurezza per il motore di database di SQL Server e il database SQL di Azure](../../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)   
 [FILESTREAM &#40;SQL Server&#41;](../../../relational-databases/blob/filestream-sql-server.md)  
  
  
