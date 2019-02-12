---
title: sys.pdw_diag_sessions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 4d23688a-cddb-4eed-8231-ecde2a0b0e65
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: bd48648719e04ca1eec15c4594b08cc1d40505b9
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56028632"
---
# <a name="syspdwdiagsessions-transact-sql"></a>sys.pdw_diag_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Contiene informazioni riguardanti le diverse sessioni di diagnostica che sono stati creati nel sistema.  
  
|Nome colonna|Tipo di dati|Descrizione|Intervallo|  
|-----------------|---------------|-----------------|-----------|  
|**name**|**nvarchar(255)**|Nome della sessione di diagnostica.<br /><br /> Chiave per questa visualizzazione.||  
|**xml_data**|**nvarchar(4000)**|Payload XML che descrive la sessione.||  
|**is_active**|**bit**|Flag che indica se il flag è attivo.||  
|**host_address**|**nvarchar(255)**|Indirizzo del computer che ospita la definizione della sessione (nodo di controllo).||  
|**principal_id**|**int**|ID dell'utente che ha creato la sessione a livello di database.||  
|**database_id**|**int**|ID del database che è l'ambito della sessione di diagnostica.|  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Data Warehouse e Parallel Data Warehouse viste del catalogo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
