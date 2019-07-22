---
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
ms.openlocfilehash: d6c68aa9859fbe7e1066ad392377d6b50289fd0a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68042396"
---
# <a name="stcurvetoline-geography-data-type"></a>STCurveToLine (tipo di dati geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Restituisce un'approssimazione poligonale di un'istanza **geography** contenente segmenti di arco circolare.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.STCurveToLine()  
```  
  
## <a name="return-types"></a>Tipi restituiti  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **geography**  
  
 Tipo CLR restituito: **SqlGeography**  
  
## <a name="remarks"></a>Remarks  
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
  
  
