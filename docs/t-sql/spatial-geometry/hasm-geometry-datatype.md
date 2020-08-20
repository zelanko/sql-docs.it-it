---
description: HasM (tipo di dati geometry)
title: HasM (tipo di dati geometry) | Microsoft Docs
ms.custom: ''
ms.date: 05/05/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- HasM geometry
ms.assetid: 15540837-c4bf-4d18-b380-13ae31f3226f
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: fa0f82d9ee71c8fb5174a4ee4d48c706315f97e0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458975"
---
# <a name="hasm-geometry-datatype"></a>HasM (tipo di dati geometry)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  Restituisce 1 (true) se un oggetto spaziale contiene almeno un valore M; in caso contrario, restituisce 0 (false).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.HasM  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipi restituiti
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **bit**  
  
 Tipo CLR restituito: **Boolean**  
  
## <a name="remarks"></a>Osservazioni  
  
## <a name="examples"></a>Esempi  
  
```sql  
DECLARE @p GEOMETRY = 'Point(1 1 1 1)'  
SELECT @p.HasM   
--Returns: 1 (true)  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi estesi sulle istanze di geometria](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [M &#40;tipo di dati geometry&#41;](../../t-sql/spatial-geometry/m-geometry-data-type.md)  
  
