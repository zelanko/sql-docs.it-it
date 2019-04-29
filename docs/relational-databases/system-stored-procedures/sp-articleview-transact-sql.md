---
title: sp_articleview (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_articleview
- sp_articleview_TSQL
helpviewer_keywords:
- sp_articleview
ms.assetid: a3d63fd6-f360-4a2f-8a82-a0dc15f650b3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 10c46ac2ff35d73453976a91276246d3e810e425
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62997981"
---
# <a name="sparticleview-transact-sql"></a>sp_articleview (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea la vista che definisce l'articolo pubblicato quando una tabella viene filtrata in senso verticale o orizzontale. Questa vista viene utilizzata come origine filtrata dello schema e dei dati per le tabelle di destinazione. Solo gli articoli non sottoscritti possono essere modificati tramite questa stored procedure. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_articleview [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @view_name = ] 'view_name']  
    [ , [ @filter_clause = ] 'filter_clause']  
    [ , [ @change_active = ] change_active ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @refreshsynctranprocs = ] refreshsynctranprocs ]  
    [ , [ @internal = ] internal ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'` È il nome della pubblicazione che contiene l'articolo. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @article = ] 'article'` È il nome dell'articolo. *articolo* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @view_name = ] 'view_name'` È il nome della vista che definisce l'articolo pubblicato. *view_name* viene **nvarchar(386)**, con un valore predefinito è NULL.  
  
`[ @filter_clause = ] 'filter_clause'` È una restrizione clausola (WHERE) che definisce un filtro orizzontale. Quando si specifica la clausola di restrizione, omettere la parola chiave WHERE. *filter_clause* viene **ntext**, con un valore predefinito è NULL.  
  
`[ @change_active = ] change_active` Consente di modificare le colonne delle pubblicazioni che dispongono di sottoscrizioni. *change_active* è un **int**, il valore predefinito è **0**. Se **0**, le colonne non vengono modificate. Se **1**, le viste possono essere create o ricreate in articoli attivi a cui sono associate sottoscrizioni.  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` Segnala che l'azione eseguita da questa stored procedure potrebbe invalidare uno snapshot esistente. *force_invalidate_snapshot* è un **bit**, il valore predefinito è **0**.  
  
 **0** specifica che le modifiche apportate all'articolo non invalidano lo snapshot non è valido. Se la stored procedure rileva che la modifica richiede un nuovo snapshot, viene generato un errore e non viene apportata alcuna modifica.  
  
 **1** specifica che le modifiche apportate all'articolo possono invalidare lo snapshot non è valido e se sono presenti sottoscrizioni esistenti richiedono un nuovo snapshot, consente lo snapshot esistente deve essere contrassegnato come obsoleto e di generarne uno nuovo.  
  
`[ @force_reinit_subscription = ] _force_reinit_subscription_` Segnala che l'azione eseguita da questa stored procedure potrebbe richiedere la reinizializzazione delle sottoscrizioni esistenti. *force_reinit_subscription* è un **bit** con valore predefinito è **0**.  
  
 **0** specifica che le modifiche apportate all'articolo non causano la reinizializzazione della sottoscrizione. Se la stored procedure rileva che la modifica richiede la reinizializzazione delle sottoscrizioni, viene generato un errore e non viene apportata alcuna modifica.  
  
 **1** specifica che le modifiche apportate all'articolo comportano la sottoscrizione esistente per la reinizializzazione e concede l'autorizzazione per la reinizializzazione della sottoscrizione.  
  
`[ @publisher = ] 'publisher'` Specifica un non - [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione. *server di pubblicazione* viene **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  *server di pubblicazione* non deve essere usata durante la pubblicazione da un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione.  
  
`[ @refreshsynctranprocs = ] refreshsynctranprocs` Indica se le stored procedure utilizzate per sincronizzare la replica vengono ricreate automaticamente. *refreshsynctranprocs* viene **bit**, con un valore predefinito è 1.  
  
 **1** significa che le stored procedure vengono ricreate.  
  
 **0** significa che le stored procedure non vengono ricreate.  
  
`[ @internal = ] internal` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_articleview** crea la vista che definisce l'articolo pubblicato e inserisce l'ID della vista nel **sync_objid** colonna il [sysarticles &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md) tabella e inserisce il testo della clausola di restrizione nella **filter_clause** colonna. Se tutte le colonne vengono replicate ed è presente alcun **filter_clause**, il **sync_objid** nel [sysarticles &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md) tabella è impostata sull'ID del tabella di base e l'utilizzo di **sp_articleview** non è obbligatorio.  
  
 Per pubblicare una tabella filtrata in verticale (vale a dire, per filtrare le colonne) della prima esecuzione **sp_addarticle** senza alcun *sync_object* parametro, eseguire [sp_articlecolumn &#40;&#41; ](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) una volta per ogni colonna da replicare (che definisce il filtro verticale) e quindi eseguire **sp_articleview** per creare la vista che definisce l'articolo pubblicato.  
  
 Per pubblicare una tabella filtrata in orizzontale (vale a dire, per filtrare le righe), eseguire [sp_addarticle &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) con nessuna *filtro* parametro. Eseguire [sp_articlefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md), specificando tutti i parametri inclusi *filter_clause*. Quindi eseguire **sp_articleview**, specificando tutti i parametri includono lo stesso *filter_clause*.  
  
 Per pubblicare una tabella filtrata in verticale e orizzontale, eseguire [sp_addarticle &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) con nessuna *sync_object* oppure *filtro* parametri. Eseguire [sp_articlecolumn &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) una volta per ogni colonna da replicare e quindi eseguire [sp_articlefilter &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) e **sp _ articleview**.  
  
 Se l'articolo contiene già una vista che definisce l'articolo pubblicato **sp_articleview** Elimina la vista esistente e crea automaticamente uno nuovo. Se la vista è stata creata manualmente (**tipo** nelle [sysarticles &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md) viene **5**), la vista esistente non è stata eliminata.  
  
 Se si crea una procedura di filtro personalizzato archiviato e una vista che definisce l'articolo pubblicato manualmente, non vengono eseguiti **sp_articleview**. Invece di fornire queste informazioni come il *filtro* e *sync_object* parametri per [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md), e i appropriato*tipo* valore.  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articleview-transact-_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_articleview**.  
  
## <a name="see-also"></a>Vedere anche  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [Definire e modificare un filtro di riga statico](../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)   
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articlefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
