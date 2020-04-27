---
title: Rimuovere i riferimenti alle tabelle di sistema non documentate | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- undocumented system tables [SQL Server]
- system tables [SQL Server]
ms.assetid: 010b1236-2219-4bf4-a6db-e3fc3abfa37a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 06249aa1849a1be9af40e183724e85b0f318f3dc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66093152"
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
  
|Anziché|Uso|  
|----------------|---------|  
|**sysfulltextnotify**|Proprietà **TableFulltextPendingChanges** della funzione OBJECTPROPERTYEX.|  
|**syslocks**|**sys. dm_tran_locks** vista a gestione dinamica o sp_lock o la vista di compatibilità **sys. syslockinfo** .|  
|**sysproperties**|**sys. extended_properties** vista del catalogo o funzione **fn_listextendedproperty**|  
|**sysxlogins**|**sys. server_principals** vista del catalogo o vista di compatibilità **syslogins** .|  
|tutte le tabelle **spt_**|Nessuna sostituzione disponibile|  
  
## <a name="see-also"></a>Vedi anche  
 [Problemi di aggiornamento motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 preparazione aggiornamento &#91;nuova&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
