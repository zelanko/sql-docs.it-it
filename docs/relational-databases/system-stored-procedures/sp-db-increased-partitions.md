---
title: sp_db_increased_partitions | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_db_increased_partitions_TSQL
- sp_db_increased_partitions
dev_langs:
- TSQL
helpviewer_keywords:
- sp_db_increased_partitions
ms.assetid: a8c043ec-b504-4929-ac0e-8babaa99d989
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 73f3eca2a2e7943d8911144a3657e4f826d9739c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62506718"
---
# <a name="spdbincreasedpartitions"></a>sp_db_increased_partitions
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Consente di abilitare e disabilitare il supporto per partizioni fino a 15.000 per il database specificato.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_dp_increased_partitions   
[ @dbname ] = 'database_name'   
[ , [ @increased_partitions = ] 'increased_partitions' ] [;]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @dbname=] '*nome_database*'  
 Nome del database. *dbname* viene **sysname** con un valore predefinito NULL. Se *dbname* viene omesso, viene utilizzato il database corrente.  
  
 [ @increased_partitions=] '*increased_partitions*'  
 Consente di abilitare e disabilitare il supporto per partizioni fino a 15.000 sul database specificato. *increased_partitions* viene **varchar(6)** con valore predefinito è NULL. I valori accettati per abilitare il supporto sono 'ON' o 'TRUE' e 'OFF' o 'FALSE' per disabilitarlo. Se *increased_partitions* non viene specificato, la procedura restituisce 1 per indicare il supporto è abilitato per il database specificato o 0 per indicare il supporto è disabilitato.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione ALTER DATABASE per il database specificato.  
  
  
