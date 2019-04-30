---
title: Usare un file di formato per ignorare un campo dati (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- format files [SQL Server], skipping data fields
- skipping data fields when importing
ms.assetid: 6a76517e-983b-47a1-8f02-661b99859a8b
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bad791f1eab5fbb31976236e6d79c08e8b9adc97
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63155821"
---
# <a name="use-a-format-file-to-skip-a-data-field-sql-server"></a>Utilizzo di un file di formato per escludere un campo di dati (SQL Server)
  È possibile che un file di dati contenga un numero di campi maggiore del numero di colonne presenti nella tabella. In questo argomento viene descritta la modifica dei file di formato XML e non XML per consentire l'utilizzo di un file di dati con un numero maggiore di campi tramite il mapping delle colonne della tabella ai campi dati corrispondenti e l'esclusione dei campi aggiuntivi.  
  
> [!NOTE]  
>  È possibile usare un file di formato non XML o XML per importare in blocco un file di dati nella tabella usando un comando **bcp**, l'istruzione BULK INSERT o l'istruzione INSERT... Istruzione SELECT * FROM OPENROWSET(BULK...). Per altre informazioni, vedere [Usare un file di formato per l'importazione in blocco dei dati &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md).  
  
## <a name="sample-data-file-and-table"></a>File di dati e tabella di esempio  
 Gli esempi di file di formato modificati contenuti in questo argomento sono basati sulla tabella e sul file di dati seguenti.  
  
### <a name="sample-table"></a>Tabella di esempio  
 Per gli esempi, è necessario che nel database di esempio `myTestSkipField` venga creata una tabella [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] basata sullo schema `dbo` . Per creare la tabella, nell'editor di query di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] eseguire il codice seguente:  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTestSkipField   
   (  
   PersonID smallint,  
   FirstName nvarchar(50) ,  
   LastName nvarchar(50)   
   );  
GO  
```  
  
### <a name="sample-data-file"></a>File di dati di esempio  
 Il file di dati `myTestSkipField-c.dat`include i record seguenti:  
  
```  
1,Skipme,DataField3,DataField4  
1,Skipme,DataField3,DataField4  
1,Skipme,DataField3,DataField4  
```  
  
 Per eseguire un'importazione bulk dei dati da `myTestSkipField-c.dat` nella tabella `myTestSkipField` , è necessario che il file di formato esegua le operazioni seguenti:  
  
-   Mapping del primo campo dati alla prima colonna `PersonID`.  
  
-   Esclusione del secondo campo dati.  
  
-   Mapping del terzo campo dati alla seconda colonna `FirstName`.  
  
-   Mapping del quarto campo dati alla terza colonna `LastName`.  
  
## <a name="non-xml-format-file-for-more-data-fields"></a>File di formato non XML per un maggior numero di campi dati  
 Il file di formato seguente, `myTestSkipField.fmt`, esegue il mapping dei campi di `myTestSkipField-c.dat` alle colonne della tabella `myTestSkipField` Il file di formato utilizza dati di tipo carattere. Per escludere il mapping di una colonna, è necessario modificare il valore relativo all'ordine della colonna impostandolo su 0, come illustrato per la colonna `ExtraField` nel file di formato.  
  
 Il file di formato `myTestSkipField.fmt` contiene le informazioni seguenti:  
  
```  
9.0  
4  
1       SQLCHAR       0       7       ","      1     PersonID               ""  
2       SQLCHAR       0       100       ","    0     ExtraField             SQL_Latin1_General_CP1_CI_AS  
3       SQLCHAR       0       100     ","      2     FirstName              SQL_Latin1_General_CP1_CI_AS  
4       SQLCHAR       0       100     "\r\n"   3     LastName               SQL_Latin1_General_CP1_CI_AS  
  
```  
  
> [!NOTE]  
>  Per informazioni sulla sintassi dei file di formato non XML, vedere [File in formato non XML &#40;SQL Server&#41;](xml-format-files-sql-server.md).  
  
### <a name="examples"></a>Esempi  
 Nell'esempio seguente viene utilizzata l'istruzione `INSERT ... SELECT * FROM OPENROWSET(BULK...)` con il file di formato `myTestSkipField.fmt` . Nell'esempio viene eseguita l'importazione bulk del file di dati `myTestSkipField-c.dat` nella tabella `myTestSkipField` . Per creare il file di dati e la tabella di esempio, vedere la sezione "File di dati e tabella di esempio" più indietro in questo argomento.  
  
 Nell'editor di query di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] eseguire il codice seguente:  
  
```  
USE AdventureWorks2012;  
GO  
INSERT INTO myTestSkipField   
   SELECT *  
      FROM  OPENROWSET(BULK  'C:\myTestSkipField-c.dat',  
      FORMATFILE='C:\myTestSkipField.fmt'    
       ) AS t1;  
GO   
```  
  
## <a name="xml-format-file-for-more-data-fields"></a>File di formato XML per un maggior numero di campi dati  
 Il file di formato utilizzato in questo esempio è basato su un altro file di formato, `myTestSkipField.xml`, che utilizza il formato di dati carattere e i cui campi corrispondono esattamente per numero e ordine alle colonne della tabella `myTestSkipField`. Per visualizzare il contenuto del file di formato, vedere [Creare un file di formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md).  
  
 Il file di formato seguente, `myTestSkipField.xml`, esegue il mapping dei campi di `myTestSkipField-c.dat` alle colonne della tabella `myTestSkipField` Il file di formato utilizza dati di tipo carattere.  
  
 Il file di formato `myTestSkipField.xml` contiene le informazioni seguenti:  
  
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
  <COLUMN SOURCE="1" NAME="PersonID" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="3" NAME="FirstName" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="4" NAME="LastName" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
### <a name="examples"></a>Esempi  
 Nell'esempio seguente viene utilizzata l'istruzione `INSERT ... SELECT * FROM OPENROWSET(BULK...)` con il file di formato `myTestSkipField.Xml` . Nell'esempio viene eseguita l'importazione bulk del file di dati `myTestSkipField-c.dat` nella tabella `myTestSkipField` . Per creare il file di dati e la tabella di esempio, vedere la sezione "File di dati e tabella di esempio" più indietro in questo argomento.  
  
 Nell'editor di query di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] eseguire il codice seguente:  
  
```  
USE AdventureWorks2012;  
GO  
INSERT INTO myTestSkipField   
  SELECT *  
      FROM  OPENROWSET(BULK  'C:\myTestSkipField-c.dat',  
      FORMATFILE='C:\myTestSkipField.xml'    
       ) AS t1;  
GO  
  
```  
  
> [!NOTE]  
>  Per altre informazioni sulla sintassi dell'XML Schema e ulteriori esempi di file di formato XML, vedere [File in formato XML &#40;SQL Server&#41;](xml-format-files-sql-server.md).  
  
## <a name="see-also"></a>Vedere anche  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [Usare un file di formato per ignorare una colonna di una tabella &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)   
 [Usare un file di formato per eseguire il mapping tra le colonne della tabella e i campi del file di dati &#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
  
