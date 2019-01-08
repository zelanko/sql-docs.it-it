---
title: Usare un file di formato per eseguire il mapping tra le colonne della tabella e i campi del file di dati (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- mapping columns to fields during import [SQL Server]
- format files [SQL Server], mapping columns to fields
ms.assetid: e7ee4f7e-24c4-4eb7-84d2-41e57ccc1ef1
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 26db59ba5dbfc6f7be8d827a86dabb1cdd845d03
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53371533"
---
# <a name="use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server"></a>Utilizzo di un file di formato per eseguire il mapping tra le colonne della tabella e i campi del file di dati (SQL Server)
  Un file di dati può includere campi disposti in un ordine diverso da quello delle colonne corrispondenti presenti nella tabella. In questo argomento vengono descritti file di formato sia non XML che XML, modificati per adattarli a un file di dati contenente campi disposti un ordine diverso da quello delle colonne della tabella. Il file di formato modificato esegue il mapping tra i campi dati e le colonne corrispondenti della tabella.  
  
> [!NOTE]  
>  Per eseguire l'importazione bulk di un file di dati nella tabella mediante un comando **bcp** o un'istruzione BULK INSERT o INSERT ..., è possibile usare un file di formato non XLM o un file di formato XML. Istruzione SELECT * FROM OPENROWSET(BULK...). Per altre informazioni, vedere [Utilizzo di un file di formato per l'importazione bulk dei dati &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md).  
  
## <a name="sample-table-and-data-file"></a>Tabella e file di dati di esempio  
 Gli esempi di file di formato modificati contenuti in questo argomento sono basati sulla tabella e sul file di dati seguenti.  
  
### <a name="sample-table"></a>Tabella di esempio  
 Per gli esempi di questo argomento è necessario creare una tabella denominata `myTestOrder` nel database di esempio [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] nello schema `dbo`. A tale scopo, nell'editor di query di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] eseguire il codice seguente:  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTestOrder   
   (  
   Col1 smallint,  
   Col2 nvarchar(50) ,  
   Col3 nvarchar(50) ,   
   Col4 nvarchar(50)   
   );  
GO  
  
```  
  
### <a name="data-file"></a>File di dati  
 Il file di dati `myTestOrder-c.txt` include i record seguenti:  
  
```  
DataField3,DataField2,1,DataField4  
DataField3,DataField2,1,DataField4  
DataField3,DataField2,1,DataField4  
  
```  
  
 Per eseguire l'importazione bulk dei dati da `myTestSkipCol2-c.dat` alla tabella `myTestSkipCol`, il file di formato deve eseguire il mapping tra il primo campo dati e `Col3`, il secondo campo dati e `Col2`, il terzo campo dati e `Col1` e il quarto campo dati e `Col4`.  
  
## <a name="using-a-non-xml-format-file"></a>Utilizzo di un file di formato non XML  
 È possibile cambiare l'ordine del mapping di una colonna modificando il valore relativo all'ordine della colonna per indicare la posizione del campo dati corrispondente.  
  
 Nel seguente file di formato non XML di esempio è illustrato un file di formato, `myTestOrder.fmt`, che esegue il mapping tra i campi in `myTestOrder-c.txt` e le colonne della tabella `myTestOrder`. Per informazioni su come creare la tabella e il file di dati, vedere "Tabella e file di dati di esempio", più indietro in questo argomento. Il file di formato utilizza dati di tipo carattere.  
  
 Il file di formato contiene le informazioni seguenti:  
  
```  
9.0  
4  
1       SQLCHAR       0       100     ","     3     Col3               SQL_Latin1_General_CP1_CI_AS  
2       SQLCHAR       0       100     ","     2     Col2               SQL_Latin1_General_CP1_CI_AS  
3       SQLCHAR       0       7       ","     1     Col1               ""  
4       SQLCHAR       0       100     "\r\n"  4     Col4               SQL_Latin1_General_CP1_CI_AS  
  
```  
  
> [!NOTE]  
>  Per altre informazioni sul layout dei file di formato non XML, vedere [File in formato non XML &#40;SQL Server&#41;](xml-format-files-sql-server.md).  
  
### <a name="example"></a>Esempio  
 Nell'esempio seguente viene utilizzata un'istruzione `BULK INSERT` per l'importazione bulk dei dati dal file di dati `myTestOrder-c.txt` alla tabella di esempio `myTestOrder` tramite il file di formato non XML `myTestOrder.fmt`.  
  
 Nell'editor di query di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] eseguire:  
  
```  
USE AdventureWorks2012;  
GO  
BULK INSERT myTestOrder  
FROM 'C:\myTestOrder-c.txt'   
WITH (formatfile='C:\myTestOrder.fmt');  
GO  
  
```  
  
## <a name="using-an-xml-format-file"></a>Utilizzo di un file di formato XML  
 Nel seguente file di formato non XML di esempio è illustrato un file di formato, `myTestOrder.xml`, che esegue il mapping tra i campi in `myTestOrder-c.txt` e le colonne della tabella `myTestOrder`. Per informazioni su come creare la tabella e il file di dati, vedere "Tabella e file di dati di esempio", più indietro in questo argomento.  
  
 Il file di formato `myTestOrder.xml` contiene le informazioni seguenti:  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format"   
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>  
  <FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="3" NAME="Col1" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Col2" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="1" NAME="Col3" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="4" NAME="Col4" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
  
```  
  
> [!NOTE]  
>  Per altre informazioni sulla sintassi dell'XML Schema e ulteriori esempi di file di formato XML, vedere [File in formato XML &#40;SQL Server&#41;](xml-format-files-sql-server.md).  
  
### <a name="example"></a>Esempio  
 Nell'esempio seguente viene utilizzato il provider di set di righe con lettura bulk `OPENROWSET` per l'importazione bulk dei dati dal file di dati `myTestOrder-c.txt` alla tabella di esempio `myTestOrder`  tramite il file di formato XML `myTestOrder.xml`. L'istruzione `INSERT... SELECT` specifica l'elenco di colonne nell'elenco di selezione.  
  
 Nell'editor di query di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] eseguire il codice seguente:  
  
```  
USE AdventureWorks2012;  
GO  
INSERT INTO myTestOrder   
  SELECT Col1, Col2, Col3, Col4  
      FROM  OPENROWSET(BULK  'C:\myTestOrder-c.txt',  
      FORMATFILE='C:\myTestOrder.Xml'    
       ) AS t1;  
GO  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo di un file di formato per ignorare una colonna di una tabella &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)   
 [Utilizzo di un file di formato per escludere un campo di dati &#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
  
