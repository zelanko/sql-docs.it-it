---
title: Creare una nuova guida di piano | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql12.swb.designer.newplanguide.f1
helpviewer_keywords:
- creating plan guides
- plan guides [SQL Server]. creating
ms.assetid: e1ad78bb-4857-40ea-a0c6-dcf5c28aef2f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9fa024e9e744fd955e4ccc323919cb22a97b7dd3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63151191"
---
# <a name="create-a-new-plan-guide"></a>Creare una nuova guida di piano
  È possibile creare una guida di piano in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Le guide di piano influiscono sull'ottimizzazione delle query mediante l'aggiunta di hint o di un piano di query fisso. Nel piano di guida si specifica l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] da ottimizzare e la clausola OPTION che contiene gli hint che si desidera utilizzare per l'ottimizzazione della query o un piano di query specifico che si desidera utilizzare per ottimizzare la query. Quando viene eseguita la query, in Query Optimizer è possibile far corrispondere l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] alla guida di piano e associare la clausola OPTION alla query in fase di esecuzione oppure utilizzare il piano di query specificato.  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per creare una Guida di piano utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Gli argomenti per sp_create_plan_guide devono essere inseriti nell'ordine illustrato. Quando si specificano valori per i parametri di `sp_create_plan_guide`, è necessario specificare in modo esplicito tutti i nomi dei parametri oppure nessuno. Se ad esempio si specifica `@name =`, è necessario specificare anche `@stmt =`, `@type =` e così via. Analogamente, se `@name =` viene omesso e viene specificato soltanto il valore del parametro, è necessario omettere anche i nomi dei parametri restanti e specificarne solo il valore. I nomi degli argomenti hanno scopo esclusivamente descrittivo, per facilitare la comprensione della sintassi. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non verifica che il nome di parametro specificato corrisponda al nome del parametro nella posizione in cui il nome viene utilizzato.  
  
-   È possibile creare più guide di piano OBJECT o SQL per la stessa query e batch o modulo. Tuttavia è possibile abilitare una sola guida di piano alla volta.  
  
-   Non è possibile creare guide di piano di tipo OBJECT per un valore @module_or_batch che fa riferimento a una stored procedure, una funzione o un trigger DML che specifica la clausola WITH ENCRYPTION o che è temporaneo.  
  
-   Se si tenta di eliminare o modificare una funzione, una stored procedure o un trigger DML a cui viene fatto riferimento in una guida di piano abilitata o disabilitata, viene generato un errore. Viene generato un errore anche se si cerca di eliminare una tabella per la quale è stato definito un trigger a cui una guida di piano fa riferimento.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Per creare una guida di piano di tipo OBJECT, è necessario disporre dell'autorizzazione ALTER per l'oggetto a cui si fa riferimento. Per creare una guida di piano di tipo SQL o TEMPLATE, è necessario disporre dell'autorizzazione ALTER per il database corrente.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-create-a-plan-guide"></a>Per creare una guida di piano  
  
1.  Fare clic sul segno più per espandere il database in cui si desidera creare una guida di piano, quindi fare clic sul segno più per espandere la cartella **Programmabilità** .  
  
2.  Fare doppio clic il **guide di piano** cartella e selezionare **nuova Guida di piano...** .  
  
3.  Nella casella **Nome** della finestra di dialogo **Nuova guida di piano** immettere il nome della guida di piano.  
  
4.  Nella casella **Istruzione** immettere l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] sulla quale deve essere applicata la guida di piano.  
  
5.  Nell'elenco **Tipo di ambito** selezionare il tipo di entità in cui l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] viene visualizzata. Viene specificato il contesto per adeguare l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] alla guida di piano. I valori possibili sono **OBJECT**, **SQL**e **TEMPLATE**.  
  
6.  Nella casella **Batch ambito** immettere il testo del batch in cui l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] viene visualizzata. Nel testo del batch non può essere inclusa un'istruzione USE``*database* . La casella **Batch ambito** è disponibile solo quando come tipo di ambito è selezionato **SQL** . Se non è stato immesso alcun dato nella casella relativa al batch ambito quando SQL è il tipo di ambito, il valore del testo del batch viene impostato sullo stesso valore inserito nella casella **Istruzione** .  
  
7.  Nell'elenco **Nome schema ambito** immettere il nome dello schema in cui è contenuto l'oggetto. La casella **Nome schema ambito** è disponibile solo quando come tipo di ambito è selezionato **Oggetto** .  
  
8.  Nella casella **Nome oggetto ambito** immettere il nome della stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] , della funzione scalare definita dall'utente, della funzione con valori di tabella con istruzioni multiple o del trigger DML in cui viene visualizzata l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] . La casella **Nome oggetto ambito** è disponibile solo quando come tipo di ambito è selezionato **Oggetto** .  
  
9. Nella casella **Parametri** immettere il nome e il tipo di dati di tutti i parametri incorporati nell'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
     I parametri vengono applicati solo nei casi seguenti:  
  
    -   Il tipo di ambito è **SQL** o **TEMPLATE**. Se **TEMPLATE**, i parametri non devono essere NULL.  
  
    -   L'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] viene sottomessa tramite sp_executesql e non viene specificato un valore per il parametro @params oppure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sottomette internamente un'istruzione dopo averla parametrizzata.  
  
10. Nella casella **Hint** immettere gli hint per la query o il piano di query da applicare all'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] . Per specificare uno o più hint per la query, immettere una clausola OPTION valida.  
  
11. Fare clic su **OK**.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-create-a-plan-guide"></a>Per creare una guida di piano  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
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
  
 Per altre informazioni, vedere [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql).  
  
  
