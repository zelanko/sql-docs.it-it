---
title: DBCC DROPCLEANBUFFERS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROPCLEANBUFFERS
- DBCC_DROPCLEANBUFFERS_TSQL
- DROPCLEANBUFFERS_TSQL
- DBCC DROPCLEANBUFFERS
dev_langs:
- TSQL
helpviewer_keywords:
- clean buffers
- cold buffer cache
- buffer pools [SQL Server]
- dropping buffers
- removing buffers
- DBCC DROPCLEANBUFFERS statement
ms.assetid: a4121927-f2ce-4926-aa2c-9b1519dac048
author: pmasl
ms.author: umajay
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a3b2d2ff81fddaae0b0ae68da9d4477819a61073
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68101927"
---
# <a name="dbcc-dropcleanbuffers-transact-sql"></a>DBCC DROPCLEANBUFFERS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

Rimuove tutti i buffer vuoti dal pool di buffer e gli oggetti columnstore dal pool di oggetti columnstore.
  
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi
Sintassi per SQL Server: 

```sql
DBCC DROPCLEANBUFFERS [ WITH NO_INFOMSGS ]  
```  
Sintassi per Azure SQL Warehouse e Parallel Data Warehouse:

```sql  
DBCC DROPCLEANBUFFERS ( COMPUTE | ALL ) [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argomenti  
 WITH NO_INFOMSGS  
 Disattiva tutti i messaggi informativi. I messaggi informativi vengono soppressi sempre in [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
 COMPUTE  
 Cancellare la cache dei dati in memoria da ogni nodo di calcolo.  
  
 ALL  
 Cancellare la cache dei dati in memoria da ogni nodo di calcolo e dal nodo di controllo. Si tratta dell'impostazione predefinita se non viene specificato alcun valore.  
  
## <a name="remarks"></a>Remarks  
Utilizzare DBCC DROPCLEANBUFFERS per testare le query con una cache dei buffer "a freddo" senza arrestare e riavviare il server.
Per eliminare i buffer vuoti dal pool dei buffer e gli oggetti columnstore dal pool di oggetti columnstore, usare innanzitutto CHECKPOINT per creare una cache dei buffer a freddo. In questo modo tutte le pagine dirty del database corrente verranno scritte su disco e i buffer verranno svuotati. A questo punto sarà possibile eseguire il comando DBCC DROPCLEANBUFFERS per rimuovere tutti i buffer dal pool dei buffer.
  
## <a name="result-sets"></a>Set di risultati  
DBCC DROPCLEANBUFFERS in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituisce:
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Autorizzazioni  

Si applica a: SQL Server, Parallel Data Warehouse 

- È richiesta l'appartenenza al ruolo predefinito del server **sysadmin** .  

Si applica a: Azure SQL Data Warehouse

- Richiede l'appartenenza al ruolo predefinito del server DB_OWNER.  
  
## <a name="see-also"></a>Vedere anche  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[CHECKPOINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)  
  
  
