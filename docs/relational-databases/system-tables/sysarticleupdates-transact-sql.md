---
description: sysarticleupdates (Transact-SQL)
title: sysarticleupdates (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysarticleupdates_TSQL
- sysarticleupdates
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticleupdates system table
ms.assetid: 11a53bcd-a215-4d0b-9db8-233981d3ef5d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9ca984460c74628f919e16c77c3a3a97fa732b52
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89518194"
---
# <a name="sysarticleupdates-transact-sql"></a>sysarticleupdates (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contiene una riga per ogni articolo che supporta sottoscrizioni ad aggiornamento immediato. Questa tabella è archiviata nel database replicato.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|Colonna Identity che include un numero di ID univoco per l'articolo.|  
|**pubid**|**int**|ID della pubblicazione a cui appartiene l'articolo.|  
|**sync_ins_proc**|**int**|ID della stored procedure che gestisce le transazioni di sincronizzazione per gli inserimenti.|  
|**sync_upd_proc**|**int**|ID della stored procedure che gestisce le transazioni di sincronizzazione per gli aggiornamenti.|  
|**sync_del_proc**|**int**|ID della stored procedure che gestisce le transazioni di sincronizzazione per le eliminazioni.|  
|**autogen**|**bit**|Indica che vengono generate automaticamente stored procedure:<br /><br /> **0** = false, non automatico.<br /><br /> **1** = true, automatica.|  
|**sync_upd_trig**|**int**|ID del trigger per la gestione automatica delle versioni nella tabella degli articoli.|  
|**conflict_tableid**|**int**|ID della tabella dei conflitti.|  
|**ins_conflict_proc**|**int**|ID della procedura utilizzata per scrivere il conflitto nell' **conflict_table**.|  
|**identity_support**|**bit**|Specifica se la gestione automatica degli intervalli di valori Identity è attivata quando si utilizza l'aggiornamento in coda. **0** indica che non è disponibile alcun supporto per l'intervallo di valori Identity.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
