---
description: Null (tipo di dati geometry)
title: Null (tipo di dati geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Null (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- Null (geometry Data Type)
ms.assetid: 67a4b019-9091-4443-85cc-f4836d0cb509
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 616ce209c7f2a047223267165fafd675455b3d47
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88479283"
---
# <a name="null-geometry-data-type"></a>Null (tipo di dati geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Proprietà di sola lettura che restituisce un'istanza Null del tipo **geometry**.
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Null  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argomenti
  
## <a name="return-types"></a>Tipi restituiti  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Osservazioni  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene recuperata un'istanza `geometry` Null.  
  
```  
DECLARE @g geometry;   
SET @g = geometry::[Null];  
SELECT @g  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di geometria statici estesi](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

