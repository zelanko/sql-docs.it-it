---
title: Specificare il comportamento di parametrizzazione delle query tramite guide di piano | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- TEMPLATE plan guide
- PARAMETERIZATION FORCED option
- PARAMETERIZATION option
- PARAMETERIZATION SIMPLE option
- parameterization [SQL Server]
- overriding parameterization behavior
- plan guides [SQL Server], parameterization
- parameterized queries [SQL Server]
ms.assetid: f0f738ff-2819-4675-a8c8-1eb6c210a7e6
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: 06ed5433d23501016a0ea308c9238fcf7bc1b3c1
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/05/2019
ms.locfileid: "67582068"
---
# <a name="specify-query-parameterization-behavior-by-using-plan-guides"></a>Definizione delle funzionalità di parametrizzazione delle query tramite guide di piano
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Quando l'opzione di database PARAMETERIZATION è impostata su SIMPLE, Query Optimizer di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può scegliere di parametrizzare le query, ovvero di sostituire con parametri i valori letterali contenuti in una query. Tale processo viene chiamato parametrizzazione semplice. Quando è attiva una parametrizzazione di tipo SIMPLE, non è possibile distinguere le query con parametri da quelle senza parametri. È tuttavia possibile specificare che devono essere parametrizzate tutte le query di un database impostando l'opzione di database PARAMETERIZATION su FORCED. Tale processo viene chiamato parametrizzazione forzata.  
  
 È possibile sostituire le funzionalità di parametrizzazione di un database nei modi seguenti:  
  
-   Quando l'opzione di database PARAMETERIZATION è impostata su SIMPLE, è possibile specificare che la parametrizzazione forzata venga tentata su una determinata classe di query. A tale scopo, è necessario creare una guida di piano TEMPLATE nel formato con parametri della query e specificare l'hint per la query PARAMETERIZATION FORCED nella stored procedure [sp_create_plan_guide](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md) . È possibile considerare questo tipo di guida di piano come uno strumento per abilitare la parametrizzazione forzata solo su una determinata classe di query, anziché su tutte le query.  
  
-   Quando l'opzione di database PARAMETERIZATION è impostata su FORCED, è possibile specificare che venga tentata solo la parametrizzazione semplice, anziché forzata, su una determinata classe di query. A tale scopo, è necessario creare una guida di piano TEMPLATE nel formato di query force-parametrized e specificare l'hint per la query PARAMETERIZATION SIMPLE nella stored procedure **sp_create_plan_guide**.  
  
 Si consideri la query seguente sul database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] :  
  
```  
SELECT pi.ProductID, SUM(pi.Quantity) AS Total  
FROM Production.ProductModel AS pm   
    INNER JOIN Production.ProductInventory AS pi   
        ON pm.ProductModelID = pi.ProductID   
WHERE pi.ProductID = 101   
GROUP BY pi.ProductID, pi.Quantity HAVING SUM(pi.Quantity) > 50;  
```  
  
 L'amministratore di database ha deciso di non abilitare la parametrizzazione forzata su tutte le query del database. Tuttavia, l'amministratore desidera evitare i costi di compilazione relativi a tutte le query sintatticamente equivalenti alla query precedente ma che si differenziano solo per i relativi valori letterali costanti. In altre parole, desidera che la query venga parametrizzata in modo da riutilizzare un piano per questo tipo di query. In tal caso, è necessario completare i passaggi seguenti:  
  
1.  Recuperare il formato con parametri della query. L'unico metodo affidabile per ottenere questo valore da usare in **sp_create_plan_guide** consiste nell'uso della stored procedure di sistema [sp_get_query_template](../../relational-databases/system-stored-procedures/sp-get-query-template-transact-sql.md) .  
  
2.  Creare la guida di piano nel formato con parametri della query, specificando l'hint per la query PARAMETERIZATION FORCED.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

    > [!IMPORTANT]  
    >  As part of parameterizing a query, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assigns a data type to the parameters that replace the literal values, depending on the value and size of the literal. The same process occurs to the value of the constant literals passed to the **@stmt** output parameter of **sp_get_query_template**. Because the data type specified in the **@params** argument of **sp_create_plan_guide** must match that of the query as it is parameterized by [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], you may have to create more than one plan guide to cover the complete range of possible parameter values for the query.  
  
 Lo script seguente può essere utilizzato sia per ottenere la query con parametri che per creare in seguito una guida di piano basata su tale query.  
  
```  
DECLARE @stmt nvarchar(max);  
DECLARE @params nvarchar(max);  
EXEC sp_get_query_template   
    N'SELECT pi.ProductID, SUM(pi.Quantity) AS Total   
      FROM Production.ProductModel AS pm   
      INNER JOIN Production.ProductInventory AS pi ON pm.ProductModelID = pi.ProductID   
      WHERE pi.ProductID = 101   
      GROUP BY pi.ProductID, pi.Quantity   
      HAVING sum(pi.Quantity) > 50',  
    @stmt OUTPUT,   
    @params OUTPUT;  
EXEC sp_create_plan_guide   
    N'TemplateGuide1',   
    @stmt,   
    N'TEMPLATE',   
    NULL,   
    @params,   
    N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
 Analogamente, in un database in cui è già abilitata la parametrizzazione forzata è possibile verificare che la query di esempio e le altre sintatticamente equivalenti, tranne per i relativi valori letterali costanti, siano con parametri in conformità alle regole della parametrizzazione semplice. A tale scopo, nella clausola OPTION è necessario specificare PARAMETERIZATION SIMPLE anziché PARAMETERIZATION FORCED.  
  
> [!NOTE]  
>  Le guide di piano TEMPLATE definiscono la corrispondenza tra le istruzioni e le query inviate in batch costituite da una singola istruzione. Le istruzioni all'interno di batch costituiti da più istruzioni non sono idonee per la corrispondenza definita dalle guide di piano TEMPLATE.  
  
  
