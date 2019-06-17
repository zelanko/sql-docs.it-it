---
title: Popolamento di una tabella con dati gerarchici esistenti | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- HierarchyID
ms.assetid: fd943d84-dbe6-4a05-912b-c88164998d80
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7b2614d090bce0ecf0c61db5c9a5222ec6b10951
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66110171"
---
# <a name="populating-a-table-with-existing-hierarchical-data"></a>Popolamento di una tabella con dati gerarchici esistenti
  Questa attività consente di creare una nuova tabella e popolarla con i dati della tabella **EmployeeDemo**. Questa attività prevede i passaggi seguenti:  
  
-   Creare una tabella nuova contenente una colonna `hierarchyid`. Questa colonna può sostituire le colonne **EmployeeID** e **ManagerID** esistenti. Tuttavia, tali colonne verranno mantenute. Questo avviene perché le applicazioni esistenti potrebbero riferirsi a tali colonne e potrebbero aiutare a capire i dati dopo il trasferimento. La definizione della tabella specifica che **OrgNode** è la chiave primaria che richiede alla colonna di contenere i valori univoci. L'indice cluster della colonna **OrgNode** archivierà la data nella sequenza **OrgNode** .  
  
-   Creare una tabella temporanea utilizzata per rilevare il numero di dipendenti che riportano direttamente a ogni responsabile.  
  
-   Popolare la nuova tabella usando i dati dalla tabella **EmployeeDemo** .  
  
### <a name="to-create-a-new-table-named-neworg"></a>Per creare una nuova tabella denominata NewOrg  
  
-   In una finestra dell'editor di query eseguire il codice seguente per creare una nuova tabella denominata **HumanResources.NewOrg**:  
  
    ```  
    CREATE TABLE NewOrg  
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
  
### <a name="to-create-a-temporary-table-named-children"></a>Per creare una tabella temporanea denominata #Children  
  
1.  Creare una tabella temporanea denominata **#Children** con una colonna denominata **Num** che conterrà il numero di elementi figlio per ogni nodo:  
  
    ```  
    CREATE TABLE #Children   
       (  
        EmployeeID int,  
        ManagerID int,  
        Num int  
    );  
    GO  
    ```  
  
2.  Aggiungere un indice per accelerare significativamente la query che popola la tabella **NewOrg** :  
  
    ```  
    CREATE CLUSTERED INDEX tmpind ON #Children(ManagerID, EmployeeID);  
    GO  
    ```  
  
### <a name="to-populate-the-neworg-table"></a>Per popolare la tabella NewOrg  
  
1.  Le query ricorsive impediscono le sottoquery con aggregazioni. In alternativa, popolare la tabella **#Children** con il codice seguente che usa il metodo [ROW_NUMBER()](/sql/t-sql/functions/row-number-transact-sql) per popolare la colonna **Num** :  
  
    ```  
    INSERT #Children (EmployeeID, ManagerID, Num)  
    SELECT EmployeeID, ManagerID,  
      ROW_NUMBER() OVER (PARTITION BY ManagerID ORDER BY ManagerID)   
    FROM EmployeeDemo  
    GO  
  
    ```  
  
2.  Rivedere la tabella **#Children** . Si noti in che modo la colonna **Num** contiene i numeri sequenziali per ogni responsabile.  
  
    ```  
    SELECT * FROM #Children ORDER BY ManagerID, Num  
    GO  
  
    ```  
  
     [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
     `EmployeeID ManagerID Num`  
  
     `---------- --------- ---`  
  
     `1        NULL       1`  
  
     `2         1         1`  
  
     `3         1         2`  
  
     `4         2         1`  
  
     `5         2         2`  
  
     `6         2         3`  
  
     `7         3         1`  
  
     `8         3         2`  
  
     `9         4         1`  
  
     `10        4         2`  
  
3.  Popolare la tabella **NewOrg** . Usare i metodi GetRoot e ToString per concatenare le **Num** i valori nel `hierarchyid` formattare e quindi aggiornare il **OrgNode** colonna con i valori gerarchici risultanti:  
  
    ```  
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
    INSERT NewOrg (OrgNode, O.EmployeeID, O.LoginID, O.ManagerID)  
    SELECT P.path, O.EmployeeID, O.LoginID, O.ManagerID  
    FROM EmployeeDemo AS O   
    JOIN Paths AS P   
       ON O.EmployeeID = P.EmployeeID  
    GO  
  
    ```  
  
4.  Una colonna `hierarchyid` è più comprensibile quando viene convertita in un formato carattere. Rivedere i dati nella tabella **NewOrg** eseguendo il codice seguente che contiene due rappresentazioni della colonna **OrgNode** :  
  
    ```  
    SELECT OrgNode.ToString() AS LogicalNode, *   
    FROM NewOrg   
    ORDER BY LogicalNode;  
    GO  
  
    ```  
  
     Il **LogicalNode** Converte la `hierarchyid` colonna in un formato di testo più leggibile che rappresenta la gerarchia. Nelle attività rimanenti, si utilizzerà il metodo `ToString()` per mostrare il formato logico delle colonne `hierarchyid`.  
  
5.  Eliminare la tabella temporanea che non risulta più essere necessaria:  
  
    ```  
    DROP TABLE #Children  
    GO  
    ```  
  
 L'attività successiva creerà indici per supportare la struttura gerarchica.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Ottimizzazione della tabella NewOrg](lesson-1-3-optimizing-the-neworg-table.md)  
  
  
