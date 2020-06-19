---
title: Importare dati in formato nativo e carattere da versioni precedenti di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- earlier versions [SQL Server], import and export data formats
- -V switch
- data formats [SQL Server], earlier versions
- previous versions [SQL Server], import and export data formats
ms.assetid: e644696f-9017-428e-a5b3-d445d1c630b3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 274c984d6ecec8af8f5bea27496450a45fc2f1df
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85026795"
---
# <a name="import-native-and-character-format-data-from-earlier-versions-of-sql-server"></a>Importare dati in formato nativo e carattere da versioni precedenti di SQL Server
  In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]è possibile usare **bcp** per importare dati in formato nativo e carattere da [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]o da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] usando l'opzione **-V** . Se si usa l'opzione **-V** , in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] vengono usati tipi di dati della versione precedente specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e il formato del file di dati corrisponderà al formato della versione precedente in questione.  
  
 Per specificare una versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precedente per un file di dati, usare l'opzione **-V** con uno dei qualificatori seguenti:  
  
|Versione di SQL Server|Qualifier|  
|------------------------|---------------|  
|[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]|**-V80**|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|**-V90**|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|**-V100**|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|**-V 110**|  
  
## <a name="interpretation-of-data-types"></a>Interpretazione dei tipi di dati  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive supportano alcuni nuovi tipi. Se si desidera importare un nuovo tipo di dati in una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è necessario archiviarlo in un formato leggibile dai client **bcp** precedenti. Nella seguente tabella viene riepilogata la modalità di conversione dei nuovi tipi di dati per la compatibilità con le versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Nuovi tipi di dati in SQL Server 2005|Tipi di dati compatibili nella versione 6*x*|Tipi di dati compatibili nella versione 70|Tipi di dati compatibili nella versione 80|  
|---------------------------------------|-------------------------------------------|-----------------------------------------|-----------------------------------------|  
|`bigint`|`decimal`|`decimal`|*|  
|`sql_variant`|`text`|`nvarchar(4000)`|*|  
|`varchar(max)`|`text`|`text`|`text`|  
|`nvarchar(max)`|`ntext`|`ntext`|`ntext`|  
|`varbinary(max)`|`image`|`image`|`image`|  
|XML|`ntext`|`ntext`|`ntext`|  
|Tipo definito dall'utente<sup>1</sup>|`image`|`image`|`image`|  
  
 \*Questo tipo è supportato in modo nativo.  
  
 <sup>1</sup> UDT indica un tipo definito dall'utente.  
  
## <a name="exporting-using--v-80"></a>Esportazione usando –V 80  
 Quando si esegue l'esportazione bulk di dati tramite l'opzione **-V80** , i dati di tipo,,, `nvarchar(max)` `varchar(max)` `varbinary(max)` XML e UDT in modalità nativa vengono archiviati con un prefisso a 4 byte, ad esempio i `text` `image` dati, e `ntext` , anziché con un prefisso a 8 byte, che è l'impostazione predefinita per [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive.  
  
## <a name="copying-date-values"></a>Copia dei valori di data  
 **bcp** consente di usare l'API della copia bulk ODBC. Quindi, per importare i valori di dati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], **bcp** usa il formato di data ODBC (*aaaa-mm-gg hh:mm:ss*[ *.f...* ]).  
  
 Il comando **bcp** Esporta i file di dati in formato carattere usando il formato predefinito ODBC per `datetime` `smalldatetime` i valori e. Ad esempio, per una colonna `datetime` contenente la data `12 Aug 1998` verrà eseguita la copia bulk in un file di dati come stringa di caratteri `1998-08-12 00:00:00.000`.  
  
> [!IMPORTANT]  
>  Quando si importano dati in un `smalldatetime` campo con **bcp**, assicurarsi che il valore per seconds sia 00,000; in caso contrario, l'operazione avrà esito negativo. Il tipo di dati `smalldatetime` contiene solo valori approssimati al minuto più vicino. In questa istanza, le istruzioni BULK INSERT e INSERT ... SELECT * FROM OPENROWSET(BULK...) verranno eseguite ma il valore dei secondi verrà troncato.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Attività correlate  
 **Per utilizzare formati di dati per l'importazione o l'esportazione bulk**  
  
-   [Utilizzo del formato carattere per l'importazione o l'esportazione di dati &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usare il formato nativo per importare o esportare dati &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Utilizzo del formato carattere Unicode per l'importazione o l'esportazione di dati &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usare il formato Unicode nativo per importare o esportare dati &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
 
  
## <a name="see-also"></a>Vedere anche  
 [Utilità bcp](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [Tipi di dati &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [Compatibilità con le versioni precedenti del motore di database di SQL Server](../../database-engine/sql-server-database-engine-backward-compatibility.md)   
 [CAST e CONVERT &#40;Transact-SQL&#41;](/sql/t-sql/functions/cast-and-convert-transact-sql)  
  
  
