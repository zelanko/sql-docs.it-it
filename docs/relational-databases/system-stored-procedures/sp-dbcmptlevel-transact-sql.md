---
title: sp_dbcmptlevel (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbcmptlevel
- sp_dbcmptlevel_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbcmptlevel
ms.assetid: 508c686d-2bd4-41ba-8602-48ebca266659
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0f6ffcb7a43fbfc2a840cbbbeb95de4bbb875cbe
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68108215"
---
# <a name="sp_dbcmptlevel-transact-sql"></a>sp_dbcmptlevel (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Imposta aspetti specifici del comportamento del database in modo che risultino compatibili con la versione specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]In alternativa, usare [ALTER DATABASE Compatibility Level](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_dbcmptlevel [ [ @dbname = ] name ]   
    [ , [ @new_cmptlevel = ] version ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @dbname = ] name`Nome del database per cui si desidera modificare il livello di compatibilità. I nomi di database devono essere conformi alle regole per gli identificatori. *Name* è di **tipo sysname**e il valore predefinito è null.  
  
`[ @new_cmptlevel = ] version`Versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con cui il database deve essere reso compatibile. *Version* è di **tinyint**e il valore predefinito è null. Il valore deve essere uno dei seguenti:  
  
 **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
  
 **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
 **110** = [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
 **120** = [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
 **130** = [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 0 (operazione completata) o 1 (operazione non riuscita)  
  
## <a name="result-sets"></a>Set di risultati  
 Se non viene specificato alcun parametro o se non si specifica il parametro *Name* , **sp_dbcmptlevel** restituisce un errore.  
  
 Se il [!INCLUDE[ssDE](../../includes/ssde-md.md)] *nome* viene specificato senza *versione*, restituisce un messaggio che Visualizza il livello di compatibilità corrente del database specificato.  
  
## <a name="remarks"></a>Osservazioni  
 Per una descrizione dei livelli di compatibilità, vedere [ALTER DATABASE Compatibility Level &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
## <a name="permissions"></a>Autorizzazioni  
 Questa procedura può essere eseguita solo dal proprietario del database, dai membri del ruolo predefinito del server **sysadmin** e dal ruolo predefinito del database **db_owner** (se si modifica il database corrente).  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di motore di database &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Parole chiave riservate &#40;&#41;Transact-SQL](../../t-sql/language-elements/reserved-keywords-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
