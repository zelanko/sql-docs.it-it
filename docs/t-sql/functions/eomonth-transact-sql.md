---
title: EOMONTH (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- EOMONTH
- EOMONTH_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- EOMONTH function
ms.assetid: 1d060d8e-3297-4244-afef-57df2f8f92e2
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9cbdb282e8a2214fdb9c45116806ca513dcde443
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/17/2020
ms.locfileid: "81636296"
---
# <a name="eomonth-transact-sql"></a>EOMONTH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

Questa funzione restituisce l'ultimo giorno del mese contenente una data specificata, con una differenza facoltativa.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```syntaxsql
EOMONTH ( start_date [, month_to_add ] )  
```  
  
## <a name="arguments"></a>Argomenti  
*start_date*  
Espressione date che specifica la data per cui restituire l'ultimo giorno del mese.  
  
*month_to_add*  
Espressione Integer facoltativa che specifica il numero di mesi da aggiungere a *start_date*.  
  
Se l'argomento *month_to_add* ha un valore, `EOMONTH` aggiunge il numero di mesi specificato a *start_date*, quindi restituisce l'ultimo giorno del mese della data risultante. Se questa aggiunta supera l'intervallo valido di date, `EOMONTH` genererà un errore.  
  
## <a name="return-type"></a>Tipo restituito  
 **date**  
  
## <a name="remarks"></a>Osservazioni  
La funzione `EOMONTH` può essere eseguita in modalità remota in server [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versioni successive, ma non in server con versioni precedenti a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-eomonth-with-explicit-datetime-type"></a>R. EOMONTH con tipo datetime esplicito  
  
```  
DECLARE @date DATETIME = '12/1/2011';  
SELECT EOMONTH ( @date ) AS Result;  
GO  
```  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
------------  
2011-12-31  
  
(1 row(s) affected)  
```  

### <a name="b-eomonth-with-string-parameter-and-implicit-conversion"></a>B. EOMONTH con parametro di tipo stringa e conversione implicita  
  
```  
DECLARE @date VARCHAR(255) = '12/1/2011';  
SELECT EOMONTH ( @date ) AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
------------  
2011-12-31  
  
(1 row(s) affected)  
```  
  
### <a name="c-eomonth-with-and-without-the-month_to_add-parameter"></a>C. EOMONTH con e senza il parametro month_to_add  
  
Nota: i valori illustrati in questi set di risultati rispecchiano una data di esecuzione inclusa tra e comprendente
        
        12/01/2011
        
        and
        
        12/31/2011

```sql  
DECLARE @date DATETIME = GETDATE();  
SELECT EOMONTH ( @date ) AS 'This Month';  
SELECT EOMONTH ( @date, 1 ) AS 'Next Month';  
SELECT EOMONTH ( @date, -1 ) AS 'Last Month';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
This Month  
-----------------------  
2011-12-31  
  
(1 row(s) affected)  
  
Next Month  
-----------------------  
2012-01-31  
  
(1 row(s) affected)  
  
Last Month  
-----------------------  
2011-11-30  
  
(1 row(s) affected)  
```  
  
  

