---
title: M (tipo di dati geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- M (geometry Data Type)
- M_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- M (geometry Data Type)
ms.assetid: 443ae2ea-739b-41ef-96cc-ac5dfd65e10b
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: b8d0c4dd1b813ce5da8f0272a0c2e19e7beab1c6
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86555668"
---
# <a name="m-geometry-data-type"></a>M (tipo di dati geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Ottiene il valore **M** (misura) dell'istanza **geometry**. La semantica del valore della misura viene definita dall'utente.  

## <a name="syntax"></a>Sintassi  
  
```  
  
.M  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argomenti
  
## <a name="return-types"></a>Tipi restituiti  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
 Tipo CLR: **SqlDouble**  
  
## <a name="remarks"></a>Osservazioni  
 Il valore di questa proprietà è Null se l'istanza **geometry** non è **Point** e per qualsiasi istanza **Point** per cui la proprietà non è impostata.  
  
 Questa proprietà è di sola lettura.  
  
 I valori **M** non vengono usati in alcun calcolo eseguito dalla libreria né verranno trasferiti ad alcun calcolo della libreria.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene creata un'istanza `Point` con valori Z (innalzamento) e M (misura) valuta e viene utilizzato `M` per recuperare il valore M dell'istanza.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(1 2 3 4)', 0);  
SELECT @g.M;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi estesi sulle istanze di geometria](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [Z &#40;tipo di dati geometry&#41;](../../t-sql/spatial-geometry/z-geometry-data-type.md)   
 [AsTextZM &#40;tipo di dati geometry&#41;](../../t-sql/spatial-geometry/astextzm-geometry-data-type.md)  
  
  

