---
title: CollectionAggregate (tipo di dati geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- CollectionAggregate method (geometry)
ms.assetid: b7c85d59-c841-4b7f-9d46-8b4b7f2a3afe
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: fcc6820db9623b989db0e679a0f6d01dc7fcd5d5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85700658"
---
# <a name="collectionaggregate-geometry-data-type"></a>CollectionAggregate (tipo di dati geometry)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

Crea un'istanza **GeometryCollection** da un set di tipi **geometry**.
  
## <a name="syntax"></a>Sintassi  
  
```  
  
CollectionAggregate ( geometry_operand )  
```  
  
## <a name="arguments"></a>Argomenti  
 *geometry_operand*  
 Colonna della tabella di tipo **geometry** che rappresenta un set di oggetti **geometry** da elencare nell'istanza **GeometryCollection**.  
  
## <a name="return-types"></a>Tipi restituiti  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **geometry**  
  
## <a name="exceptions"></a>Eccezioni  
 Genera un'eccezione `FormatException` in presenza di valori di input non validi. Vedere [STIsValid &#40;tipo di dati geometry&#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)  
  
## <a name="remarks"></a>Osservazioni  
 Il metodo restituisce **Null** quando l'input è vuoto o dispone di SRID diversi. Vedere [Identificatori SRID &#40;Spatial Reference Identifier&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)  
  
 Il metodo ignora gli input **Null**.  
  
> [!NOTE]  
>  Il metodo restituisce **Null** se tutti i valori immessi sono **Null**.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituita un'istanza `GeometryCollection` che contiene `CurvePolygon` e `Polygon`.  
  
 ```
 -- Setup table variable for CollectionAggregate example  
 DECLARE @Geom TABLE  
 (  
 shape geometry,  
 shapeType nvarchar(50)  
 )  
 INSERT INTO @Geom(shape,shapeType) VALUES('CURVEPOLYGON(CIRCULARSTRING(2 3, 4 1, 6 3, 4 5, 2 3))', 'Circle'),  
 ('POLYGON((1 1, 4 1, 4 5, 1 5, 1 1))', 'Rectangle');  
 -- Perform CollectionAggregate on @Geom.shape column  
 SELECT geometry::CollectionAggregate(shape).ToString()  
 FROM @Geom;
 ```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di geometria statici estesi](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

