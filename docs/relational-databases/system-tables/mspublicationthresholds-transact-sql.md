---
title: MSpublicationthresholds (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- mspublicationthresholds
- mspublicationthresholds_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpublicationthresholds system table
ms.assetid: 9da3879f-b1f4-4ab4-abd4-a9a8ac395eba
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2bf5659dc8a5a440b764b3264556359205646d75
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088521"
---
# <a name="mspublicationthresholds-transact-sql"></a>MSpublicationthresholds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **MSpublicationthresholds** tabella viene utilizzata per tenere traccia delle metriche delle prestazioni di replica per una pubblicazione, con una riga per ogni valore soglia monitorato. Questa tabella è archiviata nel database di distribuzione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**publication_id**|**int**|Identifica la pubblicazione per cui è stata impostato un valore soglia.|  
|**metric_id**|**int**|Identifica una misurazione delle prestazioni di replica da monitorare, definita nel [MSreplmonthresholdmetrics](../../relational-databases/system-tables/msreplmonthresholdmetrics-transact-sql.md) tabella di sistema.|  
|**Valore**|**sql_variant**|Valore soglia della misurazione da monitorare.|  
|**shouldalert**|**bit**|Un valore pari **1** indica che deve essere generato un avviso quando la metrica supera la soglia definita.|  
|**isenabled**|**bit**|Un valore pari **1** indica che il monitoraggio è abilitato per la metrica di prestazioni di replica.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
