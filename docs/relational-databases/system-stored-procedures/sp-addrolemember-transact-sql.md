---
title: sp_addrolemember (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/30/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addrolemember_TSQL
- sp_addrolemember
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addrolemember
ms.assetid: a583c087-bdb3-46d2-b9e5-3921b3e6d10b
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6d7b47670d56ab916a8c2f263f9ddee3dc85c0a6
ms.sourcegitcommit: c4870cb5bebf9556cdb4d8b35ffcca265fb07862
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2019
ms.locfileid: "55652540"
---
# <a name="spaddrolemember-transact-sql"></a>sp_addrolemember (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Aggiunge un utente del database, un ruolo del database, un account di accesso di Windows o un gruppo di Windows a un ruolo del database nel database corrente.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Uso [ALTER ROLE](../../t-sql/statements/alter-role-transact-sql.md) invece.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```
sp_addrolemember [ @rolename = ] 'role', [ @membername = ] 'security_account'  

```    
  
## <a name="arguments"></a>Argomenti  
 [ @rolename= ] '*role*'  
 Nome del ruolo del database nel database corrente. *ruolo* è un **sysname**, non prevede alcun valore predefinito.  
  
 [ @membername= ] '*security_account*'  
 Account di sicurezza aggiunto al ruolo. *account_protezione* è un **sysname**, non prevede alcun valore predefinito. *account_protezione* può essere un utente del database, ruolo predefinito del database, account di accesso di Windows o il gruppo di Windows.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Note  
 Un membro aggiunto al ruolo tramite la stored procedure sp_addrolemember eredita le autorizzazioni del ruolo. Se il nuovo membro è un'entità a livello di Windows senza un corrispondente utente del database, verrà creato un utente del database, di cui tuttavia potrebbe non essere eseguito completamente il mapping all'account di accesso. Verificare sempre che l'account di accesso esista e che sia in grado di accedere al database.  
  
 Un ruolo non può includere sé stesso come membro. Tali definizioni "circolari" non sono valide anche quando l'appartenenza è indirettamente sottintesa da una o più appartenenze intermedie.  
  
 sp_addrolemember non è possibile aggiungere un ruolo predefinito del database, ruolo predefinito del server o dbo a un ruolo. sp_addrolemember non può essere eseguita all'interno di una transazione definita dall'utente.  
  
 Utilizzare sp_addrolemember solo per aggiungere un membro a un ruolo del database. Per aggiungere un membro a un ruolo del server, utilizzare [sp_addsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Per l'aggiunta di membri ai ruoli del database flessibili è necessario uno degli elementi seguenti:  
  
-   Appartenenza al ruolo predefinito del database db_owner o db_securityadmin.  
  
-   Appartenenza al ruolo proprietario del ruolo.  
  
-   **ALTER ANY ROLE** autorizzazione oppure **ALTER** autorizzazione per il ruolo.  
  
 Per l'aggiunta di membri ai ruoli predefiniti del database è necessaria l'appartenenza al ruolo predefinito del database db_owner.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-adding-a-windows-login"></a>A. Aggiunta di un account di accesso di Windows  
 L'esempio seguente aggiunge l'account di accesso di Windows `Contoso\Mary5` per il `AdventureWorks2012` database come utente `Mary5`. L'utente `Mary5` viene quindi aggiunto al ruolo `Production`.  
  
> [!NOTE]  
>  Poiché `Contoso\Mary5` è noto come utente del database `Mary5` nel database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)], è necessario specificare il nome utente `Mary5`. L'istruzione non verrà eseguita correttamente se non esiste un account di accesso `Contoso\Mary5`. Eseguire un test mediante un account di accesso dal dominio.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE USER Mary5 FOR LOGIN [Contoso\Mary5] ;  
GO  
```  
  
### <a name="b-adding-a-database-user"></a>b. Aggiunta di un utente del database  
 Nell'esempio seguente l'utente del database `Mary5` viene aggiunto al ruolo del database `Production` nel database corrente.  
  
```  
EXEC sp_addrolemember 'Production', 'Mary5';  
```  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-adding-a-windows-login"></a>C. Aggiunta di un account di accesso di Windows  
 L'esempio seguente aggiunge l'account di accesso `LoginMary` per il `AdventureWorks2008R2` database come utente `UserMary`. L'utente `UserMary` viene quindi aggiunto al ruolo `Production`.  
  
> [!NOTE]  
>  Poiché l'account di accesso `LoginMary` è noto come utente del database `UserMary` nel [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] del database, il nome utente `UserMary` deve essere specificato. L'istruzione non verrà eseguita correttamente se non esiste un account di accesso `Mary5`. Gli account di accesso e utenti in genere hanno lo stesso nome. In questo esempio Usa nomi diversi per differenziare le azioni che interessano l'account di accesso e l'utente.  
  
```  
-- Uses AdventureWorks  
  
CREATE USER UserMary FOR LOGIN LoginMary ;  
GO  
EXEC sp_addrolemember 'Production', 'UserMary'  
```  
  
### <a name="d-adding-a-database-user"></a>D. Aggiunta di un utente del database  
 Nell'esempio seguente l'utente del database `UserMary` viene aggiunto al ruolo del database `Production` nel database corrente.  
  
```  
EXEC sp_addrolemember 'Production', 'UserMary'  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sicurezza &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)   
 [sp_droprolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [sp_grantdbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Ruoli a livello di database](../../relational-databases/security/authentication-access/database-level-roles.md)  
  
  
