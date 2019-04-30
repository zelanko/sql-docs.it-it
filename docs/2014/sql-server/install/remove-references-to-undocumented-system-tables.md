---
title: Rimuovere i riferimenti alle tabelle di sistema non documentate | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- undocumented system tables [SQL Server]
- system tables [SQL Server]
ms.assetid: 010b1236-2219-4bf4-a6db-e3fc3abfa37a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0c2c25120191b88abcf177723749aa5c46ba44ff
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63294822"
---
# <a name="remove-references-to-undocumented-system-tables"></a>Rimuovere i riferimenti alle tabelle di sistema non documentate
  Molte tabelle di sistema non documentate nelle versioni precedenti sono state modificate o non esistono più. L'utilizzo di tali tabelle potrebbe pertanto provocare errori dopo l'aggiornamento. Poiché Preparazione aggiornamento cerca i riferimenti ai nomi delle tabella di sistema, segnalerà anche i riferimenti a tutte le tabelle utente che hanno nomi uguali a quelli delle tabelle di sistema.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrizione  
 Le seguenti tabelle di sistema non documentate sono state rimosse:  
  
-   **spt_datatype_info**  
  
-   **spt_datatype_info_ext**  
  
-   **spt_provider_types**  
  
-   **spt_server_info**  
  
-   **spt_values**  
  
-   **sysfulltextnotify**  
  
-   **syslocks**  
  
-   **sysproperties**  
  
-   **sysprotects_aux**  
  
-   **sysprotects_view**  
  
-   **SYSREMOTE_CATALOGS**  
  
-   **SYSREMOTE_COLUMN_PRIVILEGES**  
  
-   **SYSREMOTE_COLUMNS**  
  
-   **SYSREMOTE_FOREIGN_KEYS**  
  
-   **SYSREMOTE_INDEXES**  
  
-   **SYSREMOTE_PRIMARY_KEYS**  
  
-   **SYSREMOTE_PROVIDER_TYPES**  
  
-   **SYSREMOTE_SCHEMATA**  
  
-   **SYSREMOTE_STATISTICS**  
  
-   **SYSREMOTE_TABLE_PRIVILEGES**  
  
-   **SYSREMOTE_TABLES**  
  
-   **SYSREMOTE_VIEWS**  
  
-   **syssegments**  
  
-   **sysxlogins**  
  
## <a name="corrective-action"></a>Azione correttiva  
 Modificare le applicazioni in base alla tabella seguente.  
  
|Anziché|Utilizzare|  
|----------------|---------|  
|**sysfulltextnotify**|**TableFulltextPendingChanges** proprietà della funzione OBJECTPROPERTYEX.|  
|**syslocks**|**DM tran_locks** vista a gestione dinamica o sp_lock, o il **Sys. syslockinfo** visualizzazione compatibilità.|  
|**sysproperties**|**Sys. extended_properties** vista del catalogo o il **fn_listextendedproperty** (funzione)|  
|**sysxlogins**|**Sys. server_principals** vista del catalogo o **syslogins** visualizzazione compatibilità.|  
|tutti i **spt _** tabelle|Nessuna sostituzione disponibile|  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento del motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Preparazione aggiornamento a SQL Server 2014 &#91;new&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
