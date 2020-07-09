---
title: Filter (tipo di dati geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Filter
- Filter_TSQL
- Filter (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- Filter method
ms.assetid: 82a8f54a-3a47-4e20-b13a-b148029c5448
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 79f35b2f228905d9d929d5198f20502d8c7197f3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85731160"
---
# <a name="filter-geography-data-type"></a>Filter (tipo di dati geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Metodo di intersezione basato solo su indici che consente di determinare in modo rapido se un'istanza **geography** interseca un'altra istanza **geography**, a condizione che sia disponibile un indice.  
  
 Restituisce 1 se un'istanza **geography** interseca potenzialmente un'altra istanza **geography**. Questo metodo può produrre un risultato falso positivo e il risultato esatto può dipendere dal piano. Restituisce un valore esatto 0 (risultato vero positivo) se non viene rilevata alcuna intersezione tra le istanze **geography**.  
  
 Nel caso in cui un indice non sia disponibile o non venga usato, il metodo restituisce gli stessi valori di **STIntersects()** se viene chiamato con gli stessi parametri.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.Filter ( other_geography )  
```  
  
## <a name="arguments"></a>Argomenti  
 *other_geography*  
 Altra istanza **geography** da confrontare con l'istanza sulla quale viene chiamato Filter().  
  
## <a name="return-types"></a>Tipi restituiti  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **bit**  
  
 Tipo CLR restituito: **SqlBoolean**  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo non è deterministico e non è preciso.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene utilizzato `Filter()` per determinare se due istanze `geography` si intersecano.  
  
```  
CREATE TABLE sample (id int primary key, g geography);  
INSERT INTO sample VALUES  
   (0, geography::Point(45, -120, 4326)),  
   (1, geography::Point(45, -120.1, 4326)),  
   (2, geography::Point(45, -120.2, 4326)),  
   (3, geography::Point(45, -120.3, 4326)),  
   (4, geography::Point(45, -120.4, 4326));  
  
CREATE SPATIAL INDEX sample_idx on sample(g);  
SELECT id  
FROM sample   
WHERE g.Filter(geography::Parse(  
   'POLYGON((-120.1 44.9, -119.9 44.9, -119.9 45.1, -120.1 45.1, -120.1 44.9))')) = 1;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi estesi sulle istanze di geografia](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [STIntersects &#40;tipo di dati geography&#41;](../../t-sql/spatial-geography/stintersects-geography-data-type.md)  
  
  
