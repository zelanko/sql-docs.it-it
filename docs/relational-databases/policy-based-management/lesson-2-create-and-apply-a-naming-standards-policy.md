---
title: 'Lezione 2: Creare e applicare criteri per gli standard di denominazione'
description: Questa esercitazione illustra come creare e applicare i criteri di denominazione per la gestione basata su criteri in SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.technology: security
ms.prod_service: database-engine
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 87e51f4e-156c-4def-8572-76a15075d75e
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 246c9d419d6f9b8fdbaae2619ef45df4d9465c36
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/09/2020
ms.locfileid: "91892431"
---
# <a name="lesson-2-create-and-apply-a-naming-standards-policy"></a>Lezione 2: Creare e applicare criteri per gli standard di denominazione
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
Alcuni tipi di criteri della gestione basata su criteri possono creare trigger per l'applicazione della conformità successiva tramite i criteri. In questa lezione verranno creati criteri per l'applicazione di uno standard di denominazione per le tabelle. Si verificheranno quindi i criteri tentando di creare una tabella che violi i criteri.  


## <a name="prerequisites"></a>Prerequisiti
Per completare questa esercitazione, sono necessari SQL Server Management Studio e l'accesso a un server che esegue SQL Server.

- Installare [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md).
- Installare [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
  
## <a name="create-the-finance-database"></a>Creare il database Finance  
  
1.  In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]aprire una finestra di query ed eseguire l'istruzione seguente:  
  
    ```sql  
    CREATE DATABASE Finance ;  
    GO  
    ```  
  
2.  In Esplora oggetti fare clic su **Database**, quindi premere F5 per aggiornare l'elenco dei database.  

## <a name="create-the-finance-tables-condition"></a>Creare la condizione Tabelle Finance 

1.  In Esplora oggetti espandere **Gestione**, espandere **Gestione criteri**, fare clic con il pulsante destro del mouse su **Condizioni**e quindi scegliere **Nuova condizione**. 

   ![Nuova condizione](Media/lesson-2-create-and-apply-a-naming-standards-policy/new-condition.png)
  
2.  Nella finestra di dialogo **Crea nuova condizione** , nella casella **Nome** digitare **Tabelle Finance**.  
    1. Nell'elenco **Facet** selezionare **Nome a più parti**. 
    1. Nella casella **Campo** dell'area **Espressione** selezionare **\@Nome**. Nella casella **Operatore** selezionare **Simile a**. Nella casella **Valore** digitare ```'fintbl%'``` per fare in modo che tutti i nomi di tabella inizino con i caratteri **fintbl**.
    1. Nella pagina **Descrizione** digitare **I nomi di tabella del database Finance devono iniziare con fintbl**e quindi scegliere **OK** per creare la condizione.  

    ![Condizione Tabelle Finance](Media/lesson-2-create-and-apply-a-naming-standards-policy/finance-tables-condition.png)
 
## <a name="create-the-finance-name-policy"></a>Creare i criteri Nome Finance  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse su **Criteri**, quindi scegliere **Nuovi criteri**.  

   ![Nuovi criteri](Media/lesson-2-create-and-apply-a-naming-standards-policy/new-policy.png)
  
2.  Nella finestra di dialogo **Crea nuovi criteri** , nella casella **Nome** digitare **Nome Finance**.
    1. Nell'elenco **Condizione di controllo** selezionare **Tabelle Finance**. Questa opzione è disponibile nell'area **Nome a più parti** . 
    1. Nell'area **In base a** viene visualizzato un elenco di oggetti di database che hanno applicato i criteri. Selezionare la casella di controllo **Ogni tabella**.
    1. Selezionare l'elenco **Abilitato** . (La casella **Abilitato** non si applica ai criteri **Su richiesta** .)
    1. Nell'elenco **Modalità di valutazione** selezionare **Su modifica: impedisci esecuzione**. Questa opzione consente di applicare i criteri tramite la creazione di un trigger di database nel database Finance. 
    1. Nell'elenco **Restrizione server** selezionare **Nessuna**. 
    1. Nella pagina **Descrizione** aggiungere la descrizione 'I nomi delle tabelle nel database Finance devono contenere 'fintbl%'.' 
    1. Tornare alla pagina **Generale** e nell'area **Ogni database** espandere **Ogni** e fare clic su **Nuova condizione**.

    ![Creare nuovi criteri Nome Finance](Media/lesson-2-create-and-apply-a-naming-standards-policy/create-new-policy-finance-name.png)
  
6.  Nella finestra di dialogo **Crea nuova condizione** , nella casella **Nome** digitare **Database Finance**.
    1. Nella casella **Espressione** completare l'espressione in modo da includere @Name = 'Finance' e quindi fare clic su **OK** per chiudere la pagina della condizione. 
  
    ![Creare la nuova condizione 'Database Finance'](Media/lesson-2-create-and-apply-a-naming-standards-policy/create-new-condition.png)

    > [!NOTE]  
    > Potrebbe essere necessario uscire dalla casella **Valore** premendo TAB per abilitare il pulsante **OK** .  
  
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="create-the-finance-policy-category"></a>Creare la categoria di criteri Finance  
  
1.  In Esplora oggetti espandere **Gestione**, fare clic con il pulsante destro del mouse su **Gestione criteri**e scegliere **Gestione categorie**.  

   ![Gestire le categorie](Media/lesson-2-create-and-apply-a-naming-standards-policy/manage-categories.png)
  
2.  Nella finestra di dialogo **Gestione categorie di criteri** , in **Nome**digitare **Finance** nella casella vuota e quindi deselezionare **Imponi sottoscrizioni di database**. Con**Imponi sottoscrizioni di database** ogni database nell'istanza verrà forzato alla sottoscrizione dei criteri appartenenti alla categoria di criteri. Ai fini di questa lezione, solo il database Finance deve sottoscrivere i criteri Nome Finance.  

    ![Gestire le categorie di criteri](Media/lesson-2-create-and-apply-a-naming-standards-policy/manage-policy-categories.png)
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="subscribe-to-the-finance-policy-category"></a>Sottoscrivere la categoria di criteri Finance  
  
1.  In Esplora oggetti, espandere **Database**, fare clic con il pulsante destro del mouse su **Finance**, scegliere **Criteri**e fare clic su **Categorie**. 

   ![Categorie di criteri Finance](Media/lesson-2-create-and-apply-a-naming-standards-policy/finance-categories.png)
  
2.  Selezionare la casella di controllo **Sottoscritto** per la categoria **Finance** .  

   ![Criteri Finance sottoscritti](Media/lesson-2-create-and-apply-a-naming-standards-policy/subscribe-to-finance.png)
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="test-the-enforcement-of-the-finance-name-policy"></a>Verificare l'applicazione dei criteri Nome Finance  
  
1.  In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]aprire una finestra di query. Eseguire le istruzioni seguenti che consentono di creare una tabella che viola i criteri **Nome Finance** . La tabella viola i criteri perché il nome della tabella non inizia con le lettere **fintbl**.  
  
    ```sql  
    USE Finance ;  
    GO  
    CREATE TABLE NewTable  
    (Col1 int) ;  
    GO    
    ```  
  
    Si noti che i criteri impediscono la creazione della tabella e restituiscono un messaggio informativo indicante il nome dei criteri. 

   ```
     Policy 'Finance Name' has been violated by 'SQLSERVER:\SQL\SQL\SQL2017\Databases\Finance\Tables\dbo.NewTable'.
     This transaction will be rolled back.
     Policy condition: '@Name LIKE 'fintbl%''
     Policy description: 'Tables names in the Finance database must contain 'fintbl%''.
     Additional help: '' : ''
     Statement: 'CREATE TABLE NewTable  
         (Col1 int)'.
     Msg 515, Level 16, State 2, Procedure msdb.sys.sp_syspolicy_execute_policy, Line 69 [Batch Start Line 2]
     Cannot insert the value NULL into column 'target_query_expression', table 'msdb.dbo.syspolicy_policy_execution_history_details_internal'; column does not allow nulls. INSERT fails.
     The statement has been terminated.
   ``` 
  
2.  Per specificare un nome valido, modificare il codice nel modo indicato di seguito ed eseguire nuovamente l'istruzione.  
  
    ```sql  
    USE Finance ;  
    GO  
    CREATE TABLE fintblNewTable  
    (Col1 int) ;  
    GO    
    ```  
  
    Questa modifica consente la creazione della tabella.  
  
## <a name="apply-the-policy-to-the-whole-server"></a>Applicare i criteri all'intero server  
  
1.  Solo il database Finance sottoscrive attualmente la categoria di criteri Finance. In molti casi è più facile applicare la categoria di criteri all'intero server. In Esplora oggetti espandere **Gestione**, fare clic con il pulsante destro del mouse su **Gestione criteri**e scegliere **Gestione categorie**.  
  
2.  Nella finestra di dialogo **Gestione categorie di criteri** individuare la categoria Finance e selezionare la casella di controllo **Imponi sottoscrizioni di database** per la categoria.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] La categoria Finance si applica ora a tutti i database, ma la condizione creata in precedenza limita i criteri Nome Finance al database Finance. In questo esempio viene illustrato come utilizzare combinazioni complesse di condizioni per i criteri in modalità valide per molti server.  
  
## <a name="summary"></a>Summary  
In questa esercitazione è stato illustrato come creare condizioni, criteri e gruppi di criteri della gestione basata su criteri e come applicare filtri e verificare la conformità delle destinazioni della gestione basata su criteri.  
  
## <a name="next"></a>Avanti  
L'esercitazione è completata. Per tornare all'inizio, vedere [Esercitazione: Amministrazione di server tramite la gestione basata su criteri](../../relational-databases/policy-based-management/tutorial-administering-servers-by-using-policy-based-management.md).  
  
Per un elenco delle esercitazioni, vedere [Esercitazioni di SQL Server 2016](../../sql-server/tutorials-for-sql-server-2016.md).  
  
## <a name="see-also"></a>Vedere anche  
[Amministrazione di server tramite la gestione basata su criteri](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)