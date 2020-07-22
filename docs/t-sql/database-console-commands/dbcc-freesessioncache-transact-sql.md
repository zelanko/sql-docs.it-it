---
title: DBCC FREESESSIONCACHE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FREESESSIONCACHE
- FREESESSIONCACHE_TSQL
- DBCC_FREESESSIONCACHE_TSQL
- DBCC FREESESSIONCACHE
dev_langs:
- TSQL
helpviewer_keywords:
- DBCC FREESESSIONCACHE statement
- distributed queries [SQL Server], cache
- clearing distributed query cache
- flushing distributed query cache
ms.assetid: a256ba63-7e11-4d5e-abc0-1fa4ed072e63
author: pmasl
ms.author: umajay
ms.openlocfilehash: 30a4245b58b9da0d51a246ba025533f42b17a715
ms.sourcegitcommit: edba1c570d4d8832502135bef093aac07e156c95
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/20/2020
ms.locfileid: "86485252"
---
# <a name="dbcc-freesessioncache-transact-sql"></a>DBCC FREESESSIONCACHE (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Scarica la cache delle connessioni di query distribuite usata dalle query distribuite per un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi  
```sql
DBCC FREESESSIONCACHE [ WITH NO_INFOMSGS ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argomenti
 WITH NO_INFOMSGS  
 Disattiva tutti i messaggi informativi.  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'appartenenza al ruolo predefinito del server **sysadmin** .  
  
## <a name="examples"></a>Esempi  
Nell'esempio seguente viene scaricata la cache delle query distribuite.
  
```sql
USE AdventureWorks2012;  
GO  
DBCC FREESESSIONCACHE WITH NO_INFOMSGS;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  
