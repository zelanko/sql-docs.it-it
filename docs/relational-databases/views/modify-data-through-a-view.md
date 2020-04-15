---
title: Modificare i dati tramite una vista | Microsoft Docs
ms.custom: ''
ms.date: 10/05/2016
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fb3c4075471394652fa5952fa60f8da9a367d834
ms.sourcegitcommit: 79d8912941d66abdac4e8402a5a742fa1cb74e6d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/02/2020
ms.locfileid: "80550225"
---
# <a name="modify-data-through-a-view"></a>Modificare i dati tramite una vista
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]
  È possibile modificare i dati di una tabella di base sottostante in SQL Server usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Vedere la sezione "Viste aggiornabili" in [CREATE VIEW & #40; Transact-SQL & #41;](../../t-sql/statements/create-view-transact-sql.md).  
  
  
###  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 È richiesta l'autorizzazione UPDATE, INSERT o DELETE per la tabella di destinazione, a seconda dell'azione eseguita.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-modify-table-data-through-a-view"></a>Per modificare i dati della tabella tramite una vista  
  
1.  In **Esplora oggetti**espandere il database contenente la vista, quindi espandere **Viste**.  
  
2.  Fare clic con il pulsante destro del mouse sulla vista e selezionare **Modifica le prime 200 righe**.  
  
3.  È possibile che sia necessario modificare l'istruzione SELECT nel riquadro **SQL** affinché vengano restituite le righe da modificare.  
  
4.  Nel riquadro dei **risultati** individuare la riga da modificare o eliminare. Per eliminare la riga, fare clic con il pulsante destro del mouse sulla riga e scegliere **Elimina**. Per modificare i dati in una o più colonne, modificare i dati nella colonna.  
  
    > **IMPORTANTE** Non è possibile eliminare una riga se la vista fa riferimento a più di una tabella di base. È possibile aggiornare solo le colonne che appartengono a una singola tabella di base.  
  
5.  Per inserire una riga, scorrere fino alla fine delle righe e inserire i nuovi valori.  

    > **IMPORTANTE** Non è possibile inserire una riga se la vista fa riferimento a più di una tabella di base.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-update-table-data-through-a-view"></a>Per aggiornare i dati della tabella tramite una vista  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
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
  
 Per altre informazioni, vedere [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md).  
  
#### <a name="to-insert-table-data-through-a-view"></a>Per inserire i dati della tabella tramite una vista  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. Nell'esempio si inserisce una nuova riga nella tabella di base `HumanResouces.Department` specificando le relative colonne dalla vista `HumanResources.vEmployeeDepartmentHistory`. L'istruzione viene completata perché sono specificate solo colonne di una singola tabella di base mentre le altre colonne in questa tabella dispongono di valori predefiniti.  
  
    ```  
    USE AdventureWorks2012 ;  
    GO  
    INSERT INTO HumanResources.vEmployeeDepartmentHistory (Department, GroupName)   
    VALUES ('MyDepartment', 'MyGroup');   
    GO  
    ```  
  
 Per altre informazioni, vedere [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md).  
  
  
