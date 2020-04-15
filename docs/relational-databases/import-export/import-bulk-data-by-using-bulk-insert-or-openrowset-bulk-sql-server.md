---
title: Usare BULK INSERT o OPENROWSET (BULK...) per importare dati in SQL Server
description: Informazioni su come usare le istruzioni Transact-SQL per eseguire l'importazione bulk di dati da un file a una tabella di SQL Server o del database SQL di Azure, incluse le considerazioni sulla sicurezza.
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- BULK INSERT statement, importing data from a remote data file
- bulk importing [SQL Server], methods
- bulk exporting [SQL Server], methods
- OPENROWSET function, BULK INSERT
- bulk importing [SQL Server], security
- bulk rowset providers [SQL Server]
- bulk exporting [SQL Server], BULK INSERT statement
- remote data access [SQL Server], bulk importing
- bulk importing [SQL Server], BULK INSERT statement
- Transact-SQL bulk export/import operations
ms.assetid: 18a64236-0285-46ea-8929-6ee9bcc020b9
author: markingmyname
ms.author: maghan
manager: jroth
ms.date: 09/25/2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.custom: seo-lt-2019
ms.openlocfilehash: fe9d407b446177004715ae5d3403e856028985d3
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80980583"
---
# <a name="use-bulk-insert-or-openrowsetbulk-to-import-data-to-sql-server"></a>Usare BULK INSERT o OPENROWSET (BULK...) per importare dati in SQL Server

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

In questo articolo viene fornita una panoramica sull'uso delle istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] BULK INSERT e INSERT...SELECT * FROM OPENROWSET(BULK...) per effettuare l'importazione bulk di dati da un file di dati in una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o del database SQL di Azure. L'articolo include anche considerazioni sulla sicurezza per l'uso di BULK INSERT e di OPENROWSET(BULK…), nonché sull'uso di questi metodi per l'importazione bulk da un'origine dati remota.

> [!NOTE]
> Quando si usa BULK INSERT o OPENROWSET(BULK...), è importante comprendere in che modo la versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gestisce la rappresentazione. Per ulteriori informazioni, vedere la sezione "Considerazioni sulla sicurezza" di seguito in questo argomento.

## <a name="bulk-insert-statement"></a>BULK INSERT - istruzione

L'istruzione BULK INSERT consente di caricare dati da un file di dati a una tabella. Questa funzionalità è analoga a quella dell'opzione **in** del comando **bcp** , ma il file di dati viene letto dal processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per una descrizione della sintassi di BULK INSERT, vedere [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md).

## <a name="bulk-insert-examples"></a>Esempi di BULK INSERT

- [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)
- [Esempi di importazione ed esportazione bulk di documenti XML &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)
- [Mantenere i valori Identity durante l'importazione in blocco dei dati &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)
- [Mantenimento dei valori Null o uso dei valori predefiniti durante un'importazione bulk &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)
- [Impostazione dei caratteri di terminazione del campo e della riga &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)
- [Usare un file di formato per l'importazione in blocco dei dati &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)
- [Utilizzo del formato carattere per l'importazione o l'esportazione di dati &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)
- [Usare il formato nativo per importare o esportare dati &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)
- [Utilizzo del formato carattere Unicode per l'importazione o l'esportazione di dati &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)
- [Usare il formato Unicode nativo per importare o esportare dati &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)
- [Utilizzo di un file di formato per ignorare una colonna di una tabella &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)
- [Utilizzo di un file di formato per eseguire il mapping tra le colonne della tabella e i campi del file di dati &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)

## <a name="openrowsetbulk-function"></a>OPENROWSET(BULK...) Funzione

Al provider bulk per set di righe OPENROWSET si accede chiamando la funzione OPENROWSET e specificando l'opzione BULK. La funzione OPENROWSET(BULK...) consente di accedere ai dati remoti connettendosi a un'origine dei dati remota, ad esempio un file di dati, con un provider OLE DB.

Per eseguire l'importazione bulk dei dati, chiamare OPENROWSET(BULK...) da una clausola SELECT...FROM all'interno di un'istruzione INSERT. La sintassi di base per l'importazione bulk dei dati è la seguente:

INSERT ... SELECT * FROM OPENROWSET(BULK...).

Quando utilizzato in un'istruzione INSERT, OPENROWSET(BULK...) supporta gli hint di tabella. Oltre agli hint di tabella normali, ad esempio TABLOCK, la clausola BULK può accettare gli hint di tabella specializzati seguenti: IGNORE_CONSTRAINTS (ignora solo i vincoli CHECK), IGNORE_TRIGGERS, KEEPDEFAULTS e KEEPIDENTITY. Per altre informazioni, vedere [Hint di tabella &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).

Per informazioni sugli usi aggiuntivi dell'opzione BULK, vedere [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md).

## <a name="insertselect--from-openrowsetbulk-statements---examples"></a>Esempi di istruzioni INSERT...SELECT * FROM OPENROWSET(BULK...):

- [Esempi di importazione ed esportazione bulk di documenti XML &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)
- [Mantenere i valori Identity durante l'importazione in blocco dei dati &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)
- [Mantenimento dei valori Null o uso dei valori predefiniti durante un'importazione bulk &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)
- [Usare un file di formato per l'importazione in blocco dei dati &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)
- [Utilizzo del formato carattere per l'importazione o l'esportazione di dati &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)
- [Utilizzo di un file di formato per ignorare una colonna di una tabella &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)
- [Utilizzo di un file di formato per escludere un campo di dati &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)
- [Utilizzo di un file di formato per eseguire il mapping tra le colonne della tabella e i campi del file di dati &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)

## <a name="security-considerations"></a>Considerazioni relative alla sicurezza

Se un utente utilizza un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , viene utilizzato il profilo di sicurezza dell'account del processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Un account di accesso basato sull'autenticazione di SQL Server non può essere autenticato all'esterno del motore di database. Pertanto, quando un comando BULK INSERT viene avviato da un account di accesso che utilizza l'autenticazione di SQL, la connessione ai dati viene effettuata utilizzando il contesto di sicurezza dell'account del processo di SQL Server (l'account utilizzato dal servizio Motore di database di SQL Server). 

Per una lettura corretta dei dati di origine è necessario concedere all'account utilizzato dal motore di database di SQL Server l'accesso ai dati di origine. Al contrario, se un utente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue l'accesso utilizzando l'autenticazione di Windows, potrà leggere solo i file accessibili dall'account utente, indipendentemente dal profilo di sicurezza del processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

Ad esempio, considerare un utente che abbia eseguito l'accesso a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando l'autenticazione di Windows. Perché l'utente sia in grado di utilizzare BULK INSERT o OPENROWSET per importare dati da un file di dati in una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è necessario che l'account utente disponga dell'accesso in lettura al file di dati. Con l'accesso al file di dati, l'utente può importare i dati dal file in una tabella anche se il processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non dispone dell'autorizzazione per accedere al file. Non è necessario che l'utente conceda l'autorizzazione di accesso al file al processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows possono essere configurati in modo da abilitare un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per connettersi a un'altra istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trasmettendo le credenziali di un utente di Windows autenticato. Questa configurazione è nota come *rappresentazione* o *delega*. La comprensione delle modalità di gestione della sicurezza da parte della versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ai fini della rappresentazione dell'utente rappresenta un elemento importante quando si usa BULK INSERT o OPENROWSET. La rappresentazione utente fa sì che i file di dati possano trovarsi su un computer diverso rispetto al processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o all'utente. Se, ad esempio, un utente nel **Computer_A** ha accesso a un file di dati presente nel **Computer_B**e la delega delle credenziali è stata impostata in modo corretto, l'utente potrà connettersi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in esecuzione nel **Computer_C**, accedere al file di dati nel **Computer_B**ed effettuare un'importazione in blocco dei dati dal file in una tabella nel **Computer_C**.

## <a name="bulk-importing-to-sql-server-from-a-remote-data-file"></a>Importazione bulk in SQL Server da un file di dati remoto

Per usare BULK INSERT o INSERT...SELECT \* FROM OPENROWSET(BULK...) per effettuare l'importazione in blocco dei dati da un altro computer, è necessario che il file di dati sia condiviso tra i due computer. Per specificare un file di dati condiviso, usare il relativo nome UNC (Universal Naming Convention), il cui formato generico è **\\\\** _Nomeserver_ **\\** _Nomecondivisione_ **\\** _Percorso_ **\\** _Nomefile_. Inoltre, è necessario che all'account utilizzato per l'accesso al file di dati siano state concesse le autorizzazioni richieste per la lettura del file sul disco remoto.

Ad esempio, l'istruzione `BULK INSERT` seguente esegue l'importazione bulk dei dati nella tabella `SalesOrderDetail` del database `AdventureWorks` da un file di dati denominato `newdata.txt`. Tale file di dati è memorizzato in una cartella condivisa denominata `\dailyorders` e presente in una directory condivisa di rete denominata `salesforce` in un sistema denominato `computer2`.

```sql
BULK INSERT AdventureWorks2012.Sales.SalesOrderDetail
   FROM '\\computer2\salesforce\dailyorders\neworders.txt';
```

> [!NOTE]
> Questa restrizione non si applica all'utilità **bcp** perché il client legge il file in modo indipendente da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

## <a name="bulk-importing-from-azure-blob-storage"></a>Importazione bulk da Archiviazione BLOB di Azure

Quando si esegue l'importazione da Archiviazione BLOB di Azure e i dati non sono pubblici (accesso anonimo), creare [credenziali con ambito database](../../t-sql/statements/create-database-scoped-credential-transact-sql.md) basate su una chiave di firma di accesso condiviso crittografata con una [chiave master](../../t-sql/statements/create-master-key-transact-sql.md) e quindi creare un'[origine del database esterna](../../t-sql/statements/create-external-data-source-transact-sql.md) da usare nel comando BULK INSERT.

### <a name="using-bulk-insert"></a>Utilizzo di BULK INSERT

L'esempio seguente illustra come usare il comando BULK INSERT per caricare dati da un file CSV in una posizione di Archiviazione BLOB di Azure in cui è stata creata una chiave di firma di accesso condiviso. La posizione di Archiviazione BLOB di Azure è configurata come origine dati esterna. Questa operazione richiede credenziali con ambito database che usano una firma di accesso condiviso crittografata con una chiave master nel database utente.

```sql
--> Optional - a MASTER KEY is not required if a DATABASE SCOPED CREDENTIAL is not required because the blob is configured for public (anonymous) access!
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'YourStrongPassword1';
GO
--> Optional - a DATABASE SCOPED CREDENTIAL is not required because the blob is configured for public (anonymous) access!
CREATE DATABASE SCOPED CREDENTIAL MyAzureBlobStorageCredential
 WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
 SECRET = '******srt=sco&sp=rwac&se=2017-02-01T00:55:34Z&st=2016-12-29T16:55:34Z***************';

 -- NOTE: Make sure that you don't have a leading ? in SAS token, and
 -- that you have at least read permission on the object that should be loaded srt=o&sp=r, and
 -- that expiration period is valid (all dates are in UTC time)

CREATE EXTERNAL DATA SOURCE MyAzureBlobStorage
WITH ( TYPE = BLOB_STORAGE,
          LOCATION = 'https://****************.blob.core.windows.net/invoices'
          , CREDENTIAL= MyAzureBlobStorageCredential --> CREDENTIAL is not required if a blob is configured for public (anonymous) access!
);

BULK INSERT Sales.Invoices
FROM 'inv-2017-12-08.csv'
WITH (DATA_SOURCE = 'MyAzureBlobStorage');
```

> [!IMPORTANT]
> Il database SQL di Azure non supporta la lettura da file di Windows.

### <a name="using-openrowset"></a>Uso di OPENROWSET

L'esempio seguente illustra come usare il comando OPENROWSET per caricare dati da un file CSV in una posizione di Archiviazione BLOB di Azure in cui è stata creata una chiave di firma di accesso condiviso. La posizione di Archiviazione BLOB di Azure è configurata come origine dati esterna. Questa operazione richiede credenziali con ambito database che usano una firma di accesso condiviso crittografata con una chiave master nel database utente.

```sql
--> Optional - a MASTER KEY is not required if a DATABASE SCOPED CREDENTIAL is not required because the blob is configured for public (anonymous) access!
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'YourStrongPassword1';
GO
--> Optional - a DATABASE SCOPED CREDENTIAL is not required because the blob is configured for public (anonymous) access!
CREATE DATABASE SCOPED CREDENTIAL MyAzureBlobStorageCredential
 WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
 SECRET = '******srt=sco&sp=rwac&se=2017-02-01T00:55:34Z&st=2016-12-29T16:55:34Z***************';

 -- NOTE: Make sure that you don't have a leading ? in SAS token, and
 -- that you have at least read permission on the object that should be loaded srt=o&sp=r, and
 -- that expiration period is valid (all dates are in UTC time)

CREATE EXTERNAL DATA SOURCE MyAzureBlobStorage
WITH ( TYPE = BLOB_STORAGE,
          LOCATION = 'https://****************.blob.core.windows.net/invoices'
          , CREDENTIAL= MyAzureBlobStorageCredential --> CREDENTIAL is not required if a blob is configured for public (anonymous) access!
);

INSERT INTO achievements with (TABLOCK) (id, description)
SELECT * FROM OPENROWSET(
   BULK  'csv/achievements.csv',
   DATA_SOURCE = 'MyAzureBlobStorage',
   FORMAT ='CSV',
   FORMATFILE='csv/achievements-c.xml',
   FORMATFILE_DATA_SOURCE = 'MyAzureBlobStorage'
    ) AS DataFile;
```

> [!IMPORTANT]
> Il database SQL di Azure non supporta la lettura da file di Windows.

## <a name="see-also"></a>Vedere anche

- [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)
- [Clausola SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-clause-transact-sql.md)
- [Informazioni sull'importazione ed esportazione bulk di dati &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)
- [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)
- [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)
- [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)
- [Utilità bcp](../../tools/bcp-utility.md)
- [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)  
