---
description: GetRoot (Motore di database)
title: GetRoot (motore di database) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GetRoot
- GetRoot_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetRoot [Database Engine]
ms.assetid: 240b70f1-eeda-44ab-b4bb-9e4af80fa7c0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: cdefe46b9e2baa546b76375af4c6a2272fe1f584
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88445931"
---
# <a name="getroot-database-engine"></a>GetRoot (Motore di database)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Restituisce la radice dell'albero gerarchico. GetRoot() è un metodo statico.
  
## <a name="syntax"></a>Sintassi  
  
```sql
-- Transact-SQL syntax  
hierarchyid::GetRoot ( )   
```  
  
```sql
-- CLR syntax  
static SqlHierarchyId GetRoot ( )   
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipi restituiti  
**Tipo SQL Server restituito: hierarchyid**
  
**Tipo CLR restituito: SqlHierarchyId**
  
## <a name="remarks"></a>Commenti  
Utilizzato per determinare il nodo radice in un albero gerarchico.
  
## <a name="examples"></a>Esempi  
  
### <a name="a-transact-sql-example"></a>R. Esempio Transact-SQL  
Nell'esempio seguente viene restituita la radice dell'albero gerarchico:
  
```sql
SELECT OrgNode.ToString() AS Text_OrgNode, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode = hierarchyid::GetRoot()  
```  
  
### <a name="b-clr-example"></a>B. Esempio CLR  
Nel frammento di codice seguente viene chiamato il metodo GetRoot():
  
```sql
SqlHierarchyId.GetRoot()  
```  
  
## <a name="see-also"></a>Vedere anche
[Guida di riferimento ai metodi per il tipo di dati hierarchyid](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[Dati gerarchici &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  
