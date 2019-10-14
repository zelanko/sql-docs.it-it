---
title: PERCENTILE_CONT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/20/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PERCENTILE_CONT_TSQL
- PERCENTILE_CONT
dev_langs:
- TSQL
helpviewer_keywords:
- analytic functions, PERCENTILE_CONT
- PERCENTILE_CONT function
ms.assetid: d019419e-5297-4994-97d5-e9c8fc61bbf4
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c5c52b80601f7b1e8e73cffe0a6cad255d91ff82
ms.sourcegitcommit: 79e6d49ae4632f282483b0be935fdee038f69cc2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/09/2019
ms.locfileid: "72172976"
---
# <a name="percentile_cont-transact-sql"></a>PERCENTILE_CONT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Calcola un percentile basato su una distribuzione continua del valore della colonna in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il risultato viene interpolato e potrebbe non essere uguale ad alcuno dei valori specifici nella colonna.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
PERCENTILE_CONT ( numeric_literal )   
    WITHIN GROUP ( ORDER BY order_by_expression [ ASC | DESC ] )  
    OVER ( [ <partition_by_clause> ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *numeric_literal*  
 Percentile da calcolare. Il valore deve essere compreso tra 0 e 1.  
  
 WITHIN GROUP **(** ORDER BY *order_by_expression* [ **ASC** | DESC ] **)**  
 Specifica un elenco di valori numerici per ordinare e calcolare il percentile. È consentito un solo *order_by_expression*. L'espressione deve restituire un tipo numerico esatto o approssimato, con nessun altro tipo di dati consentito. I tipi numerici esatti sono **int**, **bigint**, **smallint**, **tinyint**, **numeric**, **bit**, **decimal**, **smallmoney** e **money**. I tipi numerici approssimati sono **float** e **real**. Per impostazione predefinita, l'ordinamento è crescente.  
  
 OVER **(** \<partition_by_clause> **)**  
 Suddivide il set di risultati generato dalla clausola FROM in partizioni alle quali viene applicata la funzione di percentile. Per altre informazioni, vedere [Clausola OVER - &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md). Le clausole \<ORDER BY> e \<ROWS o RANGE> della sintassi OVER non possono essere specificate in una funzione PERCENTILE_CONT.  
  
## <a name="return-types"></a>Tipi restituiti  
 **float(53)**  
  
## <a name="compatibility-support"></a>Informazioni sulla compatibilità  
 Se il valore del livello di compatibilità è 110 o superiore, WITHIN GROUP è una parola chiave riservata. Per altre informazioni, vedere [Livello di compatibilità ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
## <a name="general-remarks"></a>Osservazioni generali  
 Tutti i valori Null nel set di dati vengono ignorati.  
  
 PERCENTILE_CONT è non deterministico. Per altre informazioni, vedere [Funzioni deterministiche e non deterministiche](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-basic-syntax-example"></a>A. Esempio della sintassi di base  
 Nell'esempio seguente vengono utilizzate le funzioni PERCENTILE_CONT e PERCENTILE_DISC per trovare lo stipendio medio del dipendente in ogni reparto. È possibile che queste funzioni non restituiscano lo stesso valore. PERCENTILE_CONT esegue l'interpolazione del valore appropriato, che può esistere o meno nel set di dati, mentre PERCENTILE_DISC restituisce sempre un valore effettivo dal set.  
  
```  
USE AdventureWorks2012;  
  
SELECT DISTINCT Name AS DepartmentName  
      ,PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY ph.Rate)   
                            OVER (PARTITION BY Name) AS MedianCont  
      ,PERCENTILE_DISC(0.5) WITHIN GROUP (ORDER BY ph.Rate)   
                            OVER (PARTITION BY Name) AS MedianDisc  
FROM HumanResources.Department AS d  
INNER JOIN HumanResources.EmployeeDepartmentHistory AS dh   
    ON dh.DepartmentID = d.DepartmentID  
INNER JOIN HumanResources.EmployeePayHistory AS ph  
    ON ph.BusinessEntityID = dh.BusinessEntityID  
WHERE dh.EndDate IS NULL;  
```  
  
 Set di risultati parziale:  
  
 ```
DepartmentName        MedianCont    MedianDisc
--------------------   ----------   ----------
Document Control       16.8269      16.8269
Engineering            34.375       32.6923
Executive              54.32695     48.5577
Human Resources        17.427850    16.5865
```  

### <a name="b-basic-syntax-example"></a>B. Esempio della sintassi di base  
 Nell'esempio seguente vengono utilizzate le funzioni PERCENTILE_CONT e PERCENTILE_DISC per trovare lo stipendio medio del dipendente in ogni reparto. È possibile che queste funzioni non restituiscano lo stesso valore. PERCENTILE_CONT esegue l'interpolazione del valore appropriato, che può esistere o meno nel set di dati, mentre PERCENTILE_DISC restituisce sempre un valore effettivo dal set.  
  
```  
-- Uses AdventureWorks  
  
SELECT DISTINCT DepartmentName  
,PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY BaseRate)  
    OVER (PARTITION BY DepartmentName) AS MedianCont  
,PERCENTILE_DISC(0.5) WITHIN GROUP (ORDER BY BaseRate)  
    OVER (PARTITION BY DepartmentName) AS MedianDisc  
FROM dbo.DimEmployee;  
  
```  
  
 Set di risultati parziale:  
  
 ```
DepartmentName        MedianCont    MedianDisc
--------------------   ----------   ----------
Document Control       16.826900    16.8269
Engineering            34.375000    32.6923
Human Resources        17.427850    16.5865
Shipping and Receiving 9.250000      9.0000
```  
  
## <a name="see-also"></a>Vedere anche  
 [PERCENTILE_DISC &#40;Transact-SQL&#41;](../../t-sql/functions/percentile-disc-transact-sql.md)  
  
 