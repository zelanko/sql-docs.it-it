---
title: STPointFromWKB (tipo di dati geography) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STPointFromWKB_TSQL
- STPointFromWKB (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STPointFromWKB method
ms.assetid: b3b4e3bb-47bc-4621-99c4-c97aa60cdf8b
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 97c519350024947ed6854554526b65754c6621a2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68120831"
---
# <a name="stpointfromwkb-geography-data-type"></a>STPointFromWKB (tipo di dati geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Restituisce un'istanza **geographyPoint** di una rappresentazione WKB (Well-Known Binary) OGC (Open Geospatial Consortium).
  
## <a name="syntax"></a>Sintassi  
  
```  
  
STPointFromWKB ( 'WKB_point' , SRID )  
```  
  
## <a name="arguments"></a>Argomenti  
 *WKB_point*  
 Rappresentazione WKB dell'istanza **geographyPoint** da restituire. *WKB_point* è un'espressione **varbinary(max)**.  
  
 *SRID*  
 Espressione **int** che rappresenta l'identificatore SRID dell'istanza **geographyPoint** da restituire.  
  
## <a name="return-types"></a>Tipi restituiti  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **geography**  
  
 Tipo CLR restituito: **SqlGeography**  
  
 Tipo OGC: **Point**  
  
## <a name="remarks"></a>Remarks  
 Questo metodo genera un'eccezione **FormatException** se l'input non è formattato in modo corretto.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene utilizzato il metodo `STPointFromWKB()` per creare un'istanza `geography`.  
  
```  
DECLARE @g geography;  
SET @g = geography::STPointFromWKB(0x010100000017D9CEF753D347407593180456965EC0, 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi geography statici OGC](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
