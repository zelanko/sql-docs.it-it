---
title: Usare un file di formato per l'importazione in blocco dei dati (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 09/20/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk importing [SQL Server], format files
- format files [SQL Server], importing data using
ms.assetid: 2956df78-833f-45fa-8a10-41d6522562b9
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 683e96bff8f9067c32c861582c949df0d3e531c0
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2019
ms.locfileid: "54257166"
---
# <a name="use-a-format-file-to-bulk-import-data-sql-server"></a>Utilizzo di un file di formato per l'importazione bulk dei dati (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

In questo argomento viene illustrato l'utilizzo di un file di formato per operazioni di importazione bulk.  Un file di formato esegue il mapping dei campi del file di dati alle colonne della tabella.  Per altre informazioni, vedere [Creazione di un file di formato (SQL Server)](../../relational-databases/import-export/create-a-format-file-sql-server.md) .

|Riquadro|
|---|
|[Prima di iniziare](#begin)<br />[Condizioni di test di esempio](#etc)<br />&emsp;&#9679;&emsp;[Tabella di esempio](#sample_table)<br />&emsp;&#9679;&emsp;[File di dati di esempio](#sample_data_file)<br />[Creazione dei file di formato](#create_format_file)<br />&emsp;&#9679;&emsp;[Creazione di un file di formato non XML](#nonxml_format_file)<br />&emsp;&#9679;&emsp;[Creazione di un file di formato XML](#xml_format_file)<br />[Utilizzo di un file di formato per l'importazione bulk dei dati](#import_data)<br />&emsp;&#9679;&emsp;[Uso di bcp e di un file di formato non XML](#bcp_nonxml)<br />&emsp;&#9679;&emsp;[Uso di bcp e di un file di formato XML](#bcp_xml)<br />&emsp;&#9679;&emsp;[Uso di BULK INSERT e di un file di formato non XML](#bulk_nonxml)<br />&emsp;&#9679;&emsp;[Uso di BULK INSERT e di un file di formato XML](#bulk_xml)<br />&emsp;&#9679;&emsp;[Uso di OPENROWSET(BULK...) e di un file di formato non XML](#openrowset_nonxml)<br />&emsp;&#9679;&emsp;[Uso di OPENROWSET(BULK...) e di un file di formato XML](#openrowset_xml)<p>                                                                                                                                                                                                                  </p>|
  
## Prima di iniziare<a name="begin"></a>
* Affinché un file di formato funzioni con un file di dati di formato carattere Unicode, è necessario che tutti i campi di input siano stringhe di testo Unicode, ovvero stringhe Unicode di dimensioni fisse o che terminano con un carattere.
* Per l'esportazione o l'importazione in blocchi di dati [SQLXML](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md) usare uno dei tipi di dati seguenti nel file di formato:
  * SQLCHAR o SQLVARYCHAR (i dati vengono inviati nella tabella codici del client o nella tabella codici implicita delle regole di confronto)
  * SQLNCHAR or SQLNVARCHAR (i dati vengono inviati come Unicode)
  * SQLBINARY or SQLVARYBIN (i dati vengono inviati senza conversione).
* Il database SQL di Azure e Azure SQL Data Warehouse supportano solo [bcp](../../tools/bcp-utility.md).  Per altre informazioni, vedere:
  * [Caricare i dati in Azure SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-overview-load/)
  * [Caricare dati da SQL Server in Azure SQL Data Warehouse (file flat)](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-load-from-sql-server-with-bcp/)
  * [Eseguire la migrazione dei dati](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-migrate-data/)

## Condizioni di test di esempio<a name="etc"></a>  
Gli esempi di file di formato contenuti in questo argomento sono basati sulla tabella e sul file di dati definiti di seguito.

### **Tabella di esempio**<a name="sample_table"></a>
Lo script seguente crea un database di prova e una tabella denominata `myFirstImport`.  Eseguire l'istruzione Transact-SQL seguente in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
CREATE DATABASE TestDatabase;
GO

USE TestDatabase;
CREATE TABLE dbo.MyFirstImport (
   PersonID smallint,
   FirstName varchar(25),
   LastName varchar(30),
   BirthDate Date
   );
```

### **File di dati di esempio**<a name="sample_data_file"></a>
Usando il Blocco note, creare un file `D:\BCP\myFirstImport.bcp` vuoto e inserire i dati seguenti:
```
1,Anthony,Grosse,1980-02-23
2,Alica,Fatnowna,1963-11-14
3,Stella,Rosenhain,1992-03-02
```

In alternativa, è possibile eseguire lo script PowerShell seguente per creare e popolare il file di dati:
```powershell
cls
# revise directory as desired
$dir = 'D:\BCP\';

$bcpFile = Join-Path -Path $dir -ChildPath 'MyFirstImport.bcp';

# Confirm directory exists
IF ((Test-Path -Path $dir) -eq 0)
{
    Write-Host "The path $dir does not exist; please create or modify the directory.";
    RETURN;
};

# clear content, will error if file does not exist, can be ignored
Clear-Content -Path $bcpFile -ErrorAction SilentlyContinue;

# Add data
Add-Content -Path $bcpFile -Value '1,Anthony,Grosse,1980-02-23';
Add-Content -Path $bcpFile -Value '2,Alica,Fatnowna,1963-11-14';
Add-Content -Path $bcpFile -Value '3,Stella,Rosenhain,1992-03-02';

#Review content
Get-Content -Path $bcpFile;
Invoke-Item $bcpFile;
```

## Creazione dei file di formato<a name="create_format_file"></a>
SQL Server supporta due tipi di file di formato, ovvero non XML e XML.  Il formato non XML è il formato originale supportato dalle versioni precedenti di SQL Server.

### **Creazione di un file di formato non XML**<a name="nonxml_format_file"></a>
Per informazioni dettagliate, vedere [File in formato non XML (SQL Server)](../../relational-databases/import-export/non-xml-format-files-sql-server.md) .  Il comando seguente userà l' [utility bcp](../../tools/bcp-utility.md) per generare un formato di file non XML, `myFirstImport.fmt`, sulla base dello schema di `myFirstImport`.  Per usare un comando bcp per creare un file di formato, specificare l'argomento **format** e usare **null** anziché un percorso del file di dati.  L'opzione format richiede anche l'opzione **-f** .  Inoltre, in questo esempio il qualificatore **c** viene usato per specificare dati di tipo carattere, **t,** viene usato per specificare la virgola come [carattere di terminazione del campo](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)e **T** viene usato per specificare una connessione trusted che usa la sicurezza integrata.  Al prompt dei comandi immettere il comando seguente:

```cmd
bcp TestDatabase.dbo.myFirstImport format nul -c -f D:\BCP\myFirstImport.fmt -t, -T

REM Review file
Notepad D:\BCP\myFirstImport.fmt
```

Il file di formato non XML `D:\BCP\myFirstImport.fmt` dovrebbe essere simile a questo:
```
13.0
4
1       SQLCHAR             0       7       ","      1     PersonID               ""
2       SQLCHAR             0       25      ","      2     FirstName              SQL_Latin1_General_CP1_CI_AS
3       SQLCHAR             0       30      ","      3     LastName               SQL_Latin1_General_CP1_CI_AS
4       SQLCHAR             0       11      "\r\n"   4     BirthDate              ""
```

> [!IMPORTANT]
> Verificare che il file di formato non XML termini con un ritorno a capo/avanzamento riga.  In caso contrario, è possibile che venga visualizzato il messaggio di errore seguente:
> 
> `SQLState = S1000, NativeError = 0`  
> `Error = [Microsoft][ODBC Driver 13 for SQL Server]I/O error while reading BCP format file`

### **Creazione di un file di formato XML**<a name="xml_format_file"></a>  
Per informazioni dettagliate, vedere [File in formato XML (SQL Server)](../../relational-databases/import-export/xml-format-files-sql-server.md) .  Il comando seguente userà l' [utilità bcp](../../tools/bcp-utility.md) per creare un file di formato XML, `myFirstImport.xml`, sulla base dello schema di `myFirstImport`. Per usare un comando bcp per creare un file di formato, specificare l'argomento **format** e usare **null** anziché un percorso del file di dati.  L'opzione format richiede sempre l'opzione **-f** e per creare un file di formato XML è necessario anche specificare l'opzione **-x** .  Inoltre, in questo esempio il qualificatore **c** viene usato per specificare dati di tipo carattere, **t,** viene usato per specificare la virgola come [carattere di terminazione del campo](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)e **T** viene usato per specificare una connessione trusted che usa la sicurezza integrata.  Al prompt dei comandi immettere il comando seguente:
```cmd
bcp TestDatabase.dbo.myFirstImport format nul -c -x -f D:\BCP\myFirstImport.xml -t, -T

REM Review file
Notepad D:\BCP\myFirstImport.xml
```

Il file di formato XML `D:\BCP\myFirstImport.xml` dovrebbe essere simile al seguente:
```xml
<?xml version="1.0"?>
<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
 <RECORD>
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="25" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="30" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>
  <FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="11"/>
 </RECORD>
 <ROW>
  <COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>
  <COLUMN SOURCE="2" NAME="FirstName" xsi:type="SQLVARYCHAR"/>
  <COLUMN SOURCE="3" NAME="LastName" xsi:type="SQLVARYCHAR"/>
  <COLUMN SOURCE="4" NAME="BirthDate" xsi:type="SQLDATE"/>
 </ROW>
</BCPFORMAT>
```

## Utilizzo di un file di formato per l'importazione bulk dei dati<a name="import_data"></a>
Gli esempi seguenti usano il database, il file di dati e i file di formato creati in precedenza.

### **Uso di [bcp](../../tools/bcp-utility.md) e di un [file di formato non XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bcp_nonxml"></a>
Al prompt dei comandi immettere il comando seguente:
```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.MyFirstImport;"

REM Import data
bcp TestDatabase.dbo.myFirstImport IN D:\BCP\myFirstImport.bcp -f D:\BCP\myFirstImport.fmt -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.MyFirstImport"
```


### **Uso di [bcp](../../tools/bcp-utility.md) e di un [file di formato XML](../../relational-databases/import-export/xml-format-files-sql-server.md)**<a name="bcp_xml"></a>
Al prompt dei comandi immettere il comando seguente:
```cmd
REM Truncate table (for testing)
SQLCMD -Q "TRUNCATE TABLE TestDatabase.dbo.MyFirstImport;"

REM Import data
bcp TestDatabase.dbo.myFirstImport IN D:\BCP\myFirstImport.bcp -f D:\BCP\myFirstImport.xml -T

REM Review results
SQLCMD -Q "SELECT * FROM TestDatabase.dbo.MyFirstImport;"
```


### **Uso di [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) e di un [file di formato non XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="bulk_nonxml"></a>
Eseguire l'istruzione Transact-SQL seguente in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myFirstImport; -- (for testing)
BULK INSERT dbo.myFirstImport   
   FROM 'D:\BCP\myFirstImport.bcp'   
   WITH (FORMATFILE = 'D:\BCP\myFirstImport.fmt');  
GO  

-- review results
SELECT * FROM TestDatabase.dbo.myFirstImport;
```

### **Uso di [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) e di un [file di formato XML](../../relational-databases/import-export/xml-format-files-sql-server.md)**<a name="bulk_xml"></a>
Eseguire l'istruzione Transact-SQL seguente in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myFirstImport; -- (for testing)
BULK INSERT dbo.myFirstImport   
   FROM 'D:\BCP\myFirstImport.bcp'   
   WITH (FORMATFILE = 'D:\BCP\myFirstImport.xml');  
GO  

-- review results
SELECT * FROM TestDatabase.dbo.myFirstImport;
```

### **Uso di [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) e di un [file di formato non XML](../../relational-databases/import-export/non-xml-format-files-sql-server.md)**<a name="openrowset_nonxml"></a>    
Eseguire l'istruzione Transact-SQL seguente in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
USE TestDatabase;
GO

TRUNCATE TABLE myFirstImport; -- (for testing)
INSERT INTO dbo.myFirstImport
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myFirstImport.bcp',
        FORMATFILE = 'D:\BCP\myFirstImport.fmt'
        ) AS t1;
GO

-- review results
SELECT * FROM TestDatabase.dbo.myFirstImport;
```

### **Uso di [OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) e di un [file di formato XML](../../relational-databases/import-export/xml-format-files-sql-server.md)**<a name="openrowset_xml"></a>
Eseguire l'istruzione Transact-SQL seguente in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS):
```sql
USE TestDatabase;  
GO

TRUNCATE TABLE myFirstImport; -- (for testing)
INSERT INTO dbo.myFirstImport 
    SELECT *
    FROM OPENROWSET (
        BULK 'D:\BCP\myFirstImport.bcp',
        FORMATFILE = 'D:\BCP\myFirstImport.xml'  
       ) AS t1;
GO

-- review results
SELECT * FROM TestDatabase.dbo.myFirstImport;
```
  
## <a name="more-examples"></a>Altri esempi  
 [Creazione di un file di formato &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md)  
 [Utilizzo di un file di formato per ignorare una colonna di una tabella &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
 [Utilizzo di un file di formato per escludere un campo di dati &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
 [Utilizzo di un file di formato per eseguire il mapping tra le colonne della tabella e i campi del file di dati &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Utilità bcp](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [File in formato non XML &#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md)   
 [File in formato XML &#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md)  
  [File di formato per l'importazione o l'esportazione di dati (SQL Server)](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)
  
