---
description: STCurveToLine (tipo di dati geography)
title: STCurveToLine (tipo di dati geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STCurveToLine_TSQL
- STCurveToLine
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveToLine method (geography)
ms.assetid: 2f863a85-6168-465a-b32f-bb5e3de58dee
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 2c8674e1e7ccafd59fa550fca690553050f68ffb
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/26/2020
ms.locfileid: "88479309"
---
# <a name="stcurvetoline-geography-data-type"></a>STCurveToLine (tipo di dati geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Restituisce un'approssimazione poligonale di un'istanza **geography** contenente segmenti di arco circolare.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.STCurveToLine()  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipi restituiti
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **geography**  
  
 Tipo CLR restituito: **SqlGeography**  
  
## <a name="remarks"></a>Osservazioni  
 Restituisce un'istanza **LineString** per un'istanza **CircularString** o **CompoundCurve**.  
  
 Restituisce un'istanza **Polygon** per un'istanza **CurvePolygon**.  
  
 Restituisce una copia delle istanze **geography** che non contengono istanze **CircularString**, **CompoundCurve** o **CurvePolygon**.  
  
 A differenza della specifica SQL MM, questo metodo non usa i valori della coordinata Z nel calcolo dell'approssimazione poligonale. Qualsiasi valore della coordinata Z presente nell'istanza **geometry** chiamante viene ignorato.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituita un'istanza `LineString` che rappresenta un'approssimazione poligonale di un'istanza `CircularString`.  
  
```
 DECLARE @g1 geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 DECLARE @g2 geography;  
 SET @g2 = @g1.STCurveToLine();  
 SELECT @g1.STNumPoints() AS G1, @g2.STNumPoints() AS G2;
 ```  
  
## <a name="see-also"></a>Vedere anche  
 [STLength &#40;tipo di dati geography&#41;](../../t-sql/spatial-geography/stlength-geography-data-type.md)   
 [STNumPoints &#40;tipo di dati geography&#41;](../../t-sql/spatial-geography/stnumpoints-geography-data-type.md)   
 [Panoramica dei tipi di dati spaziali](../../relational-databases/spatial/spatial-data-types-overview.md)  
  
  
