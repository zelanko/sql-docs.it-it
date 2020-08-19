---
description: sp_help_spatial_geometry_index (Transact-SQL)
title: sp_help_spatial_geometry_index (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_spatial_geometry_index
- sp_help_spatial_geometry_index_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_spatial_geometry_index procedure
ms.assetid: f1bcefb1-09c8-4b49-8c51-5d471065849f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c69826d4d76ae518cc119cfc46418ade8407c7cd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88447063"
---
# <a name="sp_help_spatial_geometry_index-transact-sql"></a>sp_help_spatial_geometry_index (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Restituisce i nomi e i valori per un set specificato di proprietà relative a un indice spaziale di **geometria** . Il risultato viene restituito in formato di tabella. È possibile scegliere di restituire un set principale di proprietà oppure tutte le proprietà dell'indice.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_help_spatial_geometry_index [ @tabname =] 'tabname'   
     [ , [ @indexname = ] 'indexname' ]   
     [ , [ @verboseoutput = ] 'verboseoutput'   
     [ , [ @query_sample = ] 'query_sample']   
```  
  
## <a name="arguments"></a>Argomenti  
 Vedere [argomenti e proprietà delle stored procedure per gli indici spaziali](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md).  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Vedere [argomenti e proprietà delle stored procedure per gli indici spaziali](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md).  
  
## <a name="permissions"></a>Autorizzazioni  
 Per accedere alla procedura, l'utente deve essere assegnato a un ruolo PUBLIC. È necessario disporre dell'autorizzazione READ ACCESS per il server e l'oggetto.  
  
## <a name="remarks"></a>Osservazioni  
 Le proprietà che contengono valori NULL non sono incluse nel set restituito.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene usato `sp_help_spatial_geometry_index` per esaminare l'indice spaziale **SIndx_SpatialTable_geometry_col2** definito nella tabella **geometry_col** per l'esempio di query specificato in ** \@ QS**. In questo esempio vengono restituite solo le proprietà principali dell'indice specificato.  
  
```  
declare @qs geometry  
        ='POLYGON((-90.0 -180.0, -90.0 180.0, 90.0 180.0, 90.0 -180.0, -90.0 -180.0))';  
exec sp_help_spatial_geometry_index 'geometry_col', 'SIndx_SpatialTable_geometry_col2', 0, @qs;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure per indici spaziali](https://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)   
 [sp_help_spatial_geometry_index_xml](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-xml-transact-sql.md)   
 [Panoramica degli indici spaziali](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [Dati spaziali &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
