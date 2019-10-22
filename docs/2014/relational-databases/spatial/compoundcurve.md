---
title: CompoundCurve | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: ae357f9b-e3e2-4cdf-af02-012acda2e466
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 48d1ca9458b4993ad509cc2bbedd8d23b127918c
ms.sourcegitcommit: 82a1ad732fb31d5fa4368c6270185c3f99827c97
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/21/2019
ms.locfileid: "72688676"
---
# <a name="compoundcurve"></a>CompoundCurve
  `CompoundCurve` è una raccolta di zero o più istanze `CircularString` o `LineString` continue di tipo geometry o geography.  
  
> [!IMPORTANT]  
>  Per una descrizione dettagliata ed esempi delle nuove funzionalità spaziali di questa versione, incluso il sottotipo `CompoundCurve`, scaricare il white paper, [nuove funzionalità spaziali in SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=226407).  
  
 È possibile creare un'istanza `CompoundCurve` vuota, ma affinché `CompoundCurve` sia valida è necessario che vengano rispettati i criteri seguenti:  
  
1.  Deve contenere almeno un'istanza `CircularString` o `LineString`.  
  
2.  La sequenza di istanze `CircularString` o `LineString` deve essere continua.  
  
 Se un `CompoundCurve` contiene una sequenza di più istanze `CircularString` e `LineString`, l'endpoint finale per ogni istanza, ad eccezione dell'ultima istanza, deve essere l'endpoint iniziale per l'istanza successiva nella sequenza. Ciò significa che se il punto finale di un'istanza precedente nella sequenza è (4 3 7 2), il punto iniziale dell'istanza successiva nella sequenza deve essere (4 3 7 2). Si noti che i valori Z (elevazione) e M (misura) del punto devono essere anch'essi uguali. Nel caso di una differenza nei due punti, viene generata un'eccezione `System.FormatException` . I punti in un'istanza `CircularString` non devono avere un valore Z o M. Se non sono presenti valori Z o M per il punto finale dell'istanza precedente, il punto iniziale dell'istanza successiva non potrà includere valori Z o M. Se il punto finale della sequenza precedente è (4 3), il punto iniziale della sequenza successiva dovrà essere (4 3). Non potrà essere (4 3 7 2). Tutti i punti in un'istanza `CompoundCurve` non devono avere alcun valore Z oppure devono avere lo stesso valore Z.  
  
## <a name="compoundcurve-instances"></a>Istanze CompoundCurve  
 Nell'immagine seguente sono illustrati tipi di `CompoundCurve` validi.  
  
 ![](../../database-engine/media/f278742e-b861-4555-8b51-3d972b7602bf.png "f278742e-b861-4555-8b51-3d972b7602bf")  
  
### <a name="accepted-instances"></a>Istanze accettate  
 L'istanza `CompoundCurve` viene accettata se è un'istanza vuota o se soddisfa i criteri seguenti.  
  
1.  Tutte le istanze contenute nell'istanza `CompoundCurve` sono istanze di segmenti di arco circolare accettate. Per altre informazioni sulle istanze di segmenti di arco circolare accettate, vedere [LineString](linestring.md) e [CircularString](circularstring.md).  
  
2.  Tutti i segmenti di arco circolare nell'istanza `CompoundCurve` sono connessi. Il primo punto di ogni segmento di arco circolare successivo è uguale all'ultimo punto del segmento di arco circolare precedente.  
  
    > [!NOTE]  
    >  Sono incluse le coordinate Z e M. È quindi necessario che tutte e quattro le coordinate X, Y, Z e M siano uguali.  
  
3.  Nessuna delle istanze contenute è un'istanza vuota.  
  
 Nell'esempio seguente vengono illustrate le istanze `CompoundCurve` accettate.  
  
```  
DECLARE @g1 geometry = 'COMPOUNDCURVE EMPTY';  
DECLARE @g2 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 0, 0 1, -1 0), (-1 0, 2 0))';  
```  
  
 Nell'esempio seguente vengono illustrate le istanze `CompoundCurve` non accettate. Queste istanze generano un'eccezione `System.FormatException`.  
  
```  
DECLARE @g1 geometry = 'COMPOUNDCURVE(CIRCULARSTRING EMPTY)';  
DECLARE @g2 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 0, 0 1, -1 0), (1 0, 2 0))';  
```  
  
### <a name="valid-instances"></a>Istanze valide  
 Un'istanza `CompoundCurve` è valida se soddisfa i criteri seguenti.  
  
1.  L'istanza `CompoundCurve` è accettata.  
  
2.  Tutte le istanze di segmenti di arco circolare contenute nell'istanza `CompoundCurve` sono istanze valide.  
  
 Nell'esempio seguente vengono illustrate le istanze `CompoundCurve` valide.  
  
```  
DECLARE @g1 geometry = 'COMPOUNDCURVE EMPTY';  
DECLARE @g2 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 0, 0 1, -1 0), (-1 0, 2 0))';  
DECLARE @g3 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 1, 1 1, 1 1), (1 1, 3 5, 5 4))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid();  
  
```  
  
 `@g3` è valida perché l'istanza `CircularString` è valida. Per ulteriori informazioni sulla validità dell'istanza di `CircularString`, vedere [CircularString](circularstring.md).  
  
 Nell'esempio seguente vengono illustrate le istanze `CompoundCurve` non valide.  
  
```  
DECLARE @g1 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 1, 1 1, 1 1), (1 1, 3 5, 5 4, 3 5))';  
DECLARE @g2 geometry = 'COMPOUNDCURVE((1 1, 1 1))';  
DECLARE @g3 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 1, 2 3, 1 1))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid();  
```  
  
 `@g1` non è valida perché la seconda istanza non è un'istanza LineString valida. `@g2` non è valida perché l'istanza `LineString` non è valida. `@g3` non è valida perché l'istanza `CircularString` non è valida. Per ulteriori informazioni sulle istanze valide `CircularString` e `LineString`, vedere [CircularString](circularstring.md) e [LineString](linestring.md).  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-instantiating-a-geometry-instance-with-an-empty-compooundcurve"></a>A. Creazione di un'istanza Geometry con un'istanza CompoundCurve vuota  
 Nell'esempio seguente viene illustrato come creare un'istanza `CompoundCurve` vuota:  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('COMPOUNDCURVE EMPTY');  
```  
  
### <a name="b-declaring-and-instantiating-a-geometry-instance-using-a-compoundcurve-in-the-same-statement"></a>b. Dichiarazione e creazione di un'istanza Geometry utilizzando un'istanza CompoundCurve nella stessa istruzione  
 L'esempio seguente illustra come dichiarare e inizializzare un'istanza `geometry` con un'istanza `CompoundCurve`nella stessa istruzione:  
  
```sql  
DECLARE @g geometry = 'COMPOUNDCURVE ((2 2, 0 0),CIRCULARSTRING (0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0))';  
```  
  
### <a name="c-instantiating-a-geography-instance-with-a-compoundcurve"></a>C. Creazione di un'istanza Geography con un'istanza CompoundCurve  
 Nell'esempio seguente viene illustrato come dichiarare e inizializzare un'istanza `geography` con un'istanza `CompoundCurve`:  
  
```sql  
DECLARE @g geography = 'COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
```  
  
### <a name="d-storing-a-square-in-a-compoundcurve-instance"></a>D. Archiviazione di un quadrato in un'istanza CompoundCurve  
 Nell'esempio seguente vengono utilizzate due diverse modalità per archiviare un quadrato tramite un'istanza `CompoundCurve` .  
  
```sql  
DECLARE @g1 geometry, @g2 geometry;  
SET @g1 = geometry::Parse('COMPOUNDCURVE((1 1, 1 3), (1 3, 3 3),(3 3, 3 1), (3 1, 1 1))');  
SET @g2 = geometry::Parse('COMPOUNDCURVE((1 1, 1 3, 3 3, 3 1, 1 1))');  
SELECT @g1.STLength(), @g2.STLength();  
```  
  
 Le lunghezze per `@g1` e `@g2` sono le stesse. Come illustrato nell'esempio, un'istanza `CompoundCurve` consente di archiviare una o più istanze di `LineString`.  
  
### <a name="e-instantiating-a-geometry-instance-using-a-compoundcurve-with-multiple-circularstrings"></a>E. Creazione di un'istanza Geometry utilizzando un'istanza CompoundCurve con più istanze CircularString  
 Nell'esempio seguente viene illustrato come utilizzare due diverse istanze `CircularString` per creare un'istanza `CompoundCurve`:  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), CIRCULARSTRING(4 2, 2 4, 0 2))');  
SELECT @g.STLength();  
```  
  
 Viene generato l'output seguente: 12,566370... che è l'equivalente di 4&#x03c0; (4 * pi). L'istanza `CompoundCurve` riportata nell'esempio consente di archiviare un cerchio con un raggio di 2. In entrambi gli esempi di codice precedenti non è stato necessario utilizzare un'istanza `CompoundCurve`. Per il primo esempio sarebbe stata più semplice un'istanza `LineString` , mentre per il secondo esempio sarebbe stata più semplice un'istanza `CircularString` . Nell'esempio successivo viene tuttavia illustrato in quale punto un'istanza `CompoundCurve` costituisce una migliore alternativa.  
  
### <a name="f-using-a-compoundcurve-to-store-a-semicircle"></a>F. Utilizzo di un'istanza CompoundCurve per archiviare un semicerchio  
 Nell'esempio seguente viene utilizzata un'istanza `CompoundCurve` per archiviare un semicerchio.  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), (4 2, 0 2))');  
SELECT @g.STLength();  
```  
  
### <a name="g-storing-multiple-circularstring-and-linestring-instances-in-a-compoundcurve"></a>G. Archiviazione di più istanze CircularString e LineString in un'istanza CompoundCurve  
 Nell'esempio seguente viene illustrato come è possibile archiviare più istanze `CircularString` e `LineString` tramite un'istanza `CompoundCurve`.  
  
```sql  
DECLARE @g geometry  
SET @g = geometry::Parse('COMPOUNDCURVE((3 5, 3 3), CIRCULARSTRING(3 3, 5 1, 7 3), (7 3, 7 5), CIRCULARSTRING(7 5, 5 7, 3 5))');  
SELECT @g.STLength();  
```  
  
### <a name="h-storing-instances-with-z-and-m-values"></a>H. Archiviazione di istanze con valori Z e M  
 Nell'esempio seguente viene illustrato come utilizzare un'istanza `CompoundCurve` per archiviare una sequenza di istanze `CircularString` e `LineString` con valori Z e M.  
  
```sql  
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(7 5 4 2, 5 7 4 2, 3 5 4 2), (3 5 4 2, 8 7 4 2))');  
```  
  
### <a name="i-illustrating-why-circularstring-instances-must-be-explicitly-declared"></a>I. Descrizione del motivo per cui le istanze CircularString devono essere dichiarate in modo esplicito  
 Nell'esempio seguente viene illustrato il motivo per cui è necessario dichiarare in modo esplicito le istanze `CircularString` . Il programmatore sta tentando di archiviare un cerchio in un'istanza `CompoundCurve` .  
  
```sql  
DECLARE @g1 geometry;    
DECLARE @g2 geometry;  
SET @g1 = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), (4 2, 2 4, 0 2))');  
SELECT 'Circle One', @g1.STLength() AS Perimeter;  -- gives an inaccurate amount  
SET @g2 = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), CIRCULARSTRING(4 2, 2 4, 0 2))');  
SELECT 'Circle Two', @g2.STLength() AS Perimeter;  -- now we get an accurate amount  
```  
  
 L'output è il seguente:  
  
```  
Circle One11.940039...  
Circle Two12.566370...  
```  
  
 Il perimetro per Circle Two è approssimativamente&#x03c0; 4 (4 * pi), ovvero il valore effettivo del perimetro. Il perimetro per Circle One, tuttavia, è significativamente impreciso. L'istanza `CompoundCurve` di Circle One consente l'archiviazione di un segmento di arco circolare (ABC) e di due segmenti di linea (CD, DA). Tramite l'istanza `CompoundCurve` devono essere archiviati due segmenti di arco circolare (ABC, CDA) per definire un cerchio. Tramite un'istanza `LineString` viene definito il secondo set di punti (4 2, 2 4, 0 2) nell'istanza `CompoundCurve` di Circle One. È necessario dichiarare in modo esplicito un'istanza `CircularString` in un'istanza `CompoundCurve`.  
  
## <a name="see-also"></a>Vedere anche  
 [STIsValid &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stisvalid-geometry-data-type)   
 [STLength &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stlength-geometry-data-type)   
 [STStartPoint &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/ststartpoint-geometry-data-type)   
 [STEndpoint &#40;tipo di dati geometry&#41;](/sql/t-sql/spatial-geometry/stendpoint-geometry-data-type)   
 [LineString](linestring.md)   
 [CircularString](circularstring.md)   
 [Panoramica dei tipi di dati spaziali](spatial-data-types-overview.md)   
 [Point](point.md)  
  
  
