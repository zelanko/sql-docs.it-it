---
title: Creare una guida di piano per le query con parametri | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- parameterized queries, plan guides for
- plan guides [SQL Server], parameterized queries
ms.assetid: b532ae16-66e7-4641-9bc8-b0d805853477
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 4a754b2e2d748ebc007918a75e17f3851e4a9dd3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85774237"
---
# <a name="create-a-plan-guide-for-parameterized-queries"></a>Creare una guida di piano per le query con parametri
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Una guida di piano di tipo TEMPLATE corrisponde alle query autonome con parametrizzazioni specifiche.  
  
 Nel seguente esempio viene creata una guida di piano corrispondente a qualsiasi query che parametrizza un formato specifico e forza in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'esecuzione della parametrizzazione della query. Le due query seguenti sono equivalenti a livello sintattico. L'unica differenza risiede nei relativi valori letterali costanti.  
  
```  
SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
    ON h.SalesOrderID = d.SalesOrderID  
WHERE h.SalesOrderID = 45639;  
  
SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
    ON h.SalesOrderID = d.SalesOrderID  
WHERE h.SalesOrderID = 45640;  
```  
  
 Di seguito è riportata la guida di piano nel formato con parametri della query:  
  
```  
EXEC sp_create_plan_guide   
    @name = N'TemplateGuide1',  
    @stmt = N'SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
              INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
                  ON h.SalesOrderID = d.SalesOrderID  
              WHERE h.SalesOrderID = @0',  
    @type = N'TEMPLATE',  
    @module_or_batch = NULL,  
    @params = N'@0 int',  
    @hints = N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
 Nell'esempio precedente il valore del parametro `@stmt` corrisponde al formato con parametri della query. L'unico modo affidabile per ottenere questo valore da usare in sp_create_plan_guide è usare la stored procedure di sistema [sp_get_query_template](../../relational-databases/system-stored-procedures/sp-get-query-template-transact-sql.md) . Lo script seguente può essere utilizzato sia per ottenere la query con parametri che per creare una guida di piano in base a essa.  
  
```  
DECLARE @stmt nvarchar(max);  
DECLARE @params nvarchar(max);  
EXEC sp_get_query_template   
    N'SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
      INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
          ON h.SalesOrderID = d.SalesOrderID  
      WHERE h.SalesOrderID = 45639;',  
    @stmt OUTPUT,   
    @params OUTPUT  
EXEC sp_create_plan_guide N'TemplateGuide1',   
    @stmt,   
    N'TEMPLATE',   
    NULL,   
    @params,   
    N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
> [!IMPORTANT]  
>  Il valore letterale costante nel parametro `@stmt` passato a `sp_get_query_template` potrebbe interessare il tipo di dati scelto per il parametro che sostituisce il valore letterale. Ciò potrebbe avere ripercussioni sulla corrispondenza eseguita in base alla guida di piano. Potrebbe essere necessario creare più guide di piano per gestire intervalli di valori dei parametri diversi.  
  
 Le guide di piano di tipo TEMPLATE possono essere utilizzate con le guide di piano di tipo SQL. Ad esempio, è possibile creare una guida di piano di tipo TEMPLATE per assicurarsi che una classe di query venga sottoposta a parametrizzazione È possibile creare una guida di piano di tipo SQL sulla query con parametri.  
  
  
