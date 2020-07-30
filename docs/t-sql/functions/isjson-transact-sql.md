---
title: ISJSON (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2020
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ISJSON
- ISJSON_TSQL
helpviewer_keywords:
- ISJSON function
- JSON, validating
ms.assetid: c836f3d3-3e17-44ae-92bf-f341918896c3
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: jroth
monikerRange: = azuresqldb-current||= azure-sqldw-latest||>= sql-server-2016||>= sql-server-linux-2017||= sqlallproducts-allversions
ms.openlocfilehash: cdf9f8c9f79ec7bf286eb1d29a9274baf9a1887f
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2020
ms.locfileid: "87395366"
---
# <a name="isjson-transact-sql"></a>ISJSON (Transact-SQL)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

  Verifica se una stringa include contenuto JSON valido.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```sql  
ISJSON ( expression )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argomenti
 *expression*  
 Stringa da testare.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce 1 se la stringa include contenuto JSON valido. In caso contrario, restituisce 0. Restituisce Null se *expression* è Null.  
  
 Non restituisce errori.  
  
## <a name="remarks"></a>Osservazioni  
 **ISJSON** non controlla l'univocità delle chiavi allo stesso livello.  
  
## <a name="examples"></a>Esempi  
  
### <a name="example-1"></a>Esempio 1  
L'esempio seguente esegue un blocco di istruzioni in modo condizionale se il valore del parametro `@param` include contenuto JSON valido.  
  
```sql  
DECLARE @param <data type>
SET @param = <value>

IF (ISJSON(@param) > 0)  
BEGIN  
     -- Do something with the valid JSON value of @param.  
END
```  
  
### <a name="example-2"></a>Esempio 2  
L'esempio seguente restituisce le righe in cui la colonna `json_col` include contenuto JSON valido.  
  
```sql  
SELECT id, json_col
FROM tab1
WHERE ISJSON(json_col) > 0 
```  
  
## <a name="see-also"></a>Vedere anche  
 [Dati JSON &#40;SQL Server&#41;](../../relational-databases/json/json-data-sql-server.md)  
  
  
