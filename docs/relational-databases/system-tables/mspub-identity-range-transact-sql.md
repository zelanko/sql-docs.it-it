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
author: stevestein
ms.author: sstein
ms.openlocfilehash: b1b204024d65e72eb65eefc9f63f914eab6ace29
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032607"
---
# <a name="mspubidentityrange-transact-sql"></a>MSpub_identity_range (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **MSpub_identity_range** tabella fornisce il supporto di gestione di identità intervallo. Questa tabella è archiviata nei database di pubblicazione e di sottoscrizione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**objid**|**int**|ID della tabella la cui colonna Identity è gestita dalla replica.|  
|**Intervallo**|**bigint**|Controlla le dimensioni dell'intervallo di valori Identity consecutivi che verrebbe assegnato nella sottoscrizione durante un intervento di regolazione.|  
|**pub_range**|**bigint**|Controlla le dimensioni dell'intervallo di valori Identity consecutivi che verrebbe assegnato nella pubblicazione durante un intervento di regolazione.|  
|**current_pub_range**|**bigint**|Intervallo corrente utilizzato dalla pubblicazione. Può essere diverso da quello *sp_changearticle* se viene visualizzato dopo essere stato modificato tramite **sp_changearticle** e prima della regolazione intervallo successiva.|  
|**threshold**|**int**|Valore percentuale che controlla quando l'agente di distribuzione assegna un nuovo intervallo di valori Identity. Quando la percentuale di valori specificato in *soglia* viene usato, l'agente di distribuzione crea un nuovo intervallo di valori identity.|  
|**last_seed**|**bigint**|Limite inferiore dell'intervallo corrente.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
