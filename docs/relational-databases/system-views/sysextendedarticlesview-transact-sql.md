---
title: sysextendedarticlesview (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysextendedarticlesview_TSQL
- sysextendedarticlesview
dev_langs:
- TSQL
helpviewer_keywords:
- sysextendedarticlesview view
ms.assetid: 8bdd22f7-c268-49b6-820c-3fe603feb128
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 40a494f4cf157b85f13327f8367b90e8db2fcce7
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52757034"
---
# <a name="sysextendedarticlesview-transact-sql"></a>sysextendedarticlesview (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **sysextendedarticlesview** consente di visualizzare informazioni sugli articoli pubblicati. Questa vista è archiviata nel database di distribuzione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|Colonna Identity che offre un numero di ID univoco per l'articolo.|  
|**creation_script**|**nvarchar(255)**|Script di creazione dello schema per l'articolo.|  
|**del_cmd**|**nvarchar(255)**|Comando da eseguire a seguito di un'istruzione DELETE; in caso contrario il comando viene ricostruito dal log.|  
|**description**|**nvarchar(255)**|Voce descrittiva per l'articolo.|  
|**dest_table**|**nvarchar(128)**|Nome della tabella di destinazione.|  
|**filter**|**int**|Identificatore di oggetto della stored procedure utilizzata per il partizionamento orizzontale.|  
|**filter_clause**|**ntext**|Clausola WHERE dell'articolo, utilizzata per il filtro orizzontale.|  
|**ins_cmd**|**nvarchar(255)**|Comando da eseguire a seguito di un'istruzione INSERT.|  
|**name**|**nvarchar(128)**|Nome associato all'articolo, univoco all'interno della pubblicazione.|  
|**objid**|**int**|ID dell'oggetto di tabella pubblicato.|  
|**pubid**|**int**|ID della pubblicazione a cui appartiene l'articolo.|  
|**pre_creation_cmd**|**tinyint**|Comando preliminare per l'istruzione DROP TABLE, DELETE TABLE o TRUNCATE:<br /><br /> **0** = none.<br /><br /> **1** = DROP.<br /><br /> **2** = DELETE.<br /><br /> **3** = TRONCAMENTO.|  
|**status**|**int**|Maschera di bit delle opzioni e dello stato dell'articolo, che può corrispondere al risultato dell'applicazione dell'operatore OR logico bit per bit a uno o più dei valori seguenti:<br /><br /> **1** = articolo è attivo.<br /><br /> **8** = Include il nome della colonna nelle istruzioni INSERT.<br /><br /> **16** = utilizza istruzioni con parametrizzata.<br /><br /> **24** = entrambi includono il nome della colonna nelle istruzioni INSERT e utilizza istruzioni con parametri.<br /><br /> Ad esempio, un articolo attivo che utilizza istruzioni con parametri includerà il valore 17 in questa colonna. Il valore 0 indica che l'articolo è inattivo e che non sono state definite proprietà aggiuntive.|  
|**sync_objid**|**int**|ID della tabella o della vista che rappresenta la definizione dell'articolo.|  
|**type**|**tinyint**|Tipo di articolo:<br /><br /> **1** = articolo basato su log.<br /><br /> **3** = articolo basato su log con filtro manuale.<br /><br /> **5** = articolo basato su log con vista manuale.<br /><br /> **7** = articolo basato su log con filtro manuale e vista manuale.|  
|**upd_cmd**|**nvarchar(255)**|Comando da eseguire a seguito di un'istruzione UPDATE; in caso contrario il comando viene ricostruito dal log.|  
|**schema_option**|**binary**|Indica le proprietà dell'oggetto pubblicato da inserire nello script dello snapshot. Per un elenco delle opzioni dello schema supportate, vedere [sp_addarticle](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).|  
|**dest_owner**|**nvarchar(128)**|Proprietario della tabella nel database di destinazione.|  
|**ins_scripting_proc**|**int**|Identificatore di oggetto della stored procedure o dello script personalizzati eseguiti quando un'istruzione INSERT viene replicata.|  
|**del_scripting_proc**|**int**|Identificatore di oggetto della stored procedure o dello script personalizzati eseguiti quando un'istruzione DELETE viene replicata.|  
|**upd_scripting_proc**|**int**|Identificatore di oggetto della stored procedure o dello script personalizzati eseguiti quando un'istruzione UPDATE viene replicata.|  
|**custom_script**|**int**|Identificatore di oggetto della stored procedure o dello script personalizzati eseguiti al completamento di un trigger DDL.|  
|**fire_triggers_on_snapshot**|**int**|Indica se i trigger replicati vengono eseguiti o meno quando lo snapshot viene applicato. I possibili valori sono i seguenti.<br /><br /> **0** = i trigger non vengono eseguiti.<br /><br /> **1** = i trigger vengono eseguiti.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica di &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sysarticles &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysarticles-transact-sql.md)  
  
  
