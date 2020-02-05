---
title: Accesso bulk ai dati nell'archiviazione BLOB di Azure
ms.description: Transact-SQL examples that use BULK INSERT and OPENROWSET to access data in an Azure Blob storage account.
ms.date: 10/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk importing [SQL Server], from Azure blob storage
- Azure blob storage, bulk import to SQL Server
- BULK INSERT, Azure blob storage
- OPENROWSET, Azure blob storage
ms.assetid: f7d85db3-7a93-400e-87af-f56247319ecd
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.custom: seo-lt-2019
ms.openlocfilehash: 08e81abbc21671881affc80fc9b7f0346cd490f7
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "74056012"
---
# <a name="examples-of-bulk-access-to-data-in-azure-blob-storage"></a>Esempi di accesso bulk ai dati nell'archiviazione BLOB di Azure

[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

Le istruzioni `BULK INSERT` e `OPENROWSET` consentono di accedere direttamente a un file nell'archiviazione BLOB di Azure. Gli esempi seguenti usano dati da un file CSV (con valori delimitati da virgola) denominato `inv-2017-01-19.csv`, archiviato in un contenitore denominato `Week3` e archiviato in un account di archiviazione denominato `newinvoices`. È possibile usare il percorso al file di formato, ma non è incluso in questi esempi.

Per l'accesso bulk all'archiviazione BLOB di Azure da SQL Server è necessario almeno [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.

> [!IMPORTANT]
> Tutti i percorsi del contenitore e dei file nel BLOB sono `CASE SENSITIVE`. Se l'impostazione non è corretta, è possibile che venga restituito un errore di tipo "Impossibile eseguire il caricamento bulk. Il file "file.csv" non esiste oppure non si dispone dell'autorizzazione per accedervi.

## <a name="create-the-credential"></a>Creare le credenziali

Per tutti gli esempi seguenti sono necessarie credenziali con ambito database che fanno riferimento a una firma di accesso condiviso.

> [!IMPORTANT]
> L'origine dati esterna deve essere creata con credenziali con ambito database che usano l'identità `SHARED ACCESS SIGNATURE`. Per creare una firma di accesso condiviso per l'account di archiviazione, vedere la proprietà **Firma di accesso condiviso** nella pagine delle proprietà dell'account di archiviazione, nel portale di Azure. Per altre informazioni sulle firme di accesso condiviso, vedere [Uso delle firme di accesso condiviso](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1). Per altre informazioni sulle credenziali, vedere [CREATE DATABASE SCOPED CREDENTIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md).

Creare credenziali con ambito database usando `IDENTITY` che deve essere `SHARED ACCESS SIGNATURE`. Usare il token di firma di accesso condiviso generato per l'account di archiviazione BLOB. Verificare che il token di firma di accesso condiviso non abbia un `?` iniziale, che sia disponibile almeno l'autorizzazione di lettura per l'oggetto che deve essere caricato e che il periodo di scadenza sia valido (tutte le date sono in ora UTC).

Ad esempio:

```sql
CREATE DATABASE SCOPED CREDENTIAL UploadInvoices
WITH IDENTITY = 'SHARED ACCESS SIGNATURE',
SECRET = 'sv=2018-03-28&ss=b&srt=sco&sp=rwdlac&se=2019-08-31T02:25:19Z&st=2019-07-30T18:25:19Z&spr=https&sig=KS51p%2BVnfUtLjMZtUTW1siyuyd2nlx294tL0mnmFsOk%3D';
```

## <a name="accessing-data-in-a-csv-file-referencing-an-azure-blob-storage-location"></a>Accesso ai dati in un file CSV che fa riferimento a un percorso di archiviazione BLOB di Azure

L'esempio seguente usa un'origine dati esterna che punta a un account di archiviazione di Azure denominato `MyAzureInvoices`.

```sql
CREATE EXTERNAL DATA SOURCE MyAzureInvoices
    WITH (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://newinvoices.blob.core.windows.net',
        CREDENTIAL = UploadInvoices
    );
```

L'istruzione `OPENROWSET` aggiunge quindi il nome del contenitore (`week3`) alla descrizione del file. Il file è denominato `inv-2017-01-19.csv`.

```sql
SELECT * FROM OPENROWSET(
   BULK 'week3/inv-2017-01-19.csv',
   DATA_SOURCE = 'MyAzureInvoices',
   FORMAT = 'CSV',
   FORMATFILE='invoices.fmt',
   FORMATFILE_DATA_SOURCE = 'MyAzureInvoices'
   ) AS DataFile;   
```

Con `BULK INSERT`, usare il contenitore e la descrizione del file:

```sql
BULK INSERT Colors2
FROM 'week3/inv-2017-01-19.csv'
WITH (DATA_SOURCE = 'MyAzureInvoices',
      FORMAT = 'CSV');
```

## <a name="accessing-data-in-a-csv-file-referencing-a-container-in-an-azure-blob-storage-location"></a>Accesso ai dati in un file CSV che fa riferimento a un contenitore in un percorso di archiviazione BLOB di Azure

L'esempio seguente usa un'origine dati esterna che punta a un contenitore denominato `week3` in un account di archiviazione di Azure.

```sql
CREATE EXTERNAL DATA SOURCE MyAzureInvoicesContainer
    WITH (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://newinvoices.blob.core.windows.net/week3',
        CREDENTIAL = UploadInvoices
    );
```

L'istruzione `OPENROWSET` non include il nome del contenitore nella descrizione del file.

```sql
SELECT * FROM OPENROWSET(
   BULK 'inv-2017-01-19.csv',
   DATA_SOURCE = 'MyAzureInvoicesContainer',
   FORMAT = 'CSV',
   FORMATFILE='invoices.fmt',
   FORMATFILE_DATA_SOURCE = 'MyAzureInvoices'
   ) AS DataFile;
```

Con `BULK INSERT`, non usare il nome del contenitore nella descrizione del file:

```sql
BULK INSERT Colors2
FROM 'inv-2017-01-19.csv'
WITH (DATA_SOURCE = 'MyAzureInvoicesContainer',
      FORMAT = 'CSV');
```

## <a name="see-also"></a>Vedere anche

- [CREATE DATABASE SCOPED CREDENTIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)
- [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md)
- [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)
- [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)
