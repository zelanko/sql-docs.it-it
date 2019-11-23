---
title: sp_help_spatial_geography_index (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_spatial_geography_index
- sp_help_spatial_geography_index_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_spatial_geography_index procedure
ms.assetid: c9bf5675-eafc-4d71-bfdb-da963384fa0c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 73bb564880cae238cdbaa7e3c13a1f18ab95dc99
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/14/2019
ms.locfileid: "72304878"
---
# <a name="sp_help_spatial_geography_index-transact-sql"></a>sp_help_spatial_geography_index (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Restituisce i nomi e i valori per un set specificato di proprietà relative a un indice spaziale **geografico** . Il risultato viene restituito in formato di tabella. È possibile scegliere di restituire un set principale di proprietà oppure tutte le proprietà dell'indice.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_help_spatial_geography_index [ @tabname =] 'tabname'   
     [ , [ @indexname = ] 'indexname' ]   
     [ , [ @verboseoutput = ] 'verboseoutput' ]   
     [ , [ @query_sample = ] 'query_sample' ]   
```  
  
## <a name="arguments"></a>Argomenti  
 Vedere [argomenti e proprietà delle stored procedure per gli indici spaziali](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md).  
  
## <a name="properties"></a>Proprietà  
 Vedere [argomenti e proprietà delle stored procedure per gli indici spaziali](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md).  
  
## <a name="permissions"></a>Autorizzazioni  
 Per accedere alla procedura, l'utente deve essere assegnato a un ruolo PUBLIC. È necessario disporre dell'autorizzazione READ ACCESS per il server e l'oggetto.  
  
## <a name="remarks"></a>Osservazioni  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene usato `sp_help_spatial_geography_index` per esaminare l'indice spaziale **geography** **SIndx_SpatialTable_geography_col2** definito nella tabella **geography_col** per l'esempio di query specificato in **\@QS**. In questo esempio vengono restituite solo le proprietà principali dell'indice specificato.  
  
```  
declare @qs geography  
        ='POLYGON((-90.0 -180, -90 180.0, 90 180.0, 90 -180, -90 -180.0))';  
exec sp_help_spatial_geography_index 'geography_col', 'SIndx_SpatialTable_geography_col2', 0, @qs;  
```  
  
 Il rettangolo di delimitazione di un'istanza **geography** è la terra intera.  
  
## <a name="requirements"></a>Requisiti  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure per indici spaziali](https://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)   
 [sp_help_spatial_geography_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md)   
 [Panoramica degli indici spaziali](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [Dati spaziali &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
