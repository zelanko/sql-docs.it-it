---
title: Creare criteri Nome Finance | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 56b2c852-fd69-4cd2-9b5d-977467b94fd9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a4484f9ccb76ea31c95a5392570e18df2c4b0ff5
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792908"
---
# <a name="create-the-finance-name-policy"></a>Creazione di criteri Nome Finance
  In questa attività verrà creato un database denominato Finance, quindi una condizione per cui tutti i nomi di tabella devono iniziare con le lettere **fintbl**. Verranno quindi creati i criteri e una categoria di criteri per applicare uno standard di denominazione per le tabelle del database Finance.  
  
### <a name="to-create-the-finance-database"></a>Per creare il database Finance  
  
1.  In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]aprire una finestra di query ed eseguire l'istruzione seguente:  
  
    ```  
    CREATE DATABASE Finance ;  
    GO  
    ```  
  
2.  In Esplora oggetti fare clic su **Database**, quindi premere F5 per aggiornare l'elenco dei database.  
  
### <a name="to-create-the-finance-tables-condition"></a>Per creare la condizione Tabelle Finance  
  
1.  In Esplora oggetti espandere **Gestione**, espandere **Gestione criteri**, fare clic con il pulsante destro del mouse su **Condizioni**e quindi scegliere **Nuova condizione**.  
  
2.  Nella finestra di dialogo **Crea nuova condizione** , nella casella **Nome** digitare **Tabelle Finance**.  
  
3.  Nell'elenco **Facet** selezionare **Nome a più parti**.  
  
4.  Nel **espressione** area, nella **campo** , quindi selezionare  **\@nome**; nella **operatore** , quindi selezionare  **Ad esempio**; e il **valore** , digitare **'fintbl %'** forzare tutti i nomi di tabella inizino con le lettere **fintbl**.  
  
5.  Nella pagina **Descrizione** digitare **I nomi di tabella del database Finance devono iniziare con fintbl**e quindi scegliere **OK** per creare la condizione.  
  
### <a name="to-create-the-finance-name-policy"></a>Per creare i criteri Nome Finance  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse su **Criteri**, quindi scegliere **Nuovi criteri**.  
  
2.  Nella finestra di dialogo **Crea nuovi criteri** , nella casella **Nome** digitare **Nome Finance**.  
  
3.  Nell'elenco **Condizione di controllo** selezionare **Tabelle Finance**. Questa opzione è disponibile nell'area **Nome a più parti** .  
  
4.  Nell'area **In base a** viene visualizzato un elenco di oggetti di database che hanno applicato i criteri. Selezionare la casella di controllo **Ogni tabella**.  
  
5.  Nell'area **Ogni database** espandere **Ogni**e fare clic su **Nuova condizione**.  
  
6.  Nella finestra di dialogo **Crea nuova condizione** , nella casella **Nome** digitare **Database Finance**.  
  
7.  Nel **espressione** completare l'espressione affinché includa  **\@Name = 'Finance'** , quindi fare clic su **OK** per chiudere la pagina della condizione.  
  
    > [!NOTE]  
    >  Potrebbe essere necessario uscire dalla casella **Valore** premendo TAB per abilitare il pulsante **OK** .  
  
8.  Nell'elenco **Modalità di valutazione** selezionare **Su modifica: impedisci esecuzione**. Questa opzione consente di applicare i criteri tramite la creazione di un trigger di database nel database Finance.  
  
9. Selezionare l'elenco **Abilitato** . (La casella **Abilitato** non si applica ai criteri **Su richiesta** .)  
  
10. Nell'elenco **Restrizione server** selezionare **Nessuna**.  
  
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-create-the-finance-policy-category"></a>Per creare la categoria di criteri Finance  
  
1.  In Esplora oggetti espandere **Gestione**, fare clic con il pulsante destro del mouse su **Gestione criteri**e scegliere **Gestione categorie**.  
  
2.  Nel **Gestione categorie di criteri** nella finestra di dialogo **Name**, digitare `Finance` nella casella vuota e quindi deselezionare **Imponi sottoscrizioni di Database**. Con**Imponi sottoscrizioni di database** ogni database nell'istanza verrà forzato alla sottoscrizione dei criteri appartenenti alla categoria di criteri. Ai fini di questa lezione, solo il database Finance deve sottoscrivere i criteri Nome Finance.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Sottoscrizione e verifica di criteri Nome Finance](lesson-2-2-subscribe-to-and-check-the-finance-name-policy.md)  
  
  
