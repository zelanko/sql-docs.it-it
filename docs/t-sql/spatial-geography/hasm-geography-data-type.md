---
title: HasM (tipo di dati geography) | Microsoft Docs
ms.custom: ''
ms.date: 05/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- HasM_TSQL
- HasM
dev_langs:
- TSQL
helpviewer_keywords:
- HasM geography
ms.assetid: e752e97f-1619-437d-b962-48c188b4e94c
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: ec68ecc0973683bc93c5e11b80eec860912ebccf
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86555246"
---
# <a name="hasm-geography-data-type"></a>HasM (tipo di dati geography)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

Restituisce 1 (true) se un oggetto spaziale contiene almeno un valore M; in caso contrario, restituisce 0 (false).  
  
## <a name="syntax"></a>Sintassi  
  
```sql  
  
.HasM  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipi restituiti
Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **bit**  
  
Tipo CLR restituito: **Boolean**  
  
## <a name="remarks"></a>Osservazioni  
  
## <a name="examples"></a>Esempi  
  
```sql  
DECLARE @p GEOGRAPHY = 'Point(1 1 1 1)'  
SELECT @p.HasM   
--Returns: 1 (true)  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi estesi sulle istanze di geografia](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [M &#40;tipo di dati geography&#41;](../../t-sql/spatial-geography/m-geography-data-type.md)  
  
  
