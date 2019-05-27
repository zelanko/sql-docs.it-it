---
title: Dati spaziali (SQL Server) | Microsoft Docs
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- geography data type [SQL Server], spatial storage design
- planar spatial data [SQL Server], designing
- spatial data types [SQL Server]
- geodetic spatial data [SQL Server]
- geometry data type [SQL Server], spatial storage design
- spatial storage [SQL Server]
- geodetic spatial data [SQL Server], designing
ms.assetid: 41a132a1-09e2-4426-b9df-225270cb8e15
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 7bd529f67f9184f86d4a9ec704e9cf7af972f3f3
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/22/2019
ms.locfileid: "66014061"
---
# <a name="spatial-data-sql-server"></a>Dati spaziali (SQL Server)
  I dati spaziali rappresentano informazioni sulla posizione fisica e sulla forma di oggetti geometrici. Questi oggetti possono essere posizioni dei punti oppure oggetti più complessi ad esempio paesi, strade o laghi.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta due tipi di dati spaziali: il tipo di dati `geometry` e il tipo di dati `geography`.  
  
-   Questo tipo `geometry` rappresenta i dati in un sistema di coordinate euclideo (piano).  
  
-   Il tipo `geography` rappresenta i dati in un sistema di coordinate di tipo terra rotonda.  
  
 Entrambi i tipi di dati sono implementati come tipi di dati Common Language Runtime (CLR) .NET in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Per una descrizione dettagliata ed esempi delle nuove funzionalità spaziali di [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], scaricare il white paper [New Spatial Features in SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=226407)(Nuove funzionalità spaziali in SQL Server 2012).  
  
##  <a name="reltasks"></a> Attività correlate  
 [Creazione, costruzione e query di istanze geometry](create-construct-and-query-geometry-instances.md)  
 Vengono descritti i metodi da utilizzare con le istanze del tipo di dati geometry.  
  
 [Creare, Costruire e Istanze geografiche di Query](create-construct-and-query-geography-instances.md)  
 Vengono descritti i metodi che è possibile utilizzare con istanze del tipo di dati geography.  
  
 [Query dei dati spaziali per Nearest Neighbor](query-spatial-data-for-nearest-neighbor.md)  
 Viene descritto il modello di query utilizzato per trovare gli oggetti spaziali più vicini a un oggetto spaziale specifico.  
  
 [Creazione, modifica ed eliminazione di indici spaziali](create-modify-and-drop-spatial-indexes.md)  
 Fornisce informazioni sulla creazione, la modifica e il rilascio di un indice spaziale.  
  
## <a name="related-content"></a>Contenuto correlato  
 [Panoramica dei tipi di dati spaziali](spatial-data-types-overview.md)  
 Sono stati introdotti i tipi di dati spaziali.  
  
-   [Punto](point.md)  
  
-   [LineString](linestring.md)  
  
-   [CircularString](circularstring.md)  
  
-   [CompoundCurve](compoundcurve.md)  
  
-   [Poligono](polygon.md)  
  
-   [CurvePolygon](curvepolygon.md)  
  
-   [MultiPoint](multipoint.md)  
  
-   [MultiLineString](multilinestring.md)  
  
-   [MultiPolygon](multipolygon.md)  
  
-   [GeometryCollection](geometrycollection.md)  
  
 [Panoramica degli indici spaziali](spatial-indexes-overview.md)  
 Sono stati introdotti indici spaziali e vengono descritti gli schemi a mosaico.  
  
  
