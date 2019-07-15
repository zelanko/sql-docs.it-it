---
title: Elemento Index (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Index element (DTA)
ms.assetid: 447d3964-b387-40f6-9189-71386774c29e
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 786aeeadec0e0b00bed087dec8c7306319e5a017
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2019
ms.locfileid: "67727626"
---
# <a name="index-element-dta"></a>Index - elemento (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Contiene informazioni su un indice che si desidera creare o eliminare per una configurazione specificata dall'utente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
<Recommendation>  
  <Create>  
    <Index [Clustered | Unique | Online | IndexSizeInMB | NumberOfRows             | QUOTED_IDENTIFIER | ARITHABORT | CONCAT_NULL_YIELDS_NULL             | ANSI_NULLS | ANSI_PADDING | ANSI_WARNINGS  
            | NUMERIC_ROUNDABORT]  
     ...code removed here...  
    </Index>  
```  
  
## <a name="element-attributes"></a>Attributi elemento  
  
|Attributo Index|Tipo di dati|Descrizione|  
|---------------------|---------------|-----------------|  
|**Cluster**|**boolean**|Facoltativo. Specifica un indice cluster. Impostare su "true" o "false", ad esempio:<br /><br /> `<Index Clustered="true">`<br /><br /> Per impostazione predefinita, questo attributo è impostato su "false".|  
|**Univoco**|**boolean**|Facoltativo. Specifica un indice univoco. Impostare su "true" o "false", ad esempio:<br /><br /> `<Index Unique="true">`<br /><br /> Per impostazione predefinita, questo attributo è impostato su "false".|  
|**Online**|**boolean**|Facoltativo. Specifica un indice in grado di eseguire operazioni che richiedono spazio su disco temporaneo mentre il server è online. Impostare su "true" o "false", ad esempio:<br /><br /> `<Index Online="true">`<br /><br /> Per impostazione predefinita, questo attributo è impostato su "false".<br /><br /> Per altre informazioni, vedere [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md).|  
|**IndexSizeInMB**|**double**|Facoltativo. Specifica le dimensioni massime dell'indice in megabyte, ad esempio:<br /><br /> `<Index IndexSizeInMB="873.75">`<br /><br /> Nessuna impostazione predefinita.|  
|**NumberOfRows**|**integer**|Facoltativo. Simula diverse dimensioni di indice, che rispecchiano in maniera efficiente diverse dimensioni di tabella, ad esempio:<br /><br /> `<Index NumberOfRows="3000">`<br /><br /> Nessuna impostazione predefinita.|  
|**QUOTED_IDENTIFIER**|**boolean**|Facoltativo. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seguirà le regole ISO relative alle virgolette che delimitano gli identificatori e le stringhe letterali. È necessario attivare questo attributo se l'indice è definito in una colonna calcolata o in una vista. La sintassi seguente, ad esempio, consente di attivare l'attributo:<br /><br /> `<Index QUOTED_IDENTIFIER [...]>`<br /><br /> Per impostazione predefinita, l'attributo è disattivato.<br /><br /> Per altre informazioni, vedere [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).|  
|**ARITHABORT**|**boolean**|Facoltativo. Interrompe una query quando si verifica un errore di divisione per zero o di overflow durante l'esecuzione della query stessa. È necessario attivare questo attributo se l'indice è definito in una colonna calcolata o in una vista. La sintassi seguente, ad esempio, consente di attivare l'attributo:<br /><br /> `<Index ARITHABORT [...]>`<br /><br /> Per impostazione predefinita, l'attributo è disattivato.<br /><br /> Per altre informazioni, vedere [SET ARITHABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-arithabort-transact-sql.md).|  
|**CONCAT_NULL_YIELDS_**<br /><br /> **NULL**|**boolean**|Facoltativo. Controlla se i risultati di concatenazione vengono considerati valori Null o stringhe vuote. È necessario attivare questo attributo se l'indice è definito in una colonna calcolata o in una vista. La sintassi seguente, ad esempio, consente di attivare l'attributo:<br /><br /> `<Index CONCAT_NULL_YIELDS_NULL [...]>`<br /><br /> Per impostazione predefinita, l'attributo è disattivato.<br /><br /> Per altre informazioni, vedere [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md).|  
|**ANSI_NULLS**|**boolean**|Facoltativo. Specifica il comportamento conforme allo standard ISO degli operatori di confronto uguale a (=) e diverso da (<>) quando questi vengono utilizzati con valori Null. È necessario attivare questo attributo se l'indice è definito in una colonna calcolata o in una vista. La sintassi seguente, ad esempio, consente di attivare l'attributo:<br /><br /> `<Index ANSI_NULLS [...]>`<br /><br /> Per impostazione predefinita, l'attributo è disattivato.<br /><br /> Per altre informazioni, vedere [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md).|  
|**ANSI_PADDING**|**boolean**|Facoltativo. Controlla la modalità di archiviazione nella colonna dei valori di dimensioni minori rispetto alle dimensioni definite. È necessario attivare questo attributo se l'indice è definito in una colonna calcolata o in una vista. La sintassi seguente, ad esempio, consente di attivare l'attributo:<br /><br /> `<Index ANSI_PADDING [...]>`<br /><br /> Per impostazione predefinita, l'attributo è disattivato.<br /><br /> Per altre informazioni, vedere [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md).|  
|**ANSI_WARNINGS**|**boolean**|Facoltativo. Specifica il funzionamento standard ISO in varie condizioni di errore. È necessario attivare questo attributo se l'indice è definito in una colonna calcolata o in una vista. La sintassi seguente, ad esempio, consente di attivare l'attributo:<br /><br /> `<Index ANSI_WARNING [...]>`<br /><br /> Per impostazione predefinita, l'attributo è disattivato.<br /><br /> Per altre informazioni, vedere [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md).|  
|**NUMERIC_ROUNDABORT**|**boolean**|Facoltativo. Specifica il livello di segnalazione degli errori generato quando l'arrotondamento in un'espressione comporta una perdita di precisione. È necessario disattivare questo attributo se l'indice è definito in una colonna calcolata o in una vista.<br /><br /> La sintassi seguente consente di attivare questo attributo:<br /><br /> `<Index ANSI_WARNING [...]>`<br /><br /> Per impostazione predefinita, l'attributo è disattivato.<br /><br /> Per altre informazioni, vedere [SET NUMERIC_ROUNDABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-numeric-roundabort-transact-sql.md).|  
  
## <a name="element-characteristics"></a>Caratteristiche elemento  
  
|Caratteristica|Descrizione|  
|--------------------|-----------------|  
|**Tipo di dati e lunghezza**|Nessuna.|  
|**Valore predefinito**|Nessuna.|  
|**Occorrenza**|Obbligatorio una sola volta per ogni elemento **Create** o **Drop** se non è specificata nessun'altra struttura di progettazione fisica tramite gli elementi **Statistics** o **Heap** .|  
  
## <a name="element-relationships"></a>Relazioni elemento  
  
|Relazione|Elementi|  
|------------------|--------------|  
|**Elemento padre**|[Elemento Create &#40;DTA&#41;](../../tools/dta/create-element-dta.md)<br /><br /> Elemento **Drop**. Per ulteriori informazioni, vedere l'XML Schema di Ottimizzazione guidata motore di database.|  
|**Elementi figlio**|[Elemento Name per Index &#40;DTA&#41;](../../tools/dta/name-element-for-index-dta.md)<br /><br /> [Elemento Column per Index &#40;DTA&#41;](../../tools/dta/column-element-for-index-dta.md)<br /><br /> Elemento**PartitionScheme** . Per ulteriori informazioni, vedere l'XML Schema di Ottimizzazione guidata motore di database.<br /><br /> Elemento**PartitionColumn** . Per ulteriori informazioni, vedere l'XML Schema di Ottimizzazione guidata motore di database.<br /><br /> [Elemento Filegroup per Index &#40;DTA&#41;](../../tools/dta/filegroup-element-for-index-dta.md)<br /><br /> Elemento**NumberOfReferences** . Per ulteriori informazioni, vedere l'XML Schema di Ottimizzazione guidata motore di database.<br /><br /> Elemento**PercentUsage** . Per ulteriori informazioni, vedere l'XML Schema di Ottimizzazione guidata motore di database.|  
  
## <a name="example"></a>Esempio  
 Per un esempio di questo elemento, vedere [Esempio di file di input XML con configurazione specificata dall'utente &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai file di input XML&#40; (Ottimizzazione guidata motore di database)&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
