---
title: conflict_&lt;schema&gt;_&lt;tabella&gt; (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/15/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- conflict_
- conflict_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- conflict_<schema>_<table>
ms.assetid: 15ddd536-db03-454e-b9b5-36efe1f756d7
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4725da28e9cd83df4979d1cc476cd60a488c0aa4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68084773"
---
# <a name="conflictltschemagtlttablegt-transact-sql"></a>conflict_&lt;schema&gt;_&lt;tabella&gt; (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il conflict_\<schema > _\<tabella > tabella contiene informazioni sulle righe in conflitto nella replica peer-to-peer. Per ogni tabella replicata di una pubblicazione è disponibile una tabella dei conflitti, il cui nome è seguito dai nomi dello schema e dell'articolo. Queste tabelle dei conflitti specifiche dell'articolo sono presenti in ogni database di pubblicazione.  
  
 Per la replica peer-to-peer, per impostazione predefinita quando viene rilevato un conflitto si verifica un errore dell'agente di distribuzione. Nel log degli errori viene registrato un errore di conflitto, ma nella tabella dei conflitti non vengono registrati dati, che non sono quindi disponibili per la visualizzazione. Se l'esecuzione dell'agente di distribuzione può continuare, viene registrato localmente un conflitto in ogni nodo in cui è stato rilevato. Per ulteriori informazioni, vedere la sezione relativa alla gestione dei conflitti in [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|__$originator_id|**int**|ID del nodo in cui ha avuto origine la modifica in conflitto. Per un elenco di ID, eseguire [sp_help_peerconflictdetection](../../relational-databases/system-stored-procedures/sp-help-peerconflictdetection-transact-sql.md).|  
|__$origin_datasource|**int**|Nodo in cui ha avuto origine la modifica in conflitto.|  
|__$tranid|**nvarchar (40)**|Numero di sequenza del file di log (LSN) della modifica in conflitto quando applicata a __$origin_datasource.|  
|__$conflict_type|**int**|Tipo di conflitto. I valori possibili sono i seguenti:<br /><br /> 1: Un aggiornamento non è riuscito perché la riga locale è stata modificata da un altro aggiornamento oppure è stato eliminato e quindi reinserito.<br /><br /> 2: Un aggiornamento non è riuscita perché la riga locale è stata già eliminata.<br /><br /> 3: Un'operazione di eliminazione non è riuscita perché la riga locale è stata modificata da un altro aggiornamento oppure è stata eliminata e quindi reinserita.<br /><br /> 4: Un'operazione di eliminazione non riuscita perché la riga locale è stata già eliminata.<br /><br /> 5: Un'istruzione insert non è riuscita perché la riga locale è stata già inserita oppure è stata inserita e quindi aggiornata.|  
|__$is_winner|**bit**|Indica se la riga presente in questa tabella è la riga confermata, ovvero se è stata applicata al nodo locale.|  
|__$pre_version|**varbinary (32)**|Versione del database in cui ha avuto origine la modifica in conflitto.|  
|__$reason_code|**int**|Codice di risoluzione del conflitto. Il valore può essere uno dei seguenti:<br /><br /> 0<br /><br /> 1<br /><br /> 2<br /><br /> <br /><br /> Per altre informazioni, vedere **_ $reason_text**.|  
|__$reason_text|**nvarchar (720)**|Risoluzione del conflitto. Il valore può essere uno dei seguenti:<br /><br /> Risolto (1)<br /><br /> Non risolto (2)<br /><br /> Sconosciuto (0)|  
|__$update_bitmap|**varbinary(** *n* **)** . Dimensioni variano a seconda del contenuto.|Bitmap che indica le colonne aggiornate nel caso di un conflitto aggiornamento-aggiornamento.|  
|__$inserted_date|**datetime**|Data e ora in cui la riga in conflitto è stata inserita in questa tabella.|  
|__$row_id|**timestamp**|Versione della riga associata alla riga che ha causato il conflitto.|  
|__$change_id|**file binario (8)**|Per una riga locale, questo valore è uguale a __$row_id della riga in ingresso in conflitto con la riga locale. Questo valore è NULL per una riga in ingresso.|  
|\<i nomi di colonna nella tabella di base >|\<tipi di colonna nella tabella di base >|Questa tabella dei conflitti contiene una colonna per ogni colonna presente nella tabella di base.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
