---
title: AsTextZM (tipo di dati geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- AsTextZM (geography Data Type)
- AsTextZM_TSQL
- AsTextZM
- AsTextZM_(geography_Data_Type)_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- AsTextZM method
ms.assetid: e9dc27f6-e945-4457-8498-7644db34008e
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: a711e81c796293f9c9ac8694b1dc32e0e60f6938
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68066597"
---
# <a name="astextzm-geography-data-type"></a>AsTextZM (tipo di dati geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Restituisce una rappresentazione WKT (Well-Known Text) OGC (Open Geospatial Consortium) di un'istanza **geography** integrata con qualsiasi valore **Z** (innalzamento) e **M** (misura) appartenente all'istanza.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.AsTextZM ()  
```  
  
## <a name="return-types"></a>Tipi restituiti  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **nvarchar(max)**  
  
 Tipo CLR restituito: **SqlChars**  
  
## <a name="remarks"></a>Osservazioni  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene creata un'istanza `Point` in cui sono contenuti i valori **Z** (innalzamento) e **M** (misura). `STAsText()` consente di selezionare i valori WKT, (-122.34900 47.65100); `AsTextZM()` consente di selezionare gli stessi valori WKT e di restituire inoltre i valori per **Z** e **M**, generando (-122.34900 47.65100 10.3 12).  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100 10.3 12)', 4326);  
SELECT @g.STAsText();  
SELECT @g.AsTextZM();  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi estesi sulle istanze di geografia](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [M &#40;tipo di dati geography&#41;](../../t-sql/spatial-geography/m-geography-data-type.md)   
 [Z &#40;tipo di dati geography&#41;](../../t-sql/spatial-geography/z-geography-data-type.md)  
  
  
