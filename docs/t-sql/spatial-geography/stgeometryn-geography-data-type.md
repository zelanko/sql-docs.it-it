---
description: STGeometryN (tipo di dati geography)
title: STGeometryN (tipo di dati geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STGeometryN (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STGeometryN method
ms.assetid: 53755f69-cd50-475b-b3b8-a1a9157cf03a
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 812a5e63f21de77028c1f00a08f1819c5a07be13
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88445244"
---
# <a name="stgeometryn-geography-data-type"></a>STGeometryN (tipo di dati geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Restituisce un elemento **geography** specificato in un tipo **GeometryCollection** o in uno dei sottotipi. Quando STGeometryN() viene usato su un sottotipo di **GeometryCollection**, ad esempio **MultiPoint** o **MultiLineString**, questo metodo restituisce l'istanza **geography** se chiamato con N = 1.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.STGeometryN ( expression )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argomenti
 *expression*  
 Espressione **int** compresa tra 1 e il numero di istanze **geography** in **GeometryCollection**.  
  
## <a name="return-types"></a>Tipi restituiti  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **geography**  
  
 Tipo CLR restituito: **SqlGeography**  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo restituisce Null se il parametro è maggiore del risultato di [STNumGeometries()](../../t-sql/spatial-geography/stnumgeometries-geography-data-type.md) e genererà un'eccezione **ArgumentOutOfRangeException** se il parametro *expression* è minore di 1.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene creata un'istanza `MultiPoint``geography` e viene usato `STGeometryN()` per trovare la seconda istanza `geography` del tipo **GeometryCollection**.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('MULTIPOINT(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STGeometryN(2).ToString();  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi OGC sulle istanze di geografia](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
