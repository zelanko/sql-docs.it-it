---
title: sp_help_category (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_category
- sp_help_category_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_category
ms.assetid: 8cad1dcc-b43e-43bd-bea0-cb0055c84169
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1b44f5962e8241afa95b9e68cf75d493dff01ad5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "72304802"
---
# <a name="sp_help_category-transact-sql"></a>sp_help_category (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni sulle classi di processi, avvisi o operatori specificate.  
   
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_help_category [ [ @class = ] 'class' ]   
     [ , [ @type = ] 'type' ]   
     [ , [ @name = ] 'name' ]   
     [ , [ @suffix = ] suffix ]   
```  
  
## <a name="arguments"></a>Argomenti  
`[ @class = ] 'class'`Classe su cui vengono richieste informazioni. la classe è di *tipo* **varchar (8)** e il valore predefinito è **Job**. la *classe* può essere uno di questi valori.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**PROCESSO**|Restituisce informazioni su una categoria di processi.|  
|**AVVISO**|Restituisce informazioni su una categoria di avvisi.|  
|**OPERATORE**|Restituisce informazioni su una categoria di operatori.|  
  
`[ @type = ] 'type'`Tipo di categoria per cui vengono richieste informazioni. il *tipo* è **varchar (12)** e il valore predefinito è null. i possibili valori sono i seguenti.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**LOCALE**|Categoria di processi locali.|  
|**MULTI -SERVER**|Categoria di processi multiserver.|  
|**NESSUNO**|Categoria per una classe diversa da **Job**.|  
  
`[ @name = ] 'name'`Nome della categoria per la quale vengono richieste informazioni. *Name* è di **tipo sysname**e il valore predefinito è null.  
  
`[ @suffix = ] suffix`Specifica se la colonna **category_type** nel set di risultati è un ID o un nome. il *suffisso* è di **bit**e il valore predefinito è **0**. **1** mostra l' **category_type** come nome e **0** lo Visualizza come ID.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 Quando ** \@il suffisso** è **0**, **sp_help_category** restituisce il set di risultati seguente:  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**category_id**|**int**|ID della categoria|  
|**category_type**|**tinyint**|Tipo di categoria:<br /><br /> **1** = locale<br /><br /> **2** = multiserver<br /><br /> **3** = nessuna|  
|**nome**|**sysname**|Nome categoria|  
  
 Quando ** \@il suffisso** è **1**, **sp_help_category** restituisce il set di risultati seguente:  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**category_id**|**int**|ID della categoria|  
|**category_type**|**sysname**|Tipo di categoria: Uno dei sistemi **locali**, **multiserver**o **None**|  
|**nome**|**sysname**|Nome categoria|  
  
## <a name="remarks"></a>Osservazioni  
 **sp_help_category** deve essere eseguito dal database **msdb** .  
  
 Se non viene specificato alcun parametro, il set di risultati include informazioni su tutte le categorie dei processi.  
  
## <a name="permissions"></a>Autorizzazioni  
 Per impostazione predefinita, i membri del ruolo predefinito del server **sysadmin** possono eseguire questo stored procedure. Gli altri utenti devono essere membri di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent seguenti nel database **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Per informazioni dettagliate sulle autorizzazioni di questi ruoli, vedere [Ruoli di database predefiniti di SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-returning-local-job-information"></a>R. Restituzione di informazioni sui processi locali  
 Nell'esempio seguente vengono restituite informazioni sui processi gestiti a livello locale.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_category  
    @type = N'LOCAL' ;  
GO  
```  
  
### <a name="b-returning-alert-information"></a>B. Restituzione di informazioni sugli avvisi  
 Nell'esempio seguente vengono restituite informazioni sulla categoria di avvisi Replication.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_category  
    @class = N'ALERT',  
    @name = N'Replication' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_add_category &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-category-transact-sql.md)   
 [sp_delete_category &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-delete-category-transact-sql.md)   
 [sp_update_category &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-update-category-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
