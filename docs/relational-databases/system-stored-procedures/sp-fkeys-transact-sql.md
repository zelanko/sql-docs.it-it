---
title: sp_fkeys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fkeys
- sp_fkeys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fkeys
ms.assetid: 18110444-d38d-4cff-90d2-d1fc6236668b
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cb5f684321a11d56a419ae73be0bfb2950fb9939
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124397"
---
# <a name="spfkeys-transact-sql"></a>sp_fkeys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce informazioni sulle chiavi esterne logiche per l'ambiente corrente. Questa procedura visualizza le relazioni di chiave esterna, incluse le chiavi esterne disabilitate.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
sp_fkeys [ @pktable_name = ] 'pktable_name'   
     [ , [ @pktable_owner = ] 'pktable_owner' ]   
     [ , [ @pktable_qualifier = ] 'pktable_qualifier' ]   
     { , [ @fktable_name = ] 'fktable_name' }   
     [ , [ @fktable_owner = ] 'fktable_owner' ]   
     [ , [ @fktable_qualifier = ] 'fktable_qualifier' ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @pktable_name=] '*pktable_name*'  
 Nome della tabella, contenente la chiave primaria, utilizzata per restituire informazioni del catalogo. *pktable_name* viene **sysname**, con un valore predefinito è NULL. I criteri di ricerca con caratteri jolly non sono supportati. Questo parametro o il *fktable_name* parametro o entrambi, deve essere forniti.  
  
 [ @pktable_owner=] '*pktable_owner*'  
 È il nome del proprietario della tabella (con la chiave primaria) utilizzata per restituire informazioni del catalogo. *pktable_owner* viene **sysname**, con un valore predefinito è NULL. I criteri di ricerca con caratteri jolly non sono supportati. Se *pktable_owner* non viene specificato, si applicano le regole di visibilità della tabella predefinite del sistema DBMS sottostante.  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se l'utente corrente è il proprietario di una tabella avente il nome specificato, vengono restituite le colonne di tale tabella. Se *pktable_owner* non viene specificato e l'utente corrente non dispone di una tabella con la proprietà specificata *pktable_name*, viene eseguita la ricerca per una tabella con la proprietà specificata *pktable_name* appartengono al proprietario del database. Se viene individuata, vengono restituite le colonne di tale tabella.  
  
 [ @pktable_qualifier =] '*pktable_qualifier*'  
 Nome del qualificatore della tabella contenente la chiave primaria. *pktable_qualifier* is sysname con valore predefinito è NULL. Vari prodotti DBMS supportano nomi di tabelle in tre parti (*composti*). In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il qualificatore rappresenta il nome del database. In altri prodotti rappresenta il nome del server dell'ambiente di database della tabella.  
  
 [ @fktable_name=] '*fktable_name*'  
 Nome della tabella contenente una chiave esterna, utilizzata per restituire informazioni del catalogo. *fktable_name* is sysname con valore predefinito è NULL. I criteri di ricerca con caratteri jolly non sono supportati. Questo parametro o il *pktable_name* parametro o entrambi, deve essere forniti.  
  
 [ @fktable_owner =] '*fktable_owner*'  
 Nome del proprietario della tabella contenente la chiave esterna, utilizzata per restituire informazioni del catalogo. *fktable_owner* viene **sysname**, con un valore predefinito è NULL. I criteri di ricerca con caratteri jolly non sono supportati. Se *fktable_owner* non viene specificato, si applicano le regole di visibilità della tabella predefinite del sistema DBMS sottostante.  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se l'utente corrente è il proprietario di una tabella avente il nome specificato, vengono restituite le colonne di tale tabella. Se *fktable_owner* non viene specificato e l'utente corrente non dispone di una tabella con la proprietà specificata *fktable_name*, viene eseguita la ricerca per una tabella con la proprietà specificata *fktable_name* appartengono al proprietario del database. Se viene individuata, vengono restituite le colonne di tale tabella.  
  
 [ @fktable_qualifier=] '*fktable_qualifier*'  
 Nome del qualificatore della tabella contenente una chiave esterna. *fktable_qualifier* viene **sysname**, con un valore predefinito è NULL. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il qualificatore rappresenta il nome del database. In altri prodotti rappresenta il nome del server dell'ambiente di database della tabella.  
  
## <a name="return-code-values"></a>Valori restituiti  
 Nessuna  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|PKTABLE_QUALIFIER|**sysname**|Nome del qualificatore della tabella contenente la chiave primaria. Questo campo può essere NULL.|  
|PKTABLE_OWNER|**sysname**|Nome del proprietario della tabella contenente la chiave primaria. Questo campo restituisce sempre un valore.|  
|PKTABLE_NAME|**sysname**|Nome della tabella contenente la chiave primaria. Questo campo restituisce sempre un valore.|  
|PKCOLUMN_NAME|**sysname**|Nome delle colonne chiave primaria, per ogni colonna della tabella TABLE_NAME restituita. Questo campo restituisce sempre un valore.|  
|FKTABLE_QUALIFIER|**sysname**|Nome del qualificatore della tabella contenente una chiave esterna. Questo campo può essere NULL.|  
|FKTABLE_OWNER|**sysname**|Nome del proprietario della tabella contenente una chiave esterna. Questo campo restituisce sempre un valore.|  
|FKTABLE_NAME|**sysname**|Nome della tabella contenente una chiave esterna. Questo campo restituisce sempre un valore.|  
|FKCOLUMN_NAME|**sysname**|Nome della colonna chiave esterna, per ogni colonna della tabella TABLE_NAME restituita. Questo campo restituisce sempre un valore.|  
|KEY_SEQ|**smallint**|Numero sequenziale della colonna in una chiave primaria a più colonne. Questo campo restituisce sempre un valore.|  
|UPDATE_RULE|**smallint**|Azione applicata alla chiave esterna quando l'operazione SQL è un aggiornamento.  I valori possibili sono:<br /> 0 = modifiche di tipo CASCADE alla chiave esterna.<br /> 1 = modifiche di tipo NO ACTION se la chiave esterna è presente.<br />   2 = impostazione su null <br /> 3 = impostazione del valore predefinito |  
|DELETE_RULE|**smallint**|Azione applicata alla chiave esterna quando l'operazione SQL è un'operazione di eliminazione. I valori possibili sono:<br /> 0 = modifiche di tipo CASCADE alla chiave esterna.<br /> 1 = modifiche di tipo NO ACTION se la chiave esterna è presente.<br />   2 = impostazione su null <br /> 3 = impostazione del valore predefinito |  
|FK_NAME|**sysname**|Identificatore della chiave esterna. NULL se non è applicabile all'origine dati. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituisce il nome del vincolo FOREIGN KEY.|  
|PK_NAME|**sysname**|Identificatore della chiave primaria. NULL se non è applicabile all'origine dati. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituisce il nome del vincolo PRIMARY KEY.|  
  
 I risultati restituiti vengono ordinati in base FKTABLE_QUALIFIER, FKTABLE_OWNER, FKTABLE_NAME e KEY_SEQ.  
  
## <a name="remarks"></a>Note  
 È possibile implementare codice di applicazione che include tabelle con chiavi esterne disabilitate nei modi seguenti:  
  
-   Disabilitazione temporanea del controllo dei vincoli ALTER TABLE NOCHECK o CREATE TABLE NOT FOR REPLICATION mentre si utilizzano le tabelle e successiva riabilitazione del controllo.  
  
-   Utilizzo di trigger o codice di applicazione per l'imposizione di relazioni.  
  
Se viene specificato il nome della tabella della chiave primaria e il nome della tabella della chiave esterna è NULL, sp_fkeys restituisce tutte le tabelle contenenti una chiave esterna per la tabella specificata. Se viene specificato il nome della tabella della chiave esterna e il nome della tabella della chiave primaria è NULL, sp_fkeys restituisce tutte le tabelle correlate tramite una relazione tra chiave primaria e chiave esterna per le chiavi esterne della tabella della chiave esterna.  
  
La stored procedure sp_fkeys è equivalente alla SQLForeignKeys in ODBC.  
  
## <a name="permissions"></a>Permissions  
 Richiede `SELECT` autorizzazione per lo schema.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene recuperato un elenco delle chiavi esterne per la tabella `HumanResources.Department` nel database `AdventureWorks2012`.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_fkeys @pktable_name = N'Department'  
    ,@pktable_owner = N'HumanResources';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Nell'esempio seguente viene recuperato un elenco delle chiavi esterne per la tabella `DimDate` nel database `AdventureWorksPDW2012`. Viene restituita alcuna riga perché [!INCLUDE[ssDW](../../includes/ssdw-md.md)] non supporta chiavi esterne.  
  
```sql  
EXEC sp_fkeys @pktable_name = N'DimDate;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Le Stored procedure del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_pkeys &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-pkeys-transact-sql.md)  
  
  

