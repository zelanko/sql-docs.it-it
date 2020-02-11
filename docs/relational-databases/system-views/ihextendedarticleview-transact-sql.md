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
ms.openlocfilehash: 0abca8ca826ec986a9cbf71f4fb577291e095e39
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68029539"
---
# <a name="ihextendedarticleview-transact-sql"></a>IHextendedArticleView (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La vista **IHextendedArticleView** espone informazioni sugli articoli di una pubblicazione non SQL Server. Questa vista è archiviata nel database di **distribuzione** .  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|Identificatore univoco del server di pubblicazione.|  
|**publication_id**|**int**|Identificatore univoco della pubblicazione.|  
|**articolo**|**sysname**|Nome dell'articolo.|  
|**destination_object**|**sysname**|Nome dell'oggetto pubblicato nel Sottoscrittore.|  
|**source_owner**|**sysname**|Proprietario dell'oggetto pubblicato nel server di pubblicazione.|  
|**source_object**|**sysname**|Nome dell'oggetto pubblicato nel server di pubblicazione.|  
|**Descrizione**|**nvarchar(255)**|Descrizione dell'articolo.|  
|**creation_script**|**nvarchar(255)**|Script di creazione dello schema per l'articolo.|  
|**del_cmd**|**nvarchar(255)**|Comando eseguito per un'operazione DELETE.|  
|**filtro**|**int**|Identificatore della stored procedure utilizzata per definire la partizione orizzontale.|  
|**filter_clause**|**ntext**|Clausola WHERE utilizzata per filtrare l'articolo in modo orizzontale.|  
|**ins_cmd**|**nvarchar(255)**|Comando eseguito per un'operazione INSERT.|  
|**pre_creation_cmd**|**tinyint**|Comando preliminare per l'istruzione DROP TABLE, DELETE TABLE o TRUNCATE:<br /><br /> **0** = nessuna.<br /><br /> **1** = Elimina.<br /><br /> **2** = Delete.<br /><br /> **3** = troncamento.|  
|**stato**|**tinyint**|Maschera di bit delle opzioni e dello stato dell'articolo, che può corrispondere al risultato dell'applicazione dell'operatore OR logico bit per bit a uno o più dei valori seguenti:<br /><br /> **1** = l'articolo è attivo.<br /><br /> **8** = include il nome della colonna nelle istruzioni INSERT.<br /><br /> **16** = usa istruzioni con parametri.<br /><br /> **24** = include il nome della colonna nelle istruzioni INSERT e usa istruzioni con parametri.<br /><br /> Ad esempio, un articolo attivo che utilizza istruzioni con parametri avrà il valore **17** in questa colonna. Il valore **0** indica che l'articolo è inattivo e non è stata definita alcuna proprietà aggiuntiva.|  
|**tipo**|**tinyint**|Tipo di articolo:<br /><br /> **1** = articolo basato su log.<br /><br /> **3** = articolo basato su log con filtro manuale.<br /><br /> **5** = articolo basato su log con vista manuale.<br /><br /> **7** = articolo basato su log con filtro manuale e vista manuale.|  
|**upd_cmd**|**nvarchar(255)**|Comando eseguito per un'operazione UPDATE.|  
|**schema_option**|**BINARY**|Indica gli elementi da inserire nello script. Per un elenco delle opzioni dello schema supportate, vedere [sp_addarticle &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) .|  
|**dest_owner**|**sysname**|Proprietario dell'oggetto pubblicato nel database di destinazione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Replica di database eterogenei](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelle di replica &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
