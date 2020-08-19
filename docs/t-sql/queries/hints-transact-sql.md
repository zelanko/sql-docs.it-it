---
description: Hint (Transact-SQL)
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
ms.openlocfilehash: 16f0e437e864ccb2bd0b4c173b40d84098c51b30
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88459189"
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
  
  
