---
title: IsDescendantOf (motore di database) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IsDescendant_TSQL
- IsDescendant
dev_langs:
- TSQL
helpviewer_keywords:
- IsDescendantOf [Database Engine]
ms.assetid: edc80444-b697-410f-9419-0f63c9b5618d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: bddc7c269443446a6b8de6498cf73dd35f218e16
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56012682"
---
# <a name="isdescendantof-database-engine"></a>IsDescendantOf (Motore di database)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Restituisce true se l'*elemento* è un discendente dell'elemento padre.
  
## <a name="syntax"></a>Sintassi  
  
```sql
-- Transact-SQL syntax  
child. IsDescendantOf ( parent )  
```  
  
```sql
-- CLR syntax  
SqlHierarchyId IsDescendantOf (SqlHierarchyId parent )  
```  
  
## <a name="arguments"></a>Argomenti  
*parent*  
Nodo **hierarchyid** per cui il test IsDescendantOf deve essere eseguito.
  
## <a name="return-types"></a>Tipi restituiti  
**Tipo SQL Server restituito: bit**
  
**Tipo CLR restituito: SqlBoolean**
  
## <a name="remarks"></a>Remarks  
Restituisce true per tutti i nodi nel sottoalbero con radice nel padre specificato e false per tutti gli altri nodi.
  
Un padre è considerato discendente di se stesso.
  
## <a name="examples"></a>Esempi  
  
### <a name="a-using-isdescendantof-in-a-where-clause"></a>A. Utilizzo di IsDescendantOf in una clausola WHERE  
Nell'esempio seguente vengono restituiti un responsabile e i relativi dipendenti diretti:
  
```sql
DECLARE @Manager hierarchyid  
SELECT @Manager = OrgNode FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\dylan0'  
  
SELECT * FROM HumanResources.EmployeeDemo  
WHERE OrgNode.IsDescendantOf(@Manager) = 1  
```  
  
### <a name="b-using-isdescendantof-to-evaluate-a-relationship"></a>b. Utilizzo di IsDescendantOf per valutare una relazione  
Nel codice seguente vengono dichiarate tre variabili cui vengono assegnati i valori relativi. Viene quindi valutata la relazione gerarchica e restituito uno dei due risultati stampati in base al confronto:
  
```sql
DECLARE @Manager hierarchyid, @Employee hierarchyid, @LoginID nvarchar(256)  
SELECT @Manager = OrgNode FROM HumanResources.EmployeeDemo  
WHERE LoginID = 'adventure-works\terri0' ;  
  
SELECT @Employee = OrgNode, @LoginID = LoginID FROM HumanResources.EmployeeDemo  
  WHERE LoginID = 'adventure-works\rob0'  
  
IF @Employee.IsDescendantOf(@Manager) = 1  
   BEGIN  
    PRINT 'LoginID ' + @LoginID + ' is a subordinate of the selected Manager.'  
   END  
ELSE  
   BEGIN  
    PRINT 'LoginID ' + @LoginID + ' is not a subordinate of the selected Manager.' ;  
   END  
```  
  
### <a name="c-calling-a-common-language-runtime-method"></a>C. Chiamata a un metodo Common Language Runtime  
Nel frammento di codice seguente viene chiamato il metodo `IsDescendantOf()`.
  
```sql
this.IsDescendantOf(Parent)  
```  
  
## <a name="see-also"></a>Vedere anche
[Guida di riferimento ai metodi per il tipo di dati hierarchyid](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[Dati gerarchici &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  
