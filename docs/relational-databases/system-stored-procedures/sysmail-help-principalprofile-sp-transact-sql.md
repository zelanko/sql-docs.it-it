---
title: sysmail_help_principalprofile_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_principalprofile_sp_TSQL
- sysmail_help_principalprofile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_principalprofile_sp
ms.assetid: 0cfd6464-09c7-4f03-9d25-58001c096a9e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5bc48bb3edbeaad5593f574676e61ab2ca7f727f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68044524"
---
# <a name="sysmailhelpprincipalprofilesp-transact-sql"></a>sysmail_help_principalprofile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce un elenco di informazioni sulle associazioni tra i profili di Posta elettronica database e le entità di database.  
  
 
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sysmail_help_principalprofile_sp [ {   [ @principal_id = ] principal_id | [ @principal_name = ] 'principal_name' } ]  
    [ [ , ] {   [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' } ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @principal_id = ] principal_id` È l'ID dell'utente del database o del ruolo nel **msdb** database per l'associazione all'elenco. *principal_id* viene **int**, con un valore predefinito è NULL. Entrambi *principal_id* oppure *principal_name* può essere specificato.  
  
`[ @principal_name = ] 'principal_name'` È il nome dell'utente del database o del ruolo nel **msdb** database per l'associazione all'elenco. *principal_name* viene **sysname**, con un valore predefinito è NULL. Entrambi *principal_id* oppure *principal_name* può essere specificato.  
  
`[ @profile_id = ] profile_id` È l'ID del profilo per l'associazione all'elenco. *profile_id* viene **int**, con un valore predefinito è NULL. Entrambi *profile_id* oppure *profile_name* può essere specificato.  
  
`[ @profile_name = ] 'profile_name'` È il nome del profilo per l'associazione all'elenco. *profile_name* viene **sysname**, con un valore predefinito è NULL. Entrambi *profile_id* oppure *profile_name* può essere specificato.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 Restituisce un set di risultati contenente le colonne elencate nella tabella seguente.  
  
||||  
|-|-|-|  
|Nome colonna|Tipo di dati|Descrizione|  
|**principal_id**|**int**|ID dell'utente del database.|  
|**principal_name**|**sysname**|Nome dell'utente del database.|  
|**profile_id**|**int**|Numero ID del profilo di Posta elettronica database.|  
|**profile_name**|**sysname**|Nome del profilo di Posta elettronica database.|  
|**is_default**|**bit**|Flag che indica se il profilo è il profilo predefinito per l'utente.|  
  
## <a name="remarks"></a>Note  
 Se **sysmail_help_principalprofile_sp** viene richiamata senza parametri, il set di risultati restituito sono elencate tutte le associazioni nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Negli altri casi il set di risultati conterrà le informazioni relative alle associazioni che corrispondono ai parametri specificati. Se ad esempio si specifica il nome di un profilo, la procedura elenca tutte le associazioni per tale profilo.  
  
 **sysmail_help_principalprofile_sp** è nel **msdb** del database ed è di proprietà il **dbo** dello schema. La procedura deve essere eseguita con un nome in tre parti se il database corrente non è **msdb**.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'appartenenza al ruolo predefinito del server **sysadmin** .  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-listing-information-for-a-specific-association"></a>R. Visualizzazione delle informazioni relative a un'associazione specifica  
 Nell'esempio seguente viene illustrato come visualizzare le informazioni relative a tutte le associazioni tra il profilo `AdventureWorks Administrator` e l'entità `ApplicationLogin` nel database `msdb`.  
  
```  
EXECUTE msdb.dbo.sysmail_help_principalprofile_sp  
    @principal_name = 'danw',  
    @profile_name = 'AdventureWorks Administrator' ;  
```  
  
 Set di risultati di esempio, riformattato in base alla lunghezza di riga:  
  
```  
principal_id principal_name     profile_id  profile_name                   is_default  
------------ ------------------ ----------- ------------------------------ ----------  
5            danw               9           AdventureWorks Administrator   1  
```  
  
### <a name="b-listing-information-for-all-associations"></a>B. Visualizzazione delle informazioni relative a tutte le associazioni  
 Nell'esempio seguente viene illustrato come visualizzare le informazioni relative a tutte le associazioni nell'istanza.  
  
```  
EXECUTE msdb.dbo.sysmail_help_principalprofile_sp ;  
```  
  
 Set di risultati di esempio, riformattato in base alla lunghezza di riga:  
  
```  
principal_id principal_name     profile_id  profile_name                   is_default  
------------ ------------------ ----------- ------------------------------ ----------  
6            terrid             3           Product Update Profile         1  
5            danw               9           AdventureWorks Administrator   1  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Posta elettronica database](../../relational-databases/database-mail/database-mail.md)   
 [Stored procedure di posta elettronica database &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
