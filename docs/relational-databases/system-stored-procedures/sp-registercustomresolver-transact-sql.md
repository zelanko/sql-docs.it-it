---
title: sp_registercustomresolver (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_registercustomresolver
- sp_registercustomresolver_TSQL
helpviewer_keywords:
- sp_registercustomresolver
ms.assetid: 6d2b0472-0e1f-4005-833c-735d1940fe93
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0187853dcf0fc16fe88feb7e2731414a69fdd183
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58536983"
---
# <a name="spregistercustomresolver-transact-sql"></a>sp_registercustomresolver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Registra un gestore della logica di business o un sistema di risoluzione personalizzato basato su COM che può essere richiamato durante il processo di sincronizzazione della replica di tipo merge. Questa stored procedure viene eseguita nel database di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_registercustomresolver [ @article_resolver = ] 'article_resolver'   
    [ , [ @resolver_clsid = ] 'resolver_clsid' ]  
    [ , [ @is_dotnet_assembly = ] 'is_dotnet_assembly' ]  
    [ , [ @dotnet_assembly_name = ] 'dotnet_assembly_name' ]  
    [ , [ @dotnet_class_name = ] 'dotnet_class_name' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @article_resolver = ] 'article_resolver'` Specifica il nome descrittivo per la logica di business personalizzata. *article_resolver* viene **nvarchar(255**, non prevede alcun valore predefinito.  
  
`[ @resolver_clsid = ] 'resolver_clsid'` Specifica il valore CLSID dell'oggetto COM in fase di registrazione. Logica di business personalizzata *resolver_clsid* viene **nvarchar (50)**, con un valore predefinito è NULL. È necessario impostare questo parametro su un valore CLSID valido oppure su NULL in caso di registrazione di un assembly di un gestore della logica di business.  
  
`[ @is_dotnet_assembly = ] 'is_dotnet_assembly'` Specifica il tipo di logica di business personalizzata in fase di registrazione. *is_dotnet_assembly* viene **nvarchar (50)**, con un valore predefinito è FALSE. **true** indica che la logica di business personalizzata è un gestore della logica di business stesso Assembly. **false** indica che è un componente COM.  
  
`[ @dotnet_assembly_name = ] 'dotnet_assembly_name'` È il nome dell'assembly che implementa il gestore della logica di business. *dotnet_assembly_name* viene **nvarchar(255**, con un valore predefinito NULL. È necessario specificare il percorso completo dell'assembly se non viene distribuito nella stessa directory dell'eseguibile dell'agente di merge, nella stessa directory dell'applicazione che avvia l'agente di merge in modalità sincrona oppure nella Global Assembly Cache (GAC).  
  
`[ @dotnet_class_name = ] 'dotnet_class_name'` È il nome della classe che esegue l'override <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> per implementare il gestore della logica di business. Il nome deve essere specificato nel formato **ClassName**. *dotnet_class_name* viene **nvarchar(255**, con un valore predefinito NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_registercustomresolver** viene utilizzata nella replica di tipo merge.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_registercustomresolver**.  
  
## <a name="see-also"></a>Vedere anche  
 [Implementare un gestore della logica di business per un articolo di merge](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)   
 [Implementare un sistema di risoluzione dei conflitti personalizzato per un articolo di tipo merge](../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)   
 [sp_lookupcustomresolver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lookupcustomresolver-transact-sql.md)   
 [sp_unregistercustomresolver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
