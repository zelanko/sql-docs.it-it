---
title: sp_helplogins (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helplogins_TSQL
- sp_helplogins
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helplogins
ms.assetid: f9ad3767-5b9f-420d-8922-b637811404f7
author: stevestein
ms.author: sstein
ms.openlocfilehash: b4c3d6ded5d85e5d38556792aaa7ea71dd9f42fa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122446"
---
# <a name="sphelplogins-transact-sql"></a>sp_helplogins (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni sugli account di accesso e sugli utenti corrispondenti in ogni database.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helplogins [ [ @LoginNamePattern = ] 'login' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @LoginNamePattern = ] 'login'` È un nome di account di accesso. *login* è di tipo **sysname** e il valore predefinito è NULL. *account di accesso* deve esistere se specificato. Se *account di accesso* viene omesso, vengono restituite informazioni su tutti gli accessi.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 Il primo report contiene le informazioni su ogni account di accesso specificato, come illustrato nella tabella seguente.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**LoginName**|**sysname**|Nome dell'account di accesso.|  
|**SID**|**varbinary(85)**|ID di sicurezza (SID) dell'account di accesso.|  
|**DefDBName**|**sysname**|Database predefinito **LoginName** Usa quando ci si connette a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**DefLangName**|**sysname**|Lingua predefinita utilizzata da **LoginName**.|  
|**Auser**|**char(5)**|Yes = **LoginName** ha un nome utente associato in un database.<br /><br /> No = **LoginName** non dispone di un nome utente associato.|  
|**Associata**|**char(7)**|Yes = **LoginName** ha un account di accesso remoto associato.<br /><br /> No = **LoginName** non ha un account di accesso associato.|  
  
 Il secondo report contiene informazioni sugli utenti sui quali viene eseguito il mapping a ogni account di accesso e le appartenenze al ruolo dell'account di acceso, come illustrato nella tabella seguente.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**LoginName**|**sysname**|Nome dell'account di accesso.|  
|**DBName**|**sysname**|Database predefinito **LoginName** Usa quando ci si connette a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**UserName**|**sysname**|Account utente su cui **LoginName** viene eseguito il mapping nei **DBName**e i ruoli che **LoginName** è un membro nel **DBName**.|  
|**UserOrAlias**|**char(8)**|MemberOf = **UserName** è un ruolo.<br /><br /> Utente = **UserName** è un account utente.|  
  
## <a name="remarks"></a>Note  
 Prima di rimuovere un account di accesso, usare **sp_helplogins** per identificare gli account utente che vengono eseguito il mapping all'account di accesso.  
  
## <a name="permissions"></a>Permissions  
 Richiede l'appartenenza al **securityadmin** ruolo predefinito del server.  
  
 Per identificare tutti gli account utente mappati a un determinato account di accesso **sp_helplogins** deve controllare tutti i database all'interno del server. Pertanto, per ogni database nel server, è necessario che sia soddisfatta almeno una delle seguenti condizioni:  
  
-   L'utente che esegue **sp_helplogins** dispone dell'autorizzazione per accedere al database.  
  
-   Il **guest** account utente è abilitato nel database.  
  
 Se **sp_helplogins** non è possibile accedere a un database, **sp_helplogins** restituirà quante più informazioni possibili e visualizzerà il messaggio di errore 15622.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente vengono restituite informazioni sull'account di accesso `John`.  
  
```  
EXEC sp_helplogins 'John';  
GO  
  
LoginName SID                        DefDBName DefLangName AUser ARemote   
--------- -------------------------- --------- ----------- ----- -------   
John      0x23B348613497D11190C100C  master    us_english  yes   no  
  
(1 row(s) affected)  
  
LoginName   DBName   UserName   UserOrAlias   
---------   ------   --------   -----------   
John        pubs     John       User          
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sicurezza &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_helpdb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdb-transact-sql.md)   
 [sp_helpuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
