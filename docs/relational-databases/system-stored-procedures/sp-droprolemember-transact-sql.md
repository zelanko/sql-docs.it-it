---
title: sp_droprolemember (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_droprolemember_TSQL
- sp_droprolemember
dev_langs:
- TSQL
helpviewer_keywords:
- sp_droprolemember
ms.assetid: c2f19ab1-e742-4d56-ba8e-8ffd40cf4925
ms.author: vanto
author: VanMSFT
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7123c1bd3fee61a3d0671a0d8fbe27c2943ba7ea
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124854"
---
# <a name="spdroprolemember-transact-sql"></a>sp_droprolemember (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Rimuove un account di sicurezza da un ruolo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel database corrente.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Uso [ALTER ROLE](../../t-sql/statements/alter-role-transact-sql.md) invece.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  

### <a name="syntax-for-both-sql-server-and-azure-sql-database"></a>Sintassi per SQL Server e Database SQL di Azure

```  
sp_droprolemember [ @rolename = ] 'role' ,   
     [ @membername = ] 'security_account'  
```  

### <a name="syntax-for-both-azure-sql-data-warehouse-and-parallel-data-warehouse"></a>Sintassi per Azure SQL Data Warehouse e Parallel Data Warehouse

```  
sp_droprolemember 'role' ,  
     'security_account'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @rolename = ] 'role'` È il nome del ruolo da cui si desidera rimuovere il membro. *ruolo* viene **sysname**, non prevede alcun valore predefinito. *ruolo* deve esistere nel database corrente.  
  
`[ @membername = ] 'security_account'` Il nome dell'account di sicurezza verrà rimosso dal ruolo. *account_protezione* viene **sysname**, non prevede alcun valore predefinito. *account_protezione* può essere un utente del database, un altro ruolo del database, un account di accesso di Windows o un gruppo di Windows. *account_protezione* deve esistere nel database corrente.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Note  
 sp_droprolemember rimuove un membro da un ruolo del database eliminando una riga dalla tabella sysmembers. Quando un membro viene rimosso da un ruolo il membro perde ogni autorizzazione di cui dispone tramite l'appartenenza a quel ruolo.  
  
 Per rimuovere un utente da un ruolo predefinito del server, usare sp_dropsrvrolemember. Gli utenti non possono essere rimossi dal ruolo public e non può essere rimosso da alcun ruolo dbo.  
  
 Usare sp_helpuser per visualizzare i membri di un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ruolo e usare ALTER ROLE per aggiungere un membro a un ruolo.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione ALTER per il ruolo.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente l'utente `JonB` viene rimosso dal ruolo `Sales`.  
  
```sql
EXEC sp_droprolemember 'Sales', 'Jonb';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Nell'esempio seguente l'utente `JonB` viene rimosso dal ruolo `Sales`.  
  
```sql
EXEC sp_droprolemember 'Sales', 'JonB'  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sicurezza &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_droprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droprole-transact-sql.md)   
 [sp_dropsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [sp_helpuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

