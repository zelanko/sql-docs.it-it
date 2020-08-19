---
description: STIsClosed (tipo di dati geometry)
title: STIsClosed (tipo di dati geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STIsClosed_TSQL
- STIsClosed (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STIsClosed (geometry Data Type)
ms.assetid: 14edbb22-df7b-4b8a-b16c-ac477a5d32c1
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: c92d311ba67c71f77fef8052bcfe8e5938d1f1b5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88445039"
---
# <a name="stisclosed-geometry-data-type"></a>STIsClosed (tipo di dati geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Restituisce 1 se i punti di inizio e di fine dell'istanza **geometry** specificata sono gli stessi. Restituisce 1 per i tipi **geometrycollection** se ogni istanza **geometry** contenuta è chiusa. Restituisce 0 se l'istanza non è chiusa.
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.STIsClosed ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipi restituiti
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **bit**  
  
 Tipo CLR restituito: **SqlBoolean**  
  
## <a name="remarks"></a>Commenti  
 Questo metodo restituisce 0 se una figura di un'istanza **geometry** è costituita da punti o se l'istanza è vuota.  
  
 Tutte le istanze **Polygon** sono considerate chiuse.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene creata un'istanza `LineString` e viene utilizzato `STIsClosed()` per verificare se l'istanza `LineString` è chiusa.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STIsClosed();  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi OGC sulle istanze di geometria](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

