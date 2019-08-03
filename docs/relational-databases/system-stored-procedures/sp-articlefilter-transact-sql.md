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
ms.openlocfilehash: d90cd0ba957da820ce5a937ae687e39ca0302025
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769063"
---
# <a name="sparticlefilter-transact-sql"></a>sp_articlefilter (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

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
`[ @publication = ] 'publication'`Nome della pubblicazione contenente l'articolo. *Publication* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @article = ] 'article'`Nome dell'articolo. *article* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @filter_name = ] 'filter_name'`Nome del filtro stored procedure da creare dall' *filter_name*. *filter_name* è di **tipo nvarchar (386)** e il valore predefinito è null. È necessario specificare un nome univoco per il filtro per gli articoli.  
  
`[ @filter_clause = ] 'filter_clause'`Clausola di restrizione (WHERE) che definisce un filtro orizzontale. Quando si specifica la clausola di restrizione, omettere la parola chiave WHERE. *filter_clause* è di tipo **ntext**e il valore predefinito è null.  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`Conferma che l'azione eseguita da questo stored procedure potrebbe invalidare uno snapshot esistente. *force_invalidate_snapshot* è di **bit**e il valore predefinito è **0**.  
  
 **0** specifica che le modifiche apportate all'articolo non invalidano lo snapshot. Se la stored procedure rileva che la modifica richiede un nuovo snapshot, viene generato un errore e non viene apportata alcuna modifica.  
  
 **1** specifica che le modifiche apportate all'articolo possono invalidare lo snapshot e, se sono presenti sottoscrizioni che richiedono un nuovo snapshot, consente di contrassegnare lo snapshot esistente come obsoleto e di generare un nuovo snapshot.  
  
`[ @force_reinit_subscription = ] force_reinit_subscription`Conferma che l'azione eseguita da questo stored procedure potrebbe richiedere la reinizializzazione delle sottoscrizioni esistenti. *force_reinit_subscription* è di **bit**e il valore predefinito è **0**.  
  
 **0** specifica che le modifiche apportate all'articolo non determinano la reinizializzazione delle sottoscrizioni. Se la stored procedure rileva che la modifica richiede la reinizializzazione delle sottoscrizioni, viene generato un errore e non viene apportata alcuna modifica.  
  
 **1** specifica che le modifiche apportate all'articolo provocano la reinizializzazione delle sottoscrizioni esistenti e consente la reinizializzazione della sottoscrizione.  
  
`[ @publisher = ] 'publisher'`Specifica un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di [!INCLUDE[msCoName](../../includes/msconame-md.md)] pubblicazione non. *Publisher* è di **tipo sysname**e il valore predefinito è null.  
  
> [!NOTE]  
>  il *server di pubblicazione* non deve essere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzato con un server di pubblicazione.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Note  
 **sp_articlefilter** viene utilizzato nella replica snapshot e nella replica transazionale.  
  
 Per eseguire **sp_articlefilter** per un articolo con sottoscrizioni esistenti, è necessario reinizializzare le sottoscrizioni.  
  
 **sp_articlefilter** crea il filtro, inserisce l'ID del filtro stored procedure nella colonna **filtro** della tabella [Transact-SQL &#40;&#41; sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md) e quindi inserisce il testo della clausola di restrizione nel **filtro. colonna _clause** .  
  
 Per creare un articolo con un filtro orizzontale, eseguire [sp_addarticle &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) senza il parametro *Filter* . Eseguire **sp_articlefilter**, specificando tutti i parametri, incluso *filter_clause*, quindi eseguire [sp_articleview &#40;Transact&#41;-SQL](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md), fornendo tutti i parametri che includono il *filter_clause*identico. Se il filtro esiste già e il **tipo** in **sysarticles** è **1** (articolo basato su log), il filtro precedente viene eliminato e viene creato un nuovo filtro.  
  
 Se non vengono specificati *filter_name* e *filter_clause* , il filtro precedente viene eliminato e l'ID del filtro viene impostato su **0**.  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articlefilter-transac_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del ruolo predefinito del server **sysadmin** o del ruolo predefinito del database **db_owner** possono eseguire **sp_articlefilter**.  
  
## <a name="see-also"></a>Vedere anche  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [Definire e modificare un filtro di riga statico](../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)   
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articleview &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
