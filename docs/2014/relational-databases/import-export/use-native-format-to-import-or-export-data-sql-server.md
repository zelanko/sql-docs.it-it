---
title: Usare il formato nativo per importare o esportare dati (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- native data format [SQL Server]
- data formats [SQL Server], native
ms.assetid: eb279b2f-0f1f-428f-9b8f-2a7fc495b79f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2dee0f6a337cab7713862e662e06bb94a0b34a5d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63065751"
---
# <a name="use-native-format-to-import-or-export-data-sql-server"></a>Utilizzo del formato nativo per importare o esportare dati (SQL Server)
  L'utilizzo del formato nativo è consigliabile per il trasferimento bulk dei dati tra più istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante un file di dati in cui non sono inclusi caratteri estesi o DBCS (Double Byte Character Set).  
  
> [!NOTE]  
>  Per il trasferimento bulk di dati tra più istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante un file di dati contenente caratteri estesi o DBCS, è consigliabile utilizzare il formato nativo Unicode. Per altre informazioni, vedere [Usare il formato Unicode nativo per importare o esportare dati &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md).  
  
 Il formato nativo mantiene i tipi di dati nativi di un database e viene utilizzato per il trasferimento dei dati ad alta velocità tra le tabelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se si utilizza un file di formato, non è necessario che le tabelle di origine e di destinazione siano identiche. Il trasferimento dei dati è costituito da due passaggi:  
  
1.  Esportazione bulk dei dati da una tabella di origine in un file di dati  
  
2.  Importazione bulk dei dati dal file di dati nella tabella di destinazione  
  
 L'utilizzo del formato nativo tra tabelle identiche consente di evitare la conversione di tipi di dati nel/dal formato carattere, risparmiando tempo e spazio. Per raggiungere la velocità di trasferimento ottimale, tuttavia, vengono eseguiti solo alcuni controlli relativi alla formattazione dei dati. Per evitare problemi relativi ai dati caricati, vedere l'elenco di restrizioni seguente.  
  
## <a name="restrictions"></a>Restrictions  
 Per importare correttamente i dati in formato nativo, verificare quanto segue:  
  
-   Il file di dati deve essere in formato nativo.  
  
-   È necessario che la tabella di destinazione sia compatibile con il file di dati (deve includere il numero di colonne, il tipo di dati e la lunghezza corretti, lo stato NULL e così via). In alternativa, è necessario utilizzare un file di formato per eseguire il mapping tra ogni campo e le colonne corrispondenti.  
  
    > [!NOTE]  
    >  Se si importano i dati da un file non corrispondente alla tabella di destinazione, è possibile che l'operazione di importazione riesca ma i dati della tabella di destinazione potrebbero non essere corretti. Ciò è dovuto al fatto che i dati del file vengono interpretati utilizzando il formato della tabella di destinazione. Pertanto, la mancata corrispondenza causa l'inserimento di valori non corretti ma in nessun caso può determinare inconsistenze di tipo logico o fisico nel database.  
  
     Per altre informazioni sull'uso dei file di formato, vedere [File di formato per l'importazione o l'esportazione di dati &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md).  
  
 Un'importazione corretta non danneggerà la tabella di destinazione.  
  
## <a name="how-bcp-handles-data-in-native-format"></a>Gestione dei dati in formato nativo mediante l'utilità bcp  
 In questa sezione sono contenute considerazioni particolari sull'importazione e sull'esportazione dei dati in formato nativo mediante l'utilità **bcp**.  
  
-   Dati non di tipo carattere  
  
     L'utilità bcp utilizza il formato di dati binario interno di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per trasferire dati non di tipo carattere da una tabella in un file di dati.  
  
-   Dati `char` o `varchar`  
  
     All'inizio della ognuno `char` oppure `varchar` campo **bcp** aggiunge la lunghezza del prefisso.  
  
    > [!IMPORTANT]  
    >  Per impostazione predefinita, quando si utilizza la modalità nativa, l'utilità **bcp** converte i caratteri di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in caratteri OEM prima di copiarli in un file di dati. L'utilità **bcp** converte i caratteri di un file di dati in caratteri ANSI prima dell'importazione bulk in una tabella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Durante queste conversioni può verificarsi la perdita dei dati con caratteri estesi. Per i caratteri estesi, è necessario utilizzare il formato nativo Unicode o specificare una tabella codici.  
  
-   Dati `sql_variant`  
  
     Se i dati `sql_variant` vengono archiviati come SQLVARIANT in un file di dati in formato nativo, verranno mantenute tutte le relative caratteristiche. I metadati che registrano il tipo di dati di ogni valore vengono archiviati insieme al valore stesso. Questi metadati vengono utilizzati per creare di nuovo il valore con lo stesso tipo di dati in una colonna di destinazione `sql_variant`.  
  
     Se il tipo di dati della colonna di destinazione è diverso da `sql_variant`, ogni valore viene convertito nel tipo di dati della colonna di destinazione, in base alle regole standard di conversione implicita dei dati. Se si verifica un errore durante la conversione dei dati, viene eseguito il rollback del batch corrente. Per i valori `char` e `varchar` trasferiti tra colonne `sql_variant` possono verificarsi problemi relativi alla conversione di tabelle codici.  
  
     Per altre informazioni sulla conversione dei dati, vedere [Conversione del tipo di dati &#40;Motore di database&#41;](/sql/t-sql/data-types/data-type-conversion-database-engine).  
  
## <a name="command-options-for-native-format"></a>Opzioni di comando per il formato nativo  
 È possibile importare i dati in formato nativo in una tabella con il comando **bcp**, l'istruzione BULK INSERT o l'istruzione INSERT ... SELECT \* FROM OPENROWSET(BULK...). Per un comando **bcp** o un'istruzione BULK INSERT, è possibile specificare il formato dati nella riga di comando. Per un'istruzione INSERT ... SELECT * FROM OPENROWSET(BULK...) è necessario specificare il formato dei dati in un file di formato.  
  
 Il formato nativo viene supportato dalle opzioni della riga di comando seguenti:  
  
|Comando|Opzione|Descrizione|  
|-------------|------------|-----------------|  
|**bcp**|**-n**|Fa sì che il **bcp** usare i tipi di dati nativi dei dati dell'utilità.<sup> 1</sup>|  
|BULK INSERT|DATAFILETYPE **='** native **'**|Utilizza i tipi di dati nativi o nativi estesi. Si noti che DATAFILETYPE non è necessario se i tipi di dati vengono specificati in un file di formato.|  
  
 <sup>1</sup> caricare nativi (**- n**) dei dati in un formato compatibile con le versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] client, utilizzare il **-V** passare. Per altre informazioni, vedere [Importare dati in formato nativo e carattere da versioni precedenti di SQL Server](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md).  
  
 Per altre informazioni, vedere [Utilità bcp](../../tools/bcp-utility.md), [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql) o [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql).  
  
> [!NOTE]  
>  In alternativa, è possibile definire la formattazione di ogni singolo campo in un file di formato. Per altre informazioni, vedere [File di formato per l'importazione o l'esportazione di dati &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md).  
  
## <a name="examples"></a>Esempi  
 Gli esempi seguenti mostrano come eseguire l'esportazione in blocco di dati nativi usando **bcp** e l'importazione in blocco degli stessi dati usando BULK INSERT.  
  
### <a name="sample-table"></a>Tabella di esempio  
 È necessario creare innanzitutto una tabella denominata **myTestNativeData** nel database di esempio **AdventureWorks** all'interno dello schema **dbo**. Prima di eseguire le procedure illustrate negli esempi, è necessario creare la tabella. Nell'editor di query di [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] eseguire:  
  
```  
USE AdventureWorks;  
GO  
CREATE TABLE myTestNativeData (  
   Col1 smallint,  
   Col2 nvarchar(50),  
   Col3 nvarchar(50)  
   );   
```  
  
 Per popolare la tabella e visualizzare il contenuto risultante, eseguire le istruzioni seguenti:  
  
```  
INSERT INTO myTestNativeData(Col1,Col2,Col3)  
   VALUES(1,'DataField2','DataField3');  
INSERT INTO myTestNativeData(Col1,Col2,Col3)  
   VALUES(2,'DataField2','DataField3');  
GO  
SELECT Col1,Col2,Col3 FROM myTestNativeData  
  
```  
  
### <a name="using-bcp-to-bulk-export-native-data"></a>Utilizzo del comando bcp per l'esportazione bulk di dati nativi  
 Per esportare i dati dalla tabella al file di dati, usare **bcp** con l'opzione **out** e i qualificatori seguenti:  
  
|Qualificatori|Descrizione|  
|----------------|-----------------|  
|**-n**|Specifica i tipi di dati nativi.|  
|**-T**|Specifica che l'utilità **bcp** si connette a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con una connessione trusted che usa la sicurezza integrata. Se non si specifica **-T** , è necessario specificare **-U** e **-P** per eseguire correttamente l'accesso.|  
  
 Nel seguente esempio viene eseguita l'esportazione bulk dei dati in formato nativo dalla tabella `myTestNativeData` in un nuovo file di dati denominato `myTestNativeData-n.Dat`. Al prompt dei comandi di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows digitare:  
  
```  
bcp AdventureWorks..myTestNativeData out C:\myTestNativeData-n.Dat -n -T  
  
```  
  
### <a name="using-bulk-insert-to-bulk-import-native-data"></a>Utilizzo dell'istruzione BULK INSERT per l'importazione bulk di dati nativi  
 Nell'esempio seguente si utilizza BULK INSERT per importare i dati dal file di dati `myTestNativeData-n.Dat` nella tabella `myTestNativeData`. Nell'editor di query di [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] eseguire:  
  
```  
USE AdventureWorks;  
GO  
BULK INSERT myTestNativeData   
    FROM 'C:\myTestNativeData-n.Dat'   
   WITH (DATAFILETYPE='native');   
GO  
SELECT Col1,Col2,Col3 FROM myTestNativeData  
GO  
  
```  
  
##  <a name="RelatedTasks"></a> Attività correlate  
 **Per utilizzare formati di dati per l'importazione o l'esportazione bulk**  
  
-   [Importare dati in formato nativo e carattere da versioni precedenti di SQL Server](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [Utilizzo del formato carattere per l'importazione o l'esportazione di dati &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Utilizzo del formato carattere Unicode per l'importazione o l'esportazione di dati &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usare il formato Unicode nativo per importare o esportare dati &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>Vedere anche  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [Tipi di dati &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [sql_variant &#40;Transact-SQL&#41;](/sql/t-sql/data-types/sql-variant-transact-sql)   
 [Importare dati in formato nativo e carattere da versioni precedenti di SQL Server](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [Usare il formato Unicode nativo per importare o esportare dati &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
  
