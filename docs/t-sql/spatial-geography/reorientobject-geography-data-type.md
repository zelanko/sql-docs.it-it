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
manager: craigg
ms.openlocfilehash: e2945b08eaf0a22c6c83bd412e97c729bedfdfea
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/20/2019
ms.locfileid: "65936346"
---
# <a name="reorientobject-geography-data-type"></a>ReorientObject (tipo di dati geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

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
  
## <a name="remarks"></a>Remarks  
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
  
