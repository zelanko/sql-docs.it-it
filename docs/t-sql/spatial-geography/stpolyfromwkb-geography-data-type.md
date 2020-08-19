---
description: STPolyFromWKB (tipo di dati geography)
title: STPolyFromWKB (tipo di dati geography) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STPolyFromWKB_TSQL
- STPolyFromWKB (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STPolyFromWKB method
ms.assetid: d236e0ea-dabe-4341-a6eb-ecc210d1f056
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: caa7913e9971a11413933ad2998f0d6042c9f4ca
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88422335"
---
# <a name="stpolyfromwkb-geography-data-type"></a>STPolyFromWKB (tipo di dati geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Restituisce un'istanza **geographyPolygon** di una rappresentazione WKB (Well-Known Binary) OGC (Open Geospatial Consortium).
  
## <a name="syntax"></a>Sintassi  
  
```  
  
STPolyFromWKB ( 'WKB_polygon' , SRID )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argomenti
 *WKB_polygon*  
 Rappresentazione WKB dell'istanza **geographyPolygon** da restituire. *WKB_polygon* è un'espressione **varbinary(max)**.  
  
 *SRID*  
 Espressione **int** che rappresenta l'identificatore SRID dell'istanza **geographyPolygon** da restituire.  
  
## <a name="return-types"></a>Tipi restituiti  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **geography**  
  
 Tipo CLR restituito: **SqlGeography**  
  
 Tipo OGC: **Polygon**  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo genera un'eccezione **FormatException** se l'input non è formattato in modo corretto.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene utilizzato il metodo `STPolyFromWKB()` per creare un'istanza `geography`.  
  
```  
DECLARE @g geography;   
SET @g = geography::STPolyFromWKB(0x01030000000100000005000000F4FDD478E9965EC0DD24068195D3474083C0CAA145965EC0508D976E12D3474083C0CAA145965EC04E62105839D44740F4FDD478E9965EC04E62105839D44740F4FDD478E9965EC0DD24068195D34740, 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi geography statici OGC](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
