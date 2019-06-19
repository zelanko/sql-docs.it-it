---
title: STPointN (tipo di dati geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STPointN_TSQL
- STPointN (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STPointN method
ms.assetid: 47670feb-b9e0-4b4b-af83-b9bba7da66ac
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 983442f724d4c2090bbface71a793bac71eb9ac7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65936094"
---
# <a name="stpointn-geography-data-type"></a>STPointN (tipo di dati geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Restituisce il punto specificato in un'istanza **geography**.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.STPointN ( expression )  
```  
  
## <a name="arguments"></a>Argomenti  
 *expression*  
 Espressione **int** compresa tra 1 e il numero di punti nell'istanza **geography**.  
  
## <a name="return-types"></a>Tipi restituiti  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **geography**  
  
 Tipo CLR restituito: **SqlGeography**  
  
 Tipo OGC (Open Geospatial Consortium): **Point**  
  
## <a name="remarks"></a>Remarks  
 Se un'istanza **geography** è creata dall'utente, restituisce il punto specificato da *expression* ordinando i punti con l'ordine di immissione originale.  
  
 Se un'istanza **geography** è costruita dal sistema, STPointN() restituisce il punto specificato da *expression* ordinando tutti i punti nello stesso ordine di restituzione, ovvero in primo luogo in base all'istanza **geography**, quindi in base all'anello all'interno dell'istanza (se appropriato), infine in base ai punti all'interno dell'anello. Questo ordine è deterministico.  
  
 Se questo metodo viene chiamato con un valore minore di 1, genera un'eccezione **ArgumentOutOfRangeException**.  
  
 Se questo metodo viene chiamato con un valore maggiore del numero di punti nell'istanza, restituisce Null.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene creata un'istanza `LineString` e viene utilizzato `STPointN()` per recuperare il secondo punto della descrizione dell'istanza.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STPointN(2).ToString();  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi OGC sulle istanze geografiche](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
