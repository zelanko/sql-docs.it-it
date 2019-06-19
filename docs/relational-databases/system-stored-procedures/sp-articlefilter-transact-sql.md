---
title: sp_articlefilter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_articlefilter_TSQL
- sp_articlefilter
helpviewer_keywords:
- sp_articlefilter
ms.assetid: 4c3fee32-a43f-4757-a029-30aef4696afb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 698a5941bc8e9920942e7ec7c962144b4ab24b62
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62998289"
---
# <a name="sparticlefilter-transact-sql"></a>sp_articlefilter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Filtra i dati da pubblicare in base a un articolo di tabella. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_articlefilter [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @filter_name = ] 'filter_name' ]  
    [ , [ @filter_clause = ] 'filter_clause' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'` È il nome della pubblicazione che contiene l'articolo. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @article = ] 'article'` È il nome dell'articolo. *articolo* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @filter_name = ] 'filter_name'` È il nome della stored procedure di filtro da creare dal *filter_name*. *filter_name* viene **nvarchar(386)** , con un valore predefinito è NULL. È necessario specificare un nome univoco per il filtro per gli articoli.  
  
`[ @filter_clause = ] 'filter_clause'` È una restrizione clausola (WHERE) che definisce un filtro orizzontale. Quando si specifica la clausola di restrizione, omettere la parola chiave WHERE. *filter_clause* viene **ntext**, con un valore predefinito è NULL.  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` Segnala che l'azione eseguita da questa stored procedure potrebbe invalidare uno snapshot esistente. *force_invalidate_snapshot* è un **bit**, il valore predefinito è **0**.  
  
 **0** specifica che le modifiche apportate all'articolo non invalidano lo snapshot non è valido. Se la stored procedure rileva che la modifica richiede un nuovo snapshot, viene generato un errore e non viene apportata alcuna modifica.  
  
 **1** specifica che le modifiche apportate all'articolo possono invalidare lo snapshot non è valido e se sono presenti sottoscrizioni esistenti richiedono un nuovo snapshot, consente lo snapshot esistente deve essere contrassegnato come obsoleto e di generarne uno nuovo.  
  
`[ @force_reinit_subscription = ] force_reinit_subscription` Segnala che l'azione eseguita da questa stored procedure potrebbe richiedere la reinizializzazione delle sottoscrizioni esistenti. *force_reinit_subscription* è un **bit**, il valore predefinito è **0**.  
  
 **0** specifica che le modifiche apportate all'articolo non causano la necessità di reinizializzazione delle sottoscrizioni. Se la stored procedure rileva che la modifica richiede la reinizializzazione delle sottoscrizioni, viene generato un errore e non viene apportata alcuna modifica.  
  
 **1** specifica che le modifiche apportate all'articolo comportano la reinizializzazione delle sottoscrizioni esistenti e autorizza la reinizializzazione della sottoscrizione.  
  
`[ @publisher = ] 'publisher'` Specifica un non - [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione. *server di pubblicazione* viene **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  *server di pubblicazione* non devono essere usati con un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_articlefilter** viene utilizzata nella replica snapshot e transazionale.  
  
 L'esecuzione **sp_articlefilter** per un articolo con le sottoscrizioni esistenti richiede che tali sottoscrizioni per la reinizializzazione.  
  
 **sp_articlefilter** crea il filtro, inserisce l'ID della stored procedure di filtro nel **filtro** della colonna della [sysarticles &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md) tabella e quindi Inserisce il testo della clausola di restrizione nella **filter_clause** colonna.  
  
 Per creare un articolo con filtro orizzontale, eseguire [sp_addarticle &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) con nessuna *filtro* parametro. Eseguire **sp_articlefilter**, specificando tutti i parametri inclusi *filter_clause*, quindi eseguire [sp_articleview &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md), specificando tutti i parametri includono lo stesso *filter_clause*. Se il filtro è già presente e se il **tipo** nelle **sysarticles** viene **1** (articolo basato su log), il filtro precedente viene eliminato e viene creato un nuovo filtro.  
  
 Se *filter_name* e *filter_clause* vengono omessi, il filtro precedente viene eliminato e l'ID del filtro è impostato su **0**.  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articlefilter-transac_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_articlefilter**.  
  
## <a name="see-also"></a>Vedere anche  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [Definire e modificare un filtro di riga statico](../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)   
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articleview &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
