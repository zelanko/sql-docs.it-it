---
title: sys.dm_db_objects_impacted_on_version_change
titleSuffix: Azure SQL Database
ms.date: 03/03/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_objects_impacted_on_version_change_TSQL
- dm_db_objects_impacted_on_version_change
- dm_db_objects_impacted_on_version_change_TSQL
- sys.dm_db_objects_impacted_on_version_change
dev_langs:
- TSQL
helpviewer_keywords:
- dm_db_objects_impacted_on_version_change
- sys.dm_db_objects_impacted_on_version_change
ms.assetid: b94af834-c4f6-4a27-80a6-e8e71fa8793a
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.custom: seo-dt-2019
ms.openlocfilehash: 0255f7260044ee5c09d020f3ba6310d24bc8cb74
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "73843856"
---
# <a name="sysdm_db_objects_impacted_on_version_change-azure-sql-database"></a>sys.dm_db_objects_impacted_on_version_change (Database di SQL Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Questa vista di sistema con ambito database è progettata per fornire un sistema di avviso anticipato per determinare gli oggetti che saranno interessati da un aggiornamento importante del [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. È possibile utilizzare la vista prima o dopo l'aggiornamento per ottenere un'enumerazione completa degli oggetti interessati. È necessario eseguire query su questa vista in ogni database per ottenere un conteggio completo per l'intero server.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|classe|**int** NOT NULL|Classe dell'oggetto che sarà interessato:<br /><br /> **1** = vincolo<br /><br /> **7** = indici e heap|  
|class_desc|**nvarchar (60)** NOT NULL|Descrizione della classe:<br /><br /> **OBJECT_OR_COLUMN**<br /><br /> **INDEX**|  
|major_id|**int** NOT NULL|ID oggetto del vincolo o ID oggetto della tabella che contiene l'indice o l'heap.|  
|minor_id|**int** NULL|**Null** per i vincoli<br /><br /> Index_id per indici e heap|  
|dipendenza|**nvarchar (60)** NOT NULL|Descrizione della dipendenza che causerà l'interessamento di un vincolo o di un indice. Lo stesso valore viene inoltre utilizzato per gli avvisi generati durante l'aggiornamento.<br /><br /> Esempi:<br /><br /> **spazio** (per intrinseco)<br /><br /> **Geometry** (per UDT di sistema)<br /><br /> **geography::P ass** (per il metodo UDT di sistema)|  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione VIEW DATABASE STATE.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene mostrata una query sulla vista **sys.dm_db_objects_impacted_on_version_change** per trovare gli oggetti interessati da un aggiornamento alla prossima versione principale del server.  
  
```  
SELECT * FROM sys.dm_db_objects_disabled_on_version_change;  
GO  
```  
  
```  
class  class_desc        major_id    minor_id    dependency                       
------ ----------------- ----------- ----------- ----------   
1      OBJECT_OR_COLUMN  181575685   NULL        geometry                        
7      INDEX             37575172    1           geometry                        
7      INDEX             2121058592  1           geometry                        
1      OBJECT_OR_COLUMN  101575400   NULL        geometry     
```  
  
## <a name="remarks"></a>Osservazioni  
  
### <a name="how-to-update-impacted-objects"></a>Come aggiornare gli oggetti interessati  
 Nei passaggi ordinati seguenti viene descritta l'azione correttiva da intraprendere dopo l'aggiornamento dalla versione del servizio di giugno.  
  
|JSON|Oggetto interessato|Azione correttiva|  
|-----------|---------------------|-----------------------|  
|1|**Indici**|Ricompilare gli indici identificati da **sys. dm_db_objects_impacted_on_version_change** ad esempio:`ALTER INDEX ALL ON <table> REBUILD`<br />o<br />`ALTER TABLE <table> REBUILD`|  
|2|**Object**|Tutti i vincoli identificati dalla vista **sys.dm_db_objects_impacted_on_version_change** devono essere riconvalidati dopo la rielaborazione dei dati geometry e geography nella tabella sottostante. Per i convalidi, riconvalidare utilizzando ALTER TABLE. <br />Ad esempio: <br />`ALTER TABLE <tab> WITH CHECK CHECK CONSTRAINT <constraint name>`<br />o<br />`ALTER TABLE <tab> WITH CHECK CONSTRAINT ALL`|  
  
  
