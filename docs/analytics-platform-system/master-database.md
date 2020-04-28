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
ms.openlocfilehash: cafef8a5b702b6df4475d34e9395bb12bc9461fb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "74400981"
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
|Creare un backup completo del database master.|Esempio:<br /><br />`BACKUP DATABASE master TO backup_directory;`<br /><br />Per ulteriori informazioni, vedere [backup database](../t-sql/statements/backup-database-parallel-data-warehouse.md).|  
|Ripristinare il database master|Per ripristinare il database master, utilizzare la pagina [Ripristina database master](restore-the-master-database.md) dello strumento Configuration Manager.|  
|Visualizzare le informazioni del catalogo del database.|`SELECT * FROM master.sys.databases;`|  
|Consente di visualizzare informazioni sulle autorizzazioni e sull'accesso a livello di sistema.|`SELECT * FROM master.sys.server_permissions;`<br /><br />`SELECT * FROM master.sys.server_principals;`<br /><br />`SELECT * FROM master.sys.sql_logins;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
