---
title: Ottimizzazione della tabella NewOrg | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- optimizing tables
ms.assetid: 89ff6d37-94c0-4773-8be9-dde943fff023
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 952043d5d001fe4fe65e6dd1aa7bb2001290429e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66110069"
---
# <a name="optimizing-the-neworg-table"></a>Ottimizzazione della tabella NewOrg
  La tabella **NewOrd** creata nell'attività popolamento di [una tabella con dati gerarchici esistenti](lesson-1-2-populating-a-table-with-existing-hierarchical-data.md) contiene tutte le informazioni sui dipendenti e rappresenta la struttura gerarchica utilizzando un `hierarchyid` tipo di dati. Questa attività aggiunge indici nuovi per supportare ricerche nella colonna `hierarchyid`.  
  
## <a name="clustered-index"></a>Indice cluster  
 La `hierarchyid` colonna (**OrgNode**) è la chiave primaria per la tabella **NewOrg** . Quando la tabella è stata creata, conteneva un indice cluster denominato **PK_NewOrg_OrgNode** per applicare l'univocità della colonna **OrgNode** . Questo indice cluster supporta anche una ricerca in profondità nella tabella.  
  
## <a name="nonclustered-index"></a>Indice non cluster  
 Questo passaggio crea due indici non cluster per supportare le ricerche tipiche.  
  
#### <a name="to-index-the-neworg-table-for-efficient-searches"></a>Per indicizzare la tabella NewOrg per eseguire ricerche efficienti  
  
1.  Per facilitare le query allo stesso livello nella gerarchia, usare il metodo [GetLevel](/sql/t-sql/data-types/getlevel-database-engine) per creare una colonna calcolata contenente il livello della gerarchia. Successivamente, creare un indice composto nel livello e `Hierarchyid`. Eseguire il codice seguente per creare la colonna calcolata e l'indice breadth-first:  
  
    ```  
    ALTER TABLE NewOrg   
       ADD H_Level AS OrgNode.GetLevel() ;  
    CREATE UNIQUE INDEX EmpBFInd   
       ON NewOrg(H_Level, OrgNode) ;  
    GO  
    ```  
  
2.  Creare un indice univoco nella colonna **EmployeeID** . Si tratta della ricerca singleton tradizionale di un solo dipendente in base al numero **EmployeeID** . Eseguire il codice seguente per creare un indice in **EmployeeID**:  
  
    ```  
    CREATE UNIQUE INDEX EmpIDs_unq ON NewOrg(EmployeeID) ;  
    GO  
    ```  
  
3.  Eseguire il codice seguente per recuperare i dati dalla tabella nell'ordine di ognuno dei tre indici:  
  
    ```  
    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID  
    FROM NewOrg   
    ORDER BY OrgNode;  
  
    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID   
    FROM NewOrg   
    ORDER BY H_Level, OrgNode;  
  
    SELECT OrgNode.ToString() AS LogicalNode,  
    OrgNode, H_Level, EmployeeID, LoginID   
    FROM NewOrg   
    ORDER BY EmployeeID;  
    GO  
    ```  
  
4.  Confrontare i set di risultati per visualizzare il modo in cui l'ordine viene archiviato in ogni tipo di indice. Seguono solo le prime quattro righe di ogni output.  
  
     [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
     Indice depth-first: i record relativi ai dipendenti vengono archiviati accanto al responsabile.  
  
     `LogicalNode OrgNode    H_Level EmployeeID LoginID`  
  
     `/             0x         0         1      zarifin`  
  
     `/1/          0x58        1         2      tplate`  
  
     `/1/1/       0x5AC0       2         4      schai`  
  
     `/1/1/1/     0x5AD6       3         9      jwang`  
  
     `/1/1/2/     0x5ADA       3        10      malexander`  
  
     `/1/2/       0x5B40       2         5      elang`  
  
     `/1/3/       0x5BC0       2         6      gsmits`  
  
     `/2/         0x68         1         3      hjensen`  
  
     `/2/1/       0x6AC0       2         7      sdavis`  
  
     `/2/2/       0x6B40       2         8      norint`  
  
     **Indice EmployeeID**-first: le righe vengono archiviate nella sequenza di **EmployeeID** .  
  
     `LogicalNode OrgNode    H_Level EmployeeID LoginID`  
  
     `/             0x         0         1      zarifin`  
  
     `/1/          0x58        1         2      tplate`  
  
     `/2/         0x68         1         3      hjensen`  
  
     `/1/1/       0x5AC0       2         4      schai`  
  
     `/1/2/       0x5B40       2         5      elang`  
  
     `/1/3/       0x5BC0       2         6      gsmits`  
  
     `/2/1/       0x6AC0       2         7      sdavis`  
  
     `/2/2/       0x6B40       2         8      norint`  
  
     `/1/1/1/     0x5AD6       3         9      jwang`  
  
     `/1/1/2/     0x5ADA       3        10      malexander`  
  
> [!NOTE]  
>  Per i diagrammi che indicano la differenza tra un indice depth-first e un indice breadth-first, vedere [Dati gerarchici &#40;SQL Server&#41;](../hierarchical-data-sql-server.md).  
  
#### <a name="to-drop-the-unnecessary-columns"></a>Per eliminare le colonne non necessarie  
  
1.  La colonna **ManagerID** rappresenta la relazione dipendente/responsabile che ora è rappresentata dalla colonna **OrgNode** . Se le altre applicazioni non richiedono la colonna **ManagerID** , si consiglia di eliminarla usando l'istruzione seguente:  
  
    ```  
    ALTER TABLE NewOrg DROP COLUMN ManagerID ;  
    GO  
    ```  
  
2.  La colonna **EmployeeID** è anche ridondante. La colonna **OrgNode** identifica in modo univoco ogni dipendente. Se le altre applicazioni non richiedono la colonna **EmployeeID** , eliminare l'indice e successivamente la colonna usando il codice seguente:  
  
    ```  
    DROP INDEX EmpIDs_unq ON NewOrg ;  
    ALTER TABLE NewOrg DROP COLUMN EmployeeID ;  
    GO  
    ```  
  
#### <a name="to-replace-the-original-table-with-the-new-table"></a>Per sostituire la tabella originale con la tabella nuova  
  
1.  Se la tabella originale contiene vincoli o indici aggiuntivi, aggiungerli alla tabella **NewOrg** .  
  
2.  Sostituire la vecchia colonna **EmployeeDemo** con la nuova tabella. Eseguire il codice seguente per rilasciare la vecchia tabella e successivamente rinominare la tabella nuova con il nome vecchio:  
  
    ```  
    DROP TABLE EmployeeDemo ;  
    GO  
    sp_rename 'NewOrg', EmployeeDemo ;  
    GO  
    ```  
  
3.  Eseguire il codice seguente per esaminare la tabella finale:  
  
    ```  
    SELECT * FROM EmployeeDemo ;  
    ```  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Riepilogo: Conversione di una tabella in una struttura gerarchica](lesson-1-4-summary-converting-a-table-to-a-hierarchical-structure.md)  
  
  
