---
description: EnvelopeAggregate (tipo di dati geography)
title: EnvelopeAggregate (tipo di dati geography) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- EnvelopeAggregate_TSQL
- EnvelopeAggregate
dev_langs:
- TSQL
helpviewer_keywords:
- EnvelopeAggregate method (geography)
ms.assetid: 4947797f-edb8-490f-beca-37df9ec06954
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 9b14db5a616f41049b5cabc845cd822356e34522
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/25/2020
ms.locfileid: "96114997"
---
# <a name="envelopeaggregate-geography-data-type"></a>EnvelopeAggregate (tipo di dati geography)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

Restituisce un oggetto di delimitazione per un set specificato di oggetti **geography**. L'oggetto **geography** risultante contiene più segmenti di arco circolare.
  
## <a name="syntax"></a>Sintassi  
  
```  
  
EnvelopeAggregate ( geography_operand )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argomenti
 *geography_operand*  
 Colonna della tabella di tipo **geography** che contiene il set di oggetti **geography** in cui eseguire un'operazione di aggregazione della busta.  
  
## <a name="return-types"></a>Tipi restituiti  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **geography**  
  
## <a name="remarks"></a>Osservazioni  
 Quando l'oggetto di delimitazione risultante ha dimensioni maggiori di un emisfero, viene restituito un oggetto **FullGlobe**. Il metodo non è preciso.  
  
 Il metodo restituisce **null** se l'input dispone di SRID diversi. Vedere [Identificatori SRID &#40;Spatial Reference Identifier&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md).  
  
 Il metodo ignora gli input **Null**.  
  
> [!NOTE]  
>  Il metodo restituisce **Null** se tutti i valori immessi sono **Null**.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene eseguito `EnvelopeAggregate` in un set di punti di percorso **geography** all'interno di una città.  
  
 ```
 USE AdventureWorks2012  
 GO  
 SELECT City,  
 geography::EnvelopeAggregate(SpatialLocation) AS SpatialLocation  
 FROM Person.Address  
 WHERE PostalCode LIKE('981%')  
 GROUP BY City;
 ```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi geography statici estesi](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  
