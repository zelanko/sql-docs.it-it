---
title: DBCC HELP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC HELP
- DBCC_HELP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DBCC statement syntax information
- DBCC HELP statement
ms.assetid: 306092c6-4354-4e47-928b-606124fbdc6e
author: pmasl
ms.author: umajay
manager: craigg
ms.openlocfilehash: 81523c69052a89b5a94c170c65be077ba17e56c6
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/09/2019
ms.locfileid: "57685178"
---
# <a name="dbcc-help-transact-sql"></a>DBCC HELP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Restituisce informazioni sulla sintassi per il comando DBCC specificato.
  
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi  
  
```sql
DBCC HELP ( 'dbcc_statement' | @dbcc_statement_var | '?' )  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argomenti  
 *dbcc_statement* | *@dbcc_statement_var*  
 Nome del comando DBCC di cui si desidera ricevere informazioni sulla sintassi. Specificare solo la parte del comando DBCC che segue DBCC, ad esempio, CHECKDB invece di DBCC CHECKDB.  
  
 ?  
 Restituisce tutti i comandi DBCC per cui sono disponibili informazioni della Guida.  
  
 WITH NO_INFOMSGS  
 Evita la visualizzazione di tutti i messaggi informativi con livello di gravità compreso tra 0 e 10.  
  
## <a name="result-sets"></a>Set di risultati  
DBCC HELP restituisce un set di risultati costituito dalla sintassi del comando DBCC specificato.
  
## <a name="permissions"></a>Permissions  
È richiesta l'appartenenza al ruolo predefinito del server **sysadmin** .
  
## <a name="examples"></a>Esempi  
### <a name="a-using-dbcc-help-with-a-variable"></a>A. Utilizzo dell'istruzione DBCC HELP con una variabile  
Nell'esempio seguente vengono restituite informazioni sulla sintassi per DBCC `CHECKDB`.
  
```sql  
DECLARE @dbcc_stmt sysname;  
SET @dbcc_stmt = 'CHECKDB';  
DBCC HELP (@dbcc_stmt);  
GO  
```  
  
### <a name="b-using-dbcc-help-with-the--option"></a>b. Utilizzo dell'istruzione DBCC HELP con ? come Opzione  
Nell'esempio seguente vengono restituite tutte le istruzioni DBCC per le quali sono disponibili informazioni della Guida.
  
```sql  
DBCC HELP ('?');  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  
