---
title: Query sui dati in una tabella temporale con controllo delle versioni di sistema | Microsoft Docs
ms.custom: ''
ms.date: 03/28/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 2d358c2e-ebd8-4eb3-9bff-cfa598a39125
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3de7c69169198302535eb7ff5dc855faa4f44974
ms.sourcegitcommit: 769b71f01052ec9b4fc5eb02d9da9a1a58118029
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56319112"
---
# <a name="querying-data-in-a-system-versioned-temporal-table"></a>Query sui dati in una tabella temporale con controllo delle versioni di sistema
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Quando occorre recuperare lo stato (effettivo) più aggiornato dei dati in una tabella temporale, è possibile eseguire query esattamente nello stesso modo valido per l'esecuzione di query in tabelle non temporali. Se le colonne PERIOD non sono nascoste, i rispettivi valori compariranno in una query SELECT \* . Se le colonne **PERIOD** sono state specificate come nascoste, i rispettivi valori non saranno visualizzati in una query SELECT \*. Quando le colonne **PERIOD** sono nascoste, è possibile fare riferimento in modo specifico alle colonne **PERIOD** nella clausola SELECT per restituire i valori per queste colonne.  
  
 Per eseguire qualsiasi tipo di analisi basata sul tempo, usare la nuova clausola **FOR SYSTEM_TIME** con quattro sottoclausole specifiche per i dati temporali per eseguire query sui dati nelle tabelle correnti e di cronologia. Per ulteriori informazioni su queste clausole, vedere [Tabelle temporali](../../relational-databases/tables/temporal-tables.md) e [FROM &#40;Transact-SQL #41;](../../t-sql/queries/from-transact-sql.md)  
  
-   AS OF <data_ora>  
  
-   FROM <data_ora_inizio> TO <data_ora_fine>  
  
-   BETWEEN <data_ora_inizio> AND <data_ora_fine>  
  
-   CONTAINED IN (<data_ora_inizio> , <data_ora_fine>)  
  
-   ALL  
  
 È possibile specificare**FOR SYSTEM_TIME** in modo indipendente per ogni tabella in una query. La clausola può essere usata all'interno di espressioni di tabella comuni, funzioni con valore di tabella e stored procedure.  
  
## <a name="query-for-a-specific-time-using-the-as-of-sub-clause"></a>Query per un data/ora specifica con la sottoclausola AS-OF  
 Usare la sottoclausola **AS OF** quando è necessario ricostruire lo stato dei dati esistente in un momento specifico nel passato. È possibile ricostruire i dati con la precisione del tipo datetime2 specificato nelle definizioni di colonna **PERIOD** .    
La sottoclausola **AS OF** può essere usata con valori letterali costanti o variabili e ciò consente di specificare in modo dinamico la condizione temporale. I valori specificati vengono interpretati come ora UTC.  
  
 Questo primo esempio restituisce lo stato della tabella dbo.Department in riferimento (AS OF) a una data specifica nel passato.  
  
```  
/*State of entire table AS OF specific date in the past*/   
SELECT [DeptID], [DeptName], [SysStartTime],[SysEndTime]   
FROM [dbo].[Department]   
FOR SYSTEM_TIME AS OF '2015-09-01 T10:00:00.7230011' ;  
  
```  
  
 Questo secondo esempio confronta i valori tra due punti nel tempo per un subset di righe.  
  
```  
DECLARE @ADayAgo datetime2   
SET @ADayAgo = DATEADD (day, -1, sysutcdatetime())   
/*Comparison between two points in time for subset of rows*/   
SELECT D_1_Ago.[DeptID], D.[DeptID],   
D_1_Ago.[DeptName], D.[DeptName],   
D_1_Ago.[SysStartTime], D.[SysStartTime],   
D_1_Ago.[SysEndTime], D.[SysEndTime]   
FROM [dbo].[Department] FOR SYSTEM_TIME AS OF @ADayAgo AS D_1_Ago   
JOIN [Department] AS D ON  D_1_Ago.[DeptID] = [D].[DeptID]    
AND D_1_Ago.[DeptID] BETWEEN 1 and 5 ;  
```  
  
### <a name="using-views-with-as-of-sub-clause-in-temporal-queries"></a>Uso delle viste con la sottoclausola AS OF nelle query temporali  
 Usare le viste è molto utile in scenari che richiedono analisi temporizzate complesse.   
Un esempio comune è la generazione di un report aziendale con i valori per il mese precedente.   
I clienti si affidano in genere a un modello di database normalizzato che include molte tabelle con relazioni di chiave esterna. Può essere molto complicato risalire allo stato dei dati in un punto nel passato da questo modello normalizzato, in quanto tutte le tabelle cambiano in modo indipendente, ognuna con un ritmo proprio.   
In questo caso, la soluzione migliore consiste nel creare una vista e applicare la sottoclausola **AS OF** all'intera vista. Questo approccio consente di separare la modellazione del livello di accesso ai dati dall'analisi temporizzata, perché SQL Server applicherà la clausola **AS OF** in modo trasparente a tutte le tabelle temporali che fanno parte della definizione della vista. Inoltre, è possibile combinare tabelle temporali e non temporali nella stessa vista e la clausola **AS OF** verrà applicata solo a quelle temporali. Se la vista non fa riferimento ad almeno una tabella temporale, l'applicazione di clausole di query temporali avrà esito negativo con un errore.  
  
```  
/* Create view that joins three temporal tables: Department, CompanyLocation, LocationDepartments */   
CREATE VIEW [dbo].[vw_GetOrgChart]   
AS   
SELECT   
     [CompanyLocation].LocID  
   , [CompanyLocation].LocName  
   , [CompanyLocation].City  
   , [Department].DeptID  
   , [Department].DeptName    
FROM [dbo].[CompanyLocation]   
LEFT JOIN [dbo].[LocationDepartments]    
   ON [CompanyLocation].LocID = LocationDepartments.LocID   
LEFT JOIN [dbo].[Department]    
   ON LocationDepartments.DeptID = [Department].DeptID ;  
GO   
/* Querying view AS OF */   
SELECT * FROM [vw_GetOrgChart]   
FOR SYSTEM_TIME AS OF '2015-09-01 T10:00:00.7230011' ;  
  
```  
  
## <a name="query-for-changes-to-specific-rows-over-time"></a>Query per le modifiche apportate a colonne specifiche nel tempo  
 Le sottoclausole temporali **FROM...TO**, **BETWEEN...AND** e **CONTAINED IN** sono utili per l'esecuzione di un controllo dei dati, ovvero quando è necessario recuperare tutte le modifiche cronologiche per una riga specifica nella tabella corrente.   
Le prime due sottoclausole restituiscono le versioni di riga che si sovrappongono a un periodo specificato (ad esempio quelle con inizio prima del periodo specificato e fine dopo tale periodo), mentre CONTAINED IN restituisce solo le righe esistenti entro i limiti del periodo specificato.  
  
> [!IMPORTANT]  
>  Se è necessario cercare solo versioni di riga non aggiornate, è consigliabile eseguire la query direttamente sulla tabella di cronologia, poiché offre le migliori prestazioni di query. Usare **ALL** quando occorre eseguire query sui dati correnti e cronologici senza restrizioni.  
  
```  
/* Query using BETWEEN...AND sub-clause*/  
SELECT   
     [DeptID]  
   , [DeptName]  
   , [SysStartTime]  
   , [SysEndTime]  
   , IIF (YEAR(SysEndTime) = 9999, 1, 0) AS IsActual   
FROM [dbo].[Department]   
FOR SYSTEM_TIME BETWEEN  '2015-01-01' AND '2015-12-31'   
WHERE DeptId = 1   
ORDER BY SysStartTime DESC;   
  
/*  Query using CONTAINED IN sub-clause */  
SELECT [DeptID], [DeptName], [SysStartTime],[SysEndTime]   
FROM [dbo].[Department]   
FOR SYSTEM_TIME CONTAINED IN ('2015-04-01', '2015-09-25')   
WHERE DeptId = 1   
ORDER BY SysStartTime DESC ;  
  
/*  Query using ALL sub-clause */   
SELECT    
     [DeptID]   
   , [DeptName]   
   , [SysStartTime]   
   , [SysEndTime]   
   , IIF (YEAR(SysEndTime) = 9999, 1, 0) AS IsActual    
FROM [dbo].[Department] FOR SYSTEM_TIME ALL   
ORDER BY [DeptID], [SysStartTime] Desc  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle temporali](../../relational-databases/tables/temporal-tables.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [Creazione di una tabella temporale con controllo delle versioni di sistema](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)   
 [Modifica dei dati in una tabella temporale con controllo delle versioni di sistema](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)   
 [Modifica dello schema di una tabella temporale con controllo delle versioni di sistema](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)   
 [Arresto del controllo delle versioni di sistema in una tabella temporale con controllo delle versioni di sistema](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)  
  
  
