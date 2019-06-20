---
title: sysarticles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysarticles
- sysarticles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticles system table
ms.assetid: 9d9d5d51-6d8f-4e42-84a9-82e58eb0301e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: df9253d534b3b3ece141d7b4aea693b4c9897ac1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62714159"
---
# <a name="sysarticles-transact-sql"></a>sysarticles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una riga per ogni articolo definito nel database locale. Questa tabella è archiviata nel database pubblicato.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|Colonna Identity che offre un numero di ID univoco per l'articolo.|  
|**creation_script**|**nvarchar(255)**|Script dello schema per l'articolo.|  
|**del_cmd**|**nvarchar(255)**|Tipo di comando di replica utilizzato per la replica delle eliminazioni con articoli di tabella. Per altre informazioni, vedere [Specificare la modalità di propagazione delle modifiche per gli articoli transazionali](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).|  
|**description**|**nvarchar(255)**|Voce descrittiva per l'articolo.|  
|**dest_table**|**sysname**|Nome della tabella di destinazione.|  
|**filter**|**int**|ID della stored procedure, utilizzato per il partizionamento orizzontale.|  
|**filter_clause**|**ntext**|Clausola WHERE dell'articolo, utilizzata per il filtro orizzontale.|  
|**ins_cmd**|**nvarchar(255)**|Tipo di comando di replica utilizzato per la replica degli inserimenti con articoli di tabella. Per altre informazioni, vedere [Specificare la modalità di propagazione delle modifiche per gli articoli transazionali](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).|  
|**name**|**sysname**|Nome associato all'articolo, univoco all'interno della pubblicazione.|  
|**objid**|**int**|ID dell'oggetto di tabella pubblicato.|  
|**pubid**|**int**|ID della pubblicazione a cui appartiene l'articolo.|  
|**pre_creation_cmd**|**tinyint**|Comando preliminare per l'istruzione DROP TABLE, DELETE TABLE o TRUNCATE:<br /><br /> **0** = none.<br /><br /> **1** = DROP.<br /><br /> **2** = DELETE.<br /><br /> **3** = TRONCAMENTO.|  
|**status**|**tinyint**|Maschera di bit delle opzioni e dello stato dell'articolo, che può corrispondere al risultato dell'applicazione dell'operatore OR logico bit per bit a uno o più dei valori seguenti:<br /><br /> **1** = articolo è attivo.<br /><br /> **8** = Include il nome della colonna nelle istruzioni INSERT.<br /><br /> **16** = utilizza istruzioni con parametrizzata.<br /><br /> **24** = entrambi includono il nome della colonna nelle istruzioni INSERT e utilizza istruzioni con parametri.<br /><br /> **64** = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> Ad esempio, un articolo attivo che utilizza istruzioni con parametri potrebbe disporre di un valore **17** in questa colonna. Un valore pari **0** significa che l'articolo è inattivo e proprietà aggiuntive non definite.|  
|**sync_objid**|**int**|ID della tabella o della vista che rappresenta la definizione dell'articolo.|  
|**type**|**tinyint**|Tipo di articolo:<br /><br /> **1** = articolo basato su log.<br /><br /> **3** = articolo basato su log con filtro manuale.<br /><br /> **5** = articolo basato su log con vista manuale.<br /><br /> **7** = articolo basato su log con filtro manuale e vista manuale.<br /><br /> **8** = esecuzione di Stored procedure.<br /><br /> **24** = esecuzione di stored procedure serializzabile.<br /><br /> **32** = Stored procedure (solo schema).<br /><br /> **64** = vista (solo schema).<br /><br /> **128** = function (solo schema).|  
|**upd_cmd**|**nvarchar(255)**|Tipo di comando di replica utilizzato per la replica degli aggiornamenti con articoli di tabella. Per altre informazioni, vedere [Specificare la modalità di propagazione delle modifiche per gli articoli transazionali](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md).|  
|**schema_option**|**binary(8)**|Maschera di bit delle opzioni di generazione dello schema per l'articolo, che controllano le parti dello schema dell'articolo inserite nello script per il recapito al Sottoscrittore. Per altre informazioni sulle opzioni di schema, vedere [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).|  
|**dest_owner**|**sysname**|Proprietario della tabella nel database di destinazione.|  
|**ins_scripting_proc**|**int**|Stored procedure o script personalizzato registrato che viene eseguito durante la replica di un'istruzione INSERT.|  
|**del_scripting_proc**|**int**|Stored procedure o script o personalizzato registrato che viene eseguito durante la replica di un'istruzione DELETE.|  
|**upd_scripting_proc**|**int**|Stored procedure o script personalizzato registrato che viene eseguito durante la replica di un'istruzione UPDATE.|  
|**custom_script**|**nvarchar(2048)**|Stored procedure o script personalizzato registrato che viene eseguito alla fine del trigger DDL.|  
|**fire_triggers_on_snapshot**|**bit**|Indica se i trigger replicati vengono eseguiti o meno quando viene applicato lo snapshot. I possibili valori sono i seguenti:<br /><br /> **0** = i trigger non vengono eseguiti.<br /><br /> **1** = i trigger vengono eseguiti.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica di &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)  
  
  
