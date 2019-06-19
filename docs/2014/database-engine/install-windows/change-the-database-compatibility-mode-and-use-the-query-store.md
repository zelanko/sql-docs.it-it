---
title: Eseguire la migrazione di piani di Query | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- query plans [SQL Server], migrating
- upgrading SQL Server, migrating query plans
- plan guides [SQL Server], migrating query plans
ms.assetid: 7e02a137-6867-4f6a-a45a-2b02674f7e65
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 66f1f8f57dca3ad2edba3f4b63100b2de3ae5659
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62779113"
---
# <a name="migrate-query-plans"></a>Migrare piani di query
  Nella maggior parte dei casi, l'aggiornamento di un database alla versione più recente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] comporta un miglioramento delle prestazioni di esecuzione delle query. Tuttavia, se sono presenti query critiche attentamente ottimizzate per le prestazioni, potrebbe essere necessario mantenere i piani per tali query prima di eseguire l'aggiornamento creando una guida di piano per ciascuna query. Se, dopo aver eseguito l'aggiornamento, Query Optimizer sceglie un piano meno efficiente per una o più query, è possibile abilitare le guide di piano e forzare il Query Optimizer a utilizzare i piani precedenti all'aggiornamento.  
  
 Per creare guide di piano prima di eseguire l'aggiornamento, eseguire la procedura seguente:  
  
1.  Registrare il piano corrente per ciascuna query critica utilizzando la [sp_create_plan_guide](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql) stored procedure e specificando il piano di query nell'hint per la query USE PLAN.  
  
2.  Verificare che la guida di piano sia applicata alla query.  
  
3.  Aggiornare il database alla versione più recente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     I piani sono persistenti nel database aggiornato nelle guide di piano e vengono utilizzati come fallback in caso di regressioni del piano dopo l'aggiornamento.  
  
     Si consiglia di non abilitare le guide di piano dopo l'aggiornamento, in quanto si potrebbero perdere opportunità per migliori piani nella nuova versione o ricompilazioni vantaggiose grazie a statistiche aggiornate.  
  
4.  Se vengono scelti piani meno efficienti dopo l'aggiornamento, attivare tutte o un subset delle guide di piano per sostituire i nuovi piani.  
  
## <a name="example"></a>Esempio  
 Nel seguente esempio viene illustrato come registrare un piano prima dell'aggiornamento per una query creando una guida di piano.  
  
### <a name="step-1-collect-the-plan"></a>Passaggio 1: Raccogliere il piano  
 Il piano di query registrato nella guida di piano deve essere in formato XML. È possibile creare piani di query in formato XML nei seguenti modi:  
  
-   [SET SHOWPLAN_XML](/sql/t-sql/statements/set-showplan-xml-transact-sql)  
  
-   [SET STATISTICS XML](/sql/t-sql/statements/set-statistics-xml-transact-sql)  
  
-   Una query sulla colonna query_plan della [DM exec_query_plan](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql) funzione a gestione dinamica.  
  
-   Il [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] [Showplan XML](../../relational-databases/event-classes/showplan-xml-event-class.md), [Showplan XML Statistics Profile](../../relational-databases/event-classes/showplan-xml-statistics-profile-event-class.md), e [Showplan XML For Query Compile](../../relational-databases/event-classes/showplan-xml-for-query-compile-event-class.md) classi di evento.  
  
 Nell'esempio seguente viene raccolto il piano di query per l'istruzione `SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;` eseguendo una query sulle DMV.  
  
```  
USE AdventureWorks;  
GO  
SELECT query_plan  
    FROM sys.dm_exec_query_stats AS qs   
    CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st  
    CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, DEFAULT, DEFAULT) AS qp  
    WHERE st.text LIKE N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;%';  
GO  
```  
  
### <a name="step-2-create-the-plan-guide-to-force-the-plan"></a>Passaggio 2: Creare la Guida di piano per forzare il piano  
 Utilizzando nella guida di piano il piano di query in formato XML ottenuto con uno dei metodi descritti in precedenza, copiare e incollare il piano di query come valore letterale stringa nell'hint per la query USE PLAN specificato nella clausola OPTION di sp_create_plan_guide.  
  
 All'interno del piano XML, aggiungere una seconda virgoletta ai caratteri di escape (') visualizzati nel piano prima di creare la guida di piano. Ad esempio, per un piano che contiene `WHERE A.varchar = 'This is a string'` è necessario utilizzare i caratteri di escape modificando il codice in `WHERE A.varchar = ''This is a string''`.  
  
 Nell'esempio seguente viene creata una guida di piano per il piano di query raccolto nel passaggio 1 e viene inserito Showplan XML per la query nel parametro `@hints`. Per brevità, nell'esempio viene incluso solo l'output Showplan parziale.  
  
```  
EXECUTE sp_create_plan_guide   
@name = N'Guide1',  
@stmt = N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;',  
@type = N'SQL',  
@module_or_batch = NULL,  
@params = NULL,  
@hints = N'OPTION(USE PLAN N''<ShowPlanXML xmlns=''''https://schemas.microsoft.com/sqlserver/2004/07/showplan''''   
    Version=''''0.5'''' Build=''''9.00.1116''''>  
    <BatchSequence><Batch><Statements><StmtSimple>  
    ...  
    </StmtSimple></Statements></Batch>  
    </BatchSequence></ShowPlanXML>'')';  
GO  
```  
  
### <a name="step-3-verify-that-the-plan-guide-is-applied-to-the-query"></a>Passaggio 3: Verificare che la Guida di piano viene applicata alla Query  
 Eseguire nuovamente la query ed esaminare il piano di query prodotto. Verificare che il piano corrisponda a quello di cui specificato nella guida.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [Hint di query &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query)   
 [Guide di piano](../../relational-databases/performance/plan-guides.md)  
  
  
