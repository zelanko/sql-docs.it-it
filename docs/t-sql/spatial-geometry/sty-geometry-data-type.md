---
description: STY (tipo di dati geometry)
title: STY (tipo di dati geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STY_TSQL
- STY (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STY (geometry Data Type)
ms.assetid: f72e0eaa-7d1d-4052-88fd-a172d8cb0d71
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: ae260a3587e3f0f9ea08829a89bfe78901cfb0e2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472391"
---
# <a name="sty-geometry-data-type"></a>STY (tipo di dati geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Proprietà relativa alla coordinata Y di un'istanza **Point**.
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.STY  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipi restituiti
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
 Tipo CLR: **SqlDouble**  
  
## <a name="remarks"></a>Osservazioni  
 Il valore di questa proprietà sarà Null se l'istanza **geometry** è un punto. Questa proprietà è di sola lettura.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene creata un'istanza `Point` e viene utilizzata `STY` per recuperare la coordinata Y dell'istanza.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(3 8)', 0);  
SELECT @g.STY;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [STX &#40;Tipo di dati geometry&#41;](../../t-sql/spatial-geometry/stx-geometry-data-type.md)   
 [STSrid &#40;tipo di dati geography&#41;](../../t-sql/spatial-geometry/stsrid-geometry-data-type.md)   
 [Metodi OGC sulle istanze di geometria](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

