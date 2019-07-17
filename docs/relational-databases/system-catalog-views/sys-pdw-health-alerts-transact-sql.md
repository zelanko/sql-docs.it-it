---
title: sys.pdw_health_alerts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: system-objects
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 49c01e5f-ee47-41a0-871d-35a759f50851
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: c47bcc342bf8a052aed93649ca0ad8475d937608
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68127536"
---
# <a name="syspdwhealthalerts-transact-sql"></a>sys.pdw_health_alerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Archivia le proprietà per i diversi avvisi che possono verificarsi nel sistema. si tratta di una tabella del catalogo per gli avvisi.  
  
|Nome colonna|Tipo di dati|Descrizione|Intervallo|  
|-----------------|---------------|-----------------|-----------|  
|alert_id|**int**|Identificatore univoco dell'avviso.<br /><br /> Chiave per questa visualizzazione.|NOT NULL|  
|component_id|**int**|ID del componente di a che questo avviso si applica. Il componente è un identificatore del componente generali, ad esempio "Stato dell'alimentatore," e non è specifico di un'installazione. Visualizzare [sys.pdw_health_components &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).|NOT NULL|  
|alert_name|**nvarchar(255)**|Nome dell'avviso.|NOT NULL|  
|state|**nvarchar(32)**|Stato dell'avviso.|NOT NULL<br /><br /> I valori possibili sono:<br /><br /> 'Operational'<br /><br /> "Non operativo"<br /><br /> "Degradato"<br /><br /> "Non riuscito"|  
|severity|**nvarchar(32)**|Gravità dell'avviso.|NOT NULL<br /><br /> I valori possibili sono:<br /><br /> 'Informational'<br /><br /> "Avviso"<br /><br /> 'Error'|  
|type|**nvarchar(32)**|Tipo di avviso.|NOT NULL<br /><br /> I valori possibili sono:<br /><br /> StatusChange - è stato modificato lo stato del dispositivo.<br /><br /> Soglia - valore ha superato il valore di soglia.|  
|description|**nvarchar(4000)**|Descrizione dell'avviso.|NOT NULL|  
|condizione|**nvarchar(255)**|Utilizzato quando tipo uguale a soglia. Definisce come viene calcolata la soglia di avviso.|NULL|  
|status|**nvarchar(32)**|Stato dell'avviso|NULL|  
|condition_value|**bit**|Indica se l'avviso può verificarsi durante il funzionamento del sistema.|NULL<br /><br /> Valori possibili<br /><br /> 0 - avviso non viene generato.<br /><br /> 1 - avviso viene generato.|  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Data Warehouse e Parallel Data Warehouse viste del catalogo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
