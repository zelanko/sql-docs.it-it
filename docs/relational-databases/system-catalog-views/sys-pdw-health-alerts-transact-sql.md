---
description: sys.pdw_health_alerts (Transact-SQL)
title: sys.pdw_health_alerts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: 49c01e5f-ee47-41a0-871d-35a759f50851
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: e2e265a7905313a988a15fb29de0a8c86b397ac8
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036751"
---
# <a name="syspdw_health_alerts-transact-sql"></a>sys.pdw_health_alerts (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Archivia le proprietà per i diversi avvisi che possono verificarsi nel sistema. si tratta di una tabella del catalogo per gli avvisi.  
  
|Nome colonna|Tipo di dati|Descrizione|Range|  
|-----------------|---------------|-----------------|-----------|  
|alert_id|**int**|Identificatore univoco dell'avviso.<br /><br /> Chiave per questa visualizzazione.|NOT NULL|  
|component_id|**int**|ID del componente a cui si applica questo avviso. Il componente è un identificatore generale del componente, ad esempio "alimentatore", e non è specifico di un'installazione. Vedere [sys.pdw_health_components &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).|NOT NULL|  
|alert_name|**nvarchar(255)**|Nome dell'avviso.|NOT NULL|  
|state|**nvarchar(32)**|Stato dell'avviso.|NOT NULL<br /><br /> Valori possibili:<br /><br /> Operativo<br /><br /> ' Non operativo '<br /><br /> Degradato<br /><br /> Fallito|  
|severity|**nvarchar(32)**|Gravità dell'avviso|NOT NULL<br /><br /> Valori possibili:<br /><br /> Informativo<br /><br /> Avviso<br /><br /> Errore|  
|tipo|**nvarchar(32)**|Tipo di avviso.|NOT NULL<br /><br /> Valori possibili:<br /><br /> StatusChange-lo stato del dispositivo è stato modificato.<br /><br /> Soglia: un valore ha superato il valore di soglia.|  
|description|**nvarchar(4000)**|Descrizione dell'avviso.|NOT NULL|  
|condizione|**nvarchar(255)**|Utilizzato quando Type = Threshold. Definisce la modalità di calcolo della soglia di avviso.|NULL|  
|status|**nvarchar(32)**|Stato dell'avviso|NULL|  
|condition_value|**bit**|Indica se l'avviso può verificarsi durante l'operazione di sistema.|NULL<br /><br /> Valori possibili<br /><br /> 0: l'avviso non viene generato.<br /><br /> 1: viene generato un avviso.|  
  
## <a name="see-also"></a>Vedere anche  
 [Viste del catalogo di Azure Synapse Analytics e Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
