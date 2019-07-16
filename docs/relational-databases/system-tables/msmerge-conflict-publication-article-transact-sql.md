---
title: Msmerge_conflict _&lt;publication&gt;_&lt;articolo&gt; (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_conflict_publication_article_TSQL
- MSmerge_conflict_publication_article
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_conflict_publication_article system table
ms.assetid: dc4490b4-02d8-4dfc-98f5-0cf8de8e11be
author: stevestein
ms.author: sstein
ms.openlocfilehash: dfae18a55ddb8b1c95aad25e27f006b28fde79af
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67895106"
---
# <a name="msmergeconflictltpublicationgtltarticlegt-transact-sql"></a>Msmerge_conflict _&lt;publication&gt;_&lt;articolo&gt; (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **msmerge_conflict _*publication*_ * articolo*** tabella contiene informazioni sulle righe che è in conflitto oppure sulle modifiche delle righe che sono state annullate per garantire la convergenza dei dati. Per ogni tabella replicata di una pubblicazione è disponibile una tabella dei conflitti, il cui nome è seguito dai nomi della pubblicazione e dell'articolo. Queste tabelle dei conflitti specifiche dell'articolo sono archiviate nel database utilizzato per la registrazione dei conflitti, che in genere corrisponde al database di pubblicazione, ma può essere il database di sottoscrizione se la registrazione dei conflitti è decentralizzata.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|***article_column_name***|**variable**|Rappresenta una colonna di una tabella replicata. Questa tabella di sistema contiene una colonna per ogni colonna dell'articolo di tabella.|  
|**rowguid**|**uniqueidentifier**|Identificatore della riga in conflitto.|  
|**ModifiedDate**|**datetime**|Data e ora in cui si è verificato il conflitto.|  
|**origin_datasource_id**|**uniqueidentifier**|Sottoscrizione per cui la modifica della riga è stata annullata oppure che non ha prevalso nel conflitto.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
