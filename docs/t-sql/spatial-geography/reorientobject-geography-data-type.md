---
title: ReorientObject (tipo di dati geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ReorientObject
- ReorientObject_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ReorientObject method (geography)
ms.assetid: e2a1a4f1-211b-4e82-abed-03fc7140a83c
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 2cb6064347176b34e4141e8c7c5c3bf466669145
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85705674"
---
# <a name="reorientobject-geography-data-type"></a>ReorientObject (tipo di dati geography)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

Restituisce un'istanza **geography** con aree esterne e interne scambiate.  
  
Questo metodo con tipo di dati **geography** supporta le istanze **FullGlobe** o le istanze spaziali con dimensioni maggiori di un emisfero.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.ReorientObject (geography)  
```  
  
## <a name="arguments"></a>Argomenti  
_geography_  
Altra istanza **geography** su cui viene richiamato `ReorientObject()`.  
  
## <a name="return-value"></a>Valore restituito  
Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **geography**  
  
Tipo CLR restituito: **SqlGeography**  
  
## <a name="remarks"></a>Osservazioni  
Questo metodo modifica l'orientamento dell'anello di tutti gli oggetti **Polygon** in un oggetto **GeometryCollection**, ma non rimuove né modifica alcun oggetto **Point** o **LineString** nella raccolta specificata.  
  
Se si passa un oggetto **GeometryCollection** a questo metodo, viene modificato l'orientamento di ogni istanza nella raccolta, ma tale operazione non si applica alla raccolta stessa.  
  
## <a name="examples"></a>Esempi  
  
```  
DECLARE @R GEOGRAPHY = GEOGRAPHY::Parse('Polygon((-10 -10, -10 10, 10 10, 10 -10, -10 -10))');  
SELECT @R.ReorientObject().STAsText();  
--Result: POLYGON ((10 10, -10 10, -10 -10, 10 -10, 10 10))  
```  
  
## <a name="see-also"></a>Vedere anche  
[Metodi estesi sulle istanze geografiche](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
