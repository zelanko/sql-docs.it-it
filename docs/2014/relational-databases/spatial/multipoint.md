---
title: MultiPoint | Microsoft Docs
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- MultiPoint geometry subtype [SQL Server]
ms.assetid: 2aaab211-3aba-4dbd-90b7-095d997b1f62
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: dc25a2ea7f37086722d83113603ef178b43d86b0
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85003286"
---
# <a name="multipoint"></a>MultiPoint
  Un `MultiPoint` è una raccolta di zero o più punti. Il limite di un'istanza `MultiPoint` è vuoto.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente è creata un'istanza `geometry MultiPoint` con SRID 23 e due punti: uno con le coordinate (2, 3), e l'altro con le coordinate (7, 8) e un valore Z di 9,5.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('MULTIPOINT((2 3), (7 8 9.5))', 23);  
```  
  
 Questa istanza `MultiPoint` può essere anche espressa utilizzando `STMPointFromText()` come mostrato di seguito.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STMPointFromText('MULTIPOINT((2 3), (7 8 9.5))', 23);  
```  
  
 Nell'esempio seguente viene utilizzato il metodo `STGeometryN()` per recuperare una descrizione del primo punto nella raccolta.  
  
```  
SELECT @g.STGeometryN(1).STAsText();  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Punto](point.md)   
 [Dati spaziali &#40;SQL Server&#41;](spatial-data-sql-server.md)  
  
  
