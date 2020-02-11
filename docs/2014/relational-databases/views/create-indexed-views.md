---
title: Creare viste indicizzate | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- indexed views [SQL Server], creating
- clustered indexes, views
- CREATE INDEX statement
- large_value_types_out_of_row option
- indexed views [SQL Server]
- views [SQL Server], indexed views
ms.assetid: f86dd29f-52dd-44a9-91ac-1eb305c1ca8d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2159178c2fd26aca54d099f7345dbb62039ee34e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68196433"
---
# <a name="create-indexed-views"></a>Creazione di viste indicizzate
  In questo argomento si illustra come creare una vista indicizzata in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[tsql](../../includes/tsql-md.md)]. Il primo indice creato per una vista deve essere un indice cluster univoco. Dopo aver creato l'indice cluster univoco, è possibile creare più indici non cluster. La creazione di un indice cluster univoco per una vista consente un miglioramento delle prestazioni delle query, in quanto la vista viene archiviata nel database in modo analogo a una tabella con un indice cluster. Le viste indicizzate possono essere usate da Query Optimizer per velocizzare l'esecuzione delle query. Non è necessario fare riferimento alla vista nella query affinché venga usata da Query Optimizer per una sostituzione.  
  
  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
 Per la creazione e la corretta implementazione di una vista indicizzata, è fondamentale effettuare le operazioni seguenti:  
  
1.  Verificare che le opzioni SET siano corrette per tutte le tabelle esistenti a cui verrà fatto riferimento nella vista.  
  
2.  Verificare che le opzioni SET della sessione siano impostate in modo corretto prima di creare qualsiasi tabella e la vista.  
  
3.  Verificare che la definizione della vista sia deterministica.  
  
4.  Creare la vista con l'opzione WITH SCHEMABINDING.  
  
5.  Creare l'indice cluster univoco per la vista.  
  
###  <a name="Restrictions"></a>Opzioni SET necessarie per le viste indicizzate  
 La valutazione di una stessa espressione può produrre risultati diversi nel [!INCLUDE[ssDE](../../includes/ssde-md.md)] se sono attive diverse opzioni SET quando la query viene eseguita. Ad esempio, se l'opzione SET CONCAT_NULL_YIELDS_NULL è impostata su ON, l'espressione **'** abc **'** + NULL restituisce il valore NULL. Se tuttavia l'opzione CONCAT_NULL_YIEDS_NULL è impostata su OFF, la stessa espressione restituisce **'** abc **'**.  
  
 Per essere certi che le viste possano essere gestite in modo corretto e restituiscano risultati coerenti, è necessario usare valori fissi per varie opzioni SET delle viste indicizzate. Le opzioni SET nella tabella seguente devono essere impostate sui valori indicati nella colonna **RequiredValue** ogni volta che si verificano le condizioni seguenti:  
  
-   Vengono creati la vista e gli indici successivi nella vista.  
  
-   Le tabelle di base a cui viene fatto riferimento nella vista quando viene creata la tabella.  
  
-   Quando viene eseguita un'operazione di inserimento, aggiornamento o eliminazione su una qualsiasi tabella usata nella vista indicizzata, incluse operazioni quali la copia bulk, la replica e le query distribuite.  
  
-   Quando la vista indicizzata viene usata in Query Optimizer per generare il piano di query.  
  
    |Opzioni SET|Valore richiesto|Valore server predefinito|Predefinito<br /><br /> OLE DB e ODBC predefinito|Predefinito<br /><br /> DB-Library predefinito|  
    |-----------------|--------------------|--------------------------|---------------------------------------|-----------------------------------|  
    |ANSI_NULLS|ATTIVA|ATTIVA|ATTIVA|OFF|  
    |ANSI_PADDING|ATTIVA|ATTIVA|ATTIVA|OFF|  
    |ANSI_WARNINGS*|ATTIVA|ATTIVA|ATTIVA|OFF|  
    |ARITHABORT|ATTIVA|ATTIVA|OFF|OFF|  
    |CONCAT_NULL_YIELDS_NULL|ATTIVA|ATTIVA|ATTIVA|OFF|  
    |NUMERIC_ROUNDABORT|OFF|OFF|OFF|OFF|  
    |QUOTED_IDENTIFIER|ATTIVA|ATTIVA|ATTIVA|OFF|  
  
     *L'impostazione di ANSI_WARNINGS su ON comporta l'impostazione implicita di ARITHABORT su ON.  
  
 Se si usano una connessione server OLE DB o ODBC, l'unico valore da modificare è l'impostazione ARITHABORT. Tutti i valori DB-Library devono essere impostati in modo corretto a livello di server tramite **sp_configure** oppure dall'applicazione tramite il comando SET.  
  
> [!IMPORTANT]  
>  È consigliabile impostare l'opzione utente ARITHABORT su ON per l'intero server immediatamente dopo la creazione della prima vista indicizzata o del primo indice in una colonna calcolata in qualsiasi database del server.  
  
### <a name="deterministic-views"></a>Viste deterministiche  
 La definizione di una vista indicizzata deve essere deterministica. Una vista è deterministica se tutte le espressioni nell'elenco di selezione, nonché nelle clausole WHERE e GROUP BY sono deterministiche. Le espressioni deterministiche restituiscono sempre lo stesso risultato ogni volta che vengono valutate con un set specifico di valori di input. Nelle espressioni deterministiche è possibile usare solo funzioni deterministiche. La funzione DATEADD, ad esempio, è deterministica perché restituisce sempre lo stesso risultato per un dato set di valori dei relativi tre parametri. GETDATE non è deterministica perché viene sempre richiamata con lo stesso argomento, ma il valore restituito cambia ogni volta che viene eseguita.  
  
 Per determinare se una colonna della vista è deterministica, usare la proprietà **IsDeterministic** della funzione [COLUMNPROPERTY](/sql/t-sql/functions/columnproperty-transact-sql) . Usare la proprietà **IsPrecise** della funzione COLUMNPROPERTY per determinare se una colonna deterministica di una vista con associazione a schema è precisa. Tramite la funzione COLUMNPROPERTY viene restituito 1 se la proprietà è TRUE, 0 se la proprietà è FALSE e NULL se il valore di input non è valido. Questo significa che la colonna non è deterministica o non è precisa.  
  
 Se in un'espressione deterministica sono contenute espressioni float, il risultato esatto può dipendere dall'architettura del processore o dalla versione del microcodice. Per garantire l'integrità dei dati, le espressioni di questo tipo possono essere usate solo come colonne non chiave delle viste indicizzate. Le espressioni deterministiche che non contengono espressioni float sono definite precise. Solo le espressioni deterministiche precise possono essere usate in colonne chiave e clausole WHERE o GROUP BY di viste indicizzate.  
  
### <a name="additional-requirements"></a>Requisiti aggiuntivi  
 Oltre alle impostazioni delle opzioni SET e ai requisiti relativi alle funzioni deterministiche, è necessario che vengano soddisfatti i requisiti seguenti:  
  
-   L'utente che esegue CREATE INDEX deve essere il proprietario della vista.  
  
-   Quando si crea l'indice, l'opzione IGNORE_DUP_KEY deve essere impostata su OFF (impostazione predefinita).  
  
-   È necessario fare riferimento alle tabelle con nomi in due parti, _schema_**.** _TableName_ nella definizione della vista.  
  
-   Le funzioni definite dall'utente a cui viene fatto riferimento nella vista devono essere create usando l'opzione WITH SCHEMABINDING.  
  
-   È necessario fare riferimento a qualsiasi funzione definita dall'utente a cui viene fatto riferimento nella vista tramite nomi in due parti, _schema_**.** _funzione_.  
  
-   La proprietà di accesso ai dati di una funzione definita dall'utente deve essere NO SQL e la proprietà di accesso esterno deve essere NO.  
  
-   Le funzioni CLR (Common Language Runtime) possono essere incluse solo nell'elenco SELECT della vista ma non possono fare parte della definizione della chiave di indice cluster. Le funzioni CLR non possono essere incluse nella clausola WHERE della vista o nella clausola ON di un'operazione JOIN nella vista.  
  
-   Le proprietà delle funzioni CLR e dei metodi di tipi CLR definiti dall'utente usati nella definizione della vista devono essere impostate come illustrato nella tabella seguente.  
  
    |Proprietà|Nota|  
    |--------------|----------|  
    |DETERMINISTIC = TRUE|Deve essere dichiarata in modo esplicito come attributo del metodo di Microsoft .NET Framework.|  
    |PRECISE = TRUE|Deve essere dichiarata in modo esplicito come attributo del metodo di .NET Framework.|  
    |DATA ACCESS = NO SQL|Determinata dall'impostazione dell'attributo DataAccess su DataAccessKind.None e dell'attributo SystemDataAccess su SystemDataAccessKind.None.|  
    |EXTERNAL ACCESS = NO|Per le routine CLR il valore predefinito di questa proprietà è NO.|  
  
-   La vista deve essere creata tramite l'opzione WITH SCHEMABINDING.  
  
-   La vista deve contenere riferimenti solo a tabelle di base che si trovano nello stesso database della vista. La vista non può fare riferimento ad altre viste.  
  
-   Nell'istruzione SELECT della definizione della vista non possono essere contenuti gli elementi Transact-SQL seguenti:  
  
    ||||  
    |-|-|-|  
    |COUNT|Funzioni ROWSET (OPENDATASOURCE, OPENQUERY, OPENROWSET E OPENXML)|OUTER join (LEFT, RIGHT o FULL)|  
    |Tabella derivata (definita specificando un'istruzione SELECT nella clausola FROM)|Self-join|Specifica delle colonne tramite SELECT \* o SELECT *nome_tabella*.*|  
    |DISTINCT|STDEV, STDEVP, VAR, VARP o AVG|Espressione di tabella comune (CTE)|  
    |`float`\*colonne `text`, `ntext`, `image`, `XML`, o `filestream`|Sottoquery|La clausola OVER, che include funzioni di rango o funzioni finestra di aggregazione|  
    |Predicati full-text (CONTAIN, FREETEXT)|Funzione SUM che fa riferimento a un'espressione che ammette i valori Null|ORDER BY|  
    |Funzione di aggregazione CLR definita dall'utente|Torna all'inizio|Operatori CUBE, ROLLUP o GROUPING SETS|  
    |MIN, MAX|Operatori UNION, EXCEPT o INTERSECT|TABLESAMPLE|  
    |Variabili di tabella|OUTER APPLY o CROSS APPLY|PIVOT, UNPIVOT|  
    |Set di colonne di tipo sparse|Funzioni inline o a più istruzioni con valori di tabella|OFFSET|  
    |CHECKSUM_AGG|||  
  
     \*La vista indicizzata può contenere `float` colonne; tali colonne, tuttavia, non possono essere incluse nella chiave di indice cluster.  
  
-   Se è presente la clausola GROUP BY, la definizione di VIEW deve contenere COUNT_BIG(*) e non deve contenere HAVING. Queste restrizioni relative alla clausola GROUP BY vengono applicate solo alla definizione della vista indicizzata. Una query può usare una vista indicizzata nel relativo piano di esecuzione anche se non soddisfa tali restrizioni.  
  
-   Se la definizione della vista include una clausola GROUP BY, la chiave dell'indice cluster univoco può contenere riferimenti solo alle colonne specificate nella clausola GROUP BY.  
  
###  <a name="Recommendations"></a> Raccomandazioni  
 Quando si fa riferimento a valori letterali stringa `datetime` e `smalldatetime` nelle viste indicizzate, è consigliabile convertire in modo esplicito il valore letterale nel tipo di dati desiderato usando uno stile del formato di data deterministico. Per un elenco degli stili del formato di data deterministici, vedere [CAST e CONVERT &#40;Transact-SQL&#41;](/sql/t-sql/functions/cast-and-convert-transact-sql). Le espressioni che prevedono la conversione implicita di stringhe di caratteri nel tipo di dati `datetime` o `smalldatetime` sono considerate non deterministiche. Ciò è dovuto al fatto che i risultati dipendono dalle impostazioni LANGUAGE e DATEFORMAT della sessione del server. I risultati dell'espressione `CONVERT (datetime, '30 listopad 1996', 113)` dipendono ad esempio dall'impostazione LANGUAGE, in quanto la stringa '`listopad`' indica mesi diversi in diverse lingue. Analogamente, nell'espressione `DATEADD(mm,3,'2000-12-01')`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpreta la stringa `'2000-12-01'` sulla base dell'impostazione DATEFORMAT.  
  
 Anche la conversione implicita di dati di tipo carattere non Unicode tra regole di confronto viene considerata non deterministica  
  
###  <a name="Considerations"></a>Considerazioni  
 L'impostazione dell'opzione **large_value_types_out_of_row** delle colonne di una vista indicizzata è ereditata dall'impostazione della colonna corrispondente nella tabella di base. Questo valore viene impostato mediante [sp_tableoption](/sql/relational-databases/system-stored-procedures/sp-tableoption-transact-sql). L'impostazione predefinita per le colonne generate da espressioni è 0. Ciò significa che i tipi per valori di grandi dimensioni vengono archiviati all'interno delle righe.  
  
 È possibile creare viste indicizzate per una tabella partizionata, nonché partizionare questo tipo di viste.  
  
 Per impedire l'utilizzo di viste indicizzate nel [!INCLUDE[ssDE](../../includes/ssde-md.md)] , includere l'hint OPTION (EXPAND VIEWS) nella query. Inoltre, l'errata impostazione di una qualsiasi delle opzione elencate impedisce l'utilizzo degli indici delle viste in Query Optimizer. Per altre informazioni sull'hint OPTION (EXPAND VIEWS), vedere [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql).  
  
 Tutti gli indici di una vista vengono eliminati con la rimozione della vista. Tutti gli indici non cluster e tutte le statistiche create automaticamente nella vista vengono eliminati con l'eliminazione dell'indice cluster. Le statistiche create dall'utente nella vista vengono conservate. È possibile eliminare gli indici non cluster singolarmente. L'eliminazione dell'indice cluster nella vista determina la rimozione del set di risultati archiviato e la vista tornerà a essere elaborata come standard da Query Optimizer.  
  
 È possibile disabilitare gli indici di tabelle e viste. Quando l'indice cluster di una tabella è disabilitato, anche gli indici delle viste associate alla tabella sono disabilitati.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Sono richieste l'autorizzazione CREATE VIEW per il database e l'autorizzazione ALTER per lo schema in cui viene creata la vista.  
  
##  <a name="TsqlProcedure"></a> Con Transact-SQL  
  
#### <a name="to-create-an-indexed-view"></a>Per creare una vista indicizzata  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. Nell'esempio vengono creati una vista e un indice per tale vista, quindi vengono eseguite due query in cui viene usata la vista indicizzata.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    --Set the options to support indexed views.  
    SET NUMERIC_ROUNDABORT OFF;  
    SET ANSI_PADDING, ANSI_WARNINGS, CONCAT_NULL_YIELDS_NULL, ARITHABORT,  
        QUOTED_IDENTIFIER, ANSI_NULLS ON;  
    GO  
    --Create view with schemabinding.  
    IF OBJECT_ID ('Sales.vOrders', 'view') IS NOT NULL  
    DROP VIEW Sales.vOrders ;  
    GO  
    CREATE VIEW Sales.vOrders  
    WITH SCHEMABINDING  
    AS  
        SELECT SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Revenue,  
            OrderDate, ProductID, COUNT_BIG(*) AS COUNT  
        FROM Sales.SalesOrderDetail AS od, Sales.SalesOrderHeader AS o  
        WHERE od.SalesOrderID = o.SalesOrderID  
        GROUP BY OrderDate, ProductID;  
    GO  
    --Create an index on the view.  
    CREATE UNIQUE CLUSTERED INDEX IDX_V1   
        ON Sales.vOrders (OrderDate, ProductID);  
    GO  
    --This query can use the indexed view even though the view is   
    --not specified in the FROM clause.  
    SELECT SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Rev,   
        OrderDate, ProductID  
    FROM Sales.SalesOrderDetail AS od  
        JOIN Sales.SalesOrderHeader AS o ON od.SalesOrderID=o.SalesOrderID  
            AND ProductID BETWEEN 700 and 800  
            AND OrderDate >= CONVERT(datetime,'05/01/2002',101)  
    GROUP BY OrderDate, ProductID  
    ORDER BY Rev DESC;  
    GO  
    --This query can use the above indexed view.  
    SELECT  OrderDate, SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Rev  
    FROM Sales.SalesOrderDetail AS od  
        JOIN Sales.SalesOrderHeader AS o ON od.SalesOrderID=o.SalesOrderID  
            AND DATEPART(mm,OrderDate)= 3  
            AND DATEPART(yy,OrderDate) = 2002  
    GROUP BY OrderDate  
    ORDER BY OrderDate ASC;  
    GO  
    ```  
  
 Per altre informazioni, vedere [CREATE VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-view-transact-sql).  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [SET ANSI_NULLS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-nulls-transact-sql)   
 [SET ANSI_PADDING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-padding-transact-sql)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-warnings-transact-sql)   
 [IMPOSTARE ARITHABORT &#40;&#41;Transact-SQL](/sql/t-sql/statements/set-arithabort-transact-sql)   
 [IMPOSTA CONCAT_NULL_YIELDS_NULL &#40;&#41;Transact-SQL](/sql/t-sql/statements/set-concat-null-yields-null-transact-sql)   
 [IMPOSTA NUMERIC_ROUNDABORT &#40;&#41;Transact-SQL](/sql/t-sql/statements/set-numeric-roundabort-transact-sql)   
 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-quoted-identifier-transact-sql)  
  
  
