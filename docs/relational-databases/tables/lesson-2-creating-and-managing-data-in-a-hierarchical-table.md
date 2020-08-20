---
description: 'Lezione 2: Creazione e gestione di dati in una tabella gerarchica'
title: 'Lezione 2: Creazione e gestione di dati in una tabella gerarchica | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- HierarchyID
ms.assetid: 95f55cff-4abb-4c08-97b3-e3ae5e8b24e2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0a774ce3918388e8df23de43a01b8b0930f9336d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460226"
---
# <a name="lesson-2-create-and-manage-data-in-a-hierarchical-table"></a>Lezione 2: Creare e gestire dati in una tabella gerarchica
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
Nella Lezione 1 è stata modificata una tabella esistente per usare il tipo di dati **hierarchyid** ed è stata popolata la colonna **hierarchyid** con la rappresentazione dei dati esistenti. In questa lezione, verrà generata una nuova tabella e verranno inseriti i dati utilizzando i metodi gerarchici. Pertanto, verrà eseguita una query e verranno modificati i dati utilizzando i metodi gerarchici. 

## <a name="prerequisites"></a>Prerequisites  
Per completare questa esercitazione, sono necessari SQL Server Management Studio, l'accesso a un server che esegue SQL Server e un database AdventureWorks.

- Installare [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
- Installare [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
- Scaricare i [database di esempio AdventureWorks2017](https://docs.microsoft.com/sql/samples/adventureworks-install-configure).

Le istruzioni per il ripristino dei database in SSMS sono disponibili in [Ripristinare un database](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms).   
  
## <a name="create-a-table-using-the-hierarchyid-data-type"></a>Creare una tabella usando il tipo di dati hierarchyid
Nell'esempio seguente viene creata una tabella denominata EmployeeOrg che include i dati del dipendente e la gerarchia del report. L'esempio crea la tabella nel database AdventureWorks2017, ma questo è facoltativo. Per mantenere l'esempio semplice, in questa tabella sono incluse solo cinque colonne:  
  
-   OrgNode è una colonna **hierarchyid** che archivia la relazione gerarchica.   
-   OrgLevel è una colonna calcolata in base alla colonna OrgNode che archivia il livello di ciascun nodo nella gerarchia. Verrà utilizzata per un indice breadth-first.  
-   Il numero di identificazione tipico del dipendente, utilizzato per applicazioni quali libro paga, è contenuto in EmployeeID. Nello sviluppo di nuove applicazioni, le applicazioni possono utilizzare la colonna OrgNode mentre la colonna separata EmployeeID non è necessaria.   
-   EmpName contiene il nome del dipendente.    
-   Title contiene la posizione del dipendente.  

## <a name="create-the-employeeorg-table"></a>Creare la tabella EmployeeOrg  
  
1.  Nella finestra dell'editor di query eseguire il codice seguente per creare la tabella `EmployeeOrg` . Specificando la colonna `OrgNode` come chiave primaria con un indice cluster, verrà creato un indice depth-first:  
  
    ```sql  
    USE AdventureWorks2017 ;  
    GO  
    
    if OBJECT_ID('HumanResources.EmployeeOrg') is not null
     drop table HumanResources.EmployeeOrg 
         
    CREATE TABLE HumanResources.EmployeeOrg  
    (  
       OrgNode hierarchyid PRIMARY KEY CLUSTERED,  
       OrgLevel AS OrgNode.GetLevel(),  
       EmployeeID int UNIQUE NOT NULL,  
       EmpName varchar(20) NOT NULL,  
       Title varchar(20) NULL  
    ) ;  
    GO  
    ```  
  
2.  Eseguire il codice riportato di seguito per creare un indice composto per le colonne `OrgLevel` e `OrgNode` al fine di supportare ricerche breadth-first efficienti:  
  
    ```sql  
    CREATE UNIQUE INDEX EmployeeOrgNc1   
    ON HumanResources.EmployeeOrg(OrgLevel, OrgNode) ;  
    GO  
    ```  
  
La tabella è ora pronta per i dati. La prossima attività popolerà la tabella utilizzando metodi gerarchici.   

## <a name="populate-a-hierarchical-table-using-hierarchical-methods"></a>Popolare una tabella gerarchica usando metodi gerarchici
AdventureWorks2017 ha 8 dipendenti che lavorano nel reparto Marketing. La gerarchia dei dipendenti è simile alla seguente:  
  
**David**, **EmployeeID** 6 è il responsabile marketing. Tre marketing specialist fanno riferimento a **David**:  
  
-   **Sariya**, **EmployeeID** 46  
  
-   **John**, **EmployeeID** 271  
  
-   **Jill**, **EmployeeID** 119  
  
**Wanida** , Marketing Assistant (**EmployeeID** 269), fa riferimento a **Sariya**, mentre **Mary** Marketing Assistant (**EmployeeID** 272), fa riferimento a **John**.  
  
### <a name="insert-the-root-of-the-hierarchy-tree"></a>Inserire la radice dell'albero gerarchico  
  
1.  Nell'esempio seguente **David** , il responsabile marketing, è inserito nella tabella alla radice della gerarchia. La colonna **OrdLevel** è una colonna calcolata. Pertanto, non è parte dell'istruzione INSERT. Questo primo record usa il metodo [GetRoot()](../../t-sql/data-types/getroot-database-engine.md) per popolarsi come radice della gerarchia.  
  
    ```sql  
    INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
    VALUES (hierarchyid::GetRoot(), 6, 'David', 'Marketing Manager') ;  
    GO  
    ```  
  
2.  Eseguire il seguente codice per esaminare la riga iniziale della tabella:  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```sql  
    Text_OrgNode OrgNode OrgLevel EmployeeID EmpName Title  
    ------------ ------- -------- ---------- ------- -----------------  
    /            Ox      0        6          David   Marketing Manager  
    ```  
  
Come illustrato nella lezione precedente, si usa il metodo `ToString()` per convertire il tipo di dati **hierarchyid** in un formato più facilmente comprensibile.  
  
### <a name="insert-a-subordinate-employee"></a>Inserire un dipendente subordinato  
  
1.  **Sariya** fa riferimento a **David**. Per inserire il nodo di **Sariya** , è necessario creare un valore **OrgNode** appropriato del tipo di dati **hierarchyid**. Il codice seguente crea una variabile di tipo dati **hierarchyid** e la popola con il valore OrgNode radice della tabella. A questo punto usa la variabile con il metodo [GetDescendant()](../../t-sql/data-types/getdescendant-database-engine.md) per inserire la riga che è un nodo subordinato. `GetDescendant` accetta due argomenti. Rivedere le opzioni seguenti per i valori dell'argomento:  
  
    -   Se il padre è NULL, `GetDescendant` restituisce NULL.  
    -   Se il padre non è NULL e child1 e child2 sono NULL, `GetDescendant` restituisce un figlio del padre.  
    -   Se il padre e child1 non sono NULL e child2 è NULL, `GetDescendant` restituisce un figlio del padre maggiore di child1.   
    -   Se il padre e child2 non sono NULL e child1 è NULL, `GetDescendant` restituisce un figlio del padre minore di child2.   
    -   Se il padre, child1 e child2 non sono NULL, `GetDescendant` restituisce un figlio del padre maggiore di child1 e uno minore di child2.  
  
    Il codice seguente utilizza gli argomenti `(NULL, NULL)` dell'elemento padre radice perché nella tabella non esiste ancora alcuna riga, ad eccezione della radice. Eseguire il codice seguente per inserire **Sariya**:  
  
    ```sql  
    DECLARE @Manager hierarchyid   
    SELECT @Manager = hierarchyid::GetRoot()  
    FROM HumanResources.EmployeeOrg ;  
  
    INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
    VALUES  
    (@Manager.GetDescendant(NULL, NULL), 46, 'Sariya', 'Marketing Specialist') ;  
  
    ```  
  
2.  Ripetere la query dalla prima procedura per eseguire una query sulla tabella e verificare come appaiono le voci:  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```  
    Text_OrgNode OrgNode OrgLevel EmployeeID EmpName Title  
    ------------ ------- -------- ---------- ------- -----------------  
    /            Ox      0        6          David   Marketing Manager  
    /1/          0x58    1        46         Sariya  Marketing Specialist  
    ```  
  
### <a name="create-a-procedure-for-entering-new-nodes"></a>Creare una procedura per l'immissione di nuovi nodi  
  
1.  Per semplificare l'inserimento di dati, creare la stored procedure seguente per aggiungere dipendenti alla tabella **EmployeeOrg** . La procedura accetta valori di input sul dipendente aggiunto. Include il numero **EmployeeID** del responsabile del nuovo dipendente, il numero **EmployeeID** del nuovo dipendente, il nome e il titolo. La procedura usa `GetDescendant()` e anche il metodo [GetAncestor()](../../t-sql/data-types/getancestor-database-engine.md) . Eseguire il codice seguente per creare la procedura:  
  
    ```sql  
    CREATE PROC AddEmp(@mgrid int, @empid int, @e_name varchar(20), @title varchar(20))   
    AS   
    BEGIN  
       DECLARE @mOrgNode hierarchyid, @lc hierarchyid  
       SELECT @mOrgNode = OrgNode   
       FROM HumanResources.EmployeeOrg   
       WHERE EmployeeID = @mgrid  
       SET TRANSACTION ISOLATION LEVEL SERIALIZABLE  
       BEGIN TRANSACTION  
          SELECT @lc = max(OrgNode)   
          FROM HumanResources.EmployeeOrg   
          WHERE OrgNode.GetAncestor(1) =@mOrgNode ;  
  
          INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
          VALUES(@mOrgNode.GetDescendant(@lc, NULL), @empid, @e_name, @title)  
       COMMIT  
    END ;  
    GO  
    ```  
  
2.  Nell'esempio seguente vengono aggiunti i 4 dipendenti rimanenti che fanno riferimento direttamente o indirettamente a **David**.  
  
    ```sql  
    EXEC AddEmp 6, 271, 'John', 'Marketing Specialist' ;  
    EXEC AddEmp 6, 119, 'Jill', 'Marketing Specialist' ;  
    EXEC AddEmp 46, 269, 'Wanida', 'Marketing Assistant' ;  
    EXEC AddEmp 271, 272, 'Mary', 'Marketing Assistant' ;  
    ```  
  
3.  Eseguire nuovamente la query seguente per esaminare le righe della tabella **EmployeeOrg** :  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    GO  
    ```  
  
    [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```sql  
    Text_OrgNode OrgNode OrgLevel EmployeeID EmpName Title  
    ------------ ------- -------- ---------- ------- -----------------  
    /            Ox      0        6          David   Marketing Manager  
    /1/          0x58    1        46         Sariya  Marketing Specialist  
    /1/1/        0x5AC0  2        269        Wanida  Marketing Assistant  
    /2/          0x68    1        271        John    Marketing Specialist  
    /2/1/        0x6AC0  2        272        Mary    Marketing Assistant  
    /3/          0x78    1        119        Jill    Marketing Specialist  
    ```  
  
La tabella ora è popolata completamente con l'organizzazione Marketing.  

## <a name="query-a-hierarchical-table-using-hierarchy-methods"></a>Eseguire query su una tabella gerarchica usando metodi gerarchici
Ora che la tabella HumanResources.EmployeeOrg è completamente popolata, in questa attività verrà illustrato come eseguire una query sulla gerarchia utilizzando alcuni dei metodi gerarchici.  
  
### <a name="find-subordinate-nodes"></a>Trovare nodi subordinati  
  
1.  Sariya ha un dipendente subordinato. Per eseguire una query sui subalterni di Sariya, eseguire la query seguente che usa il metodo [IsDescendantOf](../../t-sql/data-types/isdescendantof-database-engine.md) :  
  
    ```sql  
    DECLARE @CurrentEmployee hierarchyid  
  
    SELECT @CurrentEmployee = OrgNode  
    FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 46 ;  
  
    SELECT *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.IsDescendantOf(@CurrentEmployee ) = 1 ;  
    ```  
  
    I risultati indicano sia Sariya sia Wanida. Sariya viene indicata perché rappresenta l'elemento discendente al livello 0. Wanida rappresenta l'elemento discendente al livello 1.  
  
2.  È anche possibile eseguire una query per ottenere tali informazioni usando il metodo [GetAncestor](../../t-sql/data-types/getancestor-database-engine.md) . `GetAncestor` accetta un argomento per il livello che si tenta di restituire. Poiché Wanida è un livello sotto Sariya, utilizzare `GetAncestor(1)` come dimostrato nel codice seguente:  
  
    ```sql  
    DECLARE @CurrentEmployee hierarchyid  
  
    SELECT @CurrentEmployee = OrgNode  
    FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 46 ;  
  
    SELECT OrgNode.ToString() AS Text_OrgNode, *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.GetAncestor(1) = @CurrentEmployee  
    ```  
  
    Questa volta nei risultati viene indicata solo Wanida.  
  
3.  Ora impostare `@CurrentEmployee` su David (EmployeeID 6) e il livello su 2. Eseguire quanto segue per restituire anche Wanida:  
  
    ```sql  
    DECLARE @CurrentEmployee hierarchyid  
  
    SELECT @CurrentEmployee = OrgNode  
    FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 6 ;  
  
    SELECT OrgNode.ToString() AS Text_OrgNode, *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.GetAncestor(2) = @CurrentEmployee  
    ```  
  
    Questa volta, due livelli più in basso, viene indicata anche Mary che riporta a David.  
  
## <a name="use-getroot-and-getlevel"></a>Usare GetRoot e GetLevel  
  
1.  Con il crescere della gerarchia diventa più difficile determinare la posizione dei membri nella stessa. Usare il metodo [GetLevel](../../t-sql/data-types/getlevel-database-engine.md) per scoprire quanti livelli ci sono al di sotto di ogni riga della gerarchia. Eseguire il codice seguente per visualizzare i livelli di tutte le righe:  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode.GetLevel() AS EmpLevel, *  
    FROM HumanResources.EmployeeOrg ;  
    GO  
  
    ```  
  
2.  Usare il metodo [GetRoot](../../t-sql/data-types/getroot-database-engine.md) per cercare il nodo radice della gerarchia. Il codice seguente restituisce la singola riga che è la radice:  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode, *  
    FROM HumanResources.EmployeeOrg  
    WHERE OrgNode = hierarchyid::GetRoot() ;  
    GO  
  
    ```  
   
  
## <a name="reorder-data-in-a-hierarchical-table-using-hierarchical-methods"></a>Riordinare dati in una tabella gerarchica usando metodi gerarchici
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
La riorganizzazione di una gerarchia è un'attività di manutenzione comune. In questa attività verrà usata un'istruzione UPDATE con il metodo [GetReparentedValue](../../t-sql/data-types/getreparentedvalue-database-engine.md) per spostare innanzitutto una singola riga in un percorso nuovo della gerarchia. Verrà quindi spostato un sottoalbero intero in un nuovo percorso.  
  
Il metodo `GetReparentedValue` utilizza due argomenti. Nel primo argomento viene descritta la parte della gerarchia da modificare. Ad esempio, se una gerarchia è **/1/4/2/3/** e si vuole modificare la sezione **/1/4/** , la gerarchia diventa **/2/1/2/3/**, lasciando gli ultimi due nodi (**2/3/**) inalterati, è necessario specificare i nodi modificati (**/1/4/**) come primo argomento. Il secondo argomento specifica il nuovo livello della gerarchia, nell'esempio **/2/1/**. Non è necessario che i due argomenti contengano lo stesso numero di livelli.  
  
### <a name="move-a-single-row-to-a-new-location-in-the-hierarchy"></a>Spostare una sola riga in un percorso nuovo nella gerarchia  
  
1.  Attualmente Wanida riporta a Sariya. In questa procedura, si sposta Wanida dal nodo corrente **/1/1/,** in modo che riporti a Jill. Il suo nodo nuovo diventerà **/3/1/** e **/1/** diventa il primo argomento, mentre **/3/** diventa il secondo argomento. Gli argomenti corrispondono ai valori **OrgNode** di Sariya e Jill. Eseguire il codice seguente per spostare Wanida dall'organizzazione di Sariya a quella di Jill:  
  
    ```sql  
    DECLARE @CurrentEmployee hierarchyid , @OldParent hierarchyid, @NewParent hierarchyid  
    SELECT @CurrentEmployee = OrgNode FROM HumanResources.EmployeeOrg  
      WHERE EmployeeID = 269 ;   
    SELECT @OldParent = OrgNode FROM HumanResources.EmployeeOrg  
      WHERE EmployeeID = 46 ;   
    SELECT @NewParent = OrgNode FROM HumanResources.EmployeeOrg  
      WHERE EmployeeID = 119 ;   
  
    UPDATE HumanResources.EmployeeOrg  
    SET OrgNode = @CurrentEmployee. GetReparentedValue(@OldParent, @NewParent)   
    WHERE OrgNode = @CurrentEmployee ;  
    GO  
    ```  
  
2.  Eseguire il codice seguente per visualizzare il risultato:  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    GO  
    ```  
  
    Wanida ora è al nodo **/3/1/**.  
  
### <a name="reorganize-a-section-of-a-hierarchy"></a>Riorganizzare una sezione di una gerarchia  
  
1.  Per dimostrare come spostare contemporaneamente un numero maggiore di persone, eseguire innanzitutto il codice seguente per aggiungere un report del tirocinante a Wanida:  
  
    ```sql  
    EXEC AddEmp 269, 291, 'Kevin', 'Marketing Intern'  ;  
    GO  
    ```  
  
2.  Ora Kevin riporta a Wanida che riporta a Jill che riporta a David. Questo significa che Kevin è al livello **/3/1/1/**. Per spostare tutti i subalterni di Jill a un nuovo responsabile, verranno aggiornati tutti i nodi che hanno **/3/** in **OrgNode** con un nuovo valore. Eseguire il codice seguente per aggiornare Wanida in modo che riporti a Sariya, ma lasciando che Kevin riporti a Wanida:  
  
    ```sql  
    DECLARE @OldParent hierarchyid, @NewParent hierarchyid  
    SELECT @OldParent = OrgNode FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 119 ; -- Jill  
    SELECT @NewParent = OrgNode FROM HumanResources.EmployeeOrg  
    WHERE EmployeeID = 46 ; -- Sariya  
    DECLARE children_cursor CURSOR FOR  
    SELECT OrgNode FROM HumanResources.EmployeeOrg  
    WHERE OrgNode.GetAncestor(1) = @OldParent;  
    DECLARE @ChildId hierarchyid;  
    OPEN children_cursor  
    FETCH NEXT FROM children_cursor INTO @ChildId;  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
    START:  
        DECLARE @NewId hierarchyid;  
        SELECT @NewId = @NewParent.GetDescendant(MAX(OrgNode), NULL)  
        FROM HumanResources.EmployeeOrg WHERE OrgNode.GetAncestor(1) = @NewParent;  
  
        UPDATE HumanResources.EmployeeOrg  
        SET OrgNode = OrgNode.GetReparentedValue(@ChildId, @NewId)  
        WHERE OrgNode.IsDescendantOf(@ChildId) = 1;  
        IF @@error <> 0 GOTO START -- On error, retry  
            FETCH NEXT FROM children_cursor INTO @ChildId;  
    END  
    CLOSE children_cursor;  
    DEALLOCATE children_cursor;  
  
    ```  
  
3.  Eseguire il codice seguente per visualizzare il risultato:  
  
    ```sql  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    GO  
    ```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Text_OrgNode OrgNode OrgLevel EmployeeID EmpName Title  
------------ ------- -------- ---------- ------- -----------------  
/            Ox      0        6          David   Marketing Manager  
/1/          0x58    1        46         Sariya  Marketing Specialist  
/1/1/        0x5AC0  2        269        Wanida  Marketing Assistant  
/1/1/1/      0x5AD0  3        291        Kevin   Marketing Intern  
/2/          0x68    1        271        John    Marketing Specialist  
/2/1/        0x6AC0  2        272        Mary    Marketing Assistant  
/3/          0x78    1        119        Jill    Marketing Specialist  
```  
  
L'intero albero organizzativo che riportava a Jill (Wanida e Kevin) ora riporta a Sariya.  
  
Per riorganizzare una sezione di una gerarchia tramite una stored procedure, vedere la sezione [Spostamento di sottoalberi](../../relational-databases/hierarchical-data-sql-server.md#BKMK_MovingSubtrees).  
  
