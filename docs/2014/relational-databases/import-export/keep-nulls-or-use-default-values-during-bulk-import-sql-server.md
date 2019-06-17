---
title: Mantenere i valori Null o usare i valori predefiniti durante un'importazione bulk (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk importing [SQL Server], null values
- bulk importing [SQL Server], default values
- data formats [SQL Server], null values
- bulk rowset providers [SQL Server]
- bcp utility [SQL Server], null values
- BULK INSERT statement
- default values
- OPENROWSET function, bulk importing
- data formats [SQL Server], default values
ms.assetid: 6b91d762-337b-4345-a159-88abb3e64a81
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5999a7f3a952cd0392136a96bf3bf166c8e6b155
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011899"
---
# <a name="keep-nulls-or-use-default-values-during-bulk-import-sql-server"></a>Mantenimento dei valori Null o utilizzo dei valori predefiniti durante un'importazione bulk (SQL Server)
  Per impostazione predefinita, durante l'importazione di dati in una tabella il comando **bcp** e l'istruzione BULK INSERT osservano gli eventuali valori predefiniti che sono stati definiti per le colonne della tabella. Ad esempio, se un file di dati contiene un campo Null, verrà caricato nel campo il valore predefinito della colonna. Il comando **bcp** e l'istruzione BULK INSERT consentono entrambi di specificare che dovranno essere mantenuti i valori Null.  
  
 Un'istruzione INSERT regolare mantiene invece il valore Null anziché inserire un valore predefinito. L'istruzione INSERT ... SELECT * FROM OPENROWSET(BULK...) funziona in modo analogo a un'istruzione INSERT regolare, ma supporta inoltre un hint di tabella per l'inserimento di valori predefiniti.  
  
> [!NOTE]  
>  Per i file di formato di esempio che ignorano una colonna di tabella, vedere [Usare un file di formato per ignorare una colonna di una tabella &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md).  
  
## <a name="sample-table-and-data-file"></a>Tabella e file di dati di esempio  
 Per eseguire gli esempi riportati in questo argomento, è necessario creare una tabella e un file di dati di esempio.  
  
### <a name="sample-table"></a>Tabella di esempio  
 Gli esempi richiedono la creazione di una tabella denominata **MyTestDefaultCol2** nel database di esempio **AdventureWorks** nello schema **dbo**. Per creare la tabella, nell'editor di query di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] eseguire:  
  
```  
USE AdventureWorks;  
GO  
CREATE TABLE MyTestDefaultCol2   
(Col1 smallint,  
Col2 nvarchar(50) DEFAULT 'Default value of Col2',  
Col3 nvarchar(50)   
);  
GO  
  
```  
  
 Si noti che la seconda colonna della tabella, `Col2`, ha un valore predefinito.  
  
### <a name="sample-format-file"></a>File di formato di esempio  
 In alcuni degli esempi di importazione bulk viene utilizzato un file di formato non XML, `MyTestDefaultCol2-f-c.Fmt` che corrisponde esattamente alla tabella `MyTestDefaultCol2`. Per creare questo file di formato, al prompt dei comandi di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows digitare:  
  
```  
bcp AdventureWorks..MyTestDefaultCol2 format nul -c -f C:\MyTestDefaultCol2-f-c.Fmt -t, -r\n -T  
  
```  
  
 Per informazioni sulla creazione di file di formato, vedere [Creare un file di formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md).  
  
### <a name="sample-data-file"></a>File di dati di esempio  
 Nell'esempio viene utilizzato un file di dati di esempio, `MyTestEmptyField2-c.Dat`, che non contiene alcun valore nel secondo campo. Il file di dati `MyTestEmptyField2-c.Dat` contiene i record seguenti:  
  
```  
1,,DataField3  
2,,DataField3  
  
```  
  
## <a name="keeping-null-values-with-bcp-or-bulk-insert"></a>Mantenimento dei valori Null con bcp o BULK INSERT  
 I qualificatori seguenti specificano che un campo vuoto del file di dati mantiene il relativo valore Null durante l'importazione bulk anziché ereditare un valore predefinito (se disponibile) per le colonne della tabella.  
  
|Comando|Qualifier|Tipo di qualificatore|  
|-------------|---------------|--------------------|  
|**bcp**|`-k`|Opzione|  
|BULK INSERT|KEEPNULLS<sup>1</sup>|Argomento|  
  
 <sup>1</sup> per BULK INSERT, se i valori predefiniti non sono disponibili, la colonna della tabella deve essere definita per consentire valori null.  
  
> [!NOTE]  
>  Questi qualificatori disabilitano il controllo delle definizioni DEFAULT di una tabella mediante i comandi per l'importazione bulk. Per le istruzioni INSERT simultanee, le definizioni DEFAULT sono tuttavia previste.  
  
 Per altre informazioni, vedere [Utilità bcp](../../tools/bcp-utility.md) e [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql).  
  
### <a name="examples"></a>Esempi  
 Gli esempi in questa sezione eseguono l'importazione in blocco con **bcp** o BULK INSERT e mantengono i valori Null.  
  
 La seconda colonna della tabella, **Col2**, ha un valore predefinito. Il campo corrispondente del file di dati contiene una stringa vuota. Per impostazione predefinita, se si usa **bcp** o BULK INSERT per importare i dati di questo file di dati nella tabella **MyTestDefaultCol2**, viene inserito il valore predefinito di **Col2** e viene generato il risultato seguente:  
  
||||  
|-|-|-|  
|`1`|`Default value of Col2`|`DataField3`|  
|`2`|`Default value of Col2`|`DataField3`|  
  
 Per inserire "`NULL`"invece di"`Default value of Col2`", è necessario utilizzare il `-k` commutatore o keepnull, come illustrato nell'esempio seguente **bcp** ed esempi di BULK INSERT.  
  
#### <a name="using-bcp-and-keeping-null-values"></a>Utilizzo di bcp e mantenimento dei valori Null  
 L'esempio seguente mostra come mantenere i valori Null in un comando **bcp**. Il comando **bcp** contiene le opzioni seguenti:  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|`-f`|Specifica che il comando utilizza un file di formato.|  
|`-k`|Specifica che durante l'operazione il valore delle colonne vuote deve essere Null, ovvero che non verranno inseriti valori predefiniti in tali colonne.|  
|`-T`|Specifica che l'utilità bcp si connette a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite una connessione trusted.|  
  
 Al prompt dei comandi di Windows digitare:  
  
```  
bcp AdventureWorks..MyTestDefaultCol2 in C:\MyTestEmptyField2-c.Dat -f C:\MyTestDefaultCol2-f-c.Fmt -k -T  
  
```  
  
#### <a name="using-bulk-insert-and-keeping-null-values"></a>Utilizzo di BULK INSERT e mantenimento dei valori Null  
 Nell'esempio seguente viene illustrato come utilizzare l'opzione KEEPNULLS in un'istruzione BULK INSERT. Da uno strumento per le query, come l'editor di query di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], eseguire:  
  
```  
USE AdventureWorks;  
GO  
BULK INSERT MyTestDefaultCol2  
   FROM 'C:\MyTestEmptyField2-c.Dat'  
   WITH (  
      DATAFILETYPE = 'char',  
      FIELDTERMINATOR = ',',  
      KEEPNULLS  
   );  
GO  
  
```  
  
## <a name="keeping-default-values-with-insert--select--from-openrowsetbulk"></a>Mantenimento dei valori predefiniti con INSERT ... SELECT * FROM OPENROWSET(BULK...).  
 Per impostazione predefinita, le colonne che non sono specificate nell'operazione di importazione bulk vengono impostate su NULL da INSERT ... SELECT * FROM OPENROWSET(BULK...). È tuttavia possibile specificare che la colonna della tabella corrispondente a un campo vuoto del file di dati utilizzerà il relativo valore predefinito (se disponibile). Per utilizzare i valori predefiniti, specificare l'hint di tabella seguente:  
  
|Comando|Qualifier|Tipo di qualificatore|  
|-------------|---------------|--------------------|  
|INSERT ... SELECT * FROM OPENROWSET(BULK...).|WITH(KEEPDEFAULTS)|Hint di tabella|  
  
> [!NOTE]  
>  Per altre informazioni, vedere [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql), [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql), [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql) e [Hint di tabella &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)  
  
### <a name="examples"></a>Esempi  
 L'esempio seguente relativo a INSERT ... SELECT * FROM OPENROWSET(BULK...) esegue l'importazione bulk di dati e mantiene i valori predefiniti.  
  
 Per eseguire gli esempi, è necessario creare la tabella di esempio **MyTestDefaultCol2**, il file di dati `MyTestEmptyField2-c.Dat` e usare un file di formato, `MyTestDefaultCol2-f-c.Fmt`. Per informazioni sulla creazione di questi esempi, vedere la sezione relativa alla tabella e file di dati di esempio più indietro in questo argomento.  
  
 La seconda colonna della tabella, **Col2**, ha un valore predefinito. Il campo corrispondente del file di dati contiene una stringa vuota. Quando l'istruzione INSERT ... SELECT \* FROM OPENROWSET(BULK...) importa i campi del file di dati nella tabella **MyTestDefaultCol2**, per impostazione predefinita in **Col2** viene inserito NULL invece del valore predefinito. Questo comportamento predefinito genera il risultato seguente:  
  
||||  
|-|-|-|  
|`1`|`NULL`|`DataField3`|  
|`2`|`NULL`|`DataField3`|  
  
 Per inserire il valore predefinito "`Default value of Col2`" anziché "`NULL`", è necessario utilizzare l'hint di tabella KEEPDEFAULTS, come è illustrato nell'esempio seguente. Da uno strumento per le query, come l'editor di query di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], eseguire:  
  
```  
USE AdventureWorks;  
GO  
INSERT INTO MyTestDefaultCol2  
    WITH (KEEPDEFAULTS)  
    SELECT *  
      FROM OPENROWSET(BULK  'C:\MyTestEmptyField2-c.Dat',  
      FORMATFILE='C:\MyTestDefaultCol2-f-c.Fmt'       
      ) as t1 ;  
GO  
  
```  
  
##  <a name="RelatedTasks"></a> Attività correlate  
  
-   [Mantenere i valori Identity durante l'importazione in blocco dei dati &#40;SQL Server&#41;](keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [Preparare i dati per l'importazione o l'esportazione in blocco &#40;SQL Server&#41;](prepare-data-for-bulk-export-or-import-sql-server.md)  
  
 **Per utilizzare un file di formato**  
  
-   [Creare un file di formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md)  
  
-   [Usare un file di formato per l'importazione in blocco dei dati &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Usare un file di formato per eseguire il mapping tra le colonne della tabella e i campi del file di dati &#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
-   [Usare un file di formato per escludere un campo di dati &#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [Usare un file di formato per ignorare una colonna di una tabella &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
 **Per utilizzare formati di dati per l'importazione o l'esportazione bulk**  
  
-   [Importare dati in formato nativo e carattere da versioni precedenti di SQL Server](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [Utilizzo del formato carattere per l'importazione o l'esportazione di dati &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Utilizzo del formato nativo per importare o esportare dati &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Utilizzo del formato carattere Unicode per l'importazione o l'esportazione di dati &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usare il formato Unicode nativo per importare o esportare dati &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
 **Per specificare i formati di dati per la compatibilità mediante bcp**  
  
-   [Specificare caratteri di terminazione del campo e della riga &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)  
  
-   [Specificare la lunghezza del prefisso nei file di dati con bcp &#40;SQL Server&#41;](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
-   [Specificare il tipo di archiviazione di file con bcp &#40;SQL Server&#41;](specify-file-storage-type-by-using-bcp-sql-server.md)  
  
## <a name="see-also"></a>Vedere anche  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [Utilità bcp](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [Hint di tabella &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)  
  
  
