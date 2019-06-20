---
title: Usare un file di formato per ignorare una colonna di una tabella (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- skipping columns when importing
- format files [SQL Server], skipping columns
ms.assetid: 30e0e7b9-d131-46c7-90a4-6ccf77e3d4f3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 80c5c5b2f4e6d4f691b7c3977ae2f715f5424e7f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011687"
---
# <a name="use-a-format-file-to-skip-a-table-column-sql-server"></a>Utilizzo di un file di formato per ignorare una colonna di una tabella (SQL Server)
  In questo argomento vengono illustrati i file di formato. È possibile utilizzare un file di formato per evitare di importare la colonna di una tabella quando il campo non esiste nel file di dati. Un file di dati può contenere un numero di campi inferiore rispetto al numero di colonne della tabella solo se le colonne ignorate ammettono valori Null e/o hanno un valore predefinito.  
  
## <a name="sample-table-and-data-file"></a>Tabella e file di dati di esempio  
 Per gli esempi seguenti è necessaria una tabella denominata `myTestSkipCol` nel database di esempio [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] nello schema **dbo** . Per creare la tabella, utilizzare il codice seguente:  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTestSkipCol   
   (  
   Col1 smallint,  
   Col2 nvarchar(50) NULL,  
   Col3 nvarchar(50) not NULL  
   );  
GO  
```  
  
 Negli esempi seguenti viene utilizzato un file di dati di esempio, `myTestSkipCol2.dat`, che contiene solo due campi, mentre la tabella corrispondente contiene tre colonne:  
  
```  
1,DataForColumn3  
1,DataForColumn3  
1,DataForColumn3  
  
```  
  
 Per eseguire l'importazione bulk dei dati da `myTestSkipCol2.dat` nella tabella `myTestSkipCol` , è necessario che il file di formato esegua il mapping tra il primo campo di dati e `Col1`e tra il secondo campo e `Col3`, ignorando `Col2`.  
  
## <a name="using-a-non-xml-format-file"></a>Utilizzo di un file di formato non XML  
 È possibile modificare un file di formato non XML per ignorare una colonna di tabella. In genere, questo richiede l'uso dell'utilità **bcp** per creare un file di formato non XML predefinito e per modificare il file predefinito in un editor di testo. Il file di formato modificato deve eseguire il mapping tra ogni campo esistente e la colonna di tabella corrispondente e indicare quale colonna o quali colonne di tabella ignorare. Esistono due alternative per la modifica di un file di dati non XML predefinito. Entrambi consentono di indicare che il campo dati non esiste nel file di dati e che nella colonna della tabella corrispondente non verrà inserito alcun dato.  
  
### <a name="creating-a-default-non-xml-format-file"></a>Creazione di un file di formato non XML predefinito  
 Questo argomento usa il file di formato non XML predefinito creato per la tabella di esempio `myTestSkipCol` usando il comando **bcp** seguente:  
  
```  
bcp AdventureWorks2012..myTestSkipCol format nul -f myTestSkipCol_Default.fmt -c -T  
```  
  
 Il comando precedente crea un file di formato non XML, `myTestSkipCol_Default.fmt`. Questo file di formato è chiamato *file di formato predefinito* perché è generato da **bcp**. In genere, un file di formato predefinito descrive una corrispondenza uno-a-uno tra i campi del file di dati e le colonne di tabella.  
  
> [!IMPORTANT]  
>  Potrebbe essere necessario specificare il nome dell'istanza del server al quale ci si connette. Potrebbe inoltre essere necessario specificare il nome utente e la password. Per altre informazioni, vedere [bcp Utility](../../tools/bcp-utility.md).  
  
 Nella figura seguente vengono illustrati i valori nei file di formato predefinito di esempio. Nella figura viene inoltre indicato il nome di ogni campo del file di formato.  
  
 ![file di formato non XML predefinito per myTestSkipCol](../../database-engine/media/mytestskipcol-f-c-default-fmt.gif "file di formato non XML predefinito per myTestSkipCol")  
  
> [!NOTE]  
>  Per altre informazioni sui campi dei file di formato, vedere [File in formato non XML &#40;SQL Server&#41;](xml-format-files-sql-server.md).  
  
### <a name="methods-for-modifying-a-non-xml-format-file"></a>Modalità di modifica di un file di formato non XML  
 Per ignorare una colonna di tabella, modificare il file di formato non XML predefinito, utilizzando una delle modalità alternative seguenti:  
  
-   La modalità preferita include tre passaggi principali. Eliminare innanzitutto eventuali righe del file di formato che specifichino un campo non presente nel file di dati. Ridurre quindi il valore "Ordine dei campi nel file host" di ogni riga del file di formato che segue una riga eliminata. L'obiettivo sono i valori sequenziali "Ordine dei campi nel file host", da 1 a *n*, che riflettono l'effettiva posizione di ogni campo nel file di dati. Ridurre infine il valore nel campo "Numero di colonne" in modo da riflettere il numero effettivo di campi nel file di dati.  
  
     L'esempio seguente si basa sul file di formato predefinito per la tabella `myTestSkipCol` , creato in "Creazione di un file di formato non XML predefinito", più indietro in questo argomento. Questo file di formato modificato esegue il mapping tra il primo campo dati e `Col1`, ignora `Col2`ed esegue il mapping tra il secondo campo dati e `Col3`. La riga per `Col2` è stata eliminata. Le altre modifiche sono indicate in grassetto:  
  
    ```  
    9.0  
    2  
    1       SQLCHAR       0       7       "\t"     1     Col1         ""  
    2       SQLCHAR       0       100     "\r\n"   3     Col3         SQL_Latin1_General_CP1_CI_AS  
    ```  
  
-   In alternativa, per ignorare una colonna di tabella, è possibile modificare la definizione della riga del file di formato che corrisponde alla colonna di tabella. In questa riga del file di formato, i valori "lunghezza del prefisso," "lunghezza dei dati del file host" e "ordine delle colonne nel server" devono essere impostati su 0. Inoltre, i campi "terminatore" e "regole di confronto a livello di colonna" devono essere impostati su "" (NULL).  
  
     Il valore "nome della colonna del server" richiede una stringa non vuota, sebbene il nome di colonna effettivo non sia necessario. Per i campi di formato restanti sono necessari i relativi valori predefiniti.  
  
     L'esempio seguente deriva inoltre dal file di formato predefinito per la tabella `myTestSkipCol`. I valori che devono essere 0 o NULL sono indicati in grassetto.  
  
    ```  
    9.0  
    3  
    1       SQLCHAR       0       7       "\t"     1     Col1         ""  
    2       SQLCHAR       00""0     Col2         ""  
    3       SQLCHAR       0       100     "\r\n"   3     Col3         SQL_Latin1_General_CP1_CI_AS  
    ```  
  
### <a name="examples"></a>Esempi  
 Gli esempi seguenti sono inoltre basati sulla tabella di esempio `myTestSkipCol` e sul file di dati di esempio `myTestSkipCol2.dat` creati in "File di dati e tabella di esempio", più indietro in questo argomento.  
  
#### <a name="using-bulk-insert"></a>Utilizzo di BULK INSERT  
 Il funzionamento di questo esempio si basa sull'utilizzo dei file di formato non XML modificati creati in "Modalità di modifica di un file di formato non XML", più indietro in questo argomento. In questo esempio, il file di formato modificato è denominato `C:\myTestSkipCol2.fmt`. Per utilizzare `BULK INSERT` per l'importazione bulk dei file di dati `myTestSkipCol2.dat` , nell'editor di query di [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] eseguire il codice seguente:  
  
```  
USE AdventureWorks2012;  
GO  
BULK INSERT myTestSkipCol   
   FROM 'C:\myTestSkipCol2.dat'   
   WITH (FORMATFILE = 'C:\myTestSkipCol2.fmt');  
GO  
SELECT * FROM myTestSkipCol;  
GO  
```  
  
## <a name="using-an-xml-format-file"></a>Utilizzo di un file di formato XML  
 Con un file di formato XML non è possibile ignorare una colonna quando si sta eseguendo l'importazione diretta in una tabella usando un comando **bcp** o un'istruzione BULK INSERT. È tuttavia possibile importare un'intera tabella a eccezione dell'ultima colonna. Se si desidera ignorare una colonna diversa dall'ultima, è necessario creare una vista della tabella di destinazione che contiene solo le colonne contenute nel file di dati. In seguito sarà possibile eseguire un'importazione bulk dei dati da tale file nella vista.  
  
 Per utilizzare un file di formato XML per ignorare una colonna di una tabella tramite OPENROWSET(BULK...), è necessario specificare un elenco esplicito di colonne nell'elenco selezionato e nella tabella di destinazione, come indicato di seguito:  
  
 INSERT ...<column_list> SELECT <column_list> FROM OPENROWSET(BULK...)  
  
### <a name="creating-a-default-xml-format-file"></a>Creazione di un file di formato XML predefinito  
 Gli esempi dei file di formato modificati sono basati sulla tabella di esempio `myTestSkipCol` e sul file di dati di esempio creati in "File di dati e tabella di esempio", più indietro in questo argomento. Il comando **bcp** seguente crea un file di formato XML predefinito per la tabella `myTestSkipCol` :  
  
```  
bcp AdventureWorks2012..myTestSkipCol format nul -f myTestSkipCol_Default.xml -c -x -T  
```  
  
 Il file di formato non XML predefinito risultante descrive una corrispondenza uno-a-uno tra i campi del file di dati e le colonne di tabella, come segue:  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="\t" MAX_LENGTH="7"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="\t" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="Col1" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Col2" xsi:type="SQLNVARCHAR"/>  
  <COLUMN SOURCE="3" NAME="Col3" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
> [!NOTE]  
>  Per informazioni sulla struttura dei file di formato XML, vedere [File in formato XML &#40;SQL Server&#41;](xml-format-files-sql-server.md).  
  
### <a name="examples"></a>Esempi  
 Gli esempi in questa sezione utilizzano la tabella di esempio `myTestSkipCol` e il file di dati di esempio `myTestSkipCol2.dat` creati in "File di dati e tabella di esempio", più indietro in questo argomento. Per importare i dati da `myTestSkipCol2.dat` nella tabella `myTestSkipCol` , gli esempi utilizzano il file di formato XML modificato seguente, `myTestSkipCol2-x.xml`, basato sul file di formato creato in "Creazione di un file di formato XML predefinito" più indietro in questo argomento.  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="," MAX_LENGTH="7"/>  
  <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="100" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="Col1" xsi:type="SQLSMALLINT"/>  
  <COLUMN SOURCE="2" NAME="Col3" xsi:type="SQLNVARCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
#### <a name="using-openrowsetbulk"></a>Utilizzo di OPENROWSET(BULK...)  
 Nell'esempio seguente viene utilizzato il provider di set di righe con lettura bulk `OPENROWSET` e il file di formato `myTestSkipCol2.xml` . Nell'esempio viene eseguita l'importazione bulk del file di dati `myTestSkipCol2.dat` nella tabella `myTestSkipCol` . L'istruzione contiene un elenco esplicito di colonne nell'elenco selezionato e nella tabella di destinazione, come richiesto.  
  
 Nell'editor di query di [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] eseguire il codice seguente:  
  
```  
USE AdventureWorks2012;  
GO  
INSERT INTO myTestSkipCol  
  (Col1,Col3)  
    SELECT Col1,Col3  
      FROM  OPENROWSET(BULK  'C:\myTestSkipCol2.Dat',  
      FORMATFILE='C:\myTestSkipCol2.Xml'    
       ) as t1 ;  
GO  
```  
  
#### <a name="using-bulk-import-on-a-view"></a>Utilizzo di BULK IMPORT in una vista  
 Nell'esempio seguente viene creata la tabella `v_myTestSkipCol` nella tabella `myTestSkipCol` . Questa vista ignora la seconda colonna della tabella, `Col2`. Nell'esempio viene quindi utilizzato `BULK INSERT` per importare il file di dati `myTestSkipCol2.dat` in questa vista.  
  
 Nell'editor di query di [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] eseguire il codice seguente:  
  
```  
CREATE VIEW v_myTestSkipCol AS  
    SELECT Col1,Col3  
    FROM myTestSkipCol;  
GO  
  
USE AdventureWorks2012;  
GO  
BULK INSERT v_myTestSkipCol  
FROM 'C:\myTestSkipCol2.dat'  
WITH (FORMATFILE='C:\myTestSkipCol2.xml');  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [Utilizzo di un file di formato per ignorare una colonna di una tabella &#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)   
 [Utilizzo di un file di formato per eseguire il mapping tra le colonne della tabella e i campi del file di dati &#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)   
 [Utilizzo di un file di formato per l'importazione bulk dei dati &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)  
  
  
