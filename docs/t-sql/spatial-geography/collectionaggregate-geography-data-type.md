---
title: CollectionAggregate (tipo di dati geography) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- CollectionAggregate method (geography)
ms.assetid: e49a644a-dbf2-46c3-98f5-4b3ec197e2ad
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 20c7279bc5b7dae0b8bf80ae86508ea77f9cd83e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65935465"
---
# <a name="collectionaggregate-geography-data-type"></a>CollectionAggregate (tipo di dati geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Crea un'istanza **GeometryCollection** da un set di oggetti **geography**.
  
## <a name="syntax"></a>Sintassi  
  
```  
  
ConvexHullAggregate ( geography_operand )  
```  
  
## <a name="arguments"></a>Argomenti  
 *geography_operand*  
 Colonna della tabella di tipo **geography** che rappresenta un set di oggetti **geography** da elencare nell'istanza **GeometryCollection**.  
  
## <a name="return-types"></a>Tipi restituiti  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **geography**  
  
## <a name="exception"></a>Eccezione  
 Genera un'eccezione `FormatException` in presenza di valori di input non validi. Vedere [STIsValid &#40;tipo di dati geography&#41;](../../t-sql/spatial-geography/stisvalid-geography-data-type.md)  
  
## <a name="remarks"></a>Remarks  
 Il metodo restituisce **Null** quando l'input è vuoto o dispone di SRID diversi. Vedere [Identificatori SRID &#40;Spatial Reference Identifier&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)  
  
 Il metodo ignora gli input **Null**.  
  
> [!NOTE]  
>  Il metodo restituisce **Null** se tutti i valori immessi sono **Null**.  
  
## <a name="examples"></a>Esempi  
 L'esempio seguente restituisce un'istanza `GeometryCollection` che contiene un set di oggetti **geography**.  
  
 ```
 USE AdventureWorks2012  
 GO  
 SELECT geography::CollectionAggregate(SpatialLocation).ToString() AS SpatialLocation  
 FROM Person.Address  
 WHERE City LIKE ('Bothell')
 ```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi geography statici estesi](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  
