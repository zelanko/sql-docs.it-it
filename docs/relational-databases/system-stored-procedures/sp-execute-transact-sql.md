---
title: sp_execute (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_execute
- sp_cursor_execute_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_execute
ms.assetid: 2009acd3-0d92-435a-a8fb-057e50dc7146
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 12bfa6e7d37aae2a5ffc58828d47ace11d558487
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2020
ms.locfileid: "87392916"
---
# <a name="sp_execute-transact-sql"></a>sp_execute (Transact-SQL)
[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

  Esegue un'istruzione preparata [!INCLUDE[tsql](../../includes/tsql-md.md)] utilizzando un handle specificato e un valore di parametro facoltativo. sp_execute viene richiamato specificando ID = 12 in un pacchetto del flusso TDS (Tabular Data Stream).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
-- Syntax for SQL Server, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_execute handle OUTPUT  
    [,bound_param  ]  [,...n ]  ]  
```  
  
## <a name="arguments"></a>Argomenti  
 *gestire*  
 Valore dell' *handle* restituito da sp_prepare. *handle* è un parametro obbligatorio che richiede un valore di input **int** .  
  
 *bound_param*  
 Indica l'utilizzo di parametri aggiuntivi. *bound_param* è un parametro obbligatorio che richiede valori di input di qualsiasi tipo di dati per indicare parametri aggiuntivi per la procedura.  
  
> [!NOTE]  
>  *bound_param* deve corrispondere alle dichiarazioni effettuate dal valore dei*parametri* sp_prepare e può essere nel formato * @name = valore* o *valore*.  
  
## <a name="see-also"></a>Vedi anche  
 [Stored procedure di sistema &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_prepare &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)  
  
  
