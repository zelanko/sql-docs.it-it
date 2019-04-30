---
title: Database master - Parallel Data Warehouse | Microsoft Docs
description: Informazioni sui database master in Parallel Data Warehouse.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: bf07b9c27e08a49cb0866b177a0ec37fed4528a0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63213292"
---
# <a name="master-database---parallel-data-warehouse"></a>Database master - Parallel Data Warehouse
Il database master di SQL Server PDW archivia le informazioni di accesso a livello di dispositivo e il catalogo del database. È un database master di SQL Server che si trova nel nodo di controllo. Di conseguenza, fornisce funzionalità simili a SQL Server PDW come master consente a SQL Server.  
  
Per altre informazioni sui database di sistema, vedere [database di sistema](system-databases.md).  
  
## <a name="limitations-and-restrictions"></a>Limitazioni e restrizioni  
Nell'elenco seguente descrive le operazioni che non è possibile eseguire nel database master di SQL Server PDW.  
  
Si *non è possibile:*  
  
-   Eseguire un backup differenziale del database master.  
  
-   Creare oggetti utente nel database master.  
  
-   Modificare le regole di confronto del database master.  
  
-   Modificare il proprietario del database master.  
  
-   Eliminare o rinominare master.  
  
-   Modificare le autorizzazioni allo schema.  
  
-   Eseguire **DBCC SHRINKLOG**.  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Attività|Descrizione|  
|--------|---------------|  
|Creare un backup completo del database master.|Esempio:<br /><br />`BACKUP DATABASE master TO backup_directory;`<br /><br />Per altre informazioni, vedere [BACKUP DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md).|  
|Ripristinare il database master|Per ripristinare il database master, usare il [ripristinare il Master Database](restore-the-master-database.md) pagina dello strumento Configuration Manager.|  
|Visualizzare le informazioni del catalogo di database.|`SELECT * FROM master.sys.databases;`|  
|Visualizzare le informazioni di accesso e autorizzazione a livello di sistema.|`SELECT * FROM master.sys.server_permissions;`<br /><br />`SELECT * FROM master.sys.server_principals;`<br /><br />`SELECT * FROM master.sys.sql_logins;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
