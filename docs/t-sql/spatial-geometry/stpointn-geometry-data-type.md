---
title: STPointN (tipo di dati geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STPointN_TSQL
- STPointN (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STPointN (geometry Data Type)
ms.assetid: 8f0bb3b7-5cd9-42c2-b9f8-f04628653bd0
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: f7bbaf25715275b14deda0f2a510b40934c6f33e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65938376"
---
# <a name="stpointn-geometry-data-type"></a>STPointN (tipo di dati geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Restituisce un punto specificato in un'istanza **geometry**.
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.STPointN ( expression )  
```  
  
## <a name="arguments"></a>Argomenti  
 *expression*  
 Espressione **int** compresa tra 1 e il numero di punti nell'istanza **geometry**.  
  
## <a name="return-types"></a>Tipi restituiti  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **geometry**  
  
 Tipo CLR restituito: **SqlGeometry**  
  
 Tipo OGC (Open Geospatial Consortium): **Point**  
  
## <a name="remarks"></a>Remarks  
 Se un'istanza **geometry** è creata dall'utente, `STPointN()` restituisce il punto specificato da *expression* ordinando i punti con l'ordine di immissione originale.  
  
 Se un'istanza **geometry** è stata costruita dal sistema, `STPointN()` restituisce il punto specificato da *expression* ordinando tutti i punti nello stesso ordine di restituzione, ovvero prima in base alla geometria, quindi in base all'anello all'interno della geometria (se appropriato), infine in base ai punti all'interno dell'anello. Questo ordine è deterministico.  
  
 Se questo metodo viene chiamato con un valore minore di 1, genera un'eccezione **ArgumentOutOfRangeException**.  
  
 Se questo metodo viene chiamato con un valore maggiore del numero di punti nell'istanza, restituisce Null.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene creata un'istanza `LineString` e viene utilizzato `STPointN()` per recuperare il secondo punto della descrizione dell'istanza.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STPointN(2).ToString();  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi OGC sulle istanze di geometria](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

