---
title: Creare viste | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- views [SQL Server], creating
ms.assetid: 0b7bd2a1-544c-42ba-8e7b-4822f34d7b64
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5eaa6c702c02a3258ac66ec55081965d25a12a55
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52541825"
---
# <a name="create-views"></a>Creare viste
  È possibile creare viste in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Una vista può essere utilizzata per gli scopi seguenti:  
  
-   Per analizzare, semplificare e personalizzare la visualizzazione del database per ogni utente.  
  
-   Come meccanismo di sicurezza grazie al quale è possibile consentire agli utenti di accedere ai dati tramite una vista, senza concedere loro le autorizzazioni di accesso alle tabelle di base sottostanti.  
  
-   Per fornire un'interfaccia compatibile con le versioni precedenti con cui emulare una tabella il cui schema è stato modificato.  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per creare una vista tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
 È possibile creare una vista solo nel database corrente.  
  
 Una vista può includere al massimo 1.024 colonne.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Permissions  
 Sono richieste l'autorizzazione CREATE VIEW per il database e l'autorizzazione ALTER per lo schema in cui viene creata la vista.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-create-a-view-by-using-the-query-and-view-designer"></a>Per creare una vista tramite Progettazione query e Progettazione viste  
  
1.  In **Esplora oggetti**espandere il database in cui si desidera creare la nuova vista.  
  
2.  Fare clic con il pulsante destro del mouse sulla cartella **Viste** e quindi selezionare **Nuova vista**.  
  
3.  Nel **Aggiungi tabella** finestra di dialogo, selezionare uno o più elementi che si desidera includere nella nuova vista da una delle schede seguenti: Le tabelle, viste, funzioni e sinonimi.  
  
4.  Fare clic su **Aggiungi**, quindi su **Chiudi**.  
  
5.  In **Riquadro diagramma**selezionare le colonne o gli altri elementi da includere nella nuova vista.  
  
6.  Nel riquadro **Criteri**selezionare criteri di ordinamento o filtro aggiuntivi per le colonne.  
  
7.  Scegliere *Salva***nome vista* dal menu **File**.  
  
8.  Nella finestra di dialogo **Scegli nome** immettere un nome per la nuova vista, quindi scegliere **OK**.  
  
     Per altre informazioni su Progettazione query e Progettazione viste, vedere [Strumenti di progettazione di query e viste &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/visual-database-tools.md).  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-create-a-view"></a>Per creare una vista  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra delle query e fare clic su **Esegui**.  
  
    ```  
    USE AdventureWorks2012 ;   
    GO  
    CREATE VIEW HumanResources.EmployeeHireDate  
    AS  
    SELECT p.FirstName, p.LastName, e.HireDate  
    FROM HumanResources.Employee AS e JOIN Person.Person AS  p  
    ON e.BusinessEntityID = p.BusinessEntityID ;   
    GO  
    -- Query the view  
    SELECT FirstName, LastName, HireDate  
    FROM HumanResources.EmployeeHireDate  
    ORDER BY LastName;  
  
    ```  
  
 Per altre informazioni, vedere [CREATE VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-view-transact-sql).  
  
  
