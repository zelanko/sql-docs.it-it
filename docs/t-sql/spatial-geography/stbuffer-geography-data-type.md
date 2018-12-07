---
title: STBuffer (tipo di dati geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STBuffer (geography Data Type)
- STBuffer_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STBuffer (geography Data Type)
ms.assetid: cb4deab8-642b-44d9-b3d9-85114d64021e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a7a09c5653fe89528c49ade19e044066acfb34cd
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52403706"
---
# <a name="stbuffer-geography-data-type"></a>STBuffer (tipo di dati geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Restituisce un oggetto geografico che rappresenta l'unione di tutti i punti la cui distanza da un'istanza **geography** è minore o uguale a un valore specificato.  
  
 Questo metodo con tipo di dati geography supporta le istanze **FullGlobe** o le istanze spaziali con dimensioni maggiori di un emisfero.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.STBuffer ( distance )  
```  
  
## <a name="arguments"></a>Argomenti  
 *distance*  
 Valore di tipo **float** (**double** in .NET Framework) che specifica la distanza dall'istanza **geography** intorno alla quale calcolare il buffer.  
  
 La distanza massima del buffer non può superare 0,999 \* *π* * minorAxis \* minorAxis / majorAxis (~0,999 \* 1/2 della circonferenza della Terra) o l'intero globo.  
  
## <a name="return-types"></a>Tipi restituiti  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **geography**  
  
 Tipo CLR restituito: **SqlGeography**  
  
## <a name="remarks"></a>Osservazioni  
 STBuffer() calcola un buffer in modo analogo a [BufferWithTolerance](../../t-sql/spatial-geography/bufferwithtolerance-geography-data-type.md), specificando *tolerance* = abs(distance) \* 0,001 e *relative* = **false**.  
  
 Un buffer negativo consente di rimuovere tutti i punti all'interno della distanza specificata del limite dell'istanza **geography**.  
  
 `STBuffer()` restituisce un'istanza **FullGlobe** in determinati casi; ad esempio, `STBuffer()` restituisce un'istanza **FullGlobe** quando la distanza del buffer è maggiore della distanza dall'equatore ai poli. Un buffer non può superare l'intero globo.  
  
 Questo metodo genererà un'eccezione **ArgumentException** nelle istanze **FullGlobe** in cui la distanza del buffer supera il limite seguente:  
  
 0,999 \* *π* * minorAxis \* minorAxis / majorAxis (~0,999 \* 1/2 della circonferenza della Terra)  
  
 Il limite massimo della distanza consente la massima flessibilità per la costruzione del buffer.  
  
 L'errore tra il buffer calcolato e quello teorico è max(tolerance, extents * 1.E-7) dove tolerance = distance \* 0,001. Per altre informazioni sulle estensioni, vedere la [Guida di riferimento ai metodi per il tipo di dati geography](https://msdn.microsoft.com/library/028e6137-7128-4c74-90a7-f7bdd2d79f5e).  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene creata un'istanza `LineString``geography`. e viene utilizzato `STBuffer()` per restituire l'area all'interno di 1 metro dell'istanza.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STBuffer(1).ToString();  
```  
  
## <a name="see-also"></a>Vedere anche  
 [BufferWithTolerance &#40;tipo di dati geography&#41;](../../t-sql/spatial-geography/bufferwithtolerance-geography-data-type.md)   
 [Metodi OGC sulle istanze geografiche](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
