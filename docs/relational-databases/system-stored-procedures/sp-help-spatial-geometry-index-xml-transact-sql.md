---
title: sp_help_spatial_geometry_index_xml (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_spatial_geometry_index_xml_TSQL
- sp_help_spatial_geometry_index_xml
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_spatial_geometry_index_xml procedure
ms.assetid: 9668ae6d-9ed5-418e-bb9a-9e7b66f7dd16
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: a2834652d7a14199ccc4914091a2c8c8b7a99801
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63017787"
---
# <a name="sphelpspatialgeometryindexxml-transact-sql"></a>sp_help_spatial_geometry_index_xml (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Restituisce i nomi e valori per un set specificato di proprietà su un **geometria** indice spaziale. È possibile scegliere di restituire un set principale di proprietà oppure tutte le proprietà dell'indice.  
  
 I risultati vengono restituiti in un frammento XML in cui vengono visualizzati il nome e valore delle proprietà selezionate.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_help_spatial_geometry_index [ @tabname =] 'tabname'   
     [ , [ @indexname = ] 'indexname' ]   
     [ , [ @verboseoutput = ]'{ 0 | 1 }]   
     [ , [ @query_sample = ] 'query_sample' ]   
     [ ,.[ @xml_output = ] 'xml_output' ]   
```  
  
## <a name="arguments"></a>Argomenti  
 Visualizzare [Stored procedure di argomenti e le proprietà dell'indice spaziale](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md).  
  
## <a name="properties"></a>Proprietà  
 Visualizzare [Stored procedure di argomenti e le proprietà dell'indice spaziale](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md).  
  
## <a name="permissions"></a>Permissions  
 Utente deve essere un membro del **pubblica** ruolo. È necessario disporre dell'autorizzazione READ ACCESS per il server e l'oggetto.  
  
## <a name="remarks"></a>Note  
 Le proprietà che contengono valori NULL non sono incluse nel set XML restituito.  
  
## <a name="example"></a>Esempio  
 L'esempio seguente usa `sp_help_spatial_geometry_index_xml` per esaminare l'indice spaziale **SIndx_SpatialTable_geometry_col2** definiti nella tabella **geometry_col** per l'esempio di query specificata in **@qs** . L'esempio restituisce le proprietà principali dell'indice specificato in un frammento XML in cui vengono visualizzati il nome e il valore delle proprietà selezionate.  
  
 Un' [XQuery](../../xquery/xquery-basics.md) viene quindi eseguita nel set di risultati, la restituzione di una proprietà specifica.  
  
```  
DECLARE @qs geometry  
        ='POLYGON((-90.0 -180.0, -90.0 180.0, 90.0 180.0, 90.0 -180.0, -90.0 -180.0))';  
DECLARE @x xml;  
EXEC sp_help_spatial_geometry_index_xml 'geometry_col', 'SIndx_SpatialTable_geometry_col2', 0, @qs, @x output;  
SELECT @x.value('(/Primary_Filter_Efficiency/text())[1]', 'float');  
```  
  
 Simile a [sp_help_spatial_geometry_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md), questa stored procedure consente di accedere a livello di codice più semplice per le proprietà di un indice spaziale e restituisce il set di risultati in XML.  
  
## <a name="requirements"></a>Requisiti  
  
## <a name="see-also"></a>Vedere anche  
 [Gli argomenti e le proprietà di spaziale indicizzare le Stored procedure](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md)   
 [Stored procedure di indice spaziale](https://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)   
 [sp_help_spatial_geometry_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)   
 [Panoramica degli indici spaziali](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [Dati spaziali &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)   
 [XQuery Basics](../../xquery/xquery-basics.md)   
 [Guida di riferimento al linguaggio XQuery](../../xquery/xquery-language-reference-sql-server.md)  
  
  
