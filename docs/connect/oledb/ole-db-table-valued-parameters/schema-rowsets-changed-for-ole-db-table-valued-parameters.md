---
title: Set di righe dello schema modificati per i parametri con valori di tabella OLE DB | Microsoft Docs
description: Set di righe dello schema modificati per i parametri con valori di tabella OLE DB
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- schema rowsets [OLE DB]
- table-valued parameters (OLE DB), schema rowsets changed for (OLE DB)
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 3140a882c29a0cc319f85a861d3f341370f1a93a
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2020
ms.locfileid: "86008711"
---
# <a name="schema-rowsets-changed-for-ole-db-table-valued-parameters"></a>Set di righe dello schema modificati per i parametri con valori di tabella OLE DB
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Di seguito sono elencati i set di righe dello schema che sono stati modificati o aggiunti per il supporto dei parametri con valori di tabella.  
  
|Set di righe dello schema|Descrizione|  
|-------------------|-----------------|  
|DBSCHEMA_PROCEDURE_PARAMETERS|Alla fine del set di righe sono state aggiunte due nuove colonne denominate SS_TYPE_CATALOG_NAME e SS_TYPE_SCHEMANAME. Tali colonne potrebbero essere riutilizzate per i tipi futuri. Le colonne TYPE_NAME e LOCAL_TYPE_NAME conterranno il nome del tipo TABLE dei parametri con valori di tabella. La colonna DATA_TYPE avrà il valore DBTYPE_TABLE = 143 per i parametri con valori di tabella.|  
|DBSCHEMA_TABLE_TYPES|Questo set di righe è stato aggiunto per supportare i parametri con valori di tabella. È identico a DBSCHEMA_TABLES, con l'eccezione che restituisce metadati solo per i tipi di tabella, anziché per tabelle, viste o sinonimi. La colonna TABLE_TYPE avrà il valore TABLE TYPE.|  
|DBSCHEMA_TABLE_TYPE_PRIMARY_KEYS|Questo set di righe è stato aggiunto per supportare i parametri con valori di tabella. È identico a DBSCHEMA_PRIMARY_KEYS, con l'eccezione che restituisce chiavi primarie solo per i tipi di tabella, anziché per tabelle, viste o sinonimi.|  
|DBSCHEMA_TABLE_TYPE_COLUMNS|Questo set di righe è stato aggiunto per supportare i parametri con valori di tabella. È identico a DBSCHEMA_COLUMNS, con l'eccezione che restituisce metadati di colonna solo per i tipi di tabella, anziché per tabelle, viste o sinonimi.|  
  
## <a name="see-also"></a>Vedere anche  
 [Parametri con valori di tabella &#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usare parametri con valori di tabella &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
