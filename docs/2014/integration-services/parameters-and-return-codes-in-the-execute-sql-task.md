---
title: I parametri e codici restituiti nell'attività Esegui SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- return codes [Integration Services]
- parameters [Integration Services]
- parameterized SQL statements [Integration Services]
- Execute SQL task [Integration Services]
ms.assetid: a3ca65e8-65cf-4272-9a81-765a706b8663
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f0899922eb2cdec88e73901f14ebeb6dfe953622
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53367214"
---
# <a name="parameters-and-return-codes-in-the-execute-sql-task"></a>Parametri e codici restituiti nell’attività Esegui SQL
  Le stored procedure e le istruzioni SQL utilizzano spesso parametri di `input`, parametri di `output`e codici restituiti. In [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] l'attività Esegui SQL supporta parametri di tipo `Input`, `Output` e `ReturnValue`. Il tipo `Input` viene utilizzato per i parametri di input, il tipo `Output` per i parametri di output e il tipo `ReturnValue` per i codici restituiti.  
  
> [!NOTE]  
>  È possibile utilizzare parametri in un'attività Esegui SQL solo se il provider di dati li supporta.  
  
 Sui parametri inclusi nei comandi SQL, comprese le query e le stored procedure, viene eseguito il mapping a variabili definite dall'utente create nell'ambito dell'attività Esegui SQL, in un contenitore padre o nell'ambito del pacchetto. I valori delle variabili possono essere impostati in fase di progettazione o popolati dinamicamente in fase di esecuzione. È inoltre possibile eseguire il mapping dei parametri a variabili di sistema. Per altre informazioni, vedere [Variabili di Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md) e [Variabili di sistema](system-variables.md).  
  
 Tuttavia, l'utilizzo di parametri e di codici restituiti in un'attività Esegui SQL non si limita solo alla conoscenza dei tipi di parametro supportati dall'attività e del modo in cui si esegue il mapping di questi parametri. Sono previsti ulteriori requisiti e linee guida per utilizzare correttamente i parametri e i codici restituiti nell'attività Esegui SQL. Nella parte restante di questo argomento vengono illustrati tali requisiti e linee guida:  
  
-   [Uso di nomi e marcatori di parametro](#Parameter_names_and_markers)  
  
-   [Uso di parametri con i tipi di dati di data e ora](#Date_and_time_data_types)  
  
-   [Uso di parametri nelle clausole WHERE](#WHERE_clauses)  
  
-   [Uso di parametri con le stored procedure](#Stored_procedures)  
  
-   [Recupero dei valori dei codici restituiti](#Return_codes)  
  
-   [Configurazione di parametri e codici restituiti nell'Editor attività Esegui SQL](#Configure_parameters_and_return_codes)  
  
##  <a name="Parameter_names_and_markers"></a> Utilizzo di nomi di parametro e marcatori  
 Nella sintassi del comando SQL possono essere utilizzati marcatori di parametro diversi, a seconda del tipo di connessione utilizzato dall'attività Esegui SQL. Per il tipo di gestione connessione [!INCLUDE[vstecado](../includes/vstecado-md.md)], ad esempio, l'indicatore di parametro usato nel comando SQL deve avere il formato **\@varParameter**, mentre per il tipo di connessione OLE DB l'indicatore di parametro deve essere costituito da un punto interrogativo (?).  
  
 Anche i nomi che è possibile utilizzare come nomi di parametro nei mapping tra variabili e parametri variano a seconda del tipo di gestione connessione. Il tipo di gestione connessione [!INCLUDE[vstecado](../includes/vstecado-md.md)] usa ad esempio un nome definito dall'utente con prefisso \@, mentre il tipo di gestione connessione OLE DB richiede nomi di parametro costituiti dal valore numerico di un ordinale in base 0.  
  
 Nella tabella seguente sono riepilogati i requisiti dei comandi SQL, a seconda dei tipi di gestione connessione utilizzati dall'attività Esegui SQL.  
  
|Tipo di connessione|Marcatore di parametro|Nome parametro|Comando SQL di esempio|  
|---------------------|----------------------|--------------------|-------------------------|  
|ADO|?|Param1, Param2, ...|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|\@\<nome parametro>|\@\<nome parametro>|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = \@parmContactID|  
|ODBC|?|1, 2, 3, ...|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
|EXCEL e OLE DB|?|0, 1, 2, 3, ...|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
  
### <a name="using-parameters-with-adonet-and-ado-connection-managers"></a>Utilizzo di parametri con le gestioni connessioni ADO.NET e ADO  
 [!INCLUDE[vstecado](../includes/vstecado-md.md)] e le gestioni connessioni ADO hanno requisiti specifici per i comandi SQL che usano parametri:  
  
-   Le gestioni connessioni [!INCLUDE[vstecado](../includes/vstecado-md.md)] richiedono che il comando SQL usi nomi di parametro come indicatori di parametro. È pertanto possibile eseguire il mapping direttamente delle variabili ai parametri. Se ad esempio sulla variabile `@varName` viene eseguito il mapping a un parametro di nome `@parName` , fornirà il valore per il parametro `@parName`.  
  
-   Per le gestioni connessioni ADO, è necessario che il comando SQL utilizzi punti interrogativi (?) come marcatori di parametro. Tuttavia, come nomi di parametro è possibile utilizzare qualsiasi nome definito dall'utente, ad eccezione dei valori interi.  
  
 Per fornire i valori ai parametri sulle variabili viene eseguito il mapping ai nomi di parametro. L'attività Esegui SQL utilizza quindi il valore ordinale del nome di parametro nell'elenco dei parametri per caricare i valori dalle variabili ai parametri.  
  
### <a name="using-parameters-with-excel-odbc-and-ole-db-connection-managers"></a>Utilizzo di parametri con le gestioni connessioni EXCEL, ODBC e OLE DB  
 Per le gestioni connessioni EXCEL, ODBC e OLE DB, è necessario che il comando SQL utilizzi punti interrogativi (?) come marcatori di parametro e valori numerici in base 0 o in base 1 come nomi di parametro. Se l'attività Esegui SQL utilizza la gestione connessione ODBC, il nome del parametro di cui viene eseguito il mapping al primo parametro nella query è 1, altrimenti è 0. Per i parametri successivi, il valore numerico del nome del parametro indica il parametro del comando SQL a cui viene eseguito il mapping del nome di parametro. Sul parametro di nome 3, ad esempio, viene eseguito il mapping al terzo parametro, rappresentato dal terzo punto interrogativo (?) nel comando SQL.  
  
 Per fornire i valori ai parametri, sulle variabili viene eseguito il mapping ai nomi di parametro e l'attività Esegui SQL utilizza il valore ordinale del nome di parametro per caricare i valori dalle variabili ai parametri.  
  
 A seconda del provider utilizzato dalla gestione connessione, alcuni tipi di dati OLE DB potrebbero non essere supportati. Il driver per Excel, ad esempio, riconosce solo un set limitato di tipi di dati. Per altre informazioni sul comportamento del provider Jet usato insieme al driver per Excel, vedere [Origine Excel](data-flow/excel-source.md).  
  
#### <a name="using-parameters-with-ole-db-connection-managers"></a>Utilizzo di parametri con le gestioni connessioni OLE DB  
 Quando l'attività Esegui SQL usa la gestione connessione OLE DB, è disponibile la proprietà BypassPrepare dell'attività. Questa proprietà deve essere impostata su `true` se l'attività Esegui SQL utilizza istruzioni SQL con parametri.  
  
 Quando si utilizza una gestione connessione OLE DB, non è possibile utilizzare sottoquery con parametri, perché l'attività Esegui SQL non può derivare le informazioni sui parametri tramite il provider OLE DB. Tuttavia, è possibile utilizzare un'espressione per concatenare i valori dei parametri nella stringa di query e impostare la proprietà SqlStatementSource dell'attività.  
  
##  <a name="Date_and_time_data_types"></a> Utilizzo di parametri con tipi data e ora dei dati  
  
### <a name="using-date-and-time-parameters-with-adonet-and-ado-connection-managers"></a>Utilizzo di parametri di data e ora con le gestioni connessioni ADO.NET e ADO  
 Durante la lettura dei tipi di dati di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], `time` e `datetimeoffset`, un'attività Esegui SQL che utilizza una gestione connessione [!INCLUDE[vstecado](../includes/vstecado-md.md)] o ADO prevede i requisiti aggiuntivi seguenti:  
  
-   Per i dati `time`, una gestione connessione [!INCLUDE[vstecado](../includes/vstecado-md.md)] richiede che i dati vengano archiviati in un parametro con tipo di parametro `Input` o `Output` e con tipo di dati `string`.  
  
-   Per i dati `datetimeoffset`, una gestione connessione [!INCLUDE[vstecado](../includes/vstecado-md.md)] richiede che i dati vengano archiviati in uno dei parametri seguenti:  
  
    -   Un parametro il cui tipo di parametro è `Input` e il cui tipo di dati è `string`.  
  
    -   Un parametro il cui tipo di parametro è `Output` o `ReturnValue` e il cui tipo di dati è `datetimeoffset`, `string` o `datetime2`. Se si seleziona un parametro il cui tipo di dati è `string` o `datetime2`, [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] converte i dati in string o datetime2.  
  
-   Una gestione connessione ADO richiede che i dati `time` o `datetimeoffset` vengano archiviati in un parametro con tipo di parametro `Input` o `Output` e con tipo di dati `adVarWchar`.  
  
 Per altre informazioni sui tipi di dati [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e sul relativo mapping nei tipi di dati [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], vedere [Tipi di dati &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql) e [Tipi di dati di Integration Services](data-flow/integration-services-data-types.md).  
  
### <a name="using-date-and-time-parameters-with-ole-db-connection-managers"></a>Utilizzo di parametri di data e ora con le gestioni connessioni OLE DB  
 Quando si utilizza una gestione connessione OLE DB, un'attività Esegui SQL prevede requisiti di archiviazione specifici per i tipi di dati di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], `date`, `time`, `datetime`, `datetime2` e `datetimeoffset`. È necessario archiviare questi dati in uno dei seguenti tipi di parametro:  
  
-   Un parametro di input del tipo di dati NVARCHAR.  
  
-   Un parametro di output con il tipo di dati appropriato, come elencato nella tabella seguente.  
  
    |Tipo di parametro `Output`|Tipo di dati date|  
    |-------------------------------|--------------------|  
    |DBDATE|`date`|  
    |DBTIME2|`time`|  
    |DBTIMESTAMP|`datetime`, `datetime2`|  
    |DBTIMESTAMPOFFSET|`datetimeoffset`|  
  
 Se i dati non vengono archiviati nel parametro di input o di output appropriato, il pacchetto non viene eseguito correttamente.  
  
### <a name="using-date-and-time-parameters-with-odbc-connection-managers"></a>Utilizzo di parametri di data e ora con le gestioni connessioni ODBC  
 Quando si utilizza una gestione connessione ODBC, un'attività Esegui SQL prevede requisiti di archiviazione specifici per i tipi di dati di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], `date`, `time`, `datetime`, `datetime2` e `datetimeoffset`. È necessario archiviare questi dati in uno dei seguenti tipi di parametro:  
  
-   Un parametro di `input` del tipo di dati SQL_WVARCHAR.  
  
-   Un parametro di `output` con il tipo di dati appropriato, come elencato nella tabella seguente.  
  
    |Tipo di parametro `Output`|Tipo di dati date|  
    |-------------------------------|--------------------|  
    |SQL_DATE|`date`|  
    |SQL_SS_TIME2|`time`|  
    |SQL_TYPE_TIMESTAMP<br /><br /> oppure<br /><br /> SQL_TIMESTAMP|`datetime`, `datetime2`|  
    |SQL_SS_TIMESTAMPOFFSET|`datetimeoffset`|  
  
 Se i dati non vengono archiviati nel parametro di input o di output appropriato, il pacchetto non viene eseguito correttamente.  
  
##  <a name="WHERE_clauses"></a> Utilizzo di parametri nella posizione in cui le clausole  
 I comandi SELECT, INSERT, UPDATE e DELETE includono spesso la clausola WHERE per specificare filtri che definiscono le condizioni che ogni riga nelle tabelle di origine deve soddisfare per essere qualificata per un comando SQL. I parametri specificano i valori del filtro per la clausola WHERE.  
  
 È possibile utilizzare marcatori di parametro per specificare dinamicamente i valori dei parametri. Le regole che determinano se è possibile utilizzare marcatori di parametro e nomi di parametro in un'istruzione SQL dipendono dal tipo di gestione connessione utilizzato dall'attività Esegui SQL.  
  
 Nella tabella seguente sono elencati esempi di comandi SELECT per tipo di gestione connessione. Le istruzioni INSERT, UPDATE e DELETE sono analoghe. Negli esempi l'istruzione SELECT viene usata per recuperare dalla tabella **Product** del database [!INCLUDE[ssSampleDBUserInputNonLocal](../includes/sssampledbuserinputnonlocal-md.md)] i prodotti con **ProductID** compreso tra i valori specificati da due parametri.  
  
|Tipo di connessione|Sintassi dell'istruzione SELECT|  
|---------------------|-------------------|  
|EXCEL, ODBC e OLEDB|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
|ADO|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|`SELECT* FROM Production.Product WHERE ProductId > @parmMinProductID AND ProductID < @parmMaxProductID`|  
  
 Gli esempi richiedono parametri con i nomi seguenti:  
  
-   Per le gestioni connessioni EXCEL e OLED DB vengono utilizzati i nomi di parametro 0 e 1. Per il tipo di connessione ODBC vengono utilizzati 1 e 2.  
  
-   Per il tipo di connessione ADO è possibile utilizzare qualsiasi nome per i due parametri, ad esempio Param1 e Param2, ma è necessario eseguire il mapping di entrambi i parametri in base alla relativa posizione ordinale nell'elenco di parametri.  
  
-   Per il tipo di connessione [!INCLUDE[vstecado](../includes/vstecado-md.md)] vengono usati i nomi di parametro \@parmMinProductID e \@parmMaxProductID.  
  
##  <a name="Stored_procedures"></a> Utilizzo di parametri con Stored procedure  
 Anche i comandi SQL che eseguono stored procedure possono utilizzare il mapping dei parametri. Come avviene per le regole delle query con parametri, anche le regole che determinano la modalità di utilizzo di marcatori di parametro e nomi di parametro dipendono dal tipo di gestione connessione utilizzato dall'attività Esegui SQL.  
  
 Nella tabella seguente sono elencati esempi di comandi EXEC per tipo di gestione connessione. Gli esempi eseguono la stored procedure **uspGetBillOfMaterials** nel database [!INCLUDE[ssSampleDBUserInputNonLocal](../includes/sssampledbuserinputnonlocal-md.md)]. Tale stored procedure utilizza i parametri di `input` `@StartProductID` e `@CheckDate`.  
  
|Tipo di connessione|Sintassi dell'istruzione EXEC|  
|---------------------|-----------------|  
|EXCEL e OLEDB|`EXEC uspGetBillOfMaterials ?, ?`|  
|ODBC|`{call uspGetBillOfMaterials(?, ?)}`<br /><br /> Per altre informazioni sulla sintassi ODBC, vedere l'argomento [Procedure Parameters](https://go.microsoft.com/fwlink/?LinkId=89462) (Parametri di procedura) nella guida di riferimento per programmatori ODBC in MSDN Library.|  
|ADO|Se IsQueryStoredProcedure è impostato su `False`, `EXEC uspGetBillOfMaterials ?, ?`<br /><br /> Se IsQueryStoredProcedure è impostato su `True`, `uspGetBillOfMaterials`|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|Se IsQueryStoredProcedure è impostato su `False`, `EXEC uspGetBillOfMaterials @StartProductID, @CheckDate`<br /><br /> Se IsQueryStoredProcedure è impostato su `True`, `uspGetBillOfMaterials`|  
  
 La sintassi per l'utilizzo dei parametri di output richiede che dopo ogni marcatore di parametro venga specificata la parola chiave OUTPUT. Ad esempio, la sintassi del parametro di output seguente è corretta: `EXEC myStoredProcedure ? OUTPUT`.  
  
 Per altre informazioni sull'utilizzo di parametri di input e di output con le stored procedure Transact-SQL, vedere [EXECUTE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/execute-transact-sql).  
  
##  <a name="Return_codes"></a> Recupero dei valori dei codici restituiti  
 Una stored procedure può restituire un valore intero, denominato codice restituito, per indicare lo stato di esecuzione di una procedura. Per implementare codici restituiti nell'attività Esegui SQL, è necessario utilizzare parametri di tipo `ReturnValue`.  
  
 Nella tabella seguente sono elencati, per tipo di gestione connessione, esempi di comandi EXEC che implementano codici restituiti. In tutti gli esempi viene utilizzato un parametro di `input`. Le regole per l'uso di marcatori di parametro e i nomi dei parametri sono gli stessi per tutti i tipi di parametro -`Input`, `Output`, e `ReturnValue`.  
  
 In alcune sintassi non è supportato l'utilizzo di valori letterali come parametri. In tali casi è necessario specificare il valore del parametro utilizzando una variabile.  
  
|Tipo di connessione|Sintassi dell'istruzione EXEC|  
|---------------------|-----------------|  
|EXCEL e OLEDB|`EXEC ? = myStoredProcedure 1`|  
|ODBC|`{? = call myStoredProcedure(1)}`<br /><br /> Per altre informazioni sulla sintassi ODBC, vedere l'argomento [Procedure Parameters](https://go.microsoft.com/fwlink/?LinkId=89462) (Parametri di procedura) nella guida di riferimento per programmatori ODBC in MSDN Library.|  
|ADO|Se IsQueryStoreProcedure è impostato su `False`, `EXEC ? = myStoredProcedure 1`<br /><br /> Se IsQueryStoreProcedure è impostato su `True`, `myStoredProcedure`|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|Set IsQueryStoreProcedure è impostato su `True`.<br /><br /> `myStoredProcedure`|  
  
 Nella sintassi illustrata nella tabella precedente, l'attività Esegui SQL usa il tipo di origine **Input diretto** per eseguire la stored procedure. L'attività Esegui SQL può usare anche il tipo di origine **Connessione file** per eseguire una stored procedure. Indipendentemente dal fatto che l'attività Esegui SQL utilizzi il **Input diretto** oppure **connessione File** tipo di origine, utilizzare un parametro del `ReturnValue` tipo per implementare il codice restituito. Per altre informazioni sulla configurazione del tipo di origine dell'istruzione SQL eseguita dall'attività Esegui SQL, vedere [Editor attività Esegui SQL &#40;pagina Generale&#41;](general-page-of-integration-services-designers-options.md).  
  
 Per altre informazioni sull'utilizzo di codici restituiti con le stored procedure Transact-SQL, vedere [RETURN &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/return-transact-sql).  
  
##  <a name="Configure_parameters_and_return_codes"></a> Configurazione dei parametri e codici restituiti nell'attività Esegui SQL  
 Per altre informazioni sulle proprietà dei parametri e dei codici restituiti che è possibile impostare in Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Editor attività Esegui SQL &#40;pagina Mapping parametri&#41;](../../2014/integration-services/execute-sql-task-editor-parameter-mapping-page.md)  
  
 Per altre informazioni sull'impostazione di queste proprietà in Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Impostazione delle proprietà di un'attività o di un contenitore](../../2014/integration-services/set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-tasks"></a>Attività correlate  
 [Impostazione delle proprietà di un'attività o di un contenitore](../../2014/integration-services/set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-content"></a>Contenuto correlato  
  
-   Intervento nel blog relativo alle [stored procedure con parametri di output](https://go.microsoft.com/fwlink/?LinkId=157786) nel sito Web all'indirizzo blogs.msdn.com  
  
-   Esempio CodePlex sull' [esecuzione di parametri SQL e set di risultati](https://go.microsoft.com/fwlink/?LinkId=157863)sul sito Web msftisprodsamples.codeplex.com  
  
## <a name="see-also"></a>Vedere anche  
 [Attività Esegui SQL](control-flow/execute-sql-task.md)   
 [Set di risultati nell'attività Esegui SQL](../../2014/integration-services/result-sets-in-the-execute-sql-task.md)  
  
  
