---
title: sp_helpdb (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpdb
- sp_helpdb_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpdb
ms.assetid: 4c3e3302-6cf1-4b2b-8682-004049b578c3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7acc14d3950e0e2d1004727b2efbffd2e4963a2b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67903023"
---
# <a name="sphelpdb-transact-sql"></a>sp_helpdb (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni su un database specifico o su tutti i database.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helpdb [ [ @dbname= ] 'name' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @dbname = ] 'name'` È il nome del database per il quale vengono restituite informazioni. *nome* viene **sysname**, non prevede alcun valore predefinito. Se *nome* non viene specificato, **sp_helpdb** segnala tutti i database di **Sys. Databases** vista del catalogo.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome del database.|  
|**db_size**|**nvarchar(13)**|Dimensioni totali del database.|  
|**Proprietario**|**sysname**|Proprietario del database, ad esempio **sa**.|  
|**dbid**|**smallint**|ID del database.|  
|**created**|**nvarchar(11)**|Data di creazione del database.|  
|**status**|**nvarchar(600)**|Elenco separato da virgola dei valori delle opzioni impostate nel database.<br /><br /> Le opzioni con valori booleani vengono elencate solo se sono abilitate. Sono elencate le opzioni non booleane con i relativi valori nel formato *option_name*=*valore*.<br /><br /> Per altre informazioni, vedere [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).|  
|**compatibility_level**|**tinyint**|Livello di compatibilità del database: 60, 65, 70, 80 o 90.|  
  
 Se *nome* viene specificato, è un set di risultati aggiuntivo che mostra l'allocazione dei file per il database specificato.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**name**|**nchar(128)**|Nome logico del file.|  
|**fileid**|**smallint**|ID di file.|  
|**filename**|**nchar(260)**|Nome del file del sistema operativo, ovvero nome fisico del file.|  
|**filegroup**|**nvarchar(128)**|Filegroup a cui appartiene il file.<br /><br /> NULL = Il file è un file di log. Questo tipo di file non viene mai incluso in un filegroup.|  
|**size**|**nvarchar(18)**|Dimensione del file espressa in megabyte.|  
|**maxsize**|**nvarchar(18)**|Dimensioni massime consentite per il file. Se questo campo include il valore UNLIMITED, le dimensioni del file possono aumentare fino a riempire il disco.|  
|**growth**|**nvarchar(18)**|Incremento per l'aumento delle dimensioni del file. Indica la quantità di spazio aggiunta al file ogni volta che è necessario spazio aggiuntivo.|  
|**usage**|**varchar(9)**|Utilizzo del file. Per un file di dati, il valore è **'solo data'** e per il file di log è il valore **'di log solo'** .|  
  
## <a name="remarks"></a>Note  
 Il **stato** colonna nel risultato del set di report quali opzioni sono state impostate su ON nel database. Tutte le opzioni di database non vengono segnalate dal **stato** colonna. Per visualizzare un elenco completo delle impostazioni correnti del database, usare il **Sys. Databases** vista del catalogo.  
  
## <a name="permissions"></a>Permissions  
 Quando viene specificato un singolo database, l'appartenenza al **pubblica** ruolo del database è obbligatorio. Quando si specifica alcun database, l'appartenenza al **pubblico** ruolo nel **master** database è obbligatorio.  
  
 Se non è accessibile un database **sp_helpdb** Visualizza messaggio 15622 e tutte le informazioni sull'errore relative al database possibile.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-returning-information-about-a-single-database"></a>R. Restituzione di informazioni su un solo database  
 Nell'esempio seguente vengono visualizzate informazioni sul database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
EXEC sp_helpdb N'AdventureWorks2012';  
```  
  
### <a name="b-returning-information-about-all-databases"></a>B. Restituzione di informazioni su tutti i database  
 Nell'esempio seguente vengono visualizzate informazioni su tutti i database nel server che esegue [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```sql  
EXEC sp_helpdb;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Motore di database le Stored procedure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
