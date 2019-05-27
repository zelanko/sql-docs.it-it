---
title: Popolamento di una tabella gerarchica tramite metodi gerarchici | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- HierarchyID
helpviewer_keywords:
- HierarchyID
ms.assetid: 2c95fa60-5b8e-4a05-ac09-cffe2b05900a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0ec81ae3a078846ad9288fe75eab9fe30d547a4e
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66110054"
---
# <a name="populating-a-hierarchical-table-using-hierarchical-methods"></a>Popolamento di una tabella gerarchica utilizzando metodi gerarchici
  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] ha 8 dipendenti che lavorano nel reparto Marketing. La gerarchia dei dipendenti è simile alla seguente:  
  
 **David**, **EmployeeID** 6 è il responsabile marketing. Tre marketing specialist fanno riferimento a **David**:  
  
-   **Sariya**, **EmployeeID** 46  
  
-   **John**, **EmployeeID** 271  
  
-   **Jill**, **EmployeeID** 119  
  
 **Wanida** , Marketing Assistant (**EmployeeID** 269), fa riferimento a **Sariya**, mentre **Mary** Marketing Assistant (**EmployeeID** 272), fa riferimento a **John**.  
  
### <a name="to-insert-the-root-of-the-hierarchy-tree"></a>Per inserire la radice dell'albero gerarchico  
  
1.  Nell'esempio seguente **David** , il responsabile marketing, è inserito nella tabella alla radice della gerarchia. La colonna **OrdLevel** è una colonna calcolata. Pertanto, non è parte dell'istruzione INSERT. Questo primo record usa il metodo [GetRoot()](/sql/t-sql/data-types/getroot-database-engine) per popolarsi come radice della gerarchia.  
  
    ```  
    INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
    VALUES (hierarchyid::GetRoot(), 6, 'David', 'Marketing Manager') ;  
    GO  
    ```  
  
2.  Eseguire il seguente codice per esaminare la riga iniziale della tabella:  
  
    ```  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    ```  
  
     [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```  
    Text_OrgNode OrgNode OrgLevel EmployeeID EmpName Title  
    ------------ ------- -------- ---------- ------- -----------------  
    /            Ox      0        6          David   Marketing Manager  
    ```  
  
 Come illustrato nella lezione precedente, si utilizza il metodo `ToString()` per convertire il tipo di dati `hierarchyid` in un formato più facilmente comprensibile.  
  
### <a name="to-insert-a-subordinate-employee"></a>Per inserire un dipendente subordinato  
  
1.  **Sariya** fa riferimento a **David**. Per inserire **Sariya** nodo, è necessario creare un oggetto appropriato **OrgNode** valore del tipo di dati `hierarchyid`. Il codice seguente crea una variabile di tipo dato `hierarchyid` e la popola con il valore OrgNode radice della tabella. A questo punto usa la variabile con il metodo [GetDescendant()](/sql/t-sql/data-types/getdescendant-database-engine) per inserire la riga che è un nodo subordinato. `GetDescendant` accetta due argomenti. Rivedere le opzioni seguenti per i valori dell'argomento:  
  
    -   Se il padre è NULL, `GetDescendant` restituisce NULL.  
  
    -   Se il padre non è NULL e child1 e child2 sono NULL, `GetDescendant` restituisce un figlio del padre.  
  
    -   Se il padre e child1 non sono NULL e child2 è NULL, `GetDescendant` restituisce un figlio del padre maggiore di child1.  
  
    -   Se il padre e child2 non sono NULL e child1 è NULL, `GetDescendant` restituisce un figlio del padre minore di child2.  
  
    -   Se il padre, child1 e child2 non sono NULL, `GetDescendant` restituisce un figlio del padre maggiore di child1 e uno minore di child2.  
  
     Il codice seguente utilizza gli argomenti `(NULL, NULL)` dell'elemento padre radice perché nella tabella non esiste ancora alcuna riga, ad eccezione della radice. Eseguire il codice seguente per inserire **Sariya**:  
  
    ```  
    DECLARE @Manager hierarchyid   
    SELECT @Manager = hierarchyid::GetRoot()  
    FROM HumanResources.EmployeeOrg ;  
  
    INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
    VALUES  
    (@Manager.GetDescendant(NULL, NULL), 46, 'Sariya', 'Marketing Specialist') ;  
  
    ```  
  
2.  Ripetere la query dalla prima procedura per eseguire una query sulla tabella e verificare come appaiono le voci:  
  
    ```  
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
  
### <a name="to-create-a-procedure-for-entering-new-nodes"></a>Per creare una procedura per l'immissione di nuovi nodi  
  
1.  Per semplificare l'inserimento di dati, creare la stored procedure seguente per aggiungere dipendenti alla tabella **EmployeeOrg** . La procedura accetta valori di input sul dipendente aggiunto. Include il numero **EmployeeID** del responsabile del nuovo dipendente, il numero **EmployeeID** del nuovo dipendente, il nome e il titolo. La procedura usa `GetDescendant()` e anche il metodo [GetAncestor()](/sql/t-sql/data-types/getancestor-database-engine) . Eseguire il codice seguente per creare la procedura:  
  
    ```  
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
  
    ```  
    EXEC AddEmp 6, 271, 'John', 'Marketing Specialist' ;  
    EXEC AddEmp 6, 119, 'Jill', 'Marketing Specialist' ;  
    EXEC AddEmp 46, 269, 'Wanida', 'Marketing Assistant' ;  
    EXEC AddEmp 271, 272, 'Mary', 'Marketing Assistant' ;  
    ```  
  
3.  Eseguire nuovamente la query seguente per esaminare le righe della tabella **EmployeeOrg** :  
  
    ```  
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
    /2/          0x68    1        271        John    Marketing Specialist  
    /2/1/        0x6AC0  2        272        Mary    Marketing Assistant  
    /3/          0x78    1        119        Jill    Marketing Specialist  
    ```  
  
 La tabella ora è popolata completamente con l'organizzazione Marketing.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Esecuzione di query su una tabella gerarchica utilizzando metodi gerarchici](lesson-2-3-querying-a-hierarchical-table-using-hierarchy-methods.md)  
  
  
