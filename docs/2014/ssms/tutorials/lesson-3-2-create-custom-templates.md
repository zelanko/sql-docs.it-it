---
title: Creare modelli personalizzati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- tql
- templates [Transact-SQL], creating
- templates [Transact-SQL]
ms.assetid: 41098e78-b482-410e-bfe8-2ac10769ac4a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7d44d8d8bdda5f8c15fffe8f3aaf0eaf2d099e81
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85040894"
---
# <a name="create-custom-templates"></a>Creare modelli personalizzati
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] include modelli da usare per molte attività comuni. L'effettivo vantaggio dei modelli, tuttavia, consiste nella possibilità di creare un modello personalizzato per uno script complesso che è necessario creare frequentemente. In questa esercitazione verranno illustrate le procedure per la creazione di uno script semplice con un numero limitato di parametri, ma i modelli risultano utili anche per script complessi e ripetitivi.  
  
## <a name="using-custom-templates"></a>Utilizzo di modelli personalizzati  
  
#### <a name="to-create-a-custom-template"></a>Per creare un modello personalizzato  
  
1.  In Esplora modelli espandere **Modelli di SQL Server**, fare clic con il pulsante destro del mouse su **Stored procedure**, scegliere **Nuova**e selezionare **Cartella**.  
  
2.  Digitare **Custom** come nome della nuova cartella del modello e premere INVIO.  
  
3.  Fare clic con il pulsante destro del mouse su **Custom**, scegliere **Nuovo**e selezionare **Modello**.  
  
4.  Digitare **WorkOrdersProc** come nome del nuovo modello e premere **INVIO**.  
  
5.  Fare clic con il pulsante destro del mouse su **WorkOrdersProc**e scegliere **Modifica**.  
  
6.  Nella finestra di dialogo **Connetti al motore di database** verificare le informazioni di connessione e fare clic su **Connetti**.  
  
7.  Nell'editor di query digitare lo script seguente per creare una stored procedure che ricerca negli ordini una determinata parte, in questo caso Blade. (È possibile copiare e incollare il codice dalla finestra dell'esercitazione).  
  
    ```  
    USE AdventureWorks20012;  
    GO  
    IF EXISTS (  
    SELECT *   
       FROM INFORMATION_SCHEMA.ROUTINES   
       WHERE SPECIFIC_NAME = 'WorkOrdersForBlade')  
       DROP PROCEDURE dbo.WorkOrdersForBlade;  
    GO  
    CREATE PROCEDURE dbo.WorkOrdersForBlade  
    AS  
    SELECT Name, WorkOrderID   
    FROM Production.WorkOrder AS WO  
    JOIN Production.Product AS Prod  
    ON WO.ProductID = Prod.ProductID  
    WHERE Name = 'Blade';  
    GO  
    ```  
  
8.  Premere F5 per eseguire lo script e creare la procedura **WorkOrdersForBlade** .  
  
9. In Esplora oggetti fare clic con il pulsante destro del mouse sul server e scegliere **Nuova query**. Verrà visualizzata una nuova finestra dell'editor di query.  
  
10. Nell'editor di query digitare **EXECUTE dbo.WorkOrdersForBlade**e premere F5 per eseguire la query. Verificare che nel riquadro **Risultati** sia visualizzato l'elenco di ordini di blade richiesto.  
  
11. Modificare lo script del modello, ovvero lo script del passaggio 7, sostituendo il nome del prodotto Blade con il parametro <strong> *<* product_name</strong>, `nvarchar(50)` , <strong> *>* Name</strong>, in quattro posizioni.  
  
    > [!NOTE]  
    >  Per i parametri sono necessari tre elementi, ovvero il nome che si desidera restituire, il tipo di dati e il valore predefinito.  
  
12. Lo script dovrebbe corrispondere a quanto segue:  
  
    ```  
    USE AdventureWorks20012;  
    GO  
    IF EXISTS (  
    SELECT *   
       FROM INFORMATION_SCHEMA.ROUTINES   
       WHERE SPECIFIC_NAME = 'WorkOrdersFor<product_name, nvarchar(50), name>')  
       DROP PROCEDURE dbo.WorkOrdersFor<product_name, nvarchar(50), name>;  
    GO  
    CREATE PROCEDURE dbo.WorkOrdersFor<product_name, nvarchar(50), name>  
    AS  
    SELECT Name, WorkOrderID   
    FROM Production.WorkOrder AS WO  
    JOIN Production.Product AS Prod  
    ON WO.ProductID = Prod.ProductID  
    WHERE Name = '<product_name, nvarchar(50), name>';  
    GO  
    ```  
  
13. Scegliere **Salva WorkOrdersProc.sql** dal menu **File** per salvare il modello.  
  
#### <a name="to-test-the-custom-template"></a>Per verificare il funzionamento del modello personalizzato  
  
1.  In Esplora modelli espandere **Stored Procedure**e **Custom**e fare doppio clic su **WorkOrderProc**.  
  
2.  Nella finestra di dialogo **Connetti al motore di database** specificare le informazioni di connessione e quindi fare clic su **Connetti**. Verrà visualizzata una nuova finestra dell'editor di query che include il contenuto del modello **WorkOrderProc** .  
  
3.  Scegliere **Imposta valori per parametri modello** dal menu **Query**.  
  
4.  Nella finestra di dialogo **Sostituisci parametri modello** , per il `product_name` valore, digitare **ruota libera** (sovrascrivendo il contenuto predefinito), quindi fare clic su **OK** per chiudere la finestra di dialogo **Sostituisci parametri modello** e modificare lo script nell'editor di query.  
  
5.  Premere F5 per eseguire la query e creare la procedura.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Salvare gli script come progetti o soluzioni](lesson-3-3-save-scripts-as-projects-or-solutions.md)  
  
  
