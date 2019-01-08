---
title: sp_add_log_file_recover_suspect_db (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_log_file_recover_suspect_db_TSQL
- sp_add_log_file_recover_suspect_db
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_log_file_recover_suspect_db
ms.assetid: b41ca3a5-7222-4c22-a012-e66a577a82f6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 525af6370b7e1af1591162109382005adbbf0bac
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52505647"
---
# <a name="spaddlogfilerecoversuspectdb-transact-sql"></a>sp_add_log_file_recover_suspect_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiunge un file di log a un filegroup quando non è possibile completare il recupero di un database a causa di spazio del log insufficiente (errore 9002). Dopo aver aggiunto il file, **sp_add_log_file_recover_suspect_db** disattiva l'impostazione sospetta e completa il recupero del database. I parametri sono identici a quelli dell'istruzione ALTER DATABASE *database_name* ADD LOG FILE.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_add_log_file_recover_suspect_db [ @dbName= ] 'database' ,   
    [ @name = ] 'logical_file_name' ,   
    [ @filename= ] 'os_file_name' ,   
    [ @size = ] 'size' ,   
    [ @maxsize = ] 'max_size' ,   
    [ @filegrowth = ] 'growth_increment'  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@dbName =** ] **'**_database_**'**  
 Nome del database. *database* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@name=** ] **'**_logical_file_name_**'**  
 Nome utilizzato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per fare riferimento al file. Deve essere un nome univoco nel server. *logical_file_name* viene **nvarchar(260)**, non prevede alcun valore predefinito.  
  
 [  **@filename =** ] **'**_os_file_name_**'**  
 Percorso e nome di file utilizzato dal sistema operativo per il file. Il file deve essere disponibile nel server in cui è installato [!INCLUDE[ssDE](../../includes/ssde-md.md)]. *os_file_name* viene **nvarchar(260)**, non prevede alcun valore predefinito.  
  
 [  **@size=** ] **'**_dimensioni_ **'**  
 Dimensioni iniziali del file. *le dimensioni* viene **nvarchar(20)**, con un valore predefinito è NULL. Specificare un numero intero, ovvero non includere decimali. È possibile utilizzare i suffissi MB e KB per specificare megabyte o kilobyte. Il valore predefinito è MB. Il valore minimo è 512 KB. Se *dimensioni* non viene specificato, il valore predefinito è 1 MB.  
  
 [  **@maxsize=** ] **'**_max_size_ **'**  
 Valore massimo fino a cui possono aumentare le dimensioni del file. *max_size* viene **nvarchar(20)**, con un valore predefinito è NULL. Specificare un numero intero, ovvero non includere decimali. È possibile utilizzare i suffissi MB e KB per specificare megabyte o kilobyte. Il valore predefinito è MB.  
  
 Se *max_size* non viene specificato, il file aumenterà finché il disco è pieno. Prima che si verifichi questa situazione, l'amministratore riceve un avviso dal registro applicazioni di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
 [  **@filegrowth=** ] **'**_growth_increment_ **'**  
 Quantità di spazio aggiunta al file ogni volta che è necessario spazio aggiuntivo. *growth_increment* viene **nvarchar(20)**, con un valore predefinito è NULL. Il valore 0 indica che le dimensioni non verranno aumentate. Specificare un numero intero, ovvero non includere decimali. È possibile specificare il valore in megabyte (MB) o in kilobyte (KB) oppure in forma di percentuale (%). Se si utilizza il suffisso %, l'incremento corrisponde alla percentuale specificata delle dimensioni del file quando si verifica l'incremento. Se si specifica un valore senza il suffisso MB, KB o %, il suffisso predefinito è MB.  
  
 Se *growth_increment* è NULL, il valore predefinito è 10% e il valore minimo è 64 KB. Le dimensioni specificate vengono arrotondate al blocco di 64 KB più prossimo.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 None  
  
## <a name="permissions"></a>Permissions  
 Autorizzazioni per impostazione predefinita ai membri di eseguire la **sysadmin** ruolo predefinito del server. Queste autorizzazioni non sono trasferibili.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente, il database `db1` è stato contrassegnato come sospetto durante il recupero a causa di spazio insufficiente nel log (errore 9002).  
  
```  
USE master;  
GO  
EXEC sp_add_log_file_recover_suspect_db db1, logfile2,  
'C:\Program Files\Microsoft SQL  
    Server\MSSQL13.MSSQLSERVER\MSSQL\Data\db1_logfile2.ldf',   
    '1MB';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sp_add_data_file_recover_suspect_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-data-file-recover-suspect-db-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
