---
title: Usare un file di formato per l'importazione in blocco dei dati (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: fddec2033997a1b76f34fa9a2fe006d385bc0132
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63155872"
---
# <a name="use-a-format-file-to-bulk-import-data-sql-server"></a>Utilizzo di un file di formato per l'importazione bulk dei dati (SQL Server)
  In questo argomento viene illustrato l'utilizzo di un file di formato per operazioni di importazione bulk. Il file di formato esegue il mapping dei campi del file di dati alle colonne della tabella.  È possibile usare un file in formato XML o non XML per eseguire un'importazione in blocco dei dati quando si usa un comando **bcp** o un'istruzione BULK INSERT o INSERT. Comando SELECT * FROM OPENROWSET(BULK...) [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
> [!IMPORTANT]  
>  Affinché un file di formato sia funzionante con un file di dati di formato carattere Unicode, è necessario che tutti i campi di input siano stringhe di testo Unicode, ovvero stringhe Unicode di dimensioni fisse o che terminano con un carattere.  
  
> [!NOTE]  
>  Se non si ha familiarità con i file di formato, vedere [i file di formato Non XML &#40;SQL Server&#41; ](xml-format-files-sql-server.md) e [i file di formato XML &#40;SQL Server&#41;](xml-format-files-sql-server.md).  
  
## <a name="format-file-options-for-bulk-import-commands"></a>Opzioni del file di formato per comandi di importazione bulk  
 Nella tabella seguente vengono riepilogate le opzioni del file di formato per ogni comando di importazione bulk.  
  
|Comando di caricamento bulk|Utilizzo dell'opzione del file di formato|  
|------------------------|-----------------------------------|  
|BULK INSERT|FORMATFILE = '*format_file_path*'|  
|INSERT ... SELECT * FROM OPENROWSET(BULK...).|FORMATFILE = '*format_file_path*'|  
|**bcp** ... **in**|**-f** *format_file*|  
  
 Per altre informazioni, vedere [Utilità bcp](../../tools/bcp-utility.md), [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql) o [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql).  
  
> [!NOTE]  
>  Per eseguire l'esportazione o l'importazione bulk di dati SQLXML, utilizzare uno dei tipi di dati seguenti nel file di formato: SQLCHAR o SQLVARYCHAR (i dati vengono inviati nella tabella codici del client o nella tabella codici implicita nelle regole di confronto), SQLNCHAR o SQLNVARCHAR (i dati vengono inviati come Unicode) oppure SQLBINARY o SQLVARYBIN (i dati vengono inviati senza conversione).  
  
## <a name="examples"></a>Esempi  
 Gli esempi di questa sezione illustrano come usare i file di formato per l'importazione in blocco di dati con il comando **bcp** e le istruzioni BULK INSERT e INSERT. SELECT * FROM OPENROWSET(BULK...). Prima di eseguire uno degli esempi di importazione bulk, è necessario creare una tabella, un file di dati e un file di formato di esempio.  
  
### <a name="sample-table"></a>Tabella di esempio  
 Gli esempi richiedono la creazione di una tabella denominata **myTestFormatFiles** nel database di esempio [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] in base allo schema **dbo**. Per creare la tabella, nell'editor di query di [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] eseguire:  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTestFormatFiles (  
   Col1 smallint,  
   Col2 nvarchar(50),  
   Col3 nvarchar(50),  
   Col4 nvarchar(50)  
   );  
GO  
```  
  
### <a name="sample-data-file"></a>File di dati di esempio  
 Nell'esempio viene utilizzato un file di dati di esempio, `myTestFormatFiles-c.Dat`, che include i record riportati di seguito. Per creare il file di dati, al prompt dei comandi di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows digitare:  
  
```  
10,Field2,Field3,Field4  
15,Field2,Field3,Field4  
46,Field2,Field3,Field4  
58,Field2,Field3,Field4  
```  
  
### <a name="sample-format-files"></a>File di formato di esempio  
 In alcuni esempi di questa sezione viene utilizzato un file di formato XML, `myTestFormatFiles-f-x-c.Xml`, mentre in altri esempi viene utilizzato un file di formato non XML. In entrambi i file di formato viene utilizzato il formato carattere e un carattere di terminazione del campo non predefinito (,).  
  
#### <a name="the-sample-non-xml-format-file"></a>File di formato non XML di esempio  
 L'esempio seguente usa **bcp** per generare un file di formato XML dalla tabella `myTestFormatFiles`. Il file `myTestFormatFiles.Fmt` contiene le informazioni seguenti:  
  
```  
9.0  
4  
1       SQLCHAR       0       7       ","      1     Col1         ""  
2       SQLCHAR       0       100     ","      2     Col2         SQL_Latin1_General_CP1_CI_AS  
3       SQLCHAR       0       100     ","      3     Col3         SQL_Latin1_General_CP1_CI_AS  
4       SQLCHAR       0       100     "\r\n"   4     Col4         SQL_Latin1_General_CP1_CI_AS  
```  
  
 Per usare **bcp** con l'opzione **format** per creare questo file di formato, al prompt dei comandi di Windows digitare:  
  
```  
bcp AdventureWorks2012..MyTestFormatFiles format nul -c -t, -f myTestFormatFiles.Fmt -T  
  
```  
  
 Per altre informazioni sulla creazione di un file di formato, vedere [Creazione di un file di formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md).  
  
#### <a name="the-sample-xml-format-file"></a>File di formato XML di esempio  
 L'esempio seguente viene usa **bcp** per creare un file di formato XML dalla tabella `myTestFormatFiles`. Il file `myTestFormatFiles.Xml` contiene le informazioni seguenti:  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="Col1" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Col2" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="3" NAME="Col3" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="4" NAME="Col4" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
 Per usare **bcp** con l'opzione **format** per creare questo file di formato, al prompt dei comandi di Windows digitare:  
  
```  
bcp AdventureWorks2012..MyTestFormatFiles format nul -c -t, -x -f myTestFormatFiles.Xml -T  
```  
  
### <a name="using-bcp"></a>Utilizzo di bcp  
 L'esempio seguente usa **bcp** per l'importazione in blocco dei dati dal file di dati `myTestFormatFiles-c.Dat` nella tabella `HumanResources.myTestFormatFiles` del database di esempio. In questo esempio viene utilizzato un file di formato XML, `MyTestFormatFiles.Xml`, ed eventuali righe di tabella esistenti vengono eliminate prima dell'importazione del file di dati.  
  
 Al prompt dei comandi di Windows digitare:  
  
```  
bcp AdventureWorks2012..myTestFormatFiles in C:\myTestFormatFiles-c.Dat -f C:\myTestFormatFiles.Xml -T  
```  
  
> [!NOTE]  
>  Per altre informazioni su questo comando, vedere [Utilità bcp](../../tools/bcp-utility.md).  
  
### <a name="using-bulk-insert"></a>Utilizzo di BULK INSERT  
 Nell'esempio seguente viene utilizzato BULK INSERT per l'importazione bulk dei dati dal file di dati `myTestFormatFiles-c.Dat` nella tabella `HumanResources.myTestFormatFiles` del database di esempio [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)]. In questo esempio viene utilizzato un file di formato non XML, `MyTestFormatFiles.Fmt`, ed eventuali righe di tabella esistenti vengono eliminate prima dell'importazione del file di dati.  
  
 Nell'editor di query di [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] eseguire:  
  
```  
USE AdventureWorks2012;  
GO  
DELETE myTestFormatFiles;  
GO  
BULK INSERT myTestFormatFiles   
   FROM 'C:\myTestFormatFiles-c.Dat'   
   WITH (FORMATFILE = 'C:\myTestFormatFiles.Fmt');  
GO  
SELECT * FROM myTestFormatFiles;  
GO  
```  
  
> [!NOTE]  
>  Per altre informazioni su questa istruzione, vedere [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql).  
  
### <a name="using-the-openrowset-bulk-rowset-provider"></a>Utilizzo del provider di set di righe con lettura bulk OPENROWSET  
 Nell'esempio seguente viene utilizzato `INSERT ... SELECT * FROM OPENROWSET(BULK...)` per l'importazione bulk dei dati dal file di dati `myTestFormatFiles-c.Dat` nella tabella `HumanResources.myTestFormatFiles` del database di esempio `AdventureWorks`. In questo esempio viene utilizzato un file di formato XML, `MyTestFormatFiles.Xml`, ed eventuali righe di tabella esistenti vengono eliminate prima dell'importazione del file di dati.  
  
 Nell'editor di query di [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] eseguire:  
  
```  
USE AdventureWorks2012;  
DELETE myTestFormatFiles;  
GO  
INSERT INTO myTestFormatFiles  
    SELECT *  
      FROM  OPENROWSET(BULK  'C:\myTestFormatFiles-c.Dat',  
      FORMATFILE='C:\myTestFormatFiles.Xml'       
      ) as t1 ;  
GO  
SELECT * FROM myTestFormatFiles;  
GO  
```  
  
 Al termine dell'utilizzo della tabella di esempio, è possibile rimuoverla mediante l'istruzione seguente:  
  
```  
DROP TABLE myTestFormatFiles  
```  
  
> [!NOTE]  
>  Per altre informazioni sulla clausola OPENROWSET BULK, vedere [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql).  
  
## <a name="additional-examples"></a>Esempi aggiuntivi  
 [Creazione di un file di formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md)  
  
 [Utilizzo di un file di formato per ignorare una colonna di una tabella &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
 [Utilizzo di un file di formato per escludere un campo di dati &#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
 [Utilizzo di un file di formato per eseguire il mapping tra le colonne della tabella e i campi del file di dati &#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="see-also"></a>Vedere anche  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [File in formato non XML &#40;SQL Server&#41;](xml-format-files-sql-server.md)   
 [File in formato XML &#40;SQL Server&#41;](xml-format-files-sql-server.md)  
  
  
