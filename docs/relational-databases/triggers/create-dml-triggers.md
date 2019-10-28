---
title: Creare trigger DML | Microsoft Docs
ms.custom: ''
ms.date: 09/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- encryption [SQL Server], DML triggers
- deferred name resolution, DML triggers
- WITH ENCRYPTION clause
- IF UPDATE
- SET statement, DML triggers
- DML triggers, programming
- testing column changes
- results [SQL Server], DML triggers
ms.assetid: b2b52258-642b-462e-8e0f-18c09d2eccf4
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ed3026ae450e50bcb2d9debf93c4b90eab3afad0
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/25/2019
ms.locfileid: "72905542"
---
# <a name="create-dml-triggers"></a>Creare trigger DML.
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  Questo argomento illustra come creare un trigger DML [!INCLUDE[tsql](../../includes/tsql-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE TRIGGER.  
  
##  <a name="Top"></a> Prima di iniziare  
  
### <a name="limitations-and-restrictions"></a>Limitazioni e restrizioni  
 Per un elenco di limitazioni e restrizioni associate alla creazione di trigger DML, vedere [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md).  
  
###  <a name="Permissions"></a> Autorizzazioni  
 È necessario disporre dell'autorizzazione ALTER per la tabella o la vista in cui si desidera creare il trigger.  
  
##  <a name="Procedures"></a> Procedura: Creazione di un trigger DML  
 È possibile usare uno dei seguenti elementi:  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] , quindi espanderla.  
  
2.  Espandere **Database**, espandere il database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] , espandere **Tabelle** e quindi espandere la tabella **Purchasing.PurchaseOrderHeader**.  
  
3.  Fare clic con il pulsante destro del mouse su **Trigger**, quindi scegliere **Nuovo trigger**.  
  
4.  Scegliere **Imposta valori per parametri modello** dal menu **Query**. In alternativa, è possibile premere (CTRL+MAIUSC+M) per aprire la finestra di dialogo **Imposta valori per parametri modello** .  
  
5.  Nella finestra di dialogo **Imposta valori per parametri modello** immettere i seguenti valori per i parametri indicati.  
  
    |Parametro|valore|  
    |---------------|-----------|  
    |Autore|*Nome dell'utente*|  
    |Data di creazione|*Data corrente*|  
    |Descrizione|Prima di consentire un nuovo ordine di acquisto con il fornitore da inserire, viene controllata la posizione finanziaria del fornitore.|  
    |Schema_Name|Purchasing|  
    |Trigger_Name|NewPODetail2|  
    |Table_Name|PurchaseOrderDetail|  
    |Data_Modification_Statement|Consente di rimuovere UPDATE e DELETE dall'elenco.|  
  
6.  Fare clic su **OK**.  
  
7.  Nell' **Editor di query**sostituire il commento `-- Insert statements for trigger here` con l'istruzione seguente:  
  
    ```sql  
    IF @@ROWCOUNT = 1  
    BEGIN  
       UPDATE Purchasing.PurchaseOrderHeader  
       SET SubTotal = SubTotal + LineTotal  
       FROM inserted  
       WHERE PurchaseOrderHeader.PurchaseOrderID = inserted.PurchaseOrderID  
  
    END  
    ELSE  
    BEGIN  
          UPDATE Purchasing.PurchaseOrderHeader  
       SET SubTotal = SubTotal +   
          (SELECT SUM(LineTotal)  
          FROM inserted  
          WHERE PurchaseOrderHeader.PurchaseOrderID  
           = inserted.PurchaseOrderID)  
       WHERE PurchaseOrderHeader.PurchaseOrderID IN  
          (SELECT PurchaseOrderID FROM inserted)  
    END;  
    ```  
  
8.  Per verificare la validità della sintassi, scegliere **Analizza** dal menu **Query**. Se viene restituito un messaggio di errore, confrontare l'istruzione con le informazioni precedenti, apportare le modifiche necessarie e ripetere il passaggio.  
  
9. Per creare il trigger DML, scegliere **Esegui** dal menu **Query**. Il trigger DML viene creato come un oggetto nel database.  
  
10. Per visualizzare il trigger DML nell'elenco di Esplora oggetti, fare clic con il pulsante destro del mouse su **Trigger** e scegliere **Aggiorna**.  

 [Prima di iniziare](#Top)  
  
###  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] , quindi espanderla.  
  
2.  Nel menu **File** , fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio vengono creati gli stessi trigger DML archiviati indicati in precedenza.  
  
    ```sql  
    -- Trigger valid for multirow and single row inserts  
    -- and optimal for single row inserts.  
    USE AdventureWorks2012;  
    GO  
    CREATE TRIGGER NewPODetail3  
    ON Purchasing.PurchaseOrderDetail  
    FOR INSERT AS  
    IF @@ROWCOUNT = 1  
    BEGIN  
       UPDATE Purchasing.PurchaseOrderHeader  
       SET SubTotal = SubTotal + LineTotal  
       FROM inserted  
       WHERE PurchaseOrderHeader.PurchaseOrderID = inserted.PurchaseOrderID  
  
    END  
    ELSE  
    BEGIN  
          UPDATE Purchasing.PurchaseOrderHeader  
       SET SubTotal = SubTotal +   
          (SELECT SUM(LineTotal)  
          FROM inserted  
          WHERE PurchaseOrderHeader.PurchaseOrderID  
           = inserted.PurchaseOrderID)  
       WHERE PurchaseOrderHeader.PurchaseOrderID IN  
          (SELECT PurchaseOrderID FROM inserted)  
    END;  
    ```  
  
 
  
