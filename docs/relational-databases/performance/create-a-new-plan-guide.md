---
title: Creare una nuova guida di piano | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql13.swb.designer.newplanguide.f1
helpviewer_keywords:
- creating plan guides
- plan guides [SQL Server]. creating
ms.assetid: e1ad78bb-4857-40ea-a0c6-dcf5c28aef2f
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 5f37f0189df126054626fdd4820368911b1fa5cc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946962"
---
# <a name="create-a-new-plan-guide"></a>Creare una nuova guida di piano
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Le guide di piano influiscono sull'ottimizzazione delle query mediante l'aggiunta di hint o di un piano di query fisso. Nella guida di piano è necessario specificare l'istruzione che si vuole ottimizzare e una clausola OPTION che contiene gli hint per la query da usare. In alternativa, un piano di query specifico che si vuole usare per ottimizzare la query. Quando viene eseguita la query, in Query Optimizer è possibile far corrispondere l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] alla guida di piano e associare la clausola OPTION alla query in fase di esecuzione oppure utilizzare il piano di query specificato.  

Una guida di piano applica a una query un piano di query fisso e/o hint per la query.
  
##  <a name="Restrictions"></a> Limitazioni e restrizioni  
-   Gli argomenti per sp_create_plan_guide devono essere inseriti nell'ordine illustrato. Quando si forniscono valori per i parametri di **sp_create_plan_guide**, è necessario specificare in modo esplicito tutti i nomi dei parametri oppure nessuno. Se ad esempio si specifica **@name =** , è necessario specificare anche **@stmt =** , **@type =** e così via. Analogamente, se si omette **@name =** e viene specificato soltanto il valore del parametro, è necessario omettere anche i nomi dei parametri restanti e specificarne solo il valore. I nomi degli argomenti hanno scopo esclusivamente descrittivo, per facilitare la comprensione della sintassi. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non verifica che il nome di parametro specificato corrisponda al nome del parametro nella posizione in cui il nome viene utilizzato.  
  
-   È possibile creare più guide di piano OBJECT o SQL per la stessa query e batch o modulo. Tuttavia è possibile abilitare una sola guida di piano alla volta.  
  
-   Non è possibile creare guide di piano di tipo OBJECT per un valore @module_or_batch che fa riferimento a una stored procedure, una funzione o un trigger DML che specifica la clausola WITH ENCRYPTION o che è temporaneo.  
  
-   Se si tenta di eliminare o modificare una funzione, una stored procedure o un trigger DML a cui viene fatto riferimento in una guida di piano abilitata o disabilitata, viene generato un errore. Viene generato un errore anche se si cerca di eliminare una tabella per la quale è stato definito un trigger a cui una guida di piano fa riferimento.  

##  <a name="Permissions"></a> Autorizzazioni  
 Per creare una guida di piano di tipo OBJECT, è necessaria l'autorizzazione ALTER per l'oggetto a cui si fa riferimento. Per creare una guida di piano di tipo SQL o TEMPLATE, è necessaria l'autorizzazione ALTER per il database corrente.  
  
##  <a name="SSMSProcedure"></a> Per creare una guida di piano usando SSMS  
1.  Fare clic sul segno più per espandere il database in cui si desidera creare una guida di piano, quindi fare clic sul segno più per espandere la cartella **Programmabilità** .  
  
2.  Fare clic con il pulsante destro del mouse sulla cartella **Guide di piano** e selezionare **Nuova guida di piano…** . ![select_plan_guide](../../relational-databases/performance/media/select-plan-guide.png)
  
3.  Nella casella **Nome** della finestra di dialogo **Nuova guida di piano** immettere il nome della guida di piano.  
  
4.  Nella casella **Istruzione** immettere l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] sulla quale deve essere applicata la guida di piano.  
  
5.  Nell'elenco **Tipo di ambito** selezionare il tipo di entità in cui l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] viene visualizzata. Viene specificato il contesto per adeguare l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] alla guida di piano. I valori possibili sono **OBJECT**, **SQL**e **TEMPLATE**.  
  
6.  Nella casella **Batch ambito** immettere il testo del batch in cui l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] viene visualizzata. Nel testo del batch non può essere inclusa un'istruzione `USE`*database*. La casella **Batch ambito** è disponibile solo quando come tipo di ambito è selezionato **SQL** . Se non è stato immesso alcun dato nella casella relativa al batch ambito quando SQL è il tipo di ambito, il valore del testo del batch viene impostato sullo stesso valore inserito nella casella **Istruzione** .  
  
7.  Nell'elenco **Nome schema ambito** immettere il nome dello schema in cui è contenuto l'oggetto. La casella **Nome schema ambito** è disponibile solo quando come tipo di ambito è selezionato **Oggetto** .  
  
8.  Nella casella **Nome oggetto ambito** immettere il nome della stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] , della funzione scalare definita dall'utente, della funzione con valori di tabella con istruzioni multiple o del trigger DML in cui viene visualizzata l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] . La casella **Nome oggetto ambito** è disponibile solo quando come tipo di ambito è selezionato **Oggetto** .  
  
9. Nella casella **Parametri** immettere il nome e il tipo di dati di tutti i parametri incorporati nell'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
   I parametri vengono applicati solo nei casi seguenti:  
  
   -   Il tipo di ambito è **SQL** o **TEMPLATE**. Se **TEMPLATE**, i parametri non devono essere NULL.  
  
   -   L'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] viene sottomessa tramite sp_executesql e non viene specificato un valore per il parametro @params oppure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sottomette internamente un'istruzione dopo averla parametrizzata.  
  
10. Nella casella **Hint** immettere gli hint per la query o il piano di query da applicare all'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] . Per specificare uno o più hint per la query, immettere una clausola OPTION valida.  
  
11. Fare clic su **OK**.  

![plan_guide](../../relational-databases/performance/media/plan-guide.png)  

##  <a name="TsqlProcedure"></a> Creare una guida di piano usando T-SQL  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```sql  
    -- creates a plan guide named Guide1 based on a SQL statement  
    EXEC sp_create_plan_guide   
        @name = N'Guide1',   
        @stmt = N'SELECT TOP 1 *   
                  FROM Sales.SalesOrderHeader   
                  ORDER BY OrderDate DESC',   
        @type = N'SQL',  
        @module_or_batch = NULL,   
        @params = NULL,   
        @hints = N'OPTION (MAXDOP 1)';  
  
    ```  

Per altre informazioni, vedere [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md).  

  
