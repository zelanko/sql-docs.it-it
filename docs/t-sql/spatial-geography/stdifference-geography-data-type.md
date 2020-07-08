---
title: STDifference (tipo di dati geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STDifference_TSQL
- STDifference (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STDifference (geography Data Type)
ms.assetid: 1cde5054-b91a-41bb-812a-08c9308738af
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 39465a009ac7b7d8cc19470e3e735779337c276f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85704069"
---
# <a name="stdifference-geography-data-type"></a>STDifference (tipo di dati geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Restituisce un oggetto che rappresenta il set di punti di un'istanza **geography** che si trova all'esterno di un'altra istanza **geography**.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.STDifference ( other_geography )  
```  
  
## <a name="arguments"></a>Argomenti  
 *other_geography*  
 Altra istanza **geography** che indica i punti da rimuovere dall'istanza sulla quale viene richiamato STDifference().  
  
## <a name="return-types"></a>Tipi restituiti  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **geography**  
  
 Tipo CLR restituito: **SqlGeography**  
  
## <a name="exceptions"></a>Eccezioni  
 Questo metodo genera un'eccezione **ArgumentException** se l'istanza contiene un bordo opposto.  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo restituisce sempre Null se gli identificatori SRID delle istanze **geography** non corrispondono.  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il set di possibili risultati restituito nel server è stato esteso alle istanze **FullGlobe**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta le istanze spaziali di dimensioni maggiori di un emisfero. Il risultato può contenere segmenti di arco circolare solo se le istanze di input contengono segmenti di arco circolare. Il metodo non è preciso.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-computing-the-difference-between-two-geography-instances"></a>R. Calcolo della differenza tra due istanze di geografia  
 L'esempio seguente usa `STDifference()` per calcolare la differenza tra due istanze **geography**.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SET @h = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STDifference(@h).ToString();  
```  
  
### <a name="b-using-a-fullglobe-with-stdifference"></a>B. Utilizzo di FullGlobe con STDifference()  
 Nell'esempio seguente viene utilizzata l'istanza `FullGlobe`. Il primo risultato è un oggetto `GeometryCollection` vuoto e il secondo è un'istanza `Polygon`. `STDifference()` restituisce un oggetto `GeometryCollection` vuoto quando il parametro è un'istanza `FullGlobe`. Ogni punto in un'istanza `geography` di chiamata è contenuto in un'istanza `FullGlobe`.  
  
```
 DECLARE @g geography = 'POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 DECLARE @h geography = 'FULLGLOBE';  
 SELECT @g.STDifference(@h).ToString(),  
 @h.STDifference(@g).ToString();
 ```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi OGC sulle istanze geografiche](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
