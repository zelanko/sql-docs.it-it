---
title: sp_helprotect (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helprotect
- sp_helprotect_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helprotect
ms.assetid: faaa3e40-1c95-43c2-9fdc-c61a1d3cc0c3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8f98f62b10b38d726feec2bd427bc7d1fc6dcea9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62635868"
---
# <a name="sphelprotect-transact-sql"></a>sp_helprotect (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce un report con informazioni sulle autorizzazioni utente per un oggetto o sulle autorizzazioni per le istruzioni, nel database corrente.  
  
> [!IMPORTANT]  
>  **sp_helprotect** non restituisce invece informazioni sulle entità a protezione diretta introdotte in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Uso [Sys. database_permissions](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) e [fn_builtin_permissions](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md) invece.  
  
 Non elenca le autorizzazioni che sono sempre assegnate ai ruoli predefiniti del server o del database. Non include gli account di accesso o gli utenti che ricevono autorizzazioni in base all'appartenenza a un ruolo.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helprotect [ [ @name = ] 'object_statement' ]   
     [ , [ @username = ] 'security_account' ]   
     [ , [ @grantorname = ] 'grantor' ]   
     [ , [ @permissionarea = ] 'type' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @name = ] 'object_statement'` È il nome dell'oggetto nel database corrente, o un'istruzione, che abbia le autorizzazioni per report. *object_statement* viene **nvarchar(776)**, valore predefinito è NULL, che restituisce tutte le autorizzazioni per oggetti e istruzione. Se il valore è un oggetto, quale una tabella, una vista, una stored procedure o una stored procedure estesa, deve essere un oggetto valido nel database corrente. Il nome dell'oggetto può includere un qualificatore del proprietario nel formato _owner_**.** _oggetto_.  
  
 Se *object_statement* è un'istruzione, può essere un'istruzione CREATE.  
  
`[ @username = ] 'security_account'` È il nome dell'entità per il quale vengono restituite autorizzazioni. *account_protezione* viene **sysname**, valore predefinito è NULL, che restituisce tutte le entità nel database corrente. *account_protezione* deve esistere nel database corrente.  
  
`[ @grantorname = ] 'grantor'` È il nome dell'entità che ha le autorizzazioni concesse. *utente che concede* viene **sysname**, valore predefinito è NULL, che restituisce tutte le informazioni relative alle autorizzazioni concesse da qualsiasi entità nel database.  
  
`[ @permissionarea = ] 'type'` È una stringa di caratteri che indica se visualizzare autorizzazioni per oggetti (stringa di caratteri **o**), le autorizzazioni di istruzione (stringa di caratteri **s**), o entrambi (**os**). *tipo di* viene **varchar (10)**, il valore predefinito è **os**. *tipo di* può essere qualsiasi combinazione dei **o** e **s**, con o senza virgole o spazi tra **o** e **s**.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**Proprietario**|**sysname**|Nome del proprietario dell'oggetto.|  
|**Oggetto**|**sysname**|Nome dell'oggetto.|  
|**All'utente autorizzato**|**sysname**|Nome dell'entità a cui sono state concesse le autorizzazioni.|  
|**Utente che concede le autorizzazioni**|**sysname**|Nome dell'entità che ha concesso le autorizzazioni all'entità autorizzata specificata.|  
|**ProtectType**|**nvarchar(10)**|Nome del tipo di protezione:<br /><br /> GRANT REVOKE|  
|**Azione**|**nvarchar(60)**|Nome dell'autorizzazione. La validità delle istruzioni di autorizzazione dipende dal tipo di oggetto.|  
|**Colonna**|**sysname**|Tipo di autorizzazione:<br /><br /> All = L'autorizzazione è valida per tutte le colonne correnti dell'oggetto.<br /><br /> New = L'autorizzazione è valida per le nuove colonne che potrebbero essere modificate in futuro nell'oggetto (tramite l'istruzione ALTER).<br /><br /> All+New = L'autorizzazione è valida sia per le colonne correnti che per le nuove colonne.<br /><br /> Restituisce un punto se il tipo di autorizzazione non si applica alle colonne.|  
  
## <a name="remarks"></a>Note  
 Tutti i parametri nella procedura seguente sono facoltativi. Se vengono omessi tutti i parametri, `sp_helprotect` visualizza tutte le autorizzazioni concesse o negate nel database corrente.  
  
 Se vengono specificati alcuni parametri, ma non tutti, utilizzare i parametri denominati per identificare i vari parametri oppure utilizzare `NULL` come segnaposto dei parametri omessi. Ad esempio, per restituire tutte le autorizzazioni per il proprietario di database (`dbo`) che concede le autorizzazioni, eseguire l'istruzione seguente:  
  
```  
EXEC sp_helprotect NULL, NULL, dbo;  
```  
  
 e  
  
```  
EXEC sp_helprotect @grantorname = 'dbo';  
```  
  
 Il report di output viene ordinato in base a categoria di autorizzazioni, proprietario, oggetto, entità a cui è stata concessa l'autorizzazione, entità che ha concesso l'autorizzazione, categoria del tipo di protezione, tipo di protezione, azione e ID sequenziale di colonna.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'appartenenza al ruolo **public** .  
  
 Le informazioni restituite sono soggette a limitazioni di accesso ai metadati. Non vengono visualizzate le entità per le quali l'entità di database non dispone dell'autorizzazione. Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-listing-the-permissions-for-a-table"></a>A. Visualizzazione dell'elenco delle autorizzazioni per una tabella  
 Nell'esempio seguente vengono elencate le autorizzazioni per la tabella `titles`.  
  
```  
EXEC sp_helprotect 'titles';  
```  
  
### <a name="b-listing-the-permissions-for-a-user"></a>B. Visualizzazione dell'elenco delle autorizzazioni per un utente  
 Nell'esempio seguente vengono elencate tutte le autorizzazioni disponibili per l'utente `Judy` nel database corrente.  
  
```  
EXEC sp_helprotect NULL, 'Judy';  
```  
  
### <a name="c-listing-the-permissions-granted-by-a-specific-user"></a>C. Visualizzazione dell'elenco delle autorizzazioni concesse da un utente specifico  
 Nell'esempio seguente vengono elencate tutte le autorizzazioni concesse dall'utente `Judy` nel database corrente, utilizzando il valore `NULL` come segnaposto per i parametri omessi.  
  
```  
EXEC sp_helprotect NULL, NULL, 'Judy';  
```  
  
### <a name="d-listing-the-statement-permissions-only"></a>D. Visualizzazione del solo elenco delle autorizzazioni per le istruzioni  
 Nell'esempio seguente vengono elencate tutte le autorizzazioni per le istruzioni nel database corrente, utilizzando il valore `NULL` come segnaposto per i parametri mancanti.  
  
```  
EXEC sp_helprotect NULL, NULL, NULL, 's';   
```  
  
### <a name="e-listing-the-permissions-for-a-create-statement"></a>e. Elenco delle autorizzazioni per un'istruzione CREATE  
 Nell'elenco di esempio seguente sono inclusi tutti gli utenti che dispongono dell'autorizzazione CREATE TABLE.  
  
```  
EXEC sp_helprotect @name = 'CREATE TABLE';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sicurezza &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
