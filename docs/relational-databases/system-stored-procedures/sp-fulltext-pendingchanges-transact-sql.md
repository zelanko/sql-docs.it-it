---
title: sp_fulltext_pendingchanges (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_pendingchanges_TSQL
- sp_fulltext_pendingchanges
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_pendingchanges
ms.assetid: fee042fe-4781-4a33-a01b-d98fb5629f1b
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b360a899ed17f0b1b82a5ebcdfbd664803ed8d93
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82828383"
---
# <a name="sp_fulltext_pendingchanges-transact-sql"></a>sp_fulltext_pendingchanges (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Restituisce modifiche non ancora elaborate, ad esempio inserimenti, aggiornamenti ed eliminazioni in sospeso, per una tabella specificata che utilizza il rilevamento delle modifiche.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_fulltext_pendingchanges table_id  
```  
  
## <a name="arguments"></a>Argomenti  
 *table_id*  
 ID della tabella. Se non è una tabella con indicizzazione full-text o il rilevamento delle modifiche non è abilitato nella tabella, viene restituito un errore.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**Codice**|*|Valore di chiave full-text dalla tabella specificata.|  
|**DocId**|**bigint**|Colonna dell'identificatore interno del documento (DocID) corrispondente al valore della chiave.|  
|**Status**|**int**|0 = La riga verrà rimossa dall'indice full-text.<br /><br /> 1 = Alla riga verrà applicata l'indicizzazione full-text.<br /><br /> 2 = La riga è aggiornata.<br /><br /> -1 = La riga è in uno stato di transizione (elaborazione batch senza commit) o in uno stato di errore.|  
|**DocState**|**tinyint**|Dump non elaborato della colonna relativa allo stato del mapping dell'identificatore interno del documento (DocId).|  
  
 <sup>* Il tipo di dati per la colonna Key corrisponde al tipo di dati della colonna chiave full-text nella tabella di base.</sup>  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'appartenenza al ruolo predefinito del server **sysadmin** .  
  
## <a name="remarks"></a>Commenti  
 Se non ci sono modifiche da elaborare, viene restituito un set di righe vuoto.  
  
 Le query di ricerca full-text non restituiscono righe con un valore di **stato** 0. Questo perché la riga è stata eliminata dalla tabella di base ed è in attesa di essere eliminata dall'indice full-text.  
  
 Per verificare il numero di modifiche in attesa per una determinata tabella, utilizzare la proprietà **TableFullTextPendingChanges** della funzione OBJECTPROPERTYEX.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure per la ricerca full-text e la ricerca semantica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)   
 [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)  
  
  
