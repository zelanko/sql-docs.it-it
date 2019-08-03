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
ms.openlocfilehash: 7cc40187ccafebee672214a0926a3ca0d0bc4176
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768986"
---
# <a name="sparticleview-transact-sql"></a>sp_articleview (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

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
`[ @publication = ] 'publication'`Nome della pubblicazione contenente l'articolo. *Publication* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @article = ] 'article'`Nome dell'articolo. *article* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @view_name = ] 'view_name'`Nome della vista che definisce l'articolo pubblicato. *view_name* è di **tipo nvarchar (386)** e il valore predefinito è null.  
  
`[ @filter_clause = ] 'filter_clause'`Clausola di restrizione (WHERE) che definisce un filtro orizzontale. Quando si specifica la clausola di restrizione, omettere la parola chiave WHERE. *filter_clause* è di tipo **ntext**e il valore predefinito è null.  
  
`[ @change_active = ] change_active`Consente di modificare le colonne delle pubblicazioni con sottoscrizioni. *change_active* è di **tipo int**e il valore predefinito è **0**. Se è **0**, le colonne non vengono modificate. Se è **1**, le visualizzazioni possono essere create o ricreate in articoli attivi con sottoscrizioni.  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`Conferma che l'azione eseguita da questo stored procedure potrebbe invalidare uno snapshot esistente. *force_invalidate_snapshot* è di **bit**e il valore predefinito è **0**.  
  
 **0** specifica che le modifiche apportate all'articolo non invalidano lo snapshot. Se la stored procedure rileva che la modifica richiede un nuovo snapshot, viene generato un errore e non viene apportata alcuna modifica.  
  
 **1** specifica che le modifiche apportate all'articolo possono invalidare lo snapshot e, se sono presenti sottoscrizioni che richiedono un nuovo snapshot, consente di contrassegnare lo snapshot esistente come obsoleto e di generare un nuovo snapshot.  
  
`[ @force_reinit_subscription = ] _force_reinit_subscription_`Conferma che l'azione eseguita da questo stored procedure potrebbe richiedere la reinizializzazione delle sottoscrizioni esistenti. *force_reinit_subscription* è un **bit** il cui valore predefinito è **0**.  
  
 **0** specifica che le modifiche apportate all'articolo non provocano la reinizializzazione della sottoscrizione. Se la stored procedure rileva che la modifica richiede la reinizializzazione delle sottoscrizioni, viene generato un errore e non viene apportata alcuna modifica.  
  
 **1** specifica che le modifiche apportate all'articolo provocano la reinizializzazione della sottoscrizione esistente e consente la reinizializzazione della sottoscrizione.  
  
`[ @publisher = ] 'publisher'`Specifica un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di [!INCLUDE[msCoName](../../includes/msconame-md.md)] pubblicazione non. *Publisher* è di **tipo sysname**e il valore predefinito è null.  
  
> [!NOTE]  
>  il *Server* di pubblicazione non deve essere utilizzato per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la pubblicazione da un server di pubblicazione.  
  
`[ @refreshsynctranprocs = ] refreshsynctranprocs`Indica se le stored procedure utilizzate per sincronizzare la replica vengono ricreate automaticamente. *refreshsynctranprocs* è di **bit**e il valore predefinito è 1.  
  
 **1** indica che le stored procedure vengono ricreate.  
  
 **0** indica che le stored procedure non vengono ricreate.  
  
`[ @internal = ] internal` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Note  
 **sp_articleview** crea la vista che definisce l'articolo pubblicato e inserisce l'ID di questa visualizzazione nella colonna **sync_objid** della tabella [Transact- &#40;&#41; SQL sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md) e inserisce il testo della clausola di restrizione in colonna **filter_clause** . Se tutte le colonne vengono replicate e non è presente alcun **filter_clause**, il **sync_objid** nella tabella [Transact-&#41; &#40;SQL sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md) viene impostato sull'ID della tabella di base e l'uso di **sp_articleview** non è obbligatorio.  
  
 Per pubblicare una tabella filtrata verticalmente, ovvero per filtrare le colonne, eseguire prima **sp_addarticle** senza parametri *sync_object* , quindi eseguire [sp_articlecolumn &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) una volta per ogni colonna da replicare (definendo filtro verticale), quindi eseguire **sp_articleview** per creare la vista che definisce l'articolo pubblicato.  
  
 Per pubblicare una tabella filtrata orizzontalmente, ovvero per filtrare le righe, eseguire [sp_addarticle &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) senza il parametro *Filter* . Eseguire [sp_articlefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md), fornendo tutti i parametri, incluso *filter_clause*. Quindi eseguire **sp_articleview**, specificando tutti i parametri che includono lo stesso *filter_clause*.  
  
 Per pubblicare una tabella filtrata verticalmente e orizzontalmente, [eseguire &#40;sp_addarticle Transact-&#41; SQL](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) senza *sync_object* o parametri di *filtro* . Eseguire [sp_articlecolumn &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) una volta per ogni colonna da replicare, quindi eseguire [sp_articlefilter &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) e **sp_articleview**.  
  
 Se l'articolo dispone già di una vista che definisce l'articolo pubblicato, **sp_articleview** Elimina la vista esistente e ne crea una nuova automaticamente. Se la vista è stata creata manualmente (il**tipo** in [sysarticles &#40;Transact&#41; -SQL](../../relational-databases/system-tables/sysarticles-transact-sql.md) è **5**), la vista esistente non viene eliminata.  
  
 Se si crea un filtro personalizzato stored procedure e una vista che definisce l'articolo pubblicato manualmente, non eseguire **sp_articleview**. Specificare invece questi parametri come *filtro* e parametri *sync_object* per [sp_addarticle &#40;Transact&#41;-SQL](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md), insieme al valore di *tipo* appropriato.  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articleview-transact-_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del ruolo predefinito del server **sysadmin** o del ruolo predefinito del database **db_owner** possono eseguire **sp_articleview**.  
  
## <a name="see-also"></a>Vedere anche  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [Definire e modificare un filtro di riga statico](../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)   
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articlefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
