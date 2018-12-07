---
title: Creare vincoli CHECK | Microsoft Docs
ms.custom: ''
ms.date: 06/28/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- table constraints [SQL Server]
- attaching check constraints
- columns [SQL Server], constraints
- constraints [SQL Server], check
- CHECK constraints, attaching
ms.assetid: b8756304-9454-4d39-996a-64516831b7df
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 98ddc4f21807b9ac5185ad5e510cd83e35bbc93b
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52521657"
---
# <a name="create-check-constraints"></a>Creare vincoli CHECK
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  È possibile creare un vincolo CHECK in una tabella per specificare i valori di dati accettabili in una o più colonne in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Security](#Security)  
  
-   **Per creare un nuovo vincolo CHECK:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Permissions  
 È necessario disporre delle autorizzazioni ALTER per la tabella.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-create-a-new-check-constraint"></a>Per creare un nuovo vincolo CHECK  
  
1.  In **Esplora oggetti**espandere la tabella a cui si vuole aggiungere un vincolo CHECK, fare clic con il pulsante destro del mouse su **Vincoli** e scegliere **Nuovo vincolo**.  
  
2.  Nella finestra di dialogo **Vincoli CHECK** fare clic nel campo **Espressione** e quindi sui puntini di sospensione **(...)**.  
  
3.  Nella finestra di dialogo **Espressione vincolo CHECK** immettere le espressioni SQL per il vincolo CHECK: Ad esempio per limitare le voci nella colonna `SellEndDate` della tabella `Product` a un valore che è maggiore o uguale alla data nella colonna `SellStartDate` o è un valore NULL, digitare:  
  
    ```  
    SellEndDate >= SellStartDate OR SellEndDate IS NULL  
    ```  
  
     In alternativa, per richiedere l'immissione di un valore composto da 5 cifre nella colonna `zip` , digitare:  
  
    ```  
    zip LIKE '[0-9][0-9][0-9][0-9][0-9]'  
    ```  
  
    > [!NOTE]  
    >  Tutti i valori di vincolo non numerici devono essere racchiusi tra virgolette singole (').  
  
4.  Fare clic su **OK**.  
  
5.  Nella categoria **Identità** è possibile modificare il nome del vincolo CHECK e aggiungere una descrizione (proprietà estesa) per il vincolo.  
  
6.  Nella categoria **Progettazione tabelle** è possibile impostare quando deve essere applicato il vincolo.  
  
    |**A:**|**Selezionare Sì nei seguenti campi:**|  
    |-------------|---------------------------------------------|  
    |Testare il vincolo su dati che esistevano prima di creare il vincolo|**Verificare i dati esistenti durante la creazione o l'abilitazione**|  
    |Applicare il vincolo quando si verifica un'operazione di replica su questa tabella|**Applicare per replica**|  
    |Applicare il vincolo ogni qualvolta una riga di questa tabella viene inserita o viene aggiornata|**Attiva per istruzioni INSERTs e UPDATEs**|  
  
7.  Scegliere **Chiudi**.  
  
##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-create-a-new-check-constraint"></a>Per creare un nuovo vincolo CHECK  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra delle query e fare clic su **Esegui**.  
  
    ```  
    ALTER TABLE dbo.DocExc   
       ADD ColumnD int NULL   
       CONSTRAINT CHK_ColumnD_DocExc   
       CHECK (ColumnD > 10 AND ColumnD < 50);  
    GO  
    -- Adding values that will pass the check constraint  
    INSERT INTO dbo.DocExc (ColumnD) VALUES (49);  
    GO  
    -- Adding values that will fail the check constraint  
    INSERT INTO dbo.DocExc (ColumnD) VALUES (55);  
    GO  
  
    ```  
  
 Per altre informazioni, vedere [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).  
  
###  <a name="TsqlExample"></a>  
