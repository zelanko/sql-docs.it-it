---
title: MinDbCompatibilityLevel (tipo di dati geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- MinDbCompatibilityLevel method (geometry)
ms.assetid: c848b974-8ccb-4c5c-a7eb-b019a9538d99
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 373c9eb4a1482bf92ae41c39af2f8852d19aac9f
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86554343"
---
# <a name="mindbcompatibilitylevel-geometry-data-type"></a>MinDbCompatibilityLevel (tipo di dati geometry)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

Restituisce il livello minimo di compatibilità del database che riconosce l'istanza del tipo di dati **geometry**.
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.MinDbCompatibilityLevel ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipi restituiti
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **int**  
  
 Tipo CLR restituito: **int**  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare `MinDbCompatibilityLevel()` per verificare la compatibilità di un oggetto spaziale prima di modificare il livello di compatibilità in un database.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-testing-circularstring-type-for-compatibility-with-compatibility-level-110"></a>R. Verifica della compatibilità del tipo CircularString con livello di compatibilità 110  
 Nell'esempio seguente viene verificata la compatibilità di un'istanza `CircularString` con una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```
 DECLARE @g geometry = 'CIRCULARSTRING(3 4, 8 9, 5 6)'; 
 IF @g.MinDbCompatibilityLevel() <= 110 
 BEGIN 
 SELECT @g.ToString(); 
 END
 ```  
  
### <a name="b-testing-linestring-type-for-compatibility-with-compatibility-level-100"></a>B. Verifica della compatibilità del tipo LineString con livello di compatibilità 100  
 Nell'esempio seguente viene verificata la compatibilità di un'istanza `LineString` con [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]:  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 9, 5 6)'; 
 IF @g.MinDbCompatibilityLevel() <= 100 
 BEGIN 
 SELECT @g.ToString(); 
 END
``` 
  
## <a name="see-also"></a>Vedere anche  
 [Livello di compatibilità ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
  
  

