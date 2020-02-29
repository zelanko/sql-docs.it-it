---
title: Transparent Data Encryption (TDE) | Microsoft Docs
ms.custom: ''
ms.date: 11/23/2015
ms.prod: sql-server-2014
ms.reviewer: ''
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
author: jaszymas
ms.author: jaszymas
manager: craigg
ms.openlocfilehash: 018cc6fa8b85c4a1b09ab53a6a1a94d8a7670bae
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/28/2020
ms.locfileid: "78176761"
---
# <a name="transparent-data-encryption-tde"></a>Transparent Data Encryption (TDE)
  *Transparent Data Encryption* (Transparent Data [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Encryption [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] ) crittografa i file di dati e, noti come crittografia dei dati inattivi. È possibile adottare diverse precauzioni per proteggere il database, ad esempio la progettazione di un sistema sicuro, la crittografia di asset riservati e la creazione di un firewall che protegga i server di database. Tuttavia, nell'ipotesi del furto dei supporti fisici, come unità o nastri di backup, un malintenzionato potrebbe semplicemente ripristinare o collegare il database e accedere ai dati in esso contenuti. Una soluzione per ovviare al problema consiste nel crittografare i dati sensibili nel database e proteggere con un certificato le chiavi usate per la crittografia. In questo modo si impedisce a chi è sprovvisto delle chiavi di usare i dati; tuttavia, questo tipo di protezione deve essere pianificato in anticipo.

 TDE esegue la crittografia e la decrittografia delle operazioni di I/O di file di dati e log in tempo reale. La crittografia usa una chiave di crittografia del database (DEK) che viene archiviata nel record di avvio del database per la disponibilità durante il ripristino. La chiave di crittografia del database è una chiave simmetrica protetta tramite un certificato archiviato nel database master del server o una chiave asimmetrica protetta da un modulo EKM. TDE consente di proteggere i dati "non operativi", ovvero i file di dati e di log, e assicura la conformità a numerose leggi, normative e linee guida stabilite in vari settori. Gli sviluppatori software possono ora crittografare i dati usando gli algoritmi di crittografia AES e 3DES senza modificare applicazioni esistenti.

> [!IMPORTANT]
>  TDE non fornisce funzionalità di crittografia tramite canali di comunicazione. Per altre informazioni su come crittografare i dati su diversi canali di comunicazione, vedere [Abilitare connessioni crittografate al Motore di database &#40;Gestione configurazione SQL Server&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).
> 
>  **Argomenti correlati:**
> 
>  -   [Transparent Data Encryption con il database SQL di Azure](../../../database-engine/transparent-data-encryption-with-azure-sql-database.md)
> -   [Spostare un database protetto con Transparent Data Encryption in un altro SQL Server](move-a-tde-protected-database-to-another-sql-server.md)
> -   [Abilitare Transparent Data Encryption con EKM](enable-tde-on-sql-server-using-ekm.md)

## <a name="about-tde"></a>Informazioni su TDE
 La crittografia del file di database viene eseguita a livello di pagina. Le pagine di un database crittografato sono crittografate prima di essere scritte sul disco e decrittografate quando vengono lette in memoria. L'uso di TDE non comporta un aumento delle dimensioni del database crittografato.

 **Informazioni applicabili a[!INCLUDE[ssSDS](../../../includes/sssds-md.md)]**

 Quando si usa TDE con [!INCLUDE[sqldbesa](../../../includes/sqldbesa-md.md)] V12 ([anteprima in alcune aree](https://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag)), il certificato a livello di server archiviato nel database master viene creato automaticamente da [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]. Per spostare un database TDE nel [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] , è necessario decrittografare il database, spostarlo e quindi abilitare nuovamente TDE nel [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]di destinazione. Per istruzioni dettagliate su TDE nel [!INCLUDE[ssSDS](../../../includes/sssds-md.md)], vedere [Transparent Data Encryption with Azure SQL Database](../../../database-engine/transparent-data-encryption-with-azure-sql-database.md).

 L'anteprima dello stato di TDE si applica anche nel subset di aree geografiche in cui la famiglia di versioni V12 di [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] è stata annunciata in stato di disponibilità generale. TDE per [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] non potrà essere usato nei database di produzione finché [!INCLUDE[msCoName](../../../includes/msconame-md.md)] non ne annuncia il passaggio dalla versione di anteprima a quella di disponibilità generale. Per altre informazioni sul [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] V12, vedere l'articolo relativo alle [novità del database SQL di Azure](https://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/).

 **Informazioni applicabili a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**

 Una volta protetto, il database può essere ripristinato usando il certificato corretto. Per altre informazioni sui certificati, vedere [SQL Server Certificates and Asymmetric Keys](../sql-server-certificates-and-asymmetric-keys.md).

 Quando si abilita TDE, è consigliabile eseguire immediatamente il backup del certificato e della chiave privata associata al certificato. Se il certificato non è più disponibile o se è necessario ripristinare o collegare il database a un altro server, è necessario disporre di copie di backup del certificato e della chiave privata, altrimenti non sarà possibile aprire il database. Il certificato di crittografia deve essere mantenuto anche se la funzionalità TDE non è più abilitata nel database. Anche se il database non è crittografato, è possibile che parti del log delle transazioni restino comunque protette e che il certificato sia necessario per alcune operazioni per l'esecuzione del backup completo del database. Un certificato che ha superato la data di scadenza può ancora essere usato per crittografare e decrittografare dati con TDE.

 **Gerarchia di crittografia**

 La figura seguente illustra l'architettura della crittografia TDE: Solo gli elementi a livello di database, la chiave di crittografia del database e le parti ALTER DATABASE sono configurabili dall'utente quando si usa TDE nel [!INCLUDE[ssSDS](../../../includes/sssds-md.md)].

 ![Visualizza la gerarchia descritta nell'argomento.](../../../database-engine/media/tde-architecture.gif "Visualizza la gerarchia descritta nell'argomento")

## <a name="using-transparent-data-encryption"></a>Uso della crittografia trasparente dei dati
 Per usare TDE, eseguire le operazioni seguenti:

||
|-|
|**Si applica a**: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|

-   Creare una chiave master

-   Creare o ottenere un certificato protetto dalla chiave master

-   Creare una chiave di crittografia del database e proteggerla mediante il certificato

-   Impostare il database per l'uso della crittografia

 L'esempio seguente illustra come crittografare e decrittografare il database `AdventureWorks2012` usando un certificato installato nel server denominato `MyServerCert`.

```
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
>  I file di backup dei database in cui è abilitata la funzionalità TDE vengono crittografati anche tramite la chiave di crittografia del database. Di conseguenza, quando questi backup vengono ripristinati, è necessario disporre del certificato che protegge la chiave di crittografia del database. Pertanto, oltre ad eseguire il backup del database, è necessario assicurarsi di conservare un backup dei certificati server per impedire la perdita di dati. Se il certificato non è più disponibile, si verificherà la perdita di dati. Per altre informazioni, vedere [SQL Server Certificates and Asymmetric Keys](../sql-server-certificates-and-asymmetric-keys.md).

## <a name="commands-and-functions"></a>Comandi e funzioni
 Affinché vengano accettati dalle istruzioni indicate di seguito, è necessario che i certificati TDE siano crittografati mediante la chiave master del database. Se sono crittografati solo tramite password, verranno rifiutati dalle istruzioni come componenti di crittografia.

> [!IMPORTANT]
>  Se si modificano i certificati per abilitarne la protezione tramite password quando vengono usati da TDE, il database diventerà inaccessibile dopo un riavvio.

 Nella tabella seguente sono inclusi collegamenti e spiegazioni delle funzioni e dei comandi correlati a TDE.

|Comando o funzione|Scopo|
|-------------------------|-------------|
|[CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-database-encryption-key-transact-sql)|Consente di creare una chiave usata per crittografare un database.|
|[ALTER DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-encryption-key-transact-sql)|Consente di modificare la chiave usata per crittografare un database.|
|[DROP DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-database-transact-sql)|Consente di rimuovere la chiave usata per crittografare un database.|
|[Opzioni ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)|Viene descritta l'opzione `ALTER DATABASE`, utilizzata per abilitare Transparent Data Encryption.|

## <a name="catalog-views-and-dynamic-management-views"></a>Viste del catalogo e viste a gestione dinamica
 Nella tabella seguente vengono illustrate le viste del catalogo e le viste a gestione dinamica di TDE.

|Vista del catalogo e vista a gestione dinamica|Scopo|
|---------------------------------------------|-------------|
|[sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)|Vista del catalogo che consente di visualizzare le informazioni del database.|
|[sys.certificates &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-certificates-transact-sql)|Vista del catalogo che consente di visualizzare i certificati di un database.|
|[sys.dm_database_encryption_keys &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql)|Tramite la vista a gestione dinamica vengono fornite informazioni relative alle chiavi di crittografia usate in un database e allo stato di crittografia di un database.|

## <a name="permissions"></a>Autorizzazioni
 Ogni funzionalità e comando di TDE ha requisiti specifici relativi alle autorizzazioni, descritti nelle tabelle precedenti.

 La visualizzazione dei metadati interessati da TDE richiede l'autorizzazione VIEW DEFINITION per il certificato.

## <a name="considerations"></a>Considerazioni
 Durante un'analisi di una nuova crittografia di un database, le operazioni di manutenzione per il database sono disabilitate. È possibile usare l'impostazione modalità utente singolo per il database per eseguire operazioni di manutenzione. Per altre informazioni, vedere [Impostare un database in modalità utente singolo](../../databases/set-a-database-to-single-user-mode.md).

 È possibile determinare lo stato della crittografia del database utilizzando la vista a gestione dinamica sys.dm_database_encryption_keys. Per altre informazioni, vedere la sezione "Viste del catalogo e viste a gestione dinamica" più indietro in questo argomento.

 In TDE vengono crittografati tutti i file e i filegroup del database. Se un database include filegroup contrassegnati come READ ONLY, l'operazione di crittografia del database avrà esito negativo.

 Se un database viene usato per il mirroring del database o il log shipping, entrambi i database saranno crittografati. Le transazioni del log verranno crittografate quando vengono inviate tra i database.

> [!IMPORTANT]
>  Qualsiasi nuovo indice full-text viene crittografato quando un database è impostato per la crittografia. Gli indici full-text creati in precedenza verranno importati durante l'aggiornamento e saranno configurati per TDE in seguito al caricamento dei dati in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. L'abilitazione di un indice full-text in una colonna può provocare la scrittura in testo normale dei dati di tale colonna nel disco durante un'analisi dell'indicizzazione full-text. È consigliabile non creare un indice full-text sui dati crittografati riservati.

 I dati crittografati vengono compressi molto meno rispetto ai dati equivalenti non crittografati. Se per crittografare un database si usa TDE, l'archivio di backup non verrà compresso in modo significativo tramite l'opzione di compressione dei backup. Non è quindi consigliabile usare TDE insieme all'opzione di compressione dei backup.

### <a name="restrictions"></a>Restrizioni
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

 Per altre informazioni sull'architettura del file di log di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], vedere [Log delle transazioni &#40;SQL Server&#41;](../../logs/the-transaction-log-sql-server.md).

 Tutti i dati scritti nel log delle transazioni prima di una modifica della chiave di crittografia del database saranno crittografati usando la chiave di crittografia del database precedente.

 Dopo che una chiave di crittografia del database è stata modificata due volte, è necessario eseguire un backup del log prima che sia possibile modificare nuovamente la chiave di crittografia del database.

### <a name="transparent-data-encryption-and-the-tempdb-system-database"></a>Transparent Data Encryption e database di sistema tempdb
 Il database di sistema tempdb verrà crittografato se altri database nell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vengono crittografati tramite Transparent Data Encryption. Ciò potrebbe influire sulla prestazione dei database non crittografati presenti nella stessa istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Per altre informazioni sul database di sistema tempdb, vedere [Database tempdb](../../databases/tempdb-database.md).

### <a name="transparent-data-encryption-and-replication"></a>Transparent Data Encryption e replica
 La replica non consente di replicare automaticamente dati da un database abilitato per TDE in un formato crittografato. Per proteggere i database di distribuzione e del Sottoscrittore, è necessario abilitare separatamente TDE. La replica snapshot, nonché la distribuzione iniziale dei dati per la replica transazionale e di tipo merge, può archiviare dati in file intermedi non crittografati, ad esempio i file con estensione bcp.  Durante la replica transazionale o di tipo merge è possibile abilitare la crittografia per proteggere il canale di comunicazione. Per altre informazioni, vedere [Abilitare le connessioni crittografate al motore di database &#40;Gestione configurazione SQL Server&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).

### <a name="transparent-data-encryption-and-filestream-data"></a>Transparent Data Encryption e dati FILESTREAM
 Anche se si abilita TDE, i dati FILESTREAM non vengono crittografati.

### <a name="transparent-data-encryption-and-buffer-pool-extension"></a>Transparent Data Encryption ed estensione del pool di buffer
 I file correlati all'estensione del pool di buffer non vengono crittografati quando il database viene crittografato con TDE. Per tali file è necessario usare strumenti di crittografia a livello di file system, come Bitlocker o EFS.

## <a name="transparent-data-encryption-and-in-memory-oltp"></a>Transparent Data Encryption e OLTP in memoria
 È possibile abilitare TDE in un database contenente oggetti di OLTP in memoria. Se la funzionalità TDE è abilitata, i record del log di OLTP in memoria vengono crittografati. I dati nel filegroup MEMORY_OPTIMIZED_DATA non vengono crittografati se la funzionalità TDE è abilitata.

## <a name="see-also"></a>Vedere anche
 [Spostare un database protetto con Transparent Data Encryption in un altro SQL Server](move-a-tde-protected-database-to-another-sql-server.md) [abilitare](enable-tde-on-sql-server-using-ekm.md) Transparent data encryption [con EKM Transparent Data Encryption con il database sql di Azure](../../../database-engine/transparent-data-encryption-with-azure-sql-database.md) [SQL Server crittografia](sql-server-encryption.md) [SQL Server e chiavi di crittografia del database &#40;motore di database&#41;](sql-server-and-database-encryption-keys-database-engine.md) [Centro sicurezza per SQL Server motore di database e FileStream &#40;del database SQL di Azure](../security-center-for-sql-server-database-engine-and-azure-sql-database.md) [](../../blob/filestream-sql-server.md) SQL Server


