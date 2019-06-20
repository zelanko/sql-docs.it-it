---
title: sp_attach_single_file_db (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_attach_single_file_db
- sp_attach_single_file_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_attach_single_file_db
ms.assetid: 13bd1044-9497-4293-8390-1f12e6b8e952
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d8d2ad4c7df20b2b9649b1ad780dd40353a7796e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62996807"
---
# <a name="spattachsinglefiledb-transact-sql"></a>sp_attach_single_file_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Collega al server corrente un database che include solo un file di dati. **sp_attach_single_file_db** non può essere usato con più file di dati.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] È consigliabile utilizzare CREATE DATABASE *database_name* FOR ATTACH invece. Per alte informazioni, vedere [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md). Non utilizzare questa procedura per database replicati.  
  
> [!IMPORTANT]  
>  È consigliabile evitare di collegare o ripristinare database provenienti da origini sconosciute o non attendibili. Tali database possono contenere codice dannoso che potrebbe eseguire codice [!INCLUDE[tsql](../../includes/tsql-md.md)] indesiderato o causare errori modificando lo schema o la struttura fisica di database. Prima di utilizzare un database da un'origine sconosciuta o non attendibile, eseguire [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) sul database in un server non di produzione ed esaminare il codice contenuto nel database, ad esempio le stored procedure o altro codice definito dall'utente.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_attach_single_file_db [ @dbname= ] 'dbname'  
    , [ @physname= ] 'physical_name'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @dbname = ] 'dbname'` È il nome del database da collegare al server. Il nome deve essere univoco. *dbname* viene **sysname**, con un valore predefinito è NULL.  
  
`[ @physname = ] 'physical_name'` È il nome fisico, completo di percorso, del file di database. *physical_name* viene **nvarchar(260)**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  Questo argomento esegue il mapping al parametro FILENAME dell'istruzione CREATE DATABASE. Per alte informazioni, vedere [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md).  
  
 Quando si collega un database di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] contenente file di cataloghi full-text in un'istanza del server di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , i file di catalogo vengono collegati dal percorso precedente insieme agli altri file del database, come in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Per altre informazioni, vedere [Aggiornamento della ricerca full-text](../../relational-databases/search/upgrade-full-text-search.md).  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 None  
  
## <a name="remarks"></a>Note  
 Uso **sp_attach_single_file_db** solo sui database che sono stati precedentemente scollegati dal server tramite l'impostazione esplicita **sp_detach_db** operazione o in database copiati.  
  
 **sp_attach_single_file_db** funziona solo con i database con un singolo file di log. Quando **sp_attach_single_file_db** collega il database nel server, compila un nuovo file di log. Se il database è di sola lettura, il file di log verrà creato nella relativa posizione precedente.  
  
> [!NOTE]  
>  Non è possibile scollegare o collegare uno snapshot del database.  
  
 Non utilizzare questa procedura per database replicati.  
  
## <a name="permissions"></a>Permissions  
 Per informazioni su come gestire le autorizzazioni quando un database viene collegato, vedere [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md).  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene scollegato il database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], quindi uno dei file inclusi nel database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] viene collegato al server corrente.  
  
```  
USE master;  
GO  
EXEC sp_detach_db @dbname = 'AdventureWorks2012';  
EXEC sp_attach_single_file_db @dbname = 'AdventureWorks2012',   
    @physname =   
N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\AdventureWorks2012_Data.mdf';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Collegamento e scollegamento di un database &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [sp_detach_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)   
 [sp_helpfile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
