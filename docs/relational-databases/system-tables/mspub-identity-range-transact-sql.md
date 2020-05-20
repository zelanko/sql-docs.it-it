---
title: MSpub_identity_range (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpub_identity_range_TSQL
- MSpub_identity_range
dev_langs:
- TSQL
helpviewer_keywords:
- MSpub_identity_range system table
ms.assetid: 68746eef-32e1-42bc-aff0-9798cd0e88b8
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 733fac032af45eb81b50bae4b20316d04234223e
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82812511"
---
# <a name="mspub_identity_range-transact-sql"></a>MSpub_identity_range (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La tabella **MSpub_identity_range** fornisce supporto per la gestione degli intervalli di valori Identity. Questa tabella è archiviata nei database di pubblicazione e di sottoscrizione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**objid**|**int**|ID della tabella la cui colonna Identity è gestita dalla replica.|  
|**intervallo**|**bigint**|Controlla le dimensioni dell'intervallo di valori Identity consecutivi che verrebbe assegnato nella sottoscrizione durante un intervento di regolazione.|  
|**pub_range**|**bigint**|Controlla le dimensioni dell'intervallo di valori Identity consecutivi che verrebbe assegnato nella pubblicazione durante un intervento di regolazione.|  
|**current_pub_range**|**bigint**|Intervallo corrente utilizzato dalla pubblicazione. Può essere diverso da *pub_range* se visualizzato dopo essere stato modificato da **sp_changearticle** e prima della regolazione dell'intervallo successivo.|  
|**soglia**|**int**|Valore percentuale che controlla quando l'agente di distribuzione assegna un nuovo intervallo di valori Identity. Quando viene utilizzata la percentuale di valori specificata in *Threshold* , il agente di distribuzione crea un nuovo intervallo di valori Identity.|  
|**last_seed**|**bigint**|Limite inferiore dell'intervallo corrente.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
