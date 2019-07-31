---
title: Viste del catalogo (Transact-SQL) | Microsoft Docs
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9532ee19ec8489caa51d090feaff464e030a0da0
ms.sourcegitcommit: c70a0e2c053c2583311fcfede6ab5f25df364de0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/31/2019
ms.locfileid: "68670554"
---
# <a name="system-catalog-views-transact-sql"></a>Viste del catalogo di sistema (Transact-SQL)

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Le viste del catalogo restituiscono informazioni utilizzate da [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. È consigliabile utilizzare tali viste perché rappresentano l'interfaccia più immediata per l'accesso ai metadati del catalogo e sono inoltre lo strumento più efficiente per ottenere, trasformare e presentare tali informazioni in forme personalizzate. Tutti i metadati del catalogo disponibili per gli utenti vengono esposti tramite le viste del catalogo.

> [!NOTE]
> Le viste del catalogo non contengono informazioni sulla replica, il backup, il piano di manutenzione del database o i dati del catalogo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.

 Alcune viste del catalogo ereditano le righe da altre viste del catalogo. Ad esempio, la vista del catalogo [sys. Tables](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md) eredita dalla vista del catalogo [sys. Objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) . La vista del catalogo sys.objects viene indicata come vista di base e la vista sys.tables come vista derivata. La vista del catalogo sys.tables restituisce non solo le colonne specifiche per le tabelle, ma anche tutte le colonne restituite dalla vista del catalogo sys.objects. La vista del catalogo sys.objects restituisce le righe per gli oggetti diversi dalle tabelle, ad esempio stored procedure e viste. Al termine della creazione di una tabella, i relativi metadati vengono restituiti in entrambe le viste. Nonostante le due viste del catalogo restituiscano diversi livelli di informazioni sulla tabella, nei metadati è presente un'unica voce, con un nome e un object_id corrispondenti. Questo processo può essere riepilogato nel modo seguente:

- La vista di base contiene un subset di colonne e un superset di righe.
- La vista derivata contiene un superset di colonne e un subset di righe.

> [!IMPORTANT]
> Nelle versioni future di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è possibile che [!INCLUDE[msCoName](../../includes/msconame-md.md)] estenda la definizione delle viste del catalogo di sistema aggiungendo colonne all'elenco delle colonne. È consigliabile evitare di usare la sintassi \* Select from *sys. catalog_view_name* nel codice di produzione perché il numero di colonne restituite potrebbe cambiare e interrompere l'applicazione.

Le viste del catalogo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono organizzate nelle categorie seguenti:

|||
|-|-|
|[Always On le viste &#40;del catalogo di gruppi di disponibilità Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)|[Messaggi &#40;per gli&#41; errori viste &#40;del catalogo di&#41;Transact-SQL](../system-catalog-views/messages-for-errors-catalog-views-sys-messages.md))|
|[Viste del catalogo del database SQL di Azure](../../relational-databases/system-catalog-views/azure-sql-database-catalog-views.md)|[Transact-SQL &#40;viste del catalogo oggetti&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)|
|[Rilevamento modifiche viste &#40;del catalogo Transact-SQL&#41;](../system-catalog-views/change-tracking-catalog-views-sys-change-tracking-databases.md)|[Viste &#40;del catalogo delle funzioni di partizione Transact-SQL&#41;](../../relational-databases/system-catalog-views/partition-function-catalog-views-transact-sql.md)|
|[Transact-SQL viste &#40;del catalogo degli assembly CLR&#41;](../../relational-databases/system-catalog-views/clr-assembly-catalog-views-transact-sql.md)|[Viste di Gestione basata su criteri &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)|
|[Transact-SQL &#40;viste agente di raccolta dati&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)|[Resource Governor viste &#40;del catalogo Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)|
|[Transact- &#40;SQL per spazi dati&#41;](../../relational-databases/system-catalog-views/data-spaces-transact-sql.md)|[Viste del catalogo di Archivio query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)|
|[Viste &#40;posta elettronica database Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mail-views-transact-sql.md)|[Viste &#40;del catalogo di tipi scalari Transact-SQL&#41;](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)|
|[Viste &#40;del catalogo del server di controllo del mirroring del database Transact-SQL&#41;](../system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)|[Viste &#40;del catalogo degli schemi Transact-SQL&#41;](../system-catalog-views/schemas-catalog-views-sys-schemas.md)|
|[Viste &#40;del catalogo di database e file-Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)|[Viste del catalogo relative alla sicurezza &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)|
|[Viste &#40;del catalogo degli endpoint Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)|[Viste del catalogo di Service Broker &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/service-broker-catalog-views-transact-sql.md)|
|[Viste del catalogo degli eventi estesi &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)|[Viste &#40;del catalogo di configurazione a livello di server Transact-SQL&#41;](../../relational-databases/system-catalog-views/server-wide-configuration-catalog-views-transact-sql.md)|
|[Viste del catalogo delle proprietà estese &#40;Transact-SQL&#41;](../system-catalog-views/extended-properties-catalog-views-sys-extended-properties.md)|[Viste di Data Catalog spaziali](../../relational-databases/system-catalog-views/spatial-data-catalog-views.md)|
|[Transact-SQL viste &#40;del catalogo delle operazioni esterne&#41;](../../relational-databases/system-catalog-views/external-operations-catalog-views-transact-sql.md)|[SQL Data Warehouse e Parallel data warehouse viste del catalogo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)|
|[Transact-SQL viste &#40;del catalogo FILESTREAM e FileTable&#41;](../../relational-databases/system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)|[Stretch Database viste &#40;del catalogo Transact-SQL&#41;](../system-catalog-views/stretch-database-catalog-views-sys-remote-data-archive-databases.md)|
|[Viste &#40;del catalogo di ricerca full-text e semantico Transact-SQL&#41;](../../relational-databases/system-catalog-views/full-text-search-and-semantic-search-catalog-views-transact-sql.md)|[XML schema- &#40;viste &#40;del catalogo&#41; di sistema di tipo XML Transact-SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)|
|[Viste &#40;del catalogo di server collegati-Transact-SQL&#41;](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)||

## <a name="see-also"></a>Vedere anche

- [Viste &#40;degli schemi delle informazioni-Transact-SQL&#41;](../../relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)
- [Tabelle di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)
- [Domande frequenti sull'esecuzione di query nel catalogo di sistema di SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)
