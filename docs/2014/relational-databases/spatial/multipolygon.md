---
title: MultiPolygon | Microsoft Docs
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- MultiPolygon geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 2c5db358-2a16-49d9-aac5-a74e86813932
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: f18fd2485c9b2e62586d9f3e81f76f6cf680dbfc
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063009"
---
# <a name="multipolygon"></a>MultiPolygon
  Un'istanza `MultiPolygon` è una raccolta di zero o più istanze `Polygon`.

## <a name="polygon-instances"></a>Istanze Polygon
 Nella figura seguente vengono illustrati esempi di istanze `MultiPolygon`.

 ![Esempi di istanze di geometria MultiPolygon](../../database-engine/media/multipolygon.gif "Esempi di istanze di geometria MultiPolygon")

 Come indicato nell'illustrazione:

-   Nella figura 1 viene rappresentata un'istanza `MultiPolygon` con due elementi `Polygon`. Il limite è definito dai due anelli esterni e dai tre anelli interni.

-   Nella figura 2 viene rappresentata un'istanza `MultiPolygon` con due elementi `Polygon`. Il limite è definito dai due anelli esterni e dai tre anelli interni. I due elementi `Polygon` si intersecano in un punto di tangenza.

### <a name="accepted-instances"></a>Istanze accettate
 Viene accettata un'istanza `MultiPolygon` se viene soddisfatta una delle condizioni indicate di seguito.

-   È un'istanza `MultiPolygon` vuota.

-   Tutte le istanze che comprendono l'istanza `MultiPolygon` sono istanze `Polygon` accettate. Per ulteriori informazioni sulle istanze accettate `Polygon` , vedere [Polygon](../spatial/polygon.md).

 Negli esempi seguenti vengono illustrate alcune istanze `MultiPolygon` accettate.

```
DECLARE @g1 geometry = 'MULTIPOLYGON EMPTY';
DECLARE @g2 geometry = 'MULTIPOLYGON(((1 1, 1 -1, -1 -1, -1 1, 1 1)),((1 1, 3 1, 3 3, 1 3, 1 1)))';
DECLARE @g3 geometry = 'MULTIPOLYGON(((2 2, 2 -2, -2 -2, -2 2, 2 2)),((1 1, 3 1, 3 3, 1 3, 1 1)))';
```

 Nell'esempio seguente viene illustrata un'istanza MultiPolygon che genererà un'eccezione `System.FormatException`.

```
DECLARE @g geometry = 'MULTIPOLYGON(((1 1, 1 -1, -1 -1, -1 1, 1 1)),((1 1, 3 1, 3 3)))';
```

 La seconda istanza in MultiPolygon è un'istanza di LineString e non un'istanza Polygon accettata.

### <a name="valid-instances"></a>Istanze valide
 Un'istanza `MultiPolygon` è valida se è un'istanza `MultiPolygon` vuota o se soddisfa i criteri indicati di seguito.

1.  Tutte le istanze che comprendono l'istanza `MultiPolygon` sono istanze `Polygon` valide. Per le `Polygon` istanze valide, vedere [Polygon](../spatial/polygon.md).

2.  Nessuna delle istanze `Polygon` che comprendono l'istanza `MultiPolygon` si sovrappone.

 Nell'esempio seguente vengono indicate due istanze `MultiPolygon` valide e un'istanza `MultiPolygon` valida.

```
DECLARE @g1 geometry = 'MULTIPOLYGON EMPTY';
DECLARE @g2 geometry = 'MULTIPOLYGON(((1 1, 1 -1, -1 -1, -1 1, 1 1)),((1 1, 3 1, 3 3, 1 3, 1 1)))';
DECLARE @g3 geometry = 'MULTIPOLYGON(((2 2, 2 -2, -2 -2, -2 2, 2 2)),((1 1, 3 1, 3 3, 1 3, 1 1)))';
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid();
```

 `@g2` è valida perché le due istanze di `Polygon` si toccano solo in corrispondenza di un punto tangente. `@g3` non è valida perché gli interni delle due istanze di `Polygon` si sovrappongono.

## <a name="examples"></a>Esempi
 L'esempio seguente illustra la creazione di un'istanza `geometry``MultiPolygon` e viene restituito il Well-Known Text (WKT) del secondo componente.

```
DECLARE @g geometry;
SET @g = geometry::Parse('MULTIPOLYGON(((0 0, 0 3, 3 3, 3 0, 0 0), (1 1, 1 2, 2 1, 1 1)), ((9 9, 9 10, 10 9, 9 9)))');
SELECT @g.STGeometryN(2).STAsText();
```

 In questo esempio viene creata un'istanza `MultiPolygon` vuota.

```
DECLARE @g geometry;
SET @g = geometry::Parse('MULTIPOLYGON EMPTY');
```

## <a name="see-also"></a>Vedere anche
 [Poligono](../spatial/polygon.md) [STArea &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/starea-geometry-data-type) [STCentroid &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stcentroid-geometry-data-type) [STPointOnSurface &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stpointonsurface-geometry-data-type) [dati spaziali](../spatial/spatial-data-sql-server.md) &#40;SQL Server&#41;


