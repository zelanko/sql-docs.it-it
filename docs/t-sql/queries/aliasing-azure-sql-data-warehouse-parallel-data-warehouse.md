---
title: Aliasing
description: Aliasing in Azure SQL Data Warehouse e Parallel Data Warehouse.
titleSuffix: Azure SQL Data Warehouse
ms.custom: seo-lt-2019
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
ms.assetid: 7b3a5c74-05cf-4385-8ee6-6176d003cb8a
author: shkale-msft
ms.author: shkale
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 3b548dd789bc7e234eb527ffe5766f433a06d77e
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2019
ms.locfileid: "75244774"
---
# <a name="aliasing-azure-sql-data-warehouse-parallel-data-warehouse"></a>Alias (Azure SQL Data Warehouse, Parallel Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Gli alias consentono di sostituire temporaneamente un nome di tabella o colonna nelle query [!INCLUDE[DWsql](../../includes/dwsql-md.md)] di [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] con una stringa breve e facile da ricordare. Gli alias di tabella vengono spesso usati nelle query JOIN perché la sintassi JOIN richiede nomi di oggetto completi quando si fa riferimento alle colonne.  
  
 Gli alias devono essere singole parole conformi alle regole di denominazione degli oggetti. Per altre informazioni, vedere la sezione relativa alle regole di denominazione degli oggetti nella [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]. Gli alias non possono contenere spazi vuoti e non possono essere racchiusi tra virgolette singole o doppie.  
  
## <a name="syntax"></a>Sintassi  
  
```  
object_source [ AS ] alias  
```  
  
## <a name="arguments"></a>Argomenti  
 *object_source*  
 Nome della tabella o colonna di origine.  
  
 AS  
 Preposizione di alias facoltativo. Quando si usano alias di variabile di intervallo, la parola chiave AS non è consentita.  
  
 *alias*  
 Nome di riferimento temporaneo scelto per la tabella o la colonna. È possibile usare qualsiasi nome di oggetto valido. Per altre informazioni, vedere la sezione relativa alle regole di denominazione degli oggetti nella [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 L'esempio seguente illustra una query con più join. In questo esempio vengono illustrati alias di tabella e di colonna.  
  
-   Alias di colonna: in questo esempio viene associato un alias a colonne ed espressioni che includono colonne nell'elenco di selezione. `SalesTerritoryRegion AS SalesTR` illustra un alias di colonna semplice. Vedere `Sum(SalesAmountQuota) AS TotalSales`.  
  
-   Alias di tabella: `dbo.DimSalesTerritory AS st` illustra la creazione dell'alias `st` per la tabella `dbo.DimSalesTerritory`.  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, SUM(SalesAmountQuota) AS TotalSales, SalesTerritoryRegion AS SalesTR,  
    RANK() OVER (PARTITION BY SalesTerritoryRegion ORDER BY SUM(SalesAmountQuota) DESC ) AS RankResult  
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.FactSalesQuota AS sq ON e.EmployeeKey = sq.EmployeeKey  
INNER JOIN dbo.DimSalesTerritory AS st ON e.SalesTerritoryKey = st.SalesTerritoryKey  
WHERE SalesPersonFlag = 1 AND SalesTerritoryRegion != N'NA'  
GROUP BY LastName, SalesTerritoryRegion;  
  
```  
  
 La parola chiave AS può essere esclusa, come illustrato di seguito, ma viene spesso inclusa per migliorare la leggibilità.  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, SUM(SalesAmountQuota) TotalSales, SalesTerritoryRegion SalesTR,  
RANK() OVER (PARTITION BY SalesTerritoryRegion ORDER BY SUM(SalesAmountQuota) DESC ) RankResult  
FROM dbo.DimEmployee e  
INNER JOIN dbo.FactSalesQuota sq ON e.EmployeeKey = sq.EmployeeKey  
INNER JOIN dbo.DimSalesTerritory st ON e.SalesTerritoryKey = st.SalesTerritoryKey  
WHERE SalesPersonFlag = 1 AND SalesTerritoryRegion != N'NA'  
GROUP BY LastName, SalesTerritoryRegion;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  
  
  
