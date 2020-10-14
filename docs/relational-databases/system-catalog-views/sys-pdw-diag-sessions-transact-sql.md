---
description: sys.pdw_diag_sessions (Transact-SQL)
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
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: e8fade6ec60ada411ee78027d01f9616e499f755
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036749"
---
# <a name="syspdw_diag_sessions-transact-sql"></a>sys.pdw_diag_sessions (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Contiene informazioni relative alle varie sessioni di diagnostica create nel sistema.  
  
|Nome colonna|Tipo di dati|Descrizione|Range|  
|-----------------|---------------|-----------------|-----------|  
|**nome**|**nvarchar(255)**|Nome della sessione di diagnostica.<br /><br /> Chiave per questa visualizzazione.||  
|**xml_data**|**nvarchar(4000)**|Payload XML che descrive la sessione.||  
|**is_active**|**bit**|Flag che indica se il flag è attivo.||  
|**host_address**|**nvarchar(255)**|Indirizzo del computer che ospita la definizione di sessione (nodo di controllo).||  
|**principal_id**|**int**|ID dell'utente che ha creato la sessione a livello di database.||  
|**database_id**|**int**|ID del database che rappresenta l'ambito della sessione di diagnostica.|  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo di Azure Synapse Analytics e Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
