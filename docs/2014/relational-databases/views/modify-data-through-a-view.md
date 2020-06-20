---
title: Modificare i dati tramite una vista | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- data modifications [SQL Server], views
- views [SQL Server], modifying data through
- modifying data [SQL Server], views
ms.assetid: 410e2812-4ebe-48b2-b95f-c7784f1c4336
author: stevestein
ms.author: sstein
ms.openlocfilehash: df1eb4a33d1d10e63363e52760dad805b20c0a8f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85014226"
---
# <a name="modify-data-through-a-view"></a>Modificare i dati tramite una vista
  È possibile modificare i dati di una tabella di base sottostante in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per modificare i dati della tabella tramite una vista utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Vedere la sezione "Viste aggiornabili" in [CREATE VIEW & #40; Transact-SQL & #41;](/sql/t-sql/statements/create-view-transact-sql).  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 È richiesta l'autorizzazione UPDATE, INSERT o DELETE per la tabella di destinazione, a seconda dell'azione eseguita.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-modify-table-data-through-a-view"></a>Per modificare i dati della tabella tramite una vista  
  
1.  In **Esplora oggetti**espandere il database contenente la vista, quindi espandere **Viste**.  
  
2.  Fare clic con il pulsante destro del mouse sulla vista e selezionare **Modifica le prime 200 righe**.  
  
3.  È possibile che sia necessario modificare l'istruzione SELECT nel riquadro **SQL** affinché vengano restituite le righe da modificare.  
  
4.  Nel riquadro dei **risultati** individuare la riga da modificare o eliminare. Per eliminare la riga, fare clic con il pulsante destro del mouse sulla riga e scegliere **Elimina**. Per modificare i dati in una o più colonne, modificare i dati nella colonna.  
  
    > [!IMPORTANT]  
    >  Non è possibile eliminare una riga se la vista fa riferimento a più di una tabella di base. È possibile aggiornare solo le colonne che appartengono a una singola tabella di base.  
  
5.  Per inserire una riga, scorrere fino alla fine delle righe e inserire i nuovi valori.  
  
    > [!IMPORTANT]  
    >  Non è possibile inserire una riga se la vista fa riferimento a più di una tabella di base.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-update-table-data-through-a-view"></a>Per aggiornare i dati della tabella tramite una vista  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio si modifica il valore nelle colonne `StartDate` e `EndDate` per un dipendente specifico facendo riferimento alle colonne nella vista `HumanResources.vEmployeeDepartmentHistory`. Tramite questa vista vengono restituiti valori da due tabelle. Questa istruzione viene completata perché le colonne modificate provengono solo da una delle tabelle di base.  
  
    ```  
    USE AdventureWorks2012 ;   
    GO  
    UPDATE HumanResources.vEmployeeDepartmentHistory  
    SET StartDate = '20110203', EndDate = GETDATE()   
    WHERE LastName = N'Smith' AND FirstName = 'Samantha';   
    GO  
    ```  
  
 Per altre informazioni, vedere [UPDATE &#40;Transact-SQL&#41;](/sql/t-sql/queries/update-transact-sql).  
  
#### <a name="to-insert-table-data-through-a-view"></a>Per inserire i dati della tabella tramite una vista  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. Nell'esempio si inserisce una nuova riga nella tabella di base `HumanResouces.Department` specificando le relative colonne dalla vista `HumanResources.vEmployeeDepartmentHistory`. L'istruzione viene completata perché sono specificate solo colonne di una singola tabella di base mentre le altre colonne in questa tabella dispongono di valori predefiniti.  
  
    ```  
    USE AdventureWorks2012 ;  
    GO  
    INSERT INTO HumanResources.vEmployeeDepartmentHistory (Department, GroupName)   
    VALUES ('MyDepartment', 'MyGroup');   
    GO  
    ```  
  
 Per altre informazioni, vedere [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql).  
  
  
