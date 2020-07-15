---
title: Hints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- query optimizer [SQL Server], hints
- hints [SQL Server], about hints
- SELECT statement [SQL Server], hints
- hints [SQL Server]
- INSERT statement [SQL Server], hints
- UPDATE statement [SQL Server], hints
- DELETE statement [SQL Server], hints
ms.assetid: 99412475-b0df-4264-9938-33a0b302b41a
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 7ee01e23c544ac01ee9fb85e5b59d31b73088987
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85731291"
---
# <a name="hints-transact-sql"></a>Hint (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Gli hint sono opzioni o strategie che vengono specificati per imporre un comportamento specifico a Query Processor di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'esecuzione di istruzioni SELECT, INSERT, UPDATE o DELETE. Gli hint consentono di ignorare eventuali piani di esecuzione selezionati da Query Optimizer per una query.  
  
> [!CAUTION]  
>  Poiché Query Optimizer di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seleziona in genere il piano di esecuzione migliore per una query, gli oggetti \<join_hint>, \<query_hint> e \<table_hint> devono essere usati solo se strettamente necessari ed esclusivamente da sviluppatori e amministratori di database esperti.
  
 In questa sezione vengono descritti gli hint seguenti:  
  
-   [Hint di join](../../t-sql/queries/hints-transact-sql-join.md)  
  
-   [Query Hints](../../t-sql/queries/hints-transact-sql-query.md) (Hint per la query)  
  
-   [Hint di tabella](../../t-sql/queries/hints-transact-sql-table.md)  
  
  
