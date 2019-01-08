---
title: sp_helparticle (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helparticle_TSQL
- sp_helparticle
helpviewer_keywords:
- sp_helparticle
ms.assetid: 9c4a1a88-56f1-45a0-890c-941b8e0f0799
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0ebb3f1e81fbace678d281116643e1fcd97c3dc1
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53212506"
---
# <a name="sphelparticle-transact-sql"></a>sp_helparticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Visualizza informazioni su un articolo. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione. Per i server di pubblicazione Oracle questa stored procedure viene eseguita in qualsiasi database del server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helparticle [ @publication = ] 'publication'   
    [ , [ @article = ] 'article' ]  
    [ , [ @returnfilter = ] returnfilter ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @found = ] found OUTPUT ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@publication =**] **'***pubblicazione***'**  
 Nome della pubblicazione. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@article=**] **'***articolo***'**  
 Nome di un articolo della pubblicazione. *articolo* viene **sysname**, il valore predefinito è **%**. Se *articolo* viene omesso, vengono restituite informazioni su tutti gli articoli per la pubblicazione specificata.  
  
 [  **@returnfilter=**] *returnfilter*  
 Indica se restituire o meno la clausola di filtro. *returnfilter* viene **bit**, il valore predefinito è **1**, che restituisce la clausola di filtro.  
  
 [ **@publisher**=] **'***publisher***'**  
 Specifica un non - [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione. *server di pubblicazione* viene **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  *server di pubblicazione* non deve essere specificato quando la richiesta di informazioni in un articolo pubblicato da un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione.  
  
 [  **@found=** ] *trovato* OUTPUT  
 Solo per uso interno.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**id articolo**|**int**|ID dell'articolo.|  
|**nome dell'articolo**|**sysname**|Nome dell'articolo.|  
|**oggetto di base**|**nvarchar(257)**|Nome della tabella sottostante rappresentata dall'articolo o dalla stored procedure.|  
|**oggetto di destinazione**|**sysname**|Nome della tabella di destinazione (sottoscrizione).|  
|**oggetto di sincronizzazione**|**nvarchar(257)**|Nome della vista che definisce l'articolo pubblicato.|  
|**type**|**smallint**|Tipo di articolo:<br /><br /> **1** = basato su log.<br /><br /> **3** = basato su log con filtro manuale.<br /><br /> **5** = basato su log con vista manuale.<br /><br /> **7** = basato su log con filtro manuale e vista manuale.<br /><br /> **8** = esecuzione di Stored procedure.<br /><br /> **24** = esecuzione di stored procedure serializzabile.<br /><br /> **32** = Stored procedure (solo schema).<br /><br /> **64** = vista (solo schema).<br /><br /> **96** = funzione di aggregazione (solo schema).<br /><br /> **128** = function (solo schema).<br /><br /> **257** = vista indicizzata basato su log.<br /><br /> **259** = vista indicizzata basato su log con filtro manuale.<br /><br /> **261** = vista indicizzata basato su log con vista manuale.<br /><br /> **263** = vista indicizzata basato su log con filtro manuale e vista manuale.<br /><br /> **320** = vista indicizzata (solo schema).<br /><br />|  
|**status**|**tinyint**|Può essere il [& (AND bit per bit)](../../t-sql/language-elements/bitwise-and-transact-sql.md) risultato di una o più queste proprietà di articolo:<br /><br /> **0x00** = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> **0x01** = articolo è attivo.<br /><br /> **0x08** = Include il nome della colonna nelle istruzioni insert.<br /><br /> **0x16** = utilizza istruzioni con parametrizzata.<br /><br /> **0x32** = utilizza istruzioni con parametrizzata e includere il nome di colonna nelle istruzioni insert.|  
|**filter**|**nvarchar(257)**|Stored procedure utilizzata per filtrare la tabella in senso orizzontale. Questa stored procedure deve essere stata creata con la clausola FOR REPLICATION.|  
|**description**|**nvarchar(255)**|Voce descrittiva per l'articolo.|  
|**insert_command**|**nvarchar(255)**|Tipo di comando di replica utilizzato per la replica degli inserimenti con articoli di tabella. Per altre informazioni, vedere [Specificare la modalità di propagazione delle modifiche per gli articoli transazionali](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).|  
|**update_command**|**nvarchar(255)**|Tipo di comando di replica utilizzato per la replica degli aggiornamenti con articoli di tabella. Per altre informazioni, vedere [Specificare la modalità di propagazione delle modifiche per gli articoli transazionali](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).|  
|**delete_command**|**nvarchar(255)**|Tipo di comando di replica utilizzato per la replica delle eliminazioni con articoli di tabella. Per altre informazioni, vedere [Specificare la modalità di propagazione delle modifiche per gli articoli transazionali](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).|  
|**percorso dello script di creazione**|**nvarchar(255)**|Percorso e nome di uno script di schema dell'articolo utilizzato per la creazione delle tabelle di destinazione.|  
|**partizione verticale**|**bit**|È se il partizionamento verticale è abilitato per l'articolo. dove il valore **1** indica che il partizionamento verticale è abilitato.|  
|**pre_creation_cmd**|**tinyint**|Comando preliminare per l'istruzione DROP TABLE, DELETE TABLE o TRUNCATE TABLE.|  
|**filter_clause**|**ntext**|Clausola WHERE che specifica il filtro orizzontale.|  
|**schema_option**|**binary(8)**|Maschera di bit dell'opzione di creazione dello schema per l'articolo specificato. Per un elenco completo delle **schema_option** valori, vedere [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).|  
|**dest_owner**|**sysname**|Nome del proprietario dell'oggetto di destinazione.|  
|**source_owner**|**sysname**|Proprietario dell'oggetto di origine.|  
|**unqua_source_object**|**sysname**|Nome dell'oggetto di origine, senza il nome del proprietario.|  
|**sync_object_owner**|**sysname**|Proprietario della vista che definisce l'articolo pubblicato. .|  
|**unqualified_sync_object**|**sysname**|Nome della vista che definisce l'articolo pubblicato, senza il nome del proprietario.|  
|**filter_owner**|**sysname**|Proprietario del filtro.|  
|**unqua_filter**|**sysname**|Nome del filtro, senza il nome del proprietario.|  
|**auto_identity_range**|**int**|Flag che indica se la gestione automatica degli intervalli di valori Identity era attivata nella pubblicazione quando la pubblicazione è stata creata. **1** significa che l'intervallo di valori identity automatico è abilitato. **0** significa che è disabilitata.|  
|**publisher_identity_range**|**int**|Intervallo di dimensioni dell'intervallo di valori identity nel server di pubblicazione se l'articolo contiene *identityrangemanagementoption* impostata su **automatico** oppure **auto_identity_range** impostato su  **true**.|  
|**identity_range**|**bigint**|Intervallo di dimensioni dell'intervallo di valori identity nel Sottoscrittore se l'articolo contiene *identityrangemanagementoption* impostata su **automatico** oppure **auto_identity_range** impostato su  **true**.|  
|**soglia**|**bigint**|Valore percentuale che indica quando l'agente di distribuzione assegna un nuovo intervallo di valori Identity.|  
|**identityrangemanagementoption**|**int**|Indica la gestione degli intervalli di valori Identity per l'articolo.|  
|**fire_triggers_on_snapshot**|**bit**|Indica se i trigger utente replicati vengono eseguiti quando viene applicato lo snapshot iniziale.<br /><br /> **1** = i trigger utente vengono eseguiti.<br /><br /> **0** = utente trigger non vengono eseguiti.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_helparticle** viene utilizzata nella replica snapshot e transazionale.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server, il **db_owner** ruolo predefinito del database, o elenco di accesso alla pubblicazione per la pubblicazione corrente può eseguire **sp_helparticle**.  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_helptranarticle](../../relational-databases/replication/codesnippet/tsql/sp-helparticle-transact-_1.sql)]  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare e modificare le proprietà degli articoli](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articlecolumn &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
