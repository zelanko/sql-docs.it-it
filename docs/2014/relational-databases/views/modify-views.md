---
title: Modificare viste | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- views [SQL Server], renaming
- views [SQL Server], modifying
- modifying views
- renaming views
ms.assetid: 2d3c14dc-43e5-4324-b8fb-f2692d330b16
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b3d2581f2f086f8db5f9408502185c132a5866af
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52513219"
---
# <a name="modify-views"></a>Modifica di viste
  Dopo aver definito una vista, è possibile modificarne la definizione in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , senza eliminare e ricreare la vista, utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per modificare una vista tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   La modifica di una vista non influisce sugli oggetti dipendenti, ad esempio stored procedure o trigger, a meno che la definizione della vista non venga modificata in modo che l'oggetto dipendente non sia più valido.  
  
-   Se si modifica una vista in uso con ALTER VIEW, nel [!INCLUDE[ssDE](../../includes/ssde-md.md)] viene accettato un blocco di schema esclusivo sulla vista. Quando viene concesso il blocco e non esistono utenti attivi della vista, [!INCLUDE[ssDE](../../includes/ssde-md.md)] elimina tutte le copie della vista dalla cache delle procedure. I piani esistenti che fanno riferimento alla vista rimangono nella cache, ma vengono ricompilati per chiamate successive.  
  
-   È possibile utilizzare ALTER VIEW per viste indicizzate. Tuttavia, in questo caso vengono eliminati tutti gli indici nella vista, senza eccezioni.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Permissions  
 Per eseguire ALTER VIEW, è richiesta come minimo l'autorizzazione ALTER per OBJECT.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-modify-a-view"></a>Per modificare una vista  
  
1.  In **Esplora oggetti**fare clic sul segno più accanto al database in cui si trova la vista, quindi fare di nuovo clic sul segno più accanto alla cartella **Viste** .  
  
2.  Fare clic con il pulsante destro del mouse sulla vista che si desidera modificare, quindi scegliere **Progettazione**.  
  
3.  Nel riquadro del diagramma di Progettazione query, apportare le modifiche alla vista con uno dei metodi seguenti:  
  
    1.  Selezionare o deselezionare le caselle di controllo di qualsiasi elemento che si desidera aggiungere o rimuovere.  
  
    2.  Fare clic con il pulsante destro del mouse all'interno del riquadro del diagramma, scegliere **Aggiungi tabella** e quindi selezionare le altre colonne da aggiungere alla vista nella finestra di dialogo **Aggiungi tabella**.  
  
    3.  Fare clic con il pulsante destro del mouse sulla barra del titolo della tabella da rimuovere e selezionare **Rimuovi**.  
  
4.  Scegliere *Salva***nome vista* dal menu **File**.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-modify-a-view"></a>Per modificare una vista  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra delle query e fare clic su **Esegui**. Nell'esempio si crea innanzitutto una vista che, successivamente, viene modificata tramite ALTER VIEW. Una clausola WHERE viene aggiunta alla definizione della vista.  
  
    ```  
    USE AdventureWorks2012 ;  
    GO  
    -- Create a view.  
    CREATE VIEW HumanResources.EmployeeHireDate  
    AS  
    SELECT p.FirstName, p.LastName, e.HireDate  
    FROM HumanResources.Employee AS e JOIN Person.Person AS  p  
    ON e.BusinessEntityID = p.BusinessEntityID ;   
  
    -- Modify the view by adding a WHERE clause to limit the rows returned.  
    ALTER VIEW HumanResources.EmployeeHireDate  
    AS  
    SELECT p.FirstName, p.LastName, e.HireDate  
    FROM HumanResources.Employee AS e JOIN Person.Person AS  p  
    ON e.BusinessEntityID = p.BusinessEntityID  
    WHERE HireDate < CONVERT(DATETIME,'20020101',101) ;   
    GO  
    ```  
  
 Per altre informazioni, vedere [ALTER VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-view-transact-sql).  
  
  
