---
title: Usare il formato carattere Unicode per importare o esportare dati (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- data formats [SQL Server], Unicode character
- Unicode [SQL Server], bulk importing and exporting
ms.assetid: 74342a11-c1c0-4746-b482-7f3537744a70
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 34e8f4a5b49c9e023c224e62c23326864ef26f65
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011645"
---
# <a name="use-unicode-character-format-to-import-or-export-data-sql-server"></a>Utilizzo del formato carattere Unicode per l'importazione o l'esportazione di dati (SQL Server)
  È consigliabile utilizzare il formato carattere Unicode per il trasferimento bulk di dati tra più istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite un file di dati contenente caratteri estesi o DBCS. Questo formato di dati consente di trasferire i dati da un server utilizzando una tabella codici diversa da quella del client che esegue l'operazione. In questi casi, l'utilizzo del formato di dati carattere Unicode offre i vantaggi seguenti:  
  
-   Se i dati di origine e di destinazione sono di tipo Unicode, il formato carattere Unicode consente di mantenere tutti i dati di tipo carattere.  
  
-   Se i dati di origine e di destinazione non sono di tipo Unicode, il formato carattere Unicode consente di ridurre al minimo la perdita dei caratteri estesi nei dati di origine che non possono essere rappresentati nella destinazione.  
  
 Per i file in formato carattere Unicode vengono rispettate le convenzioni dei file Unicode. I primi due byte del file sono rappresentati da numeri esadecimali, 0xFFFE. Tali byte hanno la funzione di indicatori per l'ordine dei byte e specificano se archiviare il byte più significativo come primo o ultimo byte del file.  
  
> [!IMPORTANT]  
>  Affinché un file di formato sia funzionante con un file di dati di formato carattere Unicode, è necessario che tutti i campi di input siano stringhe di testo Unicode, ovvero stringhe Unicode di dimensioni fisse o che terminano con un carattere.  
  
 I dati `sql_variant` archiviati in un file in formato carattere Unicode funzionano allo stesso modo di quelli archiviati in un file in formato carattere, con la differenza che vengono archiviati come dati `nchar` anziché `char`. Per altre informazioni sul formato carattere, vedere [Regole di confronto e supporto Unicode](../collations/collation-and-unicode-support.md).  
  
 Per usare un carattere di terminazione del campo o della riga diverso da quello predefinito del formato carattere Unicode, vedere [Specificare caratteri di terminazione del campo e della riga &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md).  
  
## <a name="command-options-for-unicode-character-format"></a>Opzioni di comando per il formato carattere Unicode  
 È possibile importare dati in formato carattere Unicode in una tabella usando **bcp**, BULK INSERT o INSERT... SELECT \* FROM OPENROWSET(BULK...). Per un comando **bcp** o un'istruzione BULK INSERT, è possibile specificare il formato dati nella riga di comando. Per un'istruzione INSERT ... SELECT * FROM OPENROWSET(BULK...) è necessario specificare il formato dei dati in un file di formato.  
  
 Il formato carattere Unicode è supportato dalle opzioni della riga di comando riportate di seguito:  
  
|Comando|Opzione|Descrizione|  
|-------------|------------|-----------------|  
|**bcp**|**-w**|Utilizza il formato carattere Unicode.|  
|BULK INSERT|DATAFILETYPE **='** widechar **'**|Utilizza il formato carattere Unicode durante l'importazione bulk di dati.|  
  
 Per altre informazioni, vedere [Utilità bcp](../../tools/bcp-utility.md), [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql) o [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql).  
  
> [!NOTE]  
>  In alternativa, è possibile definire la formattazione di ogni singolo campo in un file di formato. Per altre informazioni, vedere [File di formato per l'importazione o l'esportazione di dati &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md).  
  
## <a name="examples"></a>Esempi  
 Gli esempi seguenti illustrano come eseguire l'esportazione in blocco di dati di tipo carattere Unicode con **bcp** e l'importazione in blocco degli stessi dati con BULK INSERT.  
  
### <a name="sample-table"></a>Tabella di esempio  
 Gli esempi richiedono che nel database di esempio [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] venga creata una tabella denominata `myTestUniCharData` in base allo schema `dbo`. Prima di eseguire le procedure illustrate negli esempi, è necessario creare la tabella. Per creare la tabella, nell'editor di query di [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] eseguire:  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTestUniCharData (  
   Col1 smallint,  
   Col2 nvarchar(50),  
   Col3 nvarchar(50)  
   );   
```  
  
 Per popolare la tabella e visualizzare il contenuto risultante, eseguire le istruzioni seguenti:  
  
```  
INSERT INTO myTestUniCharData(Col1,Col2,Col3)  
   VALUES(1,'DataField2','DataField3')   
        ,(2,'DataField2','DataField3');  
GO  
SELECT Col1,Col2,Col3 FROM myTestUniCharData;  
  
```  
  
### <a name="using-bcp-to-bulk-export-unicode-character-data"></a>Utilizzo di bcp per l'esportazione bulk di dati in formato carattere Unicode  
 Per esportare i dati dalla tabella al file di dati, usare **bcp** con l'opzione **out** e i qualificatori seguenti:  
  
|Qualificatori|Descrizione|  
|----------------|-----------------|  
|**-w**|Specifica il formato carattere Unicode.|  
|**-t** `,`|Specifica la virgola (`,`) come carattere di terminazione del campo.<br /><br /> Nota: Il valore predefinito è il carattere di tabulazione Unicode (\t). Per altre informazioni, vedere [Impostazione dei caratteri di terminazione del campo e della riga &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md).|  
|**-T**|Specifica che l'utilità **bcp** si connette a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con una connessione trusted che usa la sicurezza integrata. Se non si specifica **-T**, è necessario specificare **-U** e **-P** per eseguire correttamente l'accesso.|  
  
 Nell'esempio seguente viene eseguita l'esportazione bulk di dati in formato carattere Unicode dalla tabella `myTestUniCharData` in un nuovo file di dati denominato `myTestUniCharData-w.Dat` che utilizza la virgola (`,`) come carattere di terminazione del campo. Al prompt dei comandi di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows digitare:  
  
```  
bcp AdventureWorks2012..myTestUniCharData out C:\myTestUniCharData-w.Dat -w -t, -T  
  
```  
  
### <a name="using-bulk-insert-to-bulk-import-unicode-character-data"></a>Utilizzo di BULK INSERT per l'importazione bulk di dati in formato carattere Unicode  
 Nell'esempio seguente viene utilizzata l'istruzione `BULK INSERT` per importare i dati del file di dati `myTestUniCharData-w.Dat` nella tabella `myTestUniCharData`. Nell'istruzione è necessario dichiarare il carattere di terminazione del campo non predefinito (`,`). Nell'editor di query di [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] eseguire:  
  
```  
USE AdventureWorks2012;  
GO  
BULK INSERT myTestUniCharData   
   FROM 'C:\myTestUniCharData-w.Dat'   
   WITH (  
      DATAFILETYPE='widechar',  
      FIELDTERMINATOR=','  
   );   
GO  
SELECT Col1,Col2,Col3 FROM myTestUniCharData;  
GO  
  
```  
  
##  <a name="RelatedTasks"></a> Attività correlate  
 **Per utilizzare formati di dati per l'importazione o l'esportazione bulk**  
  
-   [Importare dati in formato nativo e carattere da versioni precedenti di SQL Server](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [Utilizzo del formato carattere per l'importazione o l'esportazione di dati &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usare il formato nativo per importare o esportare dati &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usare il formato Unicode nativo per importare o esportare dati &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>Vedere anche  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [Tipi di dati &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [Regole di confronto e supporto Unicode](../collations/collation-and-unicode-support.md)  
  
  
