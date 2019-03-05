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
manager: craigg
ms.openlocfilehash: 8bd2692d428012e0af4ea4f41059228178810abb
ms.sourcegitcommit: 670082cb47f7d3d82e987b549b6f8e3a8968b5db
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/05/2019
ms.locfileid: "57334308"
---
# <a name="hints-transact-sql"></a>Hint (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gli hint sono opzioni o strategie che vengono specificati per imporre un comportamento specifico a Query Processor di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'esecuzione di istruzioni SELECT, INSERT, UPDATE o DELETE. Gli hint consentono di ignorare eventuali piani di esecuzione selezionati da Query Optimizer per una query.  
  
> [!CAUTION]  
>  Dal momento che di norma Query Optimizer di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seleziona il miglior piano di esecuzione possibile per una query, \<join_hint>, \<query_hint> e \<table_hint> devono essere usati solo da amministratori di database e sviluppatori esperti in casi di effettiva necessità.
  
 In questa sezione vengono descritti gli hint seguenti:  
  
-   [Hint di join](../../t-sql/queries/hints-transact-sql-join.md)  
  
-   [Query Hints](../../t-sql/queries/hints-transact-sql-query.md) (Hint per la query)  
  
-   [Hint di tabella](../../t-sql/queries/hints-transact-sql-table.md)  
  
  
