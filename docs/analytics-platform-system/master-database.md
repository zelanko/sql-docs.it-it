---
title: Database master
description: Informazioni sul database master in parallelo data warehouse.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 526f7c7bea8d7ed1e7499649d929f6c732ab07a3
ms.sourcegitcommit: 3bd188e652102f3703812af53ba877cce94b44a9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/15/2020
ms.locfileid: "97489681"
---
# <a name="master-database---parallel-data-warehouse"></a>Database master-data warehouse parallela
Il database master SQL Server PDW archivia le informazioni di accesso a livello di dispositivo e il catalogo del database. Si tratta di un database master SQL Server che risiede nel nodo di controllo. Di conseguenza, fornisce funzionalità simili a SQL Server PDW come il master fornisce per SQL Server.  
  
Per ulteriori informazioni sui database di sistema, vedere [database di sistema](system-databases.md).  
  
## <a name="limitations-and-restrictions"></a>Limitazioni e restrizioni  
Nell'elenco seguente vengono descritte le operazioni che non è possibile eseguire nel database master SQL Server PDW.  
  
*Non è possibile:*  
  
-   Eseguire un backup differenziale del database master.  
  
-   Creare oggetti utente nel database master.  
  
-   Modificare le regole di confronto del database master.  
  
-   Modificare il proprietario del database master.  
  
-   Eliminare o rinominare il database master.  
  
-   Modificare le autorizzazioni per il database master.  
  
-   Eseguire **DBCC SHRINKLOG**.  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Attività|Descrizione|  
|--------|---------------|  
|Creare un backup completo del database master.|Esempio:<br /><br />`BACKUP DATABASE master TO backup_directory;`<br /><br />Per ulteriori informazioni, vedere [backup database](../t-sql/statements/backup-transact-sql.md?view=aps-pdw-2016&preserve-view=true).|  
|Ripristinare il database master|Per ripristinare il database master, utilizzare la pagina [Ripristina database master](restore-the-master-database.md) dello strumento Configuration Manager.|  
|Visualizzare le informazioni del catalogo del database.|`SELECT * FROM master.sys.databases;`|  
|Consente di visualizzare informazioni sulle autorizzazioni e sull'accesso a livello di sistema.|`SELECT * FROM master.sys.server_permissions;`<br /><br />`SELECT * FROM master.sys.server_principals;`<br /><br />`SELECT * FROM master.sys.sql_logins;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
