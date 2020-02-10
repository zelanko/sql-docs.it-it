---
title: Specificare la lunghezza del campo tramite bcp (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- native data format [SQL Server]
- default field lengths
- field length [SQL Server]
- data formats [SQL Server], field length
- bcp utility [SQL Server], field length
ms.assetid: 240f33ca-ef4a-413a-a4de-831885cb505b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: abb451611f7e102e9167561ef2c3a4b64e00fb12
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66011835"
---
# <a name="specify-field-length-by-using-bcp-sql-server"></a>Definizione della lunghezza di campo tramite bcp (SQL Server)
  La lunghezza del campo indica il numero massimo di caratteri necessari per rappresentare i dati in formato carattere. Se i dati sono archiviati in formato nativo, la lunghezza di campo è già nota. Ad esempio, il tipo di dati `int` accetta 4 byte. Se è stato indicato 0 per la lunghezza del prefisso, il comando **bcp** richiede la lunghezza del campo, le lunghezze di campo predefinite e l'effetto della lunghezza del campo sull'archiviazione dei dati in file di `char` dati contenenti dati.  
  
## <a name="the-bcp-prompt-for-field-length"></a>Richiesta di lunghezza di campo da parte di bcp  
 Se un comando interattivo **bcp** include l'opzione **in** o **out** senza l'opzione relativa al file di formato(**-f**) o al formato dei dati (**-n**, **-c**, **-w**, or **-N**), viene chiesta la lunghezza del campo di ogni campo di dati, come illustrato di seguito:  
  
 `Enter length of field <field_name> [<default>]:`  
  
 Per un esempio contestualizzato di tale richiesta, vedere [Impostazione dei formati di dati per la compatibilità mediante &#40;SQL Server&#41;](specify-data-formats-for-compatibility-when-using-bcp-sql-server.md).  
  
> [!NOTE]  
>  Dopo l'impostazione interattiva di tutti i campi in un comando **bcp**, viene richiesto di salvare le risposte relative a ogni campo in un file di formato non XML. Per altre informazioni sui file di formato non XML, vedere [File in formato non XML &#40;SQL Server&#41;](xml-format-files-sql-server.md).  
  
 La richiesta o meno della lunghezza del campo da parte del comando **bcp** dipende da diversi fattori, ad esempio:  
  
-   Quando si copiano tipi di dati con lunghezza non fissa e si specifica una lunghezza del prefisso pari a 0, **bcp** richiede una lunghezza del campo.  
  
-   Quando si convertono i dati di tipo non carattere in dati di tipo carattere, **bcp** suggerisce una lunghezza del campo predefinita sufficiente per archiviare i dati.  
  
-   Se il tipo di file di archiviazione è non carattere, il comando **bcp** non richiede l'immissione della lunghezza del campo. I dati vengono archiviati nella [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rappresentazione nativa dei dati (formato nativo).  
  
## <a name="using-default-field-lengths"></a>Utilizzo delle lunghezze di campo predefinite  
 In genere, [!INCLUDE[msCoName](../../includes/msconame-md.md)] consiglia di accettare i valori predefiniti per la lunghezza del campo proposti da **bcp**. Quando si crea un file in modalità carattere, l'utilizzo della lunghezza di campo predefinita consente di assicurare che i dati non verranno troncati e che non si verificheranno errori di overflow numerico  
  
 Se si specifica una lunghezza di campo non valida, è possibile che si verifichino errori. Ad esempio, se si copiano dati numerici e si specifica una lunghezza di campo insufficiente per i dati, l'utilità **bcp** visualizza un messaggio di overflow e i dati non vengono copiati. Inoltre, se si esportano `datetime` dati e si specifica una lunghezza di campo inferiore a 26 byte per la stringa di caratteri, l'utilità **bcp** tronca i dati senza un messaggio di errore.  
  
> [!IMPORTANT]  
>  Se si utilizza l'opzione predefinita per la dimensione, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] prevede di leggere una stringa intera. In alcuni casi, l'utilizzo di una lunghezza di campo predefinita può provocare un errore di tipo "Fine del file imprevista". In genere, questo errore si verifica `money` con `datetime` i tipi di dati e quando solo parte del campo previsto si verifica nel file di dati; ad esempio, quando un `datetime` valore di *mm*/*GG*/*AA* viene specificato senza il componente ora e è, pertanto, più breve della lunghezza prevista di 24 caratteri di un `datetime` valore nel `char` formato. Per evitare tale tipo di errore, utilizzare caratteri di terminazione del campo o campi dati di lunghezza fissa oppure modificare la lunghezza di campo predefinita, specificando un valore diverso.  
  
### <a name="default-field-lengths-for-character-file-storage"></a>Lunghezze di campo predefinite per l'archiviazione di file di caratteri  
 Nella tabella seguente vengono elencate le lunghezze di campo predefinite per i dati da archiviare come tipo di archiviazione file di caratteri. La lunghezza dei dati che ammettono valori Null è uguale alla lunghezza dei dati che non ammettono valori Null.  
  
|Tipo di dati|Lunghezza predefinita (caratteri)|  
|---------------|-----------------------------------|  
|`char`|Lunghezza definita per la colonna|  
|`varchar`|Lunghezza definita per la colonna|  
|`nchar`|Due volte la lunghezza definita per la colonna|  
|`nvarchar`|Due volte la lunghezza definita per la colonna|  
|`Text`|0|  
|`ntext`|0|  
|`bit`|1|  
|`binary`|Due volte la lunghezza definita per la colonna + 1|  
|`varbinary`|Due volte la lunghezza definita per la colonna + 1|  
|`image`|0|  
|`datetime`|24|  
|`smalldatetime`|24|  
|`float`|30|  
|`real`|30|  
|`int`|12|  
|`bigint`|19|  
|`smallint`|7|  
|`tinyint`|5|  
|`money`|30|  
|`smallmoney`|30|  
|`decimal`|41*|  
|`numeric`|41*|  
|`uniqueidentifier`|37|  
|`timestamp`|17|  
|`varchar(max)`|0|  
|`varbinary(max)`|0|  
|`nvarchar(max)`|0|  
|UDT|Lunghezza della colonna UDT|  
|XML|0|  
  
 \*Per ulteriori informazioni sui tipi `decimal` di `numeric` dati e, vedere [Decimal and numeric &#40;Transact-SQL&#41;](/sql/t-sql/data-types/decimal-and-numeric-transact-sql).  
  
> [!NOTE]  
>  Una colonna di tipo `tinyint` può contenere valori compresi tra 0 e 255. Il numero massimo di caratteri necessari per rappresentare un numero compreso nell'intervallo è tre (sono necessari tre caratteri per rappresentare i valori da 100 a 255).  
  
### <a name="default-field-lengths-for-native-file-storage"></a>Lunghezze di campo predefinite per l'archiviazione di file nativi  
 Nella tabella seguente vengono elencate le lunghezze di campo predefinite per i dati da archiviare come tipo di archiviazione file nativi. La lunghezza dei dati che ammettono valori Null è uguale alla lunghezza dei dati che non ammettono valori Null e i dati di tipo carattere vengono sempre archiviati nel formato carattere.  
  
|Tipo di dati|Lunghezza predefinita (caratteri)|  
|---------------|-----------------------------------|  
|`bit`|1|  
|`binary`|Lunghezza definita per la colonna|  
|`varbinary`|Lunghezza definita per la colonna|  
|`image`|0|  
|`datetime`|8|  
|`smalldatetime`|4|  
|`float`|8|  
|`real`|4|  
|`int`|4|  
|`bigint`|8|  
|`smallint`|2|  
|`tinyint`|1|  
|`money`|8|  
|`smallmoney`|4|  
|`decimal`<sup>1</sup>|<sup>*</sup>|  
|`numeric`<sup>1</sup>|<sup>*</sup>|  
|`uniqueidentifier`|16|  
|`timestamp`|8|  
  
 <sup>1</sup> per altre informazioni sui tipi `decimal` di `numeric` dati e, vedere [decimal and numeric &#40;Transact-SQL&#41;](/sql/t-sql/data-types/decimal-and-numeric-transact-sql).  
  
 In tutti i casi illustrati in precedenza, per creare un file di dati per un successivo ricaricamento in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ridurre al minimo lo spazio utilizzato per l'archiviazione, utilizzare un prefisso di lunghezza con il tipo di archiviazione nel file e la lunghezza di campo predefiniti.  
  
## <a name="see-also"></a>Vedere anche  
 [Utilità bcp](../../tools/bcp-utility.md)   
 [Tipi di dati &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [Specificare i terminatori del campo e della riga &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)   
 [Specificare la lunghezza del prefisso nei file di dati tramite bcp &#40;SQL Server&#41;](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)   
 [Specificare il tipo di archiviazione di file utilizzando bcp &#40;SQL Server&#41;](specify-file-storage-type-by-using-bcp-sql-server.md)   
 [Mantenimento dei valori Null o utilizzo dei valori predefiniti durante un'importazione bulk &#40;SQL Server&#41;](keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
  
