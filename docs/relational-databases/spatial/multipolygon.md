---
title: MultiPolygon | Microsoft Docs
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- MultiPolygon geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 2c5db358-2a16-49d9-aac5-a74e86813932
author: MladjoA
ms.author: mlandzic
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8522e65762e8c27ec65fb5fc4a56db0653b5f5c9
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "72907011"
---
# <a name="multipolygon"></a>MultiPolygon
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Un'istanza **MultiPolygon** è una raccolta di zero o più istanze **Polygon** .  
  
## <a name="polygon-instances"></a>Istanze Polygon  
 Nella figura seguente vengono illustrati esempi di istanze **MultiPolygon** .  
  
 ![Esempi di istanze di geometria MultiPolygon](../../relational-databases/spatial/media/multipolygon.gif "Esempi di istanze di geometria MultiPolygon")  
  
 Come indicato nell'illustrazione:  
  
-   La figura 1 rappresenta un'istanza **MultiPolygon** con due elementi **Polygon** . Il limite è definito dai due anelli esterni e dai tre anelli interni.  
  
-   La figura 2 rappresenta un'istanza **MultiPolygon** con due elementi **Polygon** . Il limite è definito dai due anelli esterni e dai tre anelli interni. I due elementi **Polygon** si intersecano in un punto di tangenza.  
  
### <a name="accepted-instances"></a>Istanze accettate  
 Viene accettata un'istanza **MultiPolygon** se viene soddisfatta una delle condizioni indicate di seguito.  
  
-   È un'istanza **MultiPolygon** vuota.  
  
-   Tutte le istanze che comprendono l'istanza **MultiPolygon** sono istanze **Polygon** accettate. Per altre informazioni sulle istanze **Polygon** accettate, vedere [Polygon](../../relational-databases/spatial/polygon.md).  
  
Negli esempi seguenti vengono illustrate alcune istanze **MultiPolygon** accettate.  
  
```sql  
DECLARE @g1 geometry = 'MULTIPOLYGON EMPTY';  
DECLARE @g2 geometry = 'MULTIPOLYGON(((1 1, 1 -1, -1 -1, -1 1, 1 1)),((1 1, 3 1, 3 3, 1 3, 1 1)))';  
DECLARE @g3 geometry = 'MULTIPOLYGON(((2 2, 2 -2, -2 -2, -2 2, 2 2)),((1 1, 3 1, 3 3, 1 3, 1 1)))';  
```  
  
Nell'esempio seguente viene illustrata un'istanza MultiPolygon che genererà un'eccezione `System.FormatException`.  
  
```sql  
DECLARE @g geometry = 'MULTIPOLYGON(((1 1, 1 -1, -1 -1, -1 1, 1 1)),((1 1, 3 1, 3 3)))';  
```  
  
La seconda istanza in MultiPolygon è un'istanza di LineString e non un'istanza Polygon accettata.  
  
### <a name="valid-instances"></a>Istanze valide  
 Un'istanza **MultiPolygon** è valida se è un'istanza **MultiPolygon** vuota o se soddisfa i criteri indicati di seguito.  
  
1.  Tutte le istanze che comprendono l'istanza **MultiPolygon** sono istanze **Polygon** valide. Per le istanze **Polygon** valide, vedere [Polygon](../../relational-databases/spatial/polygon.md).  
  
2.  Nessuna delle istanze **Polygon** che compongono l'istanza **MultiPolygon** si sovrappone.  

Nell'esempio seguente sono indicate due istanze **MultiPolygon** valide e un'istanza **MultiPolygon** non valida.  
  
```sql  
DECLARE @g1 geometry = 'MULTIPOLYGON EMPTY';  
DECLARE @g2 geometry = 'MULTIPOLYGON(((1 1, 1 -1, -1 -1, -1 1, 1 1)),((1 1, 3 1, 3 3, 1 3, 1 1)))';  
DECLARE @g3 geometry = 'MULTIPOLYGON(((2 2, 2 -2, -2 -2, -2 2, 2 2)),((1 1, 3 1, 3 3, 1 3, 1 1)))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid();  
```  
  
`@g2` è valida perché le due istanze **Polygon** si toccano solo in corrispondenza di un punto tangente. `@g3` non è valida perché gli interni delle due istanze **Polygon** si sovrappongono.  
  
## <a name="examples"></a>Esempi  
### <a name="example-a"></a>Esempio A.
L'esempio seguente illustra la creazione di un'istanza `geometry``MultiPolygon` e viene restituito il Well-Known Text (WKT) del secondo componente.  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTIPOLYGON(((0 0, 0 3, 3 3, 3 0, 0 0), (1 1, 1 2, 2 1, 1 1)), ((9 9, 9 10, 10 9, 9 9)))');  
SELECT @g.STGeometryN(2).STAsText();  
```  
  
## <a name="example-b"></a>Esempio B.
In questo esempio viene creata un'istanza `MultiPolygon` vuota.  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTIPOLYGON EMPTY');  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Polygon](../../relational-databases/spatial/polygon.md)   
 [STArea &#40;tipo di dati geometry&#41;](../../t-sql/spatial-geometry/starea-geometry-data-type.md)   
 [STCentroid &#40;tipo di dati geometry&#41;](../../t-sql/spatial-geometry/stcentroid-geometry-data-type.md)   
 [STPointOnSurface &#40;tipo di dati geometry&#41;](../../t-sql/spatial-geometry/stpointonsurface-geometry-data-type.md)   
 [Dati spaziali &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
