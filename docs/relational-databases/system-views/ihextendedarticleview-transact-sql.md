---
title: IHextendedArticleView (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHextendedArticleView_TSQL
- IHextendedArticleView
dev_langs:
- TSQL
helpviewer_keywords:
- IHextendedArticleView view
ms.assetid: 19ef0a12-3214-4bb0-9c25-a665897e65a2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7bc5734c0c8bed79516d94b96e7c6060e3650066
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52771403"
---
# <a name="ihextendedarticleview-transact-sql"></a>IHextendedArticleView (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **IHextendedArticleView** Vista espone informazioni sugli articoli in una pubblicazione non SQL Server. Questa vista è archiviata nel **distribuzione** database.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|Identificatore univoco del server di pubblicazione.|  
|**publication_id**|**int**|Identificatore univoco della pubblicazione.|  
|**article**|**sysname**|Nome dell'articolo.|  
|**destination_object**|**sysname**|Nome dell'oggetto pubblicato nel Sottoscrittore.|  
|**source_owner**|**sysname**|Proprietario dell'oggetto pubblicato nel server di pubblicazione.|  
|**source_object**|**sysname**|Nome dell'oggetto pubblicato nel server di pubblicazione.|  
|**description**|**nvarchar(255)**|Descrizione dell'articolo.|  
|**creation_script**|**nvarchar(255)**|Script di creazione dello schema per l'articolo.|  
|**del_cmd**|**nvarchar(255)**|Comando eseguito per un'operazione DELETE.|  
|**filter**|**int**|Identificatore della stored procedure utilizzata per definire la partizione orizzontale.|  
|**filter_clause**|**ntext**|Clausola WHERE utilizzata per filtrare l'articolo in modo orizzontale.|  
|**ins_cmd**|**nvarchar(255)**|Comando eseguito per un'operazione INSERT.|  
|**pre_creation_cmd**|**tinyint**|Comando preliminare per l'istruzione DROP TABLE, DELETE TABLE o TRUNCATE:<br /><br /> **0** = none.<br /><br /> **1** = DROP.<br /><br /> **2** = DELETE.<br /><br /> **3** = TRONCAMENTO.|  
|**status**|**tinyint**|Maschera di bit delle opzioni e dello stato dell'articolo, che può corrispondere al risultato dell'applicazione dell'operatore OR logico bit per bit a uno o più dei valori seguenti:<br /><br /> **1** = articolo è attivo.<br /><br /> **8** = Include il nome della colonna nelle istruzioni INSERT.<br /><br /> **16** = utilizza istruzioni con parametrizzata.<br /><br /> **24** = entrambi includono il nome della colonna nelle istruzioni INSERT e utilizza istruzioni con parametri.<br /><br /> Ad esempio, un articolo attivo che utilizza istruzioni con parametri potrebbe disporre di un valore **17** in questa colonna. Un valore pari **0** significa che l'articolo è inattivo e proprietà aggiuntive non definite.|  
|**type**|**tinyint**|Tipo di articolo:<br /><br /> **1** = articolo basato su log.<br /><br /> **3** = articolo basato su log con filtro manuale.<br /><br /> **5** = articolo basato su log con vista manuale.<br /><br /> **7** = articolo basato su log con filtro manuale e vista manuale.|  
|**upd_cmd**|**nvarchar(255)**|Comando eseguito per un'operazione UPDATE.|  
|**schema_option**|**binary**|Specifica gli elementi da inserire nello script. Visualizzare [sp_addarticle &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) per un elenco delle opzioni dello schema supportate.|  
|**dest_owner**|**sysname**|Proprietario dell'oggetto pubblicato nel database di destinazione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Replica di database eterogenei](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
