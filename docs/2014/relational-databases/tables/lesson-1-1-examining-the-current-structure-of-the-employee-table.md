---
title: Esame della struttura corrente della tabella Employee | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- examining the current structure of the employee
ms.assetid: d546a820-105a-417d-ac35-44a6d1d70ac6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b88c78a1a7f4244afe220585919a50ed06cd0ad9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66110137"
---
# <a name="examining-the-current-structure-of-the-employee-table"></a>Esame della struttura corrente della tabella Employee
  Il database di esempio [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] contiene una tabella **Employee** nello schema **HumanResources**. Per evitare di modificare la tabella originale, in questo passaggio viene creata una copia della tabella **Employee** denominata **EmployeeDemo**. Per semplificare l'esempio, copiare solo cinque colonne della tabella originale. Quindi, si esegue una query di **HumanResources. Employeedemo** tabella per verificare la modalità con cui i dati sono strutturati in una tabella senza utilizzare il `hierarchyid` tipo di dati.  
  
### <a name="to-copy-the-employee-table"></a>Per copiare la tabella Employee  
  
1.  In una finestra editor di query, eseguire il codice seguente per copiare la struttura della tabella e i dati della tabella **Employee** in una tabella nuova denominata **EmployeeDemo**.  
  
    ```  
    USE AdventureWorks ;  
    GO  
  
    SELECT EmployeeID, LoginID, ManagerID, Title, HireDate   
    INTO HumanResources.EmployeeDemo   
    FROM HumanResources.Employee ;  
    GO  
    ```  
  
### <a name="to-examine-the-structure-and-data-of-the-employeedemo-table"></a>Per esaminare la struttura e i dati della tabella EmployeeDemo  
  
-   Questa nuova tabella **EmployeeDemo** rappresenta una tabella tipica di un database esistente di cui si può eseguire la migrazione a una struttura nuova. In una finestra editor di query, eseguire il codice seguente per visualizzare il modo in cui la tabella utilizza un self-join per visualizzare le relazioni dipendente/responsabile:  
  
    ```  
    SELECT   
         Mgr.EmployeeID AS MgrID, Mgr.LoginID AS Manager,   
         Emp.EmployeeID AS E_ID, Emp.LoginID, Emp.Title  
    FROM HumanResources.EmployeeDemo AS Emp  
    LEFT JOIN HumanResources.EmployeeDemo AS Mgr  
    ON Emp.ManagerID = Mgr.EmployeeID  
    ORDER BY MgrID, E_ID  
    ```  
  
     [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```  
    MgrID Manager                 E_ID LoginID                  Title  
    NULL NULL                      109 adventure-works\ken0     Chief Executive Officer  
    3    adventure-works\roberto0  4   adventure-works\rob0     Senior Tool Designer  
    3    adventure-works\roberto0  9   adventure-works\gail0    Design Engineer  
    3    adventure-works\roberto0  11  adventure-works\jossef0  Design Engineer  
    3    adventure-works\roberto0  158 adventure-works\dylan0   Research and Development Manager  
    3    adventure-works\roberto0  263 adventure-works\ovidiu0  Senior Tool Designer  
    3    adventure-works\roberto0  267 adventure-works\michael8 Senior Design Engineer  
    3    adventure-works\roberto0  270 adventure-works\sharon0  Design Engineer  
    6    adventure-works\david0    2   adventure-works\kevin0   Marketing Assistant  
    ...  
    ```  
  
     Viene generato un totale di 290 righe di risultati.  
  
 Con la clausola `ORDER BY`, i report diretti di ogni livello di gestione vengono elencati insieme nell'output. Ad esempio, tutti i sette report diretti di **MgrID** 3 (roberto0) vengono elencati uno accanto all'altro. Anche se non impossibile, è molto più difficile raggruppare tutti coloro che riportano a **MgrID** 3.  
  
 Nell'attività successiva, verrà creata una nuova tabella con un tipo di dati `hierarchyid` e verranno spostati i dati nella nuova tabella.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Popolamento di una tabella con dati gerarchici esistenti](lesson-1-2-populating-a-table-with-existing-hierarchical-data.md)  
  
  
