---
title: 'Lezione 1: Conversione di una tabella in una struttura gerarchica | Microsoft Docs'
ms.custom: ''
ms.date: 08/22/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- HierarchyID
ms.assetid: 5ee6f19a-6dd7-4730-a91c-bbed1bd77e0b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 14b490c48cf60c01efa1a0c3fed38b4aabb10495
ms.sourcegitcommit: aeb2273d779930e76b3e907ec03397eab0866494
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716285"
---
# <a name="lesson-1-converting-a-table-to-a-hierarchical-structure"></a>Lezione 1: Conversione di una tabella in una struttura gerarchica
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
I clienti che hanno tabelle che utilizzano un self-join per esprimere relazioni gerarchiche possono convertire le tabelle in una struttura gerarchica utilizzando questa lezione come guida. È relativamente facile eseguire la migrazione da questa rappresentazione a **hierarchyid**. Dopo la migrazione, gli utenti avranno una rappresentazione gerarchica compatta e facile da capire che può essere indicizzata in molti modi per eseguire query efficienti.  
  
In questa lezione, verrà esaminata una tabella esistente, verrà creata una nuova tabella contenente una colonna **hierarchyid** , verrà popolata la tabella con i dati della tabella di origine e infine verranno illustrate tre strategie di indicizzazione. In questa lezione sono inclusi gli argomenti seguenti:  
 
  
## <a name="prerequisites"></a>Prerequisites  
Per completare questa esercitazione, sono necessari SQL Server Management Studio, l'accesso a un server che esegue SQL Server e un database AdventureWorks.

- Installare [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
- Installare [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
- Scaricare i [database di esempio AdventureWorks2017](https://docs.microsoft.com/sql/samples/adventureworks-install-configure).

Le istruzioni per il ripristino dei database in SSMS sono disponibili in [Ripristinare un database](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms).  

## <a name="examine-the-current-structure-of-the-employee-table"></a>Esaminare la struttura corrente della tabella Employee
Il database di esempio Adventureworks2017 (o versione successiva) contiene una tabella **Employee** nello schema **HumanResources**. Per evitare di modificare la tabella originale, in questo passaggio viene creata una copia della tabella **Employee** denominata **EmployeeDemo**. Per semplificare l'esempio, copiare solo cinque colonne della tabella originale. Eseguire quindi una query sulla tabella **HumanResources.EmployeeDemo** per esaminare il modo in cui viene strutturata una tabella senza usare il tipo di dati **hierarchyid** .  
  
### <a name="copy-the-employee-table"></a>Copiare la tabella Employee  
  
1.  In una finestra editor di query, eseguire il codice seguente per copiare la struttura della tabella e i dati della tabella **Employee** in una tabella nuova denominata **EmployeeDemo**. Poiché la tabella originale usa già hierarchyid, questa query essenzialmente rende flat la gerarchia per recuperare il manager del dipendente. Nelle parti successive di questa lezione questa gerarchia verrà ricostruita.

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]


   ```sql  
   USE AdventureWorks2017;  
   GO  
     if OBJECT_ID('HumanResources.EmployeeDemo') is not null
    drop table HumanResources.EmployeeDemo 

    SELECT emp.BusinessEntityID AS EmployeeID, emp.LoginID, 
     (SELECT  man.BusinessEntityID FROM HumanResources.Employee man 
        WHERE emp.OrganizationNode.GetAncestor(1)=man.OrganizationNode OR 
            (emp.OrganizationNode.GetAncestor(1) = 0x AND man.OrganizationNode IS NULL)) AS ManagerID,
          emp.JobTitle, emp.HireDate
   INTO HumanResources.EmployeeDemo   
   FROM HumanResources.Employee emp ;
   GO
   ```  
  
### <a name="examine-the-structure-and-data-of-the-employeedemo-table"></a>Esaminare la struttura e i dati della tabella EmployeeDemo  
  
-   Questa nuova tabella **EmployeeDemo** rappresenta una tabella tipica di un database esistente di cui si può eseguire la migrazione a una struttura nuova. In una finestra editor di query, eseguire il codice seguente per visualizzare il modo in cui la tabella utilizza un self-join per visualizzare le relazioni dipendente/responsabile:  
  
    ```sql  
    SELECT   
        Mgr.EmployeeID AS MgrID, Mgr.LoginID AS Manager,   
        Emp.EmployeeID AS E_ID, Emp.LoginID, Emp.JobTitle  
    FROM HumanResources.EmployeeDemo AS Emp  
    LEFT JOIN HumanResources.EmployeeDemo AS Mgr  
    ON Emp.ManagerID = Mgr.EmployeeID  
    ORDER BY MgrID, E_ID  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```  
    MgrID Manager                 E_ID LoginID                  JobTitle  
    NULL    NULL                    1   adventure-works\ken0        Chief Executive Officer
    1   adventure-works\ken0        2   adventure-works\terri0      Vice President of Engineering
    1   adventure-works\ken0       16   adventure-works\david0    Marketing Manager
    1   adventure-works\ken0       25   adventure-works\james1    Vice President of Production
    1   adventure-works\ken0      234   adventure-works\laura1    Chief Financial Officer
    1   adventure-works\ken0    263 adventure-works\jean0       Information Services Manager
    1   adventure-works\ken0      273   adventure-works\brian3    Vice President of Sales
    2   adventure-works\terri0    3 adventure-works\roberto0    Engineering Manager
    3   adventure-works\roberto0    4   adventure-works\rob0        Senior Tool Designer
    ...  
    ```  
  
    Viene generato un totale di 290 righe di risultati.  
  
Con la clausola **ORDER BY** , i report diretti di ogni livello di gestione vengono elencati insieme nell'output. Ad esempio, tutti i sette dipendenti diretti di **MgrID** 1 (ken0) vengono elencati uno accanto all'altro. Anche se non impossibile, è molto più difficile raggruppare tutti coloro che in ultima istanza sono dipendenti di **MgrID** 1.  


## <a name="populate-a-table-with-existing-hierarchical-data"></a>Popolare una tabella con dati gerarchici esistenti
Questa attività consente di creare una nuova tabella e popolarla con i dati della tabella **EmployeeDemo** . Questa attività prevede i passaggi seguenti:  
  
-   Creare una tabella nuova contenente una colonna **hierarchyid** . Questa colonna può sostituire le colonne **EmployeeID** e **ManagerID** esistenti. Tuttavia, tali colonne verranno mantenute. Questo avviene perché le applicazioni esistenti potrebbero riferirsi a tali colonne e potrebbero aiutare a capire i dati dopo il trasferimento. La definizione della tabella specifica che **OrgNode** è la chiave primaria che richiede alla colonna di contenere i valori univoci. L'indice cluster della colonna **OrgNode** archivierà la data nella sequenza **OrgNode** .    
-   Creare una tabella temporanea utilizzata per rilevare il numero di dipendenti che riportano direttamente a ogni responsabile. 
-   Popolare la nuova tabella usando i dati dalla tabella **EmployeeDemo** .  
  
### <a name="to-create-a-new-table-named-neworg"></a>Per creare una nuova tabella denominata NewOrg  
  
-   In una finestra dell'editor di query eseguire il codice seguente per creare una nuova tabella denominata **HumanResources.NewOrg**:  
  
    ```sql   
    CREATE TABLE HumanResources.NewOrg  
    (  
      OrgNode hierarchyid,  
      EmployeeID int,  
      LoginID nvarchar(50),  
      ManagerID int  
    CONSTRAINT PK_NewOrg_OrgNode  
      PRIMARY KEY CLUSTERED (OrgNode)  
    );  
    GO  
    ```  
  
### <a name="create-a-temporary-table-named-children"></a>Creare una tabella temporanea denominata #Children  
  
1.  Creare una tabella temporanea denominata **#Children** con una colonna denominata **Num** che conterrà il numero di elementi figlio per ogni nodo:  
  
    ```sql  
    CREATE TABLE #Children   
       (  
        EmployeeID int,  
        ManagerID int,  
        Num int  
    );  
    GO  
    ```  
  
2.  Aggiungere un indice per accelerare significativamente la query che popola la tabella **NewOrg** :  
  
    ```sql  
    CREATE CLUSTERED INDEX tmpind ON #Children(ManagerID, EmployeeID);  
    GO  
    ```  
  
### <a name="populate-the-neworg-table"></a>Popolare la tabella NewOrg  
  
1.  Le query ricorsive impediscono le sottoquery con aggregazioni. In alternativa, popolare la tabella **#Children** con il codice seguente che usa il metodo [ROW_NUMBER()](../../t-sql/functions/row-number-transact-sql.md) per popolare la colonna **Num** :  
  
    ```sql 
    INSERT #Children (EmployeeID, ManagerID, Num)  
    SELECT EmployeeID, ManagerID,  
      ROW_NUMBER() OVER (PARTITION BY ManagerID ORDER BY ManagerID)   
    FROM HumanResources.EmployeeDemo  
    GO 
    ```  
  
2.  Rivedere la tabella **#Children** . Si noti in che modo la colonna **Num** contiene i numeri sequenziali per ogni responsabile.  
  
    ```sql  
    SELECT * FROM #Children ORDER BY ManagerID, Num  
    GO  
  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

    ```
    EmployeeID  ManagerID   Num
    1   NULL    1
    2        1    1
    16     1      2
    25     1      3
    234    1      4
    263    1      5
    273    1      6
    3        2    1
    4        3    1
    5        3    2
    6        3    3
    7        3    4
    ```


3.  Popolare la tabella **NewOrg** . Usare i metodi GetRoot e ToString per concatenare i valori **Num** nel formato **hierarchyid** , quindi aggiornare la colonna **OrgNode** con i valori di gerarchia risultanti:  
  
    ```sql  
    WITH paths(path, EmployeeID)   
    AS (  
    -- This section provides the value for the root of the hierarchy  
    SELECT hierarchyid::GetRoot() AS OrgNode, EmployeeID   
    FROM #Children AS C   
    WHERE ManagerID IS NULL   

    UNION ALL   
    -- This section provides values for all nodes except the root  
    SELECT   
    CAST(p.path.ToString() + CAST(C.Num AS varchar(30)) + '/' AS hierarchyid),   
    C.EmployeeID  
    FROM #Children AS C   
    JOIN paths AS p   
       ON C.ManagerID = P.EmployeeID   
    )  
    INSERT HumanResources.NewOrg (OrgNode, O.EmployeeID, O.LoginID, O.ManagerID)  
    SELECT P.path, O.EmployeeID, O.LoginID, O.ManagerID  
    FROM HumanResources.EmployeeDemo AS O   
    JOIN Paths AS P   
       ON O.EmployeeID = P.EmployeeID  
    GO 
    ```  
  
4.  Una colonna **hierarchyid** risulta più comprensibile quando viene convertita in un formato carattere. Rivedere i dati nella tabella **NewOrg** eseguendo il codice seguente che contiene due rappresentazioni della colonna **OrgNode** :  
  
    ```sql  
    SELECT OrgNode.ToString() AS LogicalNode, *   
    FROM HumanResources.NewOrg   
    ORDER BY LogicalNode;  
    GO  
    ```  
  
    La colonna **LogicalNode** converte la colonna **hierarchyid** in un formato di testo più leggibile che rappresenta la gerarchia. Nelle attività rimanenti, verrà usato il metodo `ToString()` per mostrare il formato logico delle colonne **hierarchyid** .  
  
5.  Eliminare la tabella temporanea che non risulta più essere necessaria:  
  
    ```sql  
    DROP TABLE #Children  
    GO  
    ```  
  
## <a name="optimizing-the-neworg-table"></a>Ottimizzazione della tabella NewOrg
La tabella **NewOrd** creata nell'attività [Popolamento di una tabella con dati gerarchici esistenti](../../relational-databases/tables/lesson-1-2-populating-a-table-with-existing-hierarchical-data.md) contiene tutte le informazioni sul personale e rappresenta la struttura gerarchica usando un tipo di dati **hierarchyid**. Questa attività aggiunge indici nuovi per supportare ricerche nella colonna **hierarchyid** .  
  

La colonna **hierarchyid** (**OrgNode**) è la chiave primaria della tabella **NewOrg** . Quando la tabella è stata creata, conteneva un indice cluster denominato **PK_NewOrg_OrgNode** per applicare l'univocità della colonna **OrgNode** . Questo indice cluster supporta anche una ricerca in profondità nella tabella.  
  
  
### <a name="create-index-on-neworg-table-for-efficient-searches"></a>Indicizzare la tabella NewOrg per eseguire ricerche efficienti  
  
1.  Per facilitare le query allo stesso livello nella gerarchia, usare il metodo [GetLevel](../../t-sql/data-types/getlevel-database-engine.md) per creare una colonna calcolata contenente il livello della gerarchia. Quindi, creare un indice composto nel livello e **Hierarchyid**. Eseguire il codice seguente per creare la colonna calcolata e l'indice breadth-first:  
  
    ```sql  
    ALTER TABLE HumanResources.NewOrg   
       ADD H_Level AS OrgNode.GetLevel() ;  
    CREATE UNIQUE INDEX EmpBFInd   
       ON HumanResources.NewOrg(H_Level, OrgNode) ;  
    GO  
    ```  
  
2.  Creare un indice univoco nella colonna **EmployeeID** . Si tratta della ricerca singleton tradizionale di un solo dipendente in base al numero **EmployeeID** . Eseguire il codice seguente per creare un indice in **EmployeeID**:  
  
    ```sql  
    CREATE UNIQUE INDEX EmpIDs_unq ON HumanResources.NewOrg(EmployeeID) ;  
    GO
    ```  
  
3.  Eseguire il codice seguente per recuperare i dati dalla tabella nell'ordine di ognuno dei tre indici:  
  
    ```sql  
    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID  
    FROM HumanResources.NewOrg   
    ORDER BY OrgNode;  

    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID   
    FROM HumanResources.NewOrg   
    ORDER BY H_Level, OrgNode;  

    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID   
    FROM HumanResources.NewOrg   
    ORDER BY EmployeeID;  
    GO  
    ```  
  
4.  Confrontare i set di risultati per visualizzare il modo in cui l'ordine viene archiviato in ogni tipo di indice. Seguono solo le prime quattro righe di ogni output.  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    Indice depth-first: i record relativi ai dipendenti vengono archiviati accanto al responsabile.  

    ```
    LogicalNode OrgNode H_Level EmployeeID  LoginID
    /   0x  0   1   adventure-works\ken0
    /1/ 0x58    1   2   adventure-works\terri0
    /1/1/   0x5AC0  2   3   adventure-works\roberto0
    /1/1/1/ 0x5AD6  3   4   adventure-works\rob0
    /1/1/2/ 0x5ADA  3   5   adventure-works\gail0
    /1/1/3/ 0x5ADE  3   6   adventure-works\jossef0
    /1/1/4/ 0x5AE1  3   7   adventure-works\dylan0
    /1/1/4/1/   0x5AE158    4   8   adventure-works\diane1
    /1/1/4/2/   0x5AE168    4   9   adventure-works\gigi0
    /1/1/4/3/   0x5AE178    4   10  adventure-works\michael6
    /1/1/5/ 0x5AE3  3   11  adventure-works\ovidiu0
    ```

    **Indice EmployeeID**-first: le righe vengono archiviate nella sequenza di **EmployeeID**.  

    ```
    LogicalNode OrgNode H_Level EmployeeID  LoginID
    /   0x  0   1   adventure-works\ken0
    /1/ 0x58    1   2   adventure-works\terri0
    /1/1/   0x5AC0  2   3   adventure-works\roberto0
    /1/1/1/ 0x5AD6  3   4   adventure-works\rob0
    /1/1/2/ 0x5ADA  3   5   adventure-works\gail0
    /1/1/3/ 0x5ADE  3   6   adventure-works\jossef0
    /1/1/4/ 0x5AE1  3   7   adventure-works\dylan0
    /1/1/4/1/   0x5AE158    4   8   adventure-works\diane1
    /1/1/4/2/   0x5AE168    4   9   adventure-works\gigi0
    /1/1/4/3/   0x5AE178    4   10  adventure-works\michael6
    /1/1/5/ 0x5AE3  3   11  adventure-works\ovidiu0
    /1/1/5/1/   0x5AE358    4   12  adventure-works\thierry0
    ```
  
> [!NOTE]  
> Per i diagrammi che indicano la differenza tra un indice depth-first e un indice breadth-first, vedere [Dati gerarchici &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md).  
  
### <a name="drop-the-unnecessary-columns"></a>Eliminare le colonne non necessarie  
  
1.  La colonna **ManagerID** rappresenta la relazione dipendente/responsabile che ora è rappresentata dalla colonna **OrgNode** . Se le altre applicazioni non richiedono la colonna **ManagerID** , si consiglia di eliminarla usando l'istruzione seguente:  
  
    ```sql  
    ALTER TABLE HumanResources.NewOrg DROP COLUMN ManagerID ;  
    GO  
    ```  
  
2.  La colonna **EmployeeID** è anche ridondante. La colonna **OrgNode** identifica in modo univoco ogni dipendente. Se le altre applicazioni non richiedono la colonna **EmployeeID** , eliminare l'indice e successivamente la colonna usando il codice seguente:  
  
    ```sql  
    DROP INDEX EmpIDs_unq ON HumanResources.NewOrg ;  
    ALTER TABLE HumanResources.NewOrg DROP COLUMN EmployeeID ;  
    GO  
    ```  
  
### <a name="replace-the-original-table-with-the-new-table"></a>Sostituire la tabella originale con la tabella nuova  
  
1.  Se la tabella originale contiene vincoli o indici aggiuntivi, aggiungerli alla tabella **NewOrg** .  
  
2.  Sostituire la vecchia colonna **EmployeeDemo** con la nuova tabella. Eseguire il codice seguente per rilasciare la vecchia tabella e successivamente rinominare la tabella nuova con il nome vecchio:  
  
    ```sql  
    DROP TABLE HumanResources.EmployeeDemo ;  
    GO  
    sp_rename 'HumanResources.NewOrg', 'EmployeeDemo' ;  
    GO  
    ```  
  
3.  Eseguire il codice seguente per esaminare la tabella finale:  
  
    ```sql  
    SELECT * FROM HumanResources.EmployeeDemo ;  
    ```  
  
## <a name="next-steps"></a>Passaggi successivi
L'articolo successivo illustra come creare e gestire i dati in una tabella gerarchica. 

Per altre informazioni, vedere l'articolo successivo:
> [!div class="nextstepaction"]
> [Passaggi successivi](lesson-2-creating-and-managing-data-in-a-hierarchical-table.md)
