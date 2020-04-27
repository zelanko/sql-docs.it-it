---
title: Creazione di viste e stored procedure | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- creating views and stored procedures
ms.assetid: 53a0426d-07d8-4b7c-aa21-22632753bad8
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 20f16e9deeb9e07d2c63090c92100871331e0443
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "68211184"
---
# <a name="creating-views-and-stored-procedures"></a>Creazione di viste e stored procedure
  Dopo aver concesso all'utente Mary l'accesso al database **TestData** è possibile creare alcuni oggetti di database, ad esempio una vista e una stored procedure, quindi concedere a Mary l'accesso a tali oggetti. Una vista è costituita da un'istruzione SELECT, mentre una stored procedure da una o più istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)] eseguite in un batch.  
  
 Sulle viste è possibile eseguire query come con le tabelle, ad eccezione del fatto che le viste non accettano parametri. Le stored procedure sono più complesse delle viste e possono avere parametri di input e output, nonché contenere istruzioni per controllare il flusso del codice, ad esempio istruzioni IF e WHILE. È consigliabile dal punto di vista della programmazione utilizzare le stored procedure per tutte le azioni ripetitive sul database.  
  
 In questo esempio si userà CREATE VIEW per creare una vista che seleziona solo due delle colonne incluse nella tabella **Products** . Si utilizzerà quindi CREATE PROCEDURE per creare una stored procedure che accetta un parametro di prezzo e restituisce solo i prodotti il cui costo è inferiore al valore di tale parametro.  
  
### <a name="to-create-a-view"></a>Per creare una vista  
  
1.  Eseguire l'istruzione seguente per creare un vista molto semplice che esegue un'istruzione SELECT e restituisce i nomi e i prezzi dei prodotti.  
  
    ```  
    CREATE VIEW vw_Names  
       AS  
       SELECT ProductName, Price FROM Products;  
    GO  
  
    ```  
  
### <a name="test-the-view"></a>Test della vista  
  
1.  Le viste vengono utilizzate in modo analogo alle tabelle. Utilizzare un'istruzione `SELECT` per accedere a una vista.  
  
    ```  
    SELECT * FROM vw_Names;  
    GO  
  
    ```  
  
### <a name="to-create-a-stored-procedure"></a>Per creare una stored procedure  
  
1.  L'istruzione seguente crea una stored procedure denominata `pr_Names`che accetta un parametro di input denominato `@VarPrice` con tipo di dati `money`. La stored procedure visualizza il testo `Products less than` concatenata al parametro di input modificato da tipo di dati `money` in tipo di dati carattere `varchar(10)` . La procedura esegue quindi un'istruzione `SELECT` sulla vista, passando il parametro di input come parte della clausola `WHERE` . Ciò restituisce tutti i prodotti il cui costo è inferiore al valore del parametro di input.  
  
    ```  
    CREATE PROCEDURE pr_Names @VarPrice money  
       AS  
       BEGIN  
          -- The print statement returns text to the user  
          PRINT 'Products less than ' + CAST(@VarPrice AS varchar(10));  
          -- A second statement starts here  
          SELECT ProductName, Price FROM vw_Names  
                WHERE Price < @varPrice;  
       END  
    GO  
  
    ```  
  
### <a name="test-the-stored-procedure"></a>Test della stored procedure  
  
1.  Per testare la stored procedure, digitare ed eseguire l'istruzione seguente. La procedura restituirà i nomi di due prodotti immessi nella tabella `Products` nella lezione 1 con prezzo inferiore a `10.00`.  
  
    ```  
    EXECUTE pr_Names 10.00;  
    GO  
  
    ```  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Concessione dell'accesso a un oggetto di database](lesson-2-4-granting-access-to-a-database-object.md)  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-view-transact-sql)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql)  
  
  
