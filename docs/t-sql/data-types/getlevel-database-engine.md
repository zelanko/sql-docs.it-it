---
title: GetLevel (motore di database) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GetLevel
- GetLevel_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetLevel [Database Engine]
ms.assetid: 81577d7e-8ff6-4e73-b7f4-94c03d4921e7
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f205c91f7375e52a944dbcc18c026edb9712d944
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86554476"
---
# <a name="getlevel-database-engine"></a>GetLevel (Motore di database)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Restituisce un intero che rappresenta la profondità del nodo *this* nell'albero.
  
## <a name="syntax"></a>Sintassi  
  
```sql
-- Transact-SQL syntax  
node.GetLevel ( )   
```  
  
```sql
-- CLR syntax  
SqlInt16 GetLevel ( )   
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipi restituiti  
**Tipo SQL Server restituito: smallint**
  
**Tipo CLR restituito: SqlInt16**
  
## <a name="remarks"></a>Osservazioni  
Utilizzato per determinare il livello di uno o più nodi o per filtrare i nodi sui membri di un livello specificato. La radice della gerarchia si trova a livello 0.
  
GetLevel è utile per indici di ricerca breadth-first. Per altre informazioni, vedere [Dati gerarchici &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md).
  
## <a name="examples"></a>Esempi  
  
### <a name="a-returning-the-hierarchy-level-as-a-column"></a>R. Restituzione del livello della gerarchia come una colonna  
Nell'esempio seguente vengono restituiti una rappresentazione in formato testo di **hierarchyid** e quindi il livello della gerarchia come colonna **EmpLevel** per tutte le righe della tabella:
  
```sql
SELECT OrgNode.ToString() AS Text_OrgNode,   
OrgNode.GetLevel() AS EmpLevel, *  
FROM HumanResources.EmployeeDemo;  
```  
  
### <a name="b-returning-all-members-of-a-hierarchy-level"></a>B. Restituzione di tutti i membri di un livello della gerarchia  
Nell'esempio seguente vengono restituite tutte le righe della tabella a livello 2 della gerarchia:
  
```sql
SELECT OrgNode.ToString() AS Text_OrgNode,   
OrgNode.GetLevel() AS EmpLevel, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetLevel() = 2;  
```  
  
### <a name="c-returning-the-root-of-the-hierarchy"></a>C. Restituzione della radice della gerarchia  
Nell'esempio seguente viene restituita la radice del livello della gerarchia:
  
```sql
SELECT OrgNode.ToString() AS Text_OrgNode,   
OrgNode.GetLevel() AS EmpLevel, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetLevel() = 0;  
```  
  
### <a name="d-clr-example"></a>D. Esempio CLR  
Nel frammento di codice seguente viene chiamato il metodo GetLevel():
  
```sql
this.GetLevel()  
```  
  
## <a name="see-also"></a>Vedere anche
[Guida di riferimento ai metodi per il tipo di dati hierarchyid](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[Dati gerarchici &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  