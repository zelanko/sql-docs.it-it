---
title: Catalogo di visualizzazioni (Transact-SQL) | Documenti di Microsoft
ms.custom: ''
ms.date: 05/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sql13.SysViewExpandPortal.f1
dev_langs:
- TSQL
helpviewer_keywords:
- catalog metadata [SQL Server]
- system views [SQL Server], catalog
- metadata [SQL Server], views
- catalogs [SQL Server], metadata
- catalog views [SQL Server]
- Database Engine [SQL Server], metadata
- catalog views [SQL Server], about catalog views
ms.assetid: 13bccc2f-ed3c-4b58-abd0-ca8bf34a66b8
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4679c8dbc853f0bc902a59cb653330a638b2f685
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62960001"
---
# <a name="system-catalog-views-transact-sql"></a>Viste del catalogo di sistema (Transact-SQL)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Le viste del catalogo restituiscono informazioni utilizzate da [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. È consigliabile utilizzare tali viste perché rappresentano l'interfaccia più immediata per l'accesso ai metadati del catalogo e sono inoltre lo strumento più efficiente per ottenere, trasformare e presentare tali informazioni in forme personalizzate. Tutti i metadati del catalogo disponibili per gli utenti vengono esposti tramite le viste del catalogo.  
  
> [!NOTE]  
>  Le viste del catalogo non contengono informazioni sulla replica, il backup, il piano di manutenzione del database o i dati del catalogo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 Alcune viste del catalogo ereditano le righe da altre viste del catalogo. Ad esempio, il [Sys. Tables](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md) vista del catalogo eredita dal [Sys. Objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) vista del catalogo. La vista del catalogo sys.objects viene indicata come vista di base e la vista sys.tables come vista derivata. La vista del catalogo sys.tables restituisce non solo le colonne specifiche per le tabelle, ma anche tutte le colonne restituite dalla vista del catalogo sys.objects. La vista del catalogo sys.objects restituisce le righe per gli oggetti diversi dalle tabelle, ad esempio stored procedure e viste. Al termine della creazione di una tabella, i relativi metadati vengono restituiti in entrambe le viste. Nonostante le due viste del catalogo restituiscano diversi livelli di informazioni sulla tabella, nei metadati è presente un'unica voce, con un nome e un object_id corrispondenti. Questo processo può essere riepilogato nel modo seguente:  
  
-   La vista di base contiene un subset di colonne e un superset di righe.  
  
-   La vista derivata contiene un superset di colonne e un subset di righe.  
  
> [!IMPORTANT]  
>  Nelle versioni future di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è possibile che [!INCLUDE[msCoName](../../includes/msconame-md.md)] estenda la definizione delle viste del catalogo di sistema aggiungendo colonne all'elenco delle colonne. È consigliabile evitare di utilizzare la sintassi SELECT \* FROM *sys.catalog_view_name* nell'ambiente di produzione codice perché il numero di colonne restituite potrebbe cambiare e la suddivisione dell'applicazione.  
  
 Le viste del catalogo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono organizzate nelle categorie seguenti:  
  
|||  
|-|-|  
|[Gruppi di disponibilità Always On viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)|[I messaggi &#40;errori&#41; viste del catalogo &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/8ac78c53-7b97-41b3-9cbd-5f97c179f1f2)|  
|[Viste del catalogo del Database SQL di Azure](../../relational-databases/system-catalog-views/azure-sql-database-catalog-views.md)|[Viste del catalogo dell'oggetto &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)|  
|[Viste del catalogo di rilevamento delle modifiche &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/6e8fd949-5560-4b34-879f-4e25aa24b183)|[Viste del catalogo delle funzioni di partizione &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/partition-function-catalog-views-transact-sql.md)|  
|[Viste del catalogo di Assembly CLR &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/clr-assembly-catalog-views-transact-sql.md)|[Viste di Gestione basata su criteri &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)|  
|[Viste dell'agente di raccolta dati &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)|[Viste del catalogo di Resource Governor &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)|  
|[Data Spaces &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-spaces-transact-sql.md)|[Viste del catalogo di Archivio query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)|  
|[Viste di posta elettronica del database &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mail-views-transact-sql.md)|[Viste del catalogo di tipi scalari &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)|  
|[Viste del catalogo di server di controllo di mirroring del database &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/8a0c9053-5d76-4aa9-a18d-0ea1c514034d)|[Viste del catalogo schemi &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/c516fb1c-b6ed-48ae-99c7-a78bc4336c8e)|  
|[Viste del catalogo di database e i file &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)|[Viste del catalogo relative alla sicurezza &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)|  
|[Viste del catalogo degli endpoint &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)|[Viste del catalogo di Service Broker &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/service-broker-catalog-views-transact-sql.md)|  
|[Viste del catalogo degli eventi estesi &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)|[Viste del catalogo a livello di server di configurazione &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/server-wide-configuration-catalog-views-transact-sql.md)|  
|[Viste del catalogo delle proprietà estese &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/f39fd324-efd4-4468-884c-bf77ed1a026f)|[Viste del catalogo dati spaziali](../../relational-databases/system-catalog-views/spatial-data-catalog-views.md)|  
|[Operazioni esterne viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/external-operations-catalog-views-transact-sql.md)|[SQL Data Warehouse e Parallel Data Warehouse viste del catalogo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)|  
|[FileStream e viste del catalogo FileTable &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)|[Stretch Database viste del catalogo &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/bee78e39-e07d-4b0f-b8ad-09a01a5eb795)|  
|[Ricerca full-Text e semantica viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/full-text-search-and-semantic-search-catalog-views-transact-sql.md)|[XML schema &#40;sistema di tipi XML&#41; viste del catalogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)|  
|[Viste del catalogo di server collegati &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)||  
  
## <a name="see-also"></a>Vedere anche  
 [Viste degli schemi delle informazioni &#40;Transact-SQL&#41;](../../relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [Tabelle di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)   
 [Domande frequenti sull'esecuzione di query nel catalogo di sistema di SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
