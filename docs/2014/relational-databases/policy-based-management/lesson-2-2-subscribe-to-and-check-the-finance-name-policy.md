---
title: Sottoscrivere e verificare criteri Nome Finance | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 126b4c4c-2a1c-4701-a0ad-8de23fbd7306
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f1b91c1d46bc4a396a8b0358a1a3bf3aa8acbcd8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63135701"
---
# <a name="subscribe-to-and-check-the-finance-name-policy"></a>Sottoscrizione e verifica di criteri Nome Finance
  In questa attività verrà configurato il database Finance per la sottoscrizione della categoria di criteri Finance. Verranno quindi verificati i criteri Nome Finance.  
  
### <a name="to-subscribe-to-the-finance-policy-category"></a>Per sottoscrivere la categoria di criteri Finance  
  
1.  In Esplora oggetti, espandere **database**, fare doppio clic su `Finance`, scegliere **criteri**, quindi fare clic su **categorie**.  
  
2.  Selezionare il **sottoscritto** casella di controllo di `Finance` categoria.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-test-the-enforcement-of-the-finance-name-policy"></a>Per verificare l'applicazione dei criteri Nome Finance  
  
1.  In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]aprire una finestra di query. Eseguire le istruzioni seguenti che consentono di creare una tabella che viola i criteri **Nome Finance** . La tabella viola i criteri perché il nome della tabella non inizia con le lettere **fintbl**.  
  
    ```  
    USE Finance ;  
    GO  
    CREATE TABLE NewTable  
    (Col1 int) ;  
    GO  
  
    ```  
  
     Si noti che i criteri impediscono la creazione della tabella e restituiscono un messaggio informativo indicante il nome dei criteri.  
  
2.  Per specificare un nome valido, modificare il codice nel modo indicato di seguito ed eseguire nuovamente l'istruzione.  
  
    ```  
    USE Finance ;  
    GO  
    CREATE TABLE fintblNewTable  
    (Col1 int) ;  
    GO  
  
    ```  
  
     Questa modifica consente la creazione della tabella.  
  
### <a name="to-apply-the-policy-to-the-whole-server"></a>Per applicare i criteri all'intero server  
  
1.  Solo il database Finance sottoscrive attualmente la categoria di criteri Finance. In molti casi è più facile applicare la categoria di criteri all'intero server. In Esplora oggetti espandere **Gestione**, fare clic con il pulsante destro del mouse su **Gestione criteri**e scegliere **Gestione categorie**.  
  
2.  Nella finestra di dialogo **Gestione categorie di criteri** individuare la categoria Finance e selezionare la casella di controllo **Imponi sottoscrizioni di database** per la categoria.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] La categoria Finance si applica ora a tutti i database, ma la condizione creata in precedenza limita i criteri Nome Finance al database Finance. In questo esempio viene illustrato come utilizzare combinazioni complesse di condizioni per i criteri in modalità valide per molti server.  
  
## <a name="summary"></a>Riepilogo  
 In questa esercitazione è stato illustrato come creare condizioni, criteri e gruppi di criteri della gestione basata su criteri e come applicare filtri e verificare la conformità delle destinazioni della gestione basata su criteri.  
  
## <a name="next"></a>Avanti  
 L'esercitazione è completata. Per tornare all'inizio, fare clic su [esercitazione: Amministrazione di server tramite la gestione basata su criteri](tutorial-administering-servers-by-using-policy-based-management.md).  
  
 Per un elenco di esercitazioni, vedere [esercitazioni per SQL Server 2014](../../tutorials/tutorials-for-sql-server-2014.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrazione di server tramite la gestione basata su criteri](administer-servers-by-using-policy-based-management.md)  
  
  
