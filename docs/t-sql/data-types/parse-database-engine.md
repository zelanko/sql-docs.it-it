---
title: Parse (motore di database) | Microsoft Docs
ms.custom: ''
ms.date: 7/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Parse
- Parse_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Parse [Database Engine]
ms.assetid: b37e28b6-6e2e-470a-945b-ce5252da743a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 40647221fe39df637407056d8b41c0e7e75428f6
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52417142"
---
# <a name="parse-database-engine"></a>Parse (Motore di database)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Il metodo Parse esegue la conversione della rappresentazione stringa canonica di un valore **hierarchyid** in un valore **hierarchyid**. Parse viene chiamato in modo implicito quando viene eseguita una conversione da un tipo stringa in **hierarchyid**. Il metodo funziona in modo opposto a [ToString](../../t-sql/data-types/tostring-database-engine.md). Parse() è un metodo statico.
  
## <a name="syntax"></a>Sintassi  
  
```sql
-- Transact-SQL syntax  
hierarchyid::Parse ( input )  
-- This is functionally equivalent to the following syntax   
-- which implicitly calls Parse():  
CAST ( input AS hierarchyid )  
```  
  
```sql
-- CLR syntax  
static SqlHierarchyId Parse ( SqlString input )   
```  
  
## <a name="arguments"></a>Argomenti  
*input*  
[!INCLUDE[tsql](../../includes/tsql-md.md)]: valore del tipo di dati character convertito.
  
CLR: valore stringa valutato.
  
## <a name="return-types"></a>Tipi restituiti  
**Tipo SQL Server restituito: hierarchyid**
  
**Tipo CLR restituito: SqlHierarchyId**
  
## <a name="remarks"></a>Remarks  
Se Parse riceve un valore che non è una rappresentazione stringa valida di un valore **hierarchyid**, viene generata un'eccezione. Se, ad esempio, i tipi di dati **char** contengono spazi finali, viene generata un'eccezione.
  
## <a name="examples"></a>Esempi  
  
### <a name="a-converting-transact-sql-values-without-a-table"></a>A. Conversione di valori Transact-SQL senza una tabella  
Nell'esempio di codice seguente viene usato `ToString` per convertire un valore **hierarchyid** in una stringa e `Parse` per convertire un valore stringa in un valore **hierarchyid**.
  
```sql
DECLARE @StringValue AS nvarchar(4000), @hierarchyidValue AS hierarchyid  
SET @StringValue = '/1/1/3/'  
SET @hierarchyidValue = 0x5ADE  
  
SELECT hierarchyid::Parse(@StringValue) AS hierarchyidRepresentation,  
@hierarchyidValue.ToString() AS StringRepresentation ;
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
hierarchyidRepresentation    StringRepresentation
-------------------------    -----------------------
0x5ADE                       /1/1/3/
```
  
### <a name="b-clr-example"></a>B. Esempio CLR  
Nel frammento di codice seguente viene chiamato il metodo Parse():
  
```sql
string input = "/1/2/";  
SqlHierarchyId.Parse(input);  
```  
  
## <a name="see-also"></a>Vedere anche
[Guida di riferimento ai metodi per il tipo di dati hierarchyid](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)  
[Dati gerarchici &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
  
