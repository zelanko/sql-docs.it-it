---
description: MultiLineString
title: MultiLineString | Microsoft Docs
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- MultiLineString geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 95deeefe-d6c5-4a11-b347-379e4486e7b7
author: MladjoA
ms.author: mlandzic
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 14b742786f8b031e1c9c80f9c058f57d96cf240a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97475382"
---
# <a name="multilinestring"></a>MultiLineString
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]
   Un'istanza **MultiLineString** è una raccolta di zero o più istanze di tipo **geometry** o **geographyLineString**.  
  
## <a name="multilinestring-instances"></a>Istanze MultiLineString  
 La figura seguente illustra esempi di istanze **MultiLineString** .  
  
 ![Esempi di istanze di geometria MultiLineString](../../relational-databases/spatial/media/multilinestring.gif "Esempi di istanze di geometria MultiLineString")  
  
 Come indicato nell'illustrazione:  
  
-   La figura 1 è un'istanza **MultiLineString** di tipo semplice il cui limite sono i quattro endpoint dei due elementi **LineString** .  
  
-   La figura 2 è un'istanza di tipo semplice **MultiLineString** perché si intersecano solo gli endpoint degli elementi **LineString** . Il limite è rappresentato dai due endpoint non sovrapposti.  
  
-   La figura 3 è un'istanza di tipo non semplice **MultiLineString** perché l'interno di uno dei suoi elementi **LineString** è intersecato. Il limite di questa istanza **MultiLineString** è rappresentato dai quattro endpoint.  
  
-   La figura 4 rappresenta un'istanza **MultiLineString** non semplice e non chiusa.  
  
-   La figura 5 rappresenta un'istanza **MultiLineString** semplice non chiusa. Non è chiusa perché gli elementi **LineString** non sono chiusi. È semplice perché nessuna delle parti interne di alcuna istanza **LineString** si interseca.  
  
-   La figura 6 rappresenta un'istanza **MultiLineString** semplice e chiusa. È chiusa perché tutti i suoi elementi sono chiusi. È semplice perché nessuno dei suoi elementi si interseca con le parti interne.  
  
### <a name="accepted-instances"></a>Istanze accettate  
 Per poter essere accettata, un'istanza **MultiLineString** deve essere vuota oppure comprendere esclusivamente istanze **LineString** accettate. Per altre informazioni sulle istanze **LineString** accettate, vedere [LineString](../../relational-databases/spatial/linestring.md). Gli esempi seguenti illustrano alcune istanze **MultiLineString** accettate.  
  
```sql  
DECLARE @g1 geometry = 'MULTILINESTRING EMPTY';  
DECLARE @g2 geometry = 'MULTILINESTRING((1 1, 3 5), (-5 3, -8 -2))';  
DECLARE @g3 geometry = 'MULTILINESTRING((1 1, 5 5), (1 3, 3 1))';  
DECLARE @g4 geometry = 'MULTILINESTRING((1 1, 3 3, 5 5),(3 3, 5 5, 7 7))';  
```  
  
L'esempio seguente genera un'eccezione `System.FormatException` , perché la seconda istanza **LineString** non è valida.  
  
```sql  
DECLARE @g geometry = 'MULTILINESTRING((1 1, 3 5),(-5 3))';  
```  
  
### <a name="valid-instances"></a>Istanze valide  
Per poter essere valida, un'istanza **MultiLineString** deve soddisfare i criteri seguenti:  
  
1.  Tutte le istanze che comprendono l'istanza **MultiLineString** devono essere istanze **LineString** valide.  
  
2.  Due istanze **LineString** che comprendono l'istanza **MultiLineString** possono sovrapporsi a un intervallo. Le istanze **LineString** possono solo intersecarsi oppure toccarsi reciprocamente o con altre istanze **LineString** in un numero finito di punti.  

L'esempio seguente indica tre istanze **MultiLineString** valide e un'istanza **MultiLineString** non valida.  
  
```sql  
DECLARE @g1 geometry = 'MULTILINESTRING EMPTY';  
DECLARE @g2 geometry = 'MULTILINESTRING((1 1, 3 5), (-5 3, -8 -2))';  
DECLARE @g3 geometry = 'MULTILINESTRING((1 1, 5 5), (1 3, 3 1))';  
DECLARE @g4 geometry = 'MULTILINESTRING((1 1, 3 3, 5 5),(3 3, 5 5, 7 7))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();  
```  
  
`@g4` non è valida, perché la seconda istanza **LineString** si sovrappone alla prima istanza **LineString** in un intervallo. Si toccano in un numero infinito di punti.  
  
## <a name="examples"></a>Esempi  
L'esempio seguente crea un'istanza `geometry``MultiLineString` che contiene due elementi `LineString` con SRID 0.  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTILINESTRING((0 2, 1 1), (1 0, 1 1))');  
```  
  
Per creare un'istanza di questa istanza con un diverso SRID, utilizzare `STGeomFromText()` o `STMLineStringFromText()`. È anche possibile utilizzare `Parse()` e quindi modificare l'identificatore SRID, come mostrato dall'esempio seguente.  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTILINESTRING((0 2, 1 1), (1 0, 1 1))');  
SET @g.STSrid = 13;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [STLength &#40;tipo di dati geometry&#41;](../../t-sql/spatial-geometry/stlength-geometry-data-type.md)   
 [STIsClosed &#40;tipo di dati geometry&#41;](../../t-sql/spatial-geometry/stisclosed-geometry-data-type.md)   
 [LineString](../../relational-databases/spatial/linestring.md)   
 [Dati spaziali &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
