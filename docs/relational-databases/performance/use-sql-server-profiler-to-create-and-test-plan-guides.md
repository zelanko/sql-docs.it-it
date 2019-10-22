---
title: Usare SQL Server Profiler per creare e testare guide di piano | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- checking plan guides
- plan guides [SQL Server], testing
- plan guides [SQL Server], SQL Server Profiler
- matching queries to plan guides [SQL Server]
- testing plan guides
- SQL Server Profiler, plan guides
- plan guides [SQL Server], creating
- capturing query text [SQL Server]
- verifying plan guides
- Profiler [SQL Server Profiler], plan guides
- query-to-plan guide matching [SQL Server]
ms.assetid: 7018dbf0-1a1a-411a-88af-327bedf9cfbd
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 271e84ccefd43f2ce379a64435a9eb105553f606
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305083"
---
# <a name="use-sql-server-profiler-to-create-and-test-plan-guides"></a>Usare SQL Server Profiler per creare e testare guide di piano
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Quando si crea una guida di piano è possibile usare [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] per acquisire il testo esatto della query da usare nell'argomento *statement_text* della stored procedure **sp_create_plan_guide** . Questo garantisce che in fase di compilazione la guida di piano corrisponderà alla query. Dopo la creazione della guida di piano è possibile utilizzare ancora [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] per verificare che la guida di piano corrisponda effettivamente alla query. È in genere consigliabile testare le guide di piano tramite [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] per verificarne la corrispondenza con la query.  
  
## <a name="capturing-query-text-by-using-sql-server-profiler"></a>Acquisizione del testo di una query tramite SQL Server Profiler  
 Se si esegue una query e se ne acquisisce il testo esattamente come è stato inviato a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], sarà possibile creare una guida di piano di tipo SQL o TEMPLATE che corrisponderà esattamente al testo della query. Questo garantisce che la guida di piano verrà utilizzata da Query Optimizer.  
  
 Si consideri la query seguente, inviata da un'applicazione come batch autonomo:  
  
```  
SELECT COUNT(*) AS c  
FROM Sales.SalesOrderHeader AS h  
INNER JOIN Sales.SalesOrderDetail AS d  
  ON h.SalesOrderID = d.SalesOrderID  
WHERE h.OrderDate BETWEEN '20000101' and '20050101';  
```  
  
 Si supponga di voler eseguire la query tramite un'operazione di merge join, ma che SHOWPLAN indichi che la query non sta utilizzando un merge join. Non è possibile modificare la query direttamente nell'applicazione, pertanto è necessario creare una guida di piano per specificare che l'hint per la query MERGE JOIN venga accodato alla query in fase di compilazione.  
  
 Per acquisire il testo della query esattamente come viene ricevuto da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , eseguire la procedura seguente:  
  
1.  Avviare una traccia di [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] verificando che sia selezionato il tipo di evento **SQL:BatchStarting** .  
  
2.  Eseguire la query dall'applicazione.  
  
3.  Sospendere la traccia di [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] .  
  
4.  Fare clic sull'evento **SQL:BatchStarting** corrispondente alla query.  
  
5.  Fare clic con il pulsante destro del mouse e scegliere **Estrai dati eventi**.  
  
    > [!IMPORTANT]  
    >  Non tentare di copiare il testo del batch selezionandolo dal riquadro inferiore della finestra di traccia di SQL Profiler. In caso contrario, la guida di piano creata potrebbe non corrispondere al batch originale.  
  
6.  Salvare i dati degli eventi in un file. Si ottiene in tal modo il testo del batch.  
  
7.  Aprire il file del testo del batch nel Blocco note e copiare il testo.  
  
8.  Creare la guida di piano e incollare il testo copiato tra le virgolette ( **"** ) specificate per l'argomento **\@stmt**. È necessario usare caratteri di escape per ogni virgoletta singola nell'argomento **\@stmt** facendola precedere da un'altra virgoletta singola. Fare attenzione a non aggiungere o rimuovere altri caratteri quando si inseriscono queste virgolette. Ad esempio, il valore letterale di data **'** 20000101 **'** deve essere delimitato come **''** 20000101 **''** .  
  
 La guida di piano ottenuta è la seguente:  
  
```  
EXEC sp_create_plan_guide   
    @name = N'MyGuide1',  
    @stmt = N'<paste the text copied from the batch text file here>',  
    @type = N'SQL',  
    @module_or_batch = NULL,  
    @params = NULL,  
    @hints = N'OPTION (MERGE JOIN)';  
```  
  
## <a name="testing-plan-guides-by-using-sql-server-profiler"></a>Test della guida di piano tramite SQL Server Profiler  
 Per verificare la corrispondenza tra una guida di piano e una query, eseguire la procedura seguente:  
  
1.  Avviare una traccia di [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] verificando che sia selezionato il tipo di evento **Showplan XML** , disponibile nel nodo **Performance** .  
  
2.  Eseguire la query dall'applicazione.  
  
3.  Sospendere la traccia di [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] .  
  
4.  Trovare l'evento **Showplan XML** relativo alla query interessata.  
  
    > [!NOTE]  
    >  L'evento **Showplan XML for Query Compile** non può essere usato. **PlanGuideDB** non esiste nell'evento in questione.  
  
5.  Se la guida di piano è di tipo OBJECT o SQL, verificare che nell'evento **Showplan XML** siano contenuti gli attributi **PlanGuideDB** e **PlanGuideName** per la guida di piano che si prevedeva corrispondesse alla query. In alternativa, se la guida di piano è di tipo TEMPLATE, verificare che l'evento **Showplan XML** contenga gli attributi **TemplatePlanGuideDB** e **TemplatePlanGuideName** per la guida di piano prevista. Se tali attributi sono presenti, la guida di piano funziona regolarmente. Questi attributi sono contenuti nell'elemento **\<StmtSimple>** del piano.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
  
  
