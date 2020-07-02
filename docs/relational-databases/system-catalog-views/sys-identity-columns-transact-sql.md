---
title: sys. identity_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- identity_columns
- sys.identity_columns
- sys.identity_columns_TSQL
- identity_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.identity_columns catalog view
ms.assetid: 97ee01e6-9c9e-4fd9-884b-68b4084669d5
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: dbdb7e8b57469dc025dbc9729758c72199dfb18d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85790529"
---
# <a name="sysidentity_columns-transact-sql"></a>sys.identity_columns (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asdw-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  Contiene una riga per ogni colonna Identity.  
  
 La vista **sys. identity_columns** eredita le righe dalla vista **sys. Columns** . La vista **sys. identity_columns** restituisce le colonne della vista **sys. Columns** , oltre alle colonne **seed_value**, **increment_value**, **LAST_VALUE**e **is_not_for_replication** . Per altre informazioni, vedere [Viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md).  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**\<columns inherited from sys.columns>**||La vista **sys. identity_columns** restituisce tutte le colonne della vista **sys. Columns** . Vengono inoltre restituite le colonne aggiuntive descritte di seguito. Per una descrizione delle colonne ereditate dalla vista **sys. identity_columns** da **sys. Columns**, vedere [sys. Columns &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md).|  
|**seed_value**|**sql_variant**|Valore di inizializzazione per la colonna Identity. Il tipo di dati del valore di inizializzazione è uguale al tipo di dati della colonna.|  
|**increment_value**|**sql_variant**|Valore di incremento per la colonna Identity. Il tipo di dati del valore di inizializzazione è uguale al tipo di dati della colonna.|  
|**last_value**|**sql_variant**|Ultimo valore generato per la colonna Identity. Il tipo di dati del valore di inizializzazione è uguale al tipo di dati della colonna.|  
|**is_not_for_replication**|**bit**|Per la colonna Identity è dichiarata l'opzione NOT FOR REPLICATION. **Nota:** Questa colonna non si applica ad analisi sinapsi di Azure.|  
  
> [!NOTE]  
>  Per creare un numero a incremento automatico da usare in più tabelle o da chiamare dalle applicazioni senza fare riferimento ad alcuna tabella, vedere [Numeri di sequenza](../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
## <a name="permissions"></a>Autorizzazioni  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo oggetti &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Viste del catalogo &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Domande frequenti sull'esecuzione di query sul catalogo di sistema di SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
