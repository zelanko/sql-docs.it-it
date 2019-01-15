---
title: Applicare un piano di query fisso a una guida di piano | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: bbf401f9-af7c-48e7-8a43-bf25e8af2fd7
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: 6dd1148be3e8b01bb8db9150106903c862207c57
ms.sourcegitcommit: dd794633466b1da8ead9889f5e633bdf4b3389cd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54143041"
---
# <a name="apply-a-fixed-query-plan-to-a-plan-guide"></a>Applicare un piano di query fisso a una guida di piano
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  È possibile applicare un piano di query fisso a una guida di piano di tipo OBJECT o SQL. Le guide di piano che applicano un piano di query fisso risultano utili quando per una specifica query esiste un piano di esecuzione che offre prestazioni migliori rispetto a quello selezionato da Query Optimizer.  
  
 Nell'esempio seguente viene creata una guida di piano per una semplice istruzione SQL ad hoc. Il piano di query desiderato per questa istruzione è fornito nella guida di piano specificando lo Showplan XML per la query direttamente nel parametro `@hints` . Viene innanzitutto eseguita l'istruzione SQL per generare un piano nella cache dei piani. Ai fini di questo esempio, si presuppone che il piano generato sia il piano desiderato, senza che sia richiesta alcuna ottimizzazione aggiuntiva della query. Lo Showplan XML per la query si ottiene eseguendo una query sulle viste a gestione dinamica `sys.dm_exec_query_stats`, `sys.dm_exec_sql_text`e `sys.dm_exec_text_query_plan` e assegnandolo alla variabile `@xml_showplan` . La variabile `@xml_showplan` passa quindi all'istruzione `sp_create_plan_guide` nel parametro `@hints` . In alternativa, è possibile creare una guida di piano da un piano di query nella cache dei piani usando la stored procedure [sp_create_plan_guide_from_handle](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md) .  
  
```  
USE AdventureWorks2012;  
GO  
SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;  
GO  
DECLARE @xml_showplan nvarchar(max);  
SET @xml_showplan = (SELECT query_plan  
    FROM sys.dm_exec_query_stats AS qs   
    CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st  
    CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, DEFAULT, DEFAULT) AS qp  
    WHERE st.text LIKE N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;%');  
  
EXEC sp_create_plan_guide   
    @name = N'Guide1_from_XML_showplan',   
    @stmt = N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = @xml_showplan;  
GO  
```  
  
  
