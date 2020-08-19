---
description: RingN (tipo di dati geography)
title: RingN (tipo di dati geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- RingN
- RingN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- RingN method
ms.assetid: 30f47275-2727-4d22-bbec-c0c54bcb3ac2
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 58325135db25b79d7c38fb3447f6b7e5bfd8c89a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88417017"
---
# <a name="ringn-geography-data-type"></a>RingN (tipo di dati geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Restituisce l'anello specificato dell'istanza **geography**: `1 ≤ n ≤ NumRings()`.  
  
## <a name="syntax"></a>Sintassi  
  
```syntaxsql
.RingN (expression )
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argomenti
 *expression*  
 Espressione **int** compresa tra 1 e il numero di anelli in un'istanza **polygon**.  
  
## <a name="return-value"></a>Valore restituito  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **geography**  
  
 Tipo CLR restituito: **SqlGeography**  
  
## <a name="remarks"></a>Osservazioni  
 Se il valore dell'indice degli anelli **n** è minore di 1, questo metodo genera un'eccezione **ArgumentOutOfRangeException.** Il valore dell'indice dell'anello deve essere maggiore o uguale a 1 e dovrebbe essere minore o uguale al numero restituito da `NumRings()`.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio viene creata un'istanza `Polygon` con due anelli e viene restituito il secondo anello.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653), (-122.357 47.654, -122.357 47.657, -122.349 47.657, -122.349 47.650, -122.357 47.654))', 4326);  
SELECT @g.RingN(2).ToString();  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi estesi sulle istanze di geografia](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [NumRings &#40;tipo di dati geography&#41;](../../t-sql/spatial-geography/numrings-geography-data-type.md)  
  
  
