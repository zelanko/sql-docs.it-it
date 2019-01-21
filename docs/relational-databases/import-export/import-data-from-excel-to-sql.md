---
title: Importare dati da Excel a SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 09/23/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 77acf33ae4cdc4626f5467f136d8fb96b5ba96ed
ms.sourcegitcommit: 96032813f6bf1cba680b5e46d82ae1f0f2da3d11
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/15/2019
ms.locfileid: "54299549"
---
# <a name="import-data-from-excel-to-sql-server-or-azure-sql-database"></a>Importare dati da Excel a SQL Server o al database SQL di Azure
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

> [!div class="nextstepaction"]
> [Condividi il feedback sul sommario della documentazione SQL](https://aka.ms/sqldocsurvey)

Sono disponibili vari modi per importare dati da file di Excel a SQL Server o al database SQL di Azure. Alcuni metodi consentono di importare dati in un unico passaggio direttamente dai file di Excel. Altri metodi richiedono l'esportazione dei dati di Excel in formato testo prima di poterli importare. Questo articolo riepiloga i metodi usati di frequente e include collegamenti a informazioni più dettagliate.

## <a name="list-of-methods"></a>Elenco di metodi

-   È possibile importare i dati in un unico passaggio direttamente da Excel a SQL usando uno degli strumenti seguenti:
    -   [Importazione/Esportazione guidata SQL Server](#wiz)
    -   [SQL Server Integration Services (SSIS)](#ssis)
    -   Funzione [OPENROWSET](#openrowset)
-   È possibile importare i dati in due passaggi, esportandoli da Excel come testo e usando uno degli strumenti seguenti per importare il file di testo:
    -   [Procedura guidata Importa file flat](#import-wiz)
    -   Istruzione [BULK INSERT](#bulk-insert)
    -   [BCP](#bcp)
    -   [Copia guidata (Azure Data Factory)](#adf-wiz)
    -   [Azure Data Factory](#adf)

Se si vogliono importare più fogli di lavoro da una cartella di lavoro di Excel, è generalmente necessario eseguire una volta ogni strumento per ogni foglio.

Una descrizione completa degli strumenti e dei servizi complessi come Azure Data Factory o SSIS esula dagli scopi di questo elenco. Per altre informazioni sulla soluzione a cui si è interessati, seguire i collegamenti indicati.

> [!IMPORTANT]
> Per informazioni dettagliate sulla connessione ai file di Excel e sulle limitazioni e i problemi noti per il caricamento di dati da o a file di Excel, vedere [Caricare i dati da o in Excel con SQL Server Integration Services (SSIS)](../../integration-services/load-data-to-from-excel-with-ssis.md).

## <a name="wiz"></a> Importazione/Esportazione guidata SQL Server

È possibile importare i dati direttamente dai file di Excel scorrendo le pagine dell'Importazione/Esportazione guidata SQL Server. Facoltativamente, salvare le impostazioni come pacchetto di SQL Server Integration Services (SSIS) che è possibile personalizzare e riusare in seguito.

Per informazioni su come avviare la procedura guidata, vedere [Avviare l'Importazione/Esportazione guidata SQL Server](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md).

Per un esempio di come usare la procedura guidata per l'importazione da Excel a SQL Server, vedere [Get started with this simple example of the Import and Export Wizard](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md) (Iniziare con un semplice esempio dell'Importazione/Esportazione guidata).

![Connettersi a un'origine dati Excel](media/excel-connection.png)

## <a name="ssis"></a> SQL Server Integration Services (SSIS)

Se si ha familiarità con SSIS e si preferisce non eseguire l'Importazione/Esportazione guidata di SQL Server, creare un pacchetto SSIS che usa Excel come origine e SQL Server come destinazione nel flusso di dati.

Per altre informazioni su questi componenti di SSIS, vedere gli argomenti seguenti:
-   [Origine Excel](../../integration-services/data-flow/excel-source.md)
-   [Destinazione SQL Server](../../integration-services/data-flow/sql-server-destination.md)

Per istruzioni su come creare pacchetti SSIS, vedere l'esercitazione [Creazione di un pacchetto ETL](../../integration-services/ssis-how-to-create-an-etl-package.md).

![Componenti del flusso di dati](media/excel-to-sql-data-flow.png)

## <a name="openrowset"></a> OPENROWSET e server collegati

> [!NOTE]
> In Azure le funzioni OPENROWSET e OPENDATASOURCE sono disponibili solo in Istanza gestita di database SQL.

> [!NOTE]
> Il provider ACE (in precedenza provider Jet) che si connette alle origini dati di Excel è destinato all'uso interattivo sul lato client. Se si usa il provider ACE nel server, in particolare in processi automatizzati o processi in esecuzione in parallelo, si possono ottenere risultati imprevisti.

### <a name="distributed-queries"></a>Query distribuite

Importare i dati direttamente dai file di Excel usando la funzione `OPENROWSET` o `OPENDATASOURCE` di Transact-SQL. Questo utilizzo è noto come *query distribuita*.

Prima di eseguire una query distribuita, è necessario abilitare l'opzione di configurazione del server `ad hoc distributed queries`, come illustrato nell'esempio seguente. Per altre informazioni, vedere [Opzione di configurazione del server ad hoc distributed queries](../../database-engine/configure-windows/ad-hoc-distributed-queries-server-configuration-option.md).

```sql
sp_configure 'show advanced options', 1;
RECONFIGURE;
GO
sp_configure 'Ad Hoc Distributed Queries', 1;
RECONFIGURE;
GO
```

L'esempio di codice seguente usa `OPENROWSET` per importare i dati dal foglio di lavoro di Excel `Data` in una nuova tabella di database.

```sql
USE ImportFromExcel;
GO
SELECT * INTO Data_dq
FROM OPENROWSET('Microsoft.ACE.OLEDB.12.0',
    'Excel 12.0; Database=D:\Desktop\Data.xlsx', [Data$]);
GO
```

Ecco lo stesso esempio con `OPENDATASOURCE`.

```sql
USE ImportFromExcel;
GO
SELECT * INTO Data_dq
FROM OPENDATASOURCE('Microsoft.ACE.OLEDB.12.0',
    'Data Source=D:\Desktop\Data.xlsx;Extended Properties=Excel 12.0')...[Data$];
GO
```

Per *aggiungere* i dati importati a una tabella *esistente* invece di creare una nuova tabella, usare la sintassi `INSERT INTO ... SELECT ... FROM ...` al posto della sintassi `SELECT ... INTO ... FROM ...` usata negli esempi precedenti.

Per eseguire una query sui dati di Excel senza eseguirne l'importazione, usare la sintassi standard `SELECT ... FROM ...`.

Per altre informazioni sulle query distribuite, vedere gli argomenti seguenti:
-   [Query distribuite](https://msdn.microsoft.com/library/ms188721(v=sql.105).aspx) (Le query distribuite sono ancora supportate in SQL Server 2016, ma la documentazione relativa a questa funzionalità non è stata aggiornata.)
-   [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)
-   [OPENDATASOURCE](../../t-sql/functions/openquery-transact-sql.md)

### <a name="linked-servers"></a>Server collegati

È anche possibile configurare una connessione permanente al file di Excel come *server collegato*. L'esempio seguente importa i dati dal foglio di lavoro `Data` nel server collegato di Excel esistente `EXCELLINK` in una nuova tabella di database denominata `Data_ls`.

```sql
USE ImportFromExcel;
GO
SELECT * INTO Data_ls FROM EXCELLINK...[Data$];
GO
```

È possibile creare un server collegato da SQL Server Management Studio o eseguendo la stored procedure di sistema `sp_addlinkedserver`, come illustrato nell'esempio seguente.

```sql
DECLARE @RC int

DECLARE @server     nvarchar(128)
DECLARE @srvproduct nvarchar(128)
DECLARE @provider   nvarchar(128)
DECLARE @datasrc    nvarchar(4000)
DECLARE @location   nvarchar(4000)
DECLARE @provstr    nvarchar(4000)
DECLARE @catalog    nvarchar(128)

-- Set parameter values
SET @server =     'EXCELLINK'
SET @srvproduct = 'Excel'
SET @provider =   'Microsoft.ACE.OLEDB.12.0'
SET @datasrc =    'D:\Desktop\Data.xlsx'
SET @provstr =    'Excel 12.0'

EXEC @RC = [master].[dbo].[sp_addlinkedserver] @server, @srvproduct, @provider,
@datasrc, @location, @provstr, @catalog
```

Per altre informazioni sui server collegati, vedere gli argomenti seguenti:
-   [Creare server collegati](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md)
-   [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md)

Per altri esempi e informazioni sia sui server collegati che sulle query distribuite, vedere gli argomenti seguenti:
-   [How to use Excel with SQL Server linked servers and distributed queries](https://support.microsoft.com/help/306397/how-to-use-excel-with-sql-server-linked-servers-and-distributed-queries) (Come usare Excel con server collegati e query distribuite di SQL Server)
-   [Come importare dati da Excel a SQL Server](https://support.microsoft.com/help/321686/how-to-import-data-from-excel-to-sql-server)

## <a name="prereq"></a> Prerequisito: salvare i dati di Excel come testo
Per usare i restanti metodi descritti in questa pagina, ovvero l'istruzione BULK INSERT, lo strumento BCP o Azure Data Factory, è prima di tutto necessario esportare i dati di Excel in un file di testo.

In Excel selezionare **File | Salva con nome** e quindi selezionare **Testo (con valori delimitati da tabulazioni) (\*.txt)** o **CSV (delimitato dal separatore di elenco) (\*.csv)** come tipo di file di destinazione.

Se si vuole esportare più fogli di lavoro dalla cartella di lavoro, selezionare ogni foglio e ripetere questa procedura. Il comando **Salva con nome** esporta solo il foglio attivo.

> [!TIP]
> Per ottenere risultati ottimali con gli strumenti per l'importazione dei dati, salvare fogli che contengono solo le intestazioni di colonna e le righe di dati. Se i dati salvati contengono titoli di pagina, righe vuote, note e così via, possono verificarsi risultati imprevisti in un secondo momento quando si importano i dati.

## <a name="import-wiz"></a> Procedura guidata Importa file flat

È possibile importare i dati salvati come file di testo seguendo le varie pagine della procedura guidata Importa file flat.

Come descritto in precedenza nella sezione [Prerequisito](#prereq), è necessario esportare i dati Excel come testo prima di poter usare la procedura guidata Importa file flat per eseguire l'importazione.

Per altre informazioni sulla procedura guidata Importa File Flat, vedere [Procedura guidata per l'importazione di file flat in SQL](import-flat-file-wizard.md).

## <a name="bulk-insert"></a> Comando BULK INSERT

`BULK INSERT` è un comando Transact-SQL che è possibile eseguire da SQL Server Management Studio. L'esempio seguente carica i dati dal file con valori delimitati da virgole `Data.csv` in una tabella di database esistente.

Come descritto in precedenza nella sezione [Prerequisito](#prereq), è necessario esportare i dati Excel come testo prima di usare l'istruzione BULK INSERT per eseguire l'importazione. L'istruzione BULK INSERT non legge direttamente i file di Excel.

```sql
USE ImportFromExcel;
GO
BULK INSERT Data_bi FROM 'D:\Desktop\data.csv'
   WITH (
      FIELDTERMINATOR = ',',
      ROWTERMINATOR = '\n'
);
GO
```

Per altre informazioni, vedere gli argomenti seguenti:
-   [Importare dati per operazioni bulk usando BULK INSERT o OPENROWSET (BULK...)](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)
-   [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)

## <a name="bcp"></a> Strumento BCP

BCP è un programma eseguibile dal prompt dei comandi. L'esempio seguente carica i dati dal file con valori delimitati da virgole `Data.csv` nella tabella di database `Data_bcp` esistente.

Come descritto in precedenza nella sezione [Prerequisito](#prereq), è necessario esportare i dati Excel come testo prima di usare BCP per eseguire l'importazione. BCP non legge direttamente i file di Excel.

```sql
bcp.exe ImportFromExcel..Data_bcp in "D:\Desktop\data.csv" -T -c -t ,
```

Per altre informazioni su BCP, vedere gli argomenti seguenti:
-   [Importare ed esportare dati per operazioni bulk usando l'utilità bcp](../../relational-databases/import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)
-   [Utilità bcp](../../tools/bcp-utility.md)
-   [Preparare i dati per l'importazione o l'esportazione bulk](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)

## <a name="adf-wiz"></a> Copia guidata (Azure Data Factory)
È possibile importare i dati salvati come file di testo seguendo le varie pagine della Copia guidata di Azure Data Factory.

Come descritto in precedenza nella sezione [Prerequisito](#prereq), è necessario esportare i dati Excel come testo prima di usare Azure Data Factory per eseguire l'importazione. Azure Data Factory non legge direttamente i file di Excel.

Per altre informazioni sulla Copia guidata, vedere gli argomenti seguenti:
-   [Copia guidata di Azure Data Factory](https://docs.microsoft.com/azure/data-factory/data-factory-azure-copy-wizard)
-   [Esercitazione: Creare una pipeline con l'attività di copia usando la Copia guidata di Data Factory](https://docs.microsoft.com/azure/data-factory/data-factory-copy-data-wizard-tutorial).

## <a name="adf"></a> Azure Data Factory
Se si ha familiarità con Azure Data Factory e si preferisce non eseguire la Copia guidata, creare una pipeline con un'attività di copia dal file di testo a SQL Server o al database SQL di Azure.

Come descritto in precedenza nella sezione [Prerequisito](#prereq), è necessario esportare i dati Excel come testo prima di usare Azure Data Factory per eseguire l'importazione. Azure Data Factory non legge direttamente i file di Excel.

Per altre informazioni sull'uso di questi sink e origini di Data Factory, vedere gli argomenti seguenti:
-   [File system](https://docs.microsoft.com/azure/data-factory/data-factory-onprem-file-system-connector)
-   [SQL Server](https://docs.microsoft.com/azure/data-factory/data-factory-sqlserver-connector)
-   [Database SQL di Azure](https://docs.microsoft.com/azure/data-factory/data-factory-azure-sql-connector)

Per istruzioni su come copiare dati con Azure Data Factory, vedere gli argomenti seguenti:
-   [Spostare dati con l'attività di copia](https://docs.microsoft.com/azure/data-factory/data-factory-data-movement-activities)
-   [Esercitazione: Creare una pipeline con l'attività di copia usando il portale di Azure](https://docs.microsoft.com/azure/data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database)

## <a name="see-also"></a>Vedere anche
[Caricare dati da o in Excel con SQL Server Integration Services (SSIS)](../../integration-services/load-data-to-from-excel-with-ssis.md)
