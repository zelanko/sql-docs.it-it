---
title: MSmerge_conflict_publication_article (T-SQL)
description: Viene descritta la MSmerge_conflict_publication_article stored procedure che contiene informazioni sulle righe in conflitto oppure sulle modifiche di riga che sono state annullate per ottenere la convergenza dei dati.
ms.custom: seo-lt-2019
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 17f6d7920589e4797369f96d69727fa21917cc00
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545690"
---
# <a name="msmerge_conflict_publication_article-transact-sql"></a>MSmerge_conflict_publication_article (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La tabella **MSmerge_conflict_publication_article** contiene informazioni sulle righe in conflitto oppure sulle modifiche di riga che sono state annullate per ottenere la convergenza dei dati. Per ogni tabella replicata di una pubblicazione è disponibile una tabella dei conflitti, il cui nome è seguito dai nomi della pubblicazione e dell'articolo. Queste tabelle dei conflitti specifiche dell'articolo sono archiviate nel database utilizzato per la registrazione dei conflitti, che in genere corrisponde al database di pubblicazione, ma può essere il database di sottoscrizione se la registrazione dei conflitti è decentralizzata.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**_\_nome colonna \_ articolo_**|**variable**|Rappresenta una colonna di una tabella replicata. Questa tabella di sistema contiene una colonna per ogni colonna dell'articolo di tabella.|  
|**rowguid**|**uniqueidentifier**|Identificatore della riga in conflitto.|  
|**ModifiedDate**|**datetime**|Data e ora in cui si è verificato il conflitto.|  
|**\_ID origine dati origine \_**|**uniqueidentifier**|Sottoscrizione per cui la modifica della riga è stata annullata oppure che non ha prevalso nel conflitto.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
