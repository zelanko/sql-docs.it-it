---
title: Mantenere i valori Identity durante l'importazione bulk dei dati (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- identity values [SQL Server], bulk imports
- data formats [SQL Server], identity values
- bulk importing [SQL Server], identity values
ms.assetid: 45894a3f-2d8a-4edd-9568-afa7d0d3061f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 07f6714f27f60afda91134034509ff439d92f071
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050482"
---
# <a name="keep-identity-values-when-bulk-importing-data-sql-server"></a>Mantenere i valori Identity durante l'importazione bulk dei dati (SQL Server)
  È possibile eseguire l'importazione bulk dei file di dati contenenti valori Identity in un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per impostazione predefinita, i valori per la colonna Identity del file di dati importato vengono ignorati e sostituiti automaticamente da valori univoci assegnati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . I valori univoci si basano sui valori di inizializzazione e incremento specificati durante la creazione della tabella.  
  
 Se il file di dati non contiene valori per la colonna dell'identificatore nella tabella, utilizzare un file di formato per specificare di ignorare la colonna dell'identificatore nella tabella durante l'importazione dei dati. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assegna automaticamente valori univoci per la colonna.  
  
 Per impedire l'assegnazione da parte di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di valori Identity durante l'importazione bulk delle righe di dati in una tabella, utilizzare il qualificatore per il mantenimento dei valori Identity corretto. Quando si specifica un qualificatore per il mantenimento dei valori Identity, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizza i valori Identity nel file di dati. Sono disponibili i qualificatori seguenti:  
  
|Comando|Qualificatore per il mantenimento dei valori Identity|Tipo di qualificatore|  
|-------------|------------------------------|--------------------|  
|`bcp`|**-E**|Opzione|  
|BULK INSERT|KEEPIDENTITY|Argomento|  
|INSERT ... SELECT * FROM OPENROWSET(BULK...).|KEEPIDENTITY|Hint di tabella|  
  
 Per altre informazioni, vedere [Utilità bcp](../../tools/bcp-utility.md), [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql), [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql), [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql), [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql) e [Hint di tabella &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table).  
  
> [!NOTE]  
>  Per creare un numero a incremento automatico da usare in più tabelle o da chiamare dalle applicazioni senza fare riferimento ad alcuna tabella, vedere [Numeri di sequenza](../sequence-numbers/sequence-numbers.md).  
  
## <a name="examples"></a>Esempi  
 Negli esempi di questo argomento viene utilizzata l'importazione bulk dei dati tramite INSERT... Selezionare * FROM OPENROWSET (BULK...) e mantenere i valori predefiniti.  
  
### <a name="sample-table"></a>Tabella di esempio  
 Gli esempi di importazione in blocco richiedono la creazione di una tabella denominata **myTestKeepNulls** nel database di esempio **AdventureWorks** nello schema **dbo**. Per creare la tabella seguente. nell'editor di query di [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] eseguire:  
  
```  
USE AdventureWorks;  
GO  
SELECT * INTO HumanResources.myDepartment   
   FROM HumanResources.Department  
      WHERE 1=0;  
GO  
SELECT * FROM HumanResources.myDepartment;  
```  
  
 L'istruzione IDENTITY_INSERT nella tabella **Department** su cui si basa `myDepartment` è impostata su OFF. Pertanto, per importare i dati in una colonna Identity, è necessario specificare KEEPIDENTITY oppure **-E**.  
  
### <a name="sample-data-file"></a>File di dati di esempio  
 Nel file di dati utilizzato negli esempi di importazione bulk sono inclusi i dati esportati dalla tabella `HumanResources.Department` nel formato nativo. Per creare il file di dati, al prompt dei comandi di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows digitare:  
  
```  
bcp AdventureWorks.HumanResources.Department out myDepartment-n.Dat -n -T  
```  
  
### <a name="sample-format-file"></a>File di formato di esempio  
 In questi esempi di importazione bulk viene impiegato un file di formato XML, `myDepartment-f-x-n.Xml`, che utilizza formati nativi. Negli esempi viene utilizzato `bcp` per creare il file di formato dalla tabella `HumanResources.Department` del database `AdventureWorks`. Al prompt dei comandi di Windows digitare:  
  
```  
bcp AdventureWorks.HumanResources.Department format nul -n -x -f myDepartment-f-n-x.Xml -T  
```  
  
 Per altre informazioni sulla creazione di un file di formato, vedere [Creazione di un file di formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md).  
  
### <a name="a-using-bcp-and-keeping-identity-values"></a>R. Utilizzo di bcp mantenendo i valori Identity  
 Nell'esempio seguente viene illustrato come mantenere i valori Identity quando si utilizza `bcp` per l'importazione bulk dei dati. Il comando `bcp` utilizza il file di formato `myDepartment-f-n-x.Xml` e include le opzioni seguenti:  
  
|Qualificatori|Descrizione|  
|----------------|-----------------|  
|**-E**|Specifica che il valore o i valori Identity inclusi nel file di dati devono essere utilizzati per la colonna Identity.|  
|**-T**|Specifica che l' `bcp` utilità si connette a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con una connessione trusted.|  
  
 Al prompt dei comandi di Windows digitare:  
  
```  
bcp AdventureWorks.HumanResources.myDepartment in C:\myDepartment-n.Dat -f C:\myDepartment-f-n-x.Xml -E -T  
  
```  
  
### <a name="b-using-bulk-insert-and-keeping-identity-values"></a>B. Utilizzo di BULK INSERT mantenendo i valori Identity  
 Nell'esempio seguente viene utilizzato BULK INSERT per l'importazione bulk dei dati dal file `myDepartment-c.Dat` nella tabella `AdventureWorks.HumanResources.myDepartment` . L'istruzione utilizza il file di formato `myDepartment-f-n-x.Xml` e include l'opzione KEEPIDENTITY per garantire che i valori Identity vengano mantenuti nel file di dati.  
  
 Nell'editor di query di [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] eseguire:  
  
```  
USE AdventureWorks;  
GO  
DELETE HumanResources.myDepartment;  
GO  
BULK INSERT HumanResources.myDepartment  
   FROM 'C:\myDepartment-n.Dat'  
   WITH (  
      KEEPIDENTITY,  
      FORMATFILE='C:\myDepartment-f-n-x.Xml'  
   );  
GO  
SELECT * FROM HumanResources.myDepartment;  
  
```  
  
### <a name="c-using-openrowset-and-keeping-identity-values"></a>C. Utilizzo di OPENROWSET mantenendo i valori Identity  
 Nell'esempio seguente viene utilizzato il provider di set di righe con lettura bulk OPENROWSET per l'importazione bulk dei dati dal file `myDepartment-c.Dat` nella tabella `AdventureWorks.HumanResources.myDepartment` . L'istruzione utilizza il file di formato `myDepartment-f-n-x.Xml` e include l'hint KEEPIDENTITY per garantire che i valori Identity vengano mantenuti nel file di dati.  
  
 Nell'editor di query di [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] eseguire:  
  
```  
USE AdventureWorks;  
GO  
DELETE HumanResources.myDepartment;  
GO  
  
INSERT INTO HumanResources.myDepartment  
   with (KEEPIDENTITY)  
   (DepartmentID, Name, GroupName, ModifiedDate)  
   SELECT *  
      FROM  OPENROWSET(BULK 'C:\myDepartment-n.Dat',  
      FORMATFILE='C:\myDepartment-f-n-x.Xml') as t1;  
GO  
  
```  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Attività correlate  
  
-   [Mantenimento dei valori Null o uso dei valori predefiniti durante un'importazione bulk &#40;SQL Server&#41;](keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [Preparare i dati per l'importazione o l'esportazione in blocco &#40;SQL Server&#41;](prepare-data-for-bulk-export-or-import-sql-server.md)  
  
 **Per utilizzare un file di formato**  
  
-   [Creazione di un file di formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md)  
  
-   [Usare un file di formato per l'importazione in blocco dei dati &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Utilizzo di un file di formato per eseguire il mapping tra le colonne della tabella e i campi del file di dati &#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
-   [Utilizzo di un file di formato per escludere un campo di dati &#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [Utilizzo di un file di formato per ignorare una colonna di una tabella &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
 **Per utilizzare formati di dati per l'importazione o l'esportazione bulk**  
  
-   [Importare dati in formato nativo e carattere da versioni precedenti di SQL Server](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [Utilizzo del formato carattere per l'importazione o l'esportazione di dati &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usare il formato nativo per importare o esportare dati &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Utilizzo del formato carattere Unicode per l'importazione o l'esportazione di dati &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usare il formato Unicode nativo per importare o esportare dati &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
 **Per specificare i formati di dati per la compatibilità mediante bcp**  
  
1.  [Impostazione dei caratteri di terminazione del campo e della riga &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)  
  
2.  [Specificare la lunghezza del prefisso nei file di dati con bcp &#40;SQL Server&#41;](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
3.  [Specifica del tipo di archiviazione di file tramite bcp &#40;SQL Server&#41;](specify-file-storage-type-by-using-bcp-sql-server.md)  
  
## <a name="see-also"></a>Vedere anche  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [Utilità bcp](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [Hint di tabella &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)  
  
  
