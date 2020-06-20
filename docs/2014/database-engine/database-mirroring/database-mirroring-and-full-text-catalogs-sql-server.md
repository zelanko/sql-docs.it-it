---
title: Mirroring di database e cataloghi full-text (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- full-text catalogs [SQL Server], database mirroring
- catalogs [SQL Server], database mirroring
ms.assetid: e34072ae-fe8a-462d-bb03-02fa0987f793
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 39929f4bed6edbd1e8ec5c1b72dbe8f7aefeec68
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934350"
---
# <a name="database-mirroring-and-full-text-catalogs-sql-server"></a>Mirroring di database e cataloghi full-text (SQL Server)
  Per eseguire il mirroring di un database che include un catalogo full-text, eseguire le consuete operazioni di backup per creare un backup completo del database principale e quindi ripristinare il backup per copiare il database nel server mirror. Per altre informazioni, vedere [Preparazione di un database mirror per il mirroring &#40;SQL Server&#41;](prepare-a-mirror-database-for-mirroring-sql-server.md).  
  
## <a name="full-text-catalog-and-indexes-before-failover"></a>Catalogo e indici full-text prima del failover  
 Il catalogo full-text di un nuovo database mirror corrisponde a quello disponibile al momento del backup del database. Dopo l'avvio del mirroring del database, tutte le modifiche a livello di catalogo apportate dall'istruzione (CREATE FULLTEXT CATALOG, ALTER FULLTEXT CATALOG, DROP FULLTEXT CATALOG) vengono registrare e inviate al server mirror per la riproduzione nel database mirror. Le modifiche a livello di indice, invece, non vengono replicate nel database mirror perché non vengono registrate nel server principale. Pertanto, quando cambia il contenuto del catalogo full-text nel database principale, il contenuto del catalogo full-text nel database mirror non sarà sincronizzato.  
  
## <a name="full-text-indexes-after-failover"></a>Indici full-text dopo il failover  
 Dopo un failover, la ricerca completa di un indice full-text sul nuovo server principale può risultare utile o necessaria nelle situazioni seguenti:  
  
-   Se è disabilitato il rilevamento delle modifiche su un indice full-text, è necessario avviare una ricerca per indicizzazione completa utilizzando l'istruzione seguente:  
  
     ALTER FULLTEXT INDEX ON *table_name* avviare il popolamento completo  
  
-   Se un indice full-text è configurato per il rilevamento automatico delle modifiche, l'indice viene sincronizzato automaticamente. La sincronizzazione, tuttavia, determina un rallentamento delle prestazioni full-text. In caso di rallentamento eccessivo delle prestazioni, è possibile eseguire una ricerca per indicizzazione completa disattivando il rilevamento delle modifiche e quindi reimpostando il rilevamento automatico:  
  
    -   Per disattivare il rilevamento delle modifiche:  
  
         ALTER FULLTEXT INDEX ON *nome_tabella* SET CHANGE_TRACKING OFF  
  
    -   Per impostare il rilevamento automatico delle modifiche:  
  
         ALTER FULLTEXT INDEX ON *nome_tabella* SET CHANGE_TRACKING AUTO  
  
    > [!NOTE]  
    >  Per determinare se il rilevamento automatico delle modifiche è attivo, è possibile usare la funzione [OBJECTPROPERTYEX](/sql/t-sql/functions/objectproperty-transact-sql) per eseguire una query sulla proprietà **TableFullTextBackgroundUpdateIndexOn** della tabella.  
  
 Per altre informazioni, vedere [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql).  
  
> [!NOTE]  
>  L'avvio di una ricerca per indicizzazione dopo un failover viene eseguito esattamente come l'avvio di una ricerca per indicizzazione dopo un ripristino.  
  
## <a name="after-forcing-service"></a>Dopo la forzatura del servizio  
 Dopo la forzatura del servizio nel server mirror, con possibile perdita di dati, avviare una ricerca per indicizzazione completa. Il metodo da utilizzare per l'avvio di una ricerca per indicizzazione completa dipende dall'attivazione o disattivazione del rilevamento delle modifiche nell'indice full-text. Per ulteriori informazioni, vedere "Indici full-text dopo il failover" più indietro in questo argomento.  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)   
 [DROP FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-fulltext-index-transact-sql)   
 [&#40;SQL Server di mirroring del database&#41;](database-mirroring-sql-server.md)   
 [Backup e ripristino di indici e cataloghi full-text](../../relational-databases/indexes/indexes.md)  
  
  
