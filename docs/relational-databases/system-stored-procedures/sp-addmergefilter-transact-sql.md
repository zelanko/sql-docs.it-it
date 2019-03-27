---
title: sp_addmergefilter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergefilter
- sp_addmergefilter_TSQL
helpviewer_keywords:
- sp_addmergefilter
ms.assetid: 4c118cb1-2008-44e2-a797-34b7dc34d6b1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6f2843456f4f95d1019b51f82082d59977ce14d5
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58493696"
---
# <a name="spaddmergefilter-transact-sql"></a>sp_addmergefilter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiunge un nuovo filtro di merge per la creazione di una partizione in base a un join con un'altra tabella. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_addmergefilter [ @publication = ] 'publication'   
        , [ @article = ] 'article'   
        , [ @filtername = ] 'filtername'   
        , [ @join_articlename = ] 'join_articlename'   
        , [ @join_filterclause = ] join_filterclause  
    [ , [ @join_unique_key = ] join_unique_key ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @filter_type = ] filter_type ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'` È il nome della pubblicazione in cui viene aggiunto il filtro di merge. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @article = ] 'article'` È il nome dell'articolo nel quale viene aggiunto il filtro di merge. *articolo* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @filtername = ] 'filtername'` È il nome del filtro. *FilterName* è un parametro obbligatorio. *FilterName*viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @join_articlename = ] 'join_articlename'` Articolo padre al quale l'articolo figlio specificato da *articolo*, deve essere unito tramite la clausola join specificata da *join_filterclause*per determinare le righe dell'articolo figlio che soddisfano il criterio di filtro di filtro di merge. *join_articlename* viene **sysname**, non prevede alcun valore predefinito. L'articolo deve essere incluso nella pubblicazione specificata da *publication*.  
  
`[ @join_filterclause = ] join_filterclause` Clausola join che deve essere utilizzata per unire l'articolo figlio specificato da *articolo*e l'articolo padre specificato da *join_article*per determinare le righe che soddisfano il filtro di merge. *join_filterclause* viene **nvarchar(1000)**.  
  
`[ @join_unique_key = ] join_unique_key` Specifica se il join tra l'articolo figlio *articolo*e l'articolo padre *join_article*è uno-a-molti, uno a uno, molti-a-uno oppure molti-a-molti. *join_unique_key* viene **int**, con un valore predefinito è 0. **0** indica un join molti-a-uno o molti-a-molti. **1** indica un join uno a uno o uno-a-molti. Questo valore è **1** quando le colonne di join formano una chiave univoca *join_article*, o se *join_filterclause* tra una chiave esterna in *articolo* e una chiave primaria *join_article*.  
  
> [!CAUTION]  
>  Impostare questo parametro solo **1** se si dispone di un vincolo nella colonna unita tramite join nella tabella sottostante per l'articolo padre che garantisce l'univocità. Se *join_unique_key* è impostata su **1** in modo errato, si verifichi la non convergenza dei dati.  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` Segnala che l'azione eseguita da questa stored procedure potrebbe invalidare uno snapshot esistente. *force_invalidate_snapshot* è un **bit**, con un valore predefinito **0**.  
  
 **0** specifica che le modifiche apportate all'articolo di merge verranno non invalidano lo snapshot non è valido. Se la stored procedure rileva che la modifica richiede un nuovo snapshot, viene generato un errore e non viene apportata alcuna modifica.  
  
 **1** specifica che le modifiche apportate all'articolo di merge potrebbero invalidare lo snapshot non è valida e, se sono disponibili sottoscrizioni che richiedono un nuovo snapshot, consente l'autorizzazione per lo snapshot esistente deve essere contrassegnato come obsoleto e un nuovo snapshot generato.  
  
`[ @force_reinit_subscription = ] force_reinit_subscription` Segnala che l'azione eseguita da questa stored procedure potrebbe richiedere la reinizializzazione delle sottoscrizioni esistenti. *force_reinit_subscription* è un **bit**, con un valore predefinito è 0.  
  
 **0** indica che le modifiche apportate all'articolo di merge non comportano la reinizializzazione della sottoscrizione. Se la stored procedure rileva che la modifica richiede la reinizializzazione delle sottoscrizioni, viene generato un errore e non viene apportata alcuna modifica.  
  
 **1** indica che le modifiche apportate all'articolo di merge comportano la reinizializzazione delle sottoscrizioni esistenti e autorizza la reinizializzazione della sottoscrizione.  
  
`[ @filter_type = ] filter_type` Specifica il tipo di filtro da aggiungere. *filter_type* viene **tinyint**, e può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1**|Solo filtro di join. Necessario per supportare [!INCLUDE[ssEW](../../includes/ssew-md.md)] sottoscrittori.|  
|**2**|Solo relazione tra record logici.|  
|**3**|Filtro di join e relazione tra record logici.|  
  
 Per altre informazioni, vedere [Raggruppare modifiche alle righe correlate con record logici](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_addmergefilter** viene utilizzata nella replica di tipo merge.  
  
 **sp_addmergefilter** utilizzabile solo con articoli di tabella. Gli articoli di vista e di vista indicizzata non sono supportati.  
  
 Questa procedura può inoltre essere utilizzata per aggiungere una relazione logica tra due articoli che possono essere uniti o meno tramite un filtro di join. *filter_type* consente di specificare se il filtro di merge da aggiungere è un filtro di join, una relazione logica oppure entrambi.  
  
 Per utilizzare record logici, è necessario che la pubblicazione e gli articoli soddisfino alcuni requisiti. Per altre informazioni, vedere [Raggruppare modifiche alle righe correlate con record logici](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
 Questa opzione viene generalmente utilizzata per gli articoli che includono un riferimento di chiave esterna a una chiave primaria su una tabella pubblicata e tale tabella include un filtro definito nell'articolo corrispondente. Il subset di righe della chiave primaria viene utilizzato per determinare le righe di chiave esterna da replicare nel Sottoscrittore.  
  
 Non è possibile aggiungere un filtro di join tra due articoli pubblicati se le tabelle di origine per entrambi gli articoli condividono lo stesso nome di oggetto tabella. In questo caso, anche se entrambe le tabelle appartengono a schemi diversi e sono caratterizzate da nomi di articolo univoci, la creazione del filtro di join avrà esito negativo.  
  
 In caso di utilizzo di un filtro di riga con parametri e un filtro di join in un articolo di tabella, la replica determina se una riga appartiene a una partizione del Sottoscrittore Ciò avviene tramite la valutazione della funzione di filtro o il filtro di join (usando il [OR](../../t-sql/language-elements/or-transact-sql.md) operatore), anziché la valutazione dell'intersezione delle due condizioni (usando la [AND](../../t-sql/language-elements/and-transact-sql.md) operator).  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_addmergefilter](../../relational-databases/replication/codesnippet/tsql/sp-addmergefilter-transa_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_addmergefilter**.  
  
## <a name="see-also"></a>Vedere anche  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [Definizione e modifica di un filtro di join tra articoli di merge](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [Join Filters](../../relational-databases/replication/merge/join-filters.md)   
 [sp_changemergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergefilter-transact-sql.md)   
 [sp_dropmergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql.md)   
 [sp_helpmergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergefilter-transact-sql.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
