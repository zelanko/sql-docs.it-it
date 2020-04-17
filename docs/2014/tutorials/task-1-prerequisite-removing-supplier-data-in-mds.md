---
title: 'Attività 1 (Prerequisito): Rimozione dei dati dei fornitori in MDS . Documenti Microsoft'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 6f0a4287-7fd4-4f18-b7e4-a5191a9d4a3c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 0290f033be47bec61e9ccce8465892d8cc98608c
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81484631"
---
# <a name="task-1-prerequisite-removing-supplier-data-in-mds"></a>Attività 1 (prerequisito): Rimozione dei dati fornitore in MDS
  In questa attività vengono rimossi i dati fornitore archiviati in MDS. I dati sono stati caricati manualmente utilizzando il componente **aggiuntivo MDS di Excel** nella lezione precedente. Tramite il pacchetto SSIS creato durante questa lezione i dati vengono caricati automaticamente in MDS. Pertanto, prima di testare il pacchetto SSIS, è necessario rimuovere i dati fornitore da MDS, la gerarchia derivata, le entità Supplier e State e creare l'entità Supplier senza alcun dato.  
  
1.  Avviare **Master Data** Manager `http://localhost/MDS` o il sito Web e l'applicazione specificati durante la configurazione di MDS. Se Master **Data Manager** master è aperto, fare clic su **SQL Server 2012 Master Data Services** nella parte superiore per passare alla home **page.**  
  
2.  Fare clic su **Amministrazione sistema** nella sezione **Attività amministrative.**  
  
3.  Passare il mouse su **Gestisci** dal menu e scegliere **Gerarchie derivate**. È necessario eliminare la gerarchia derivata **SuppliersInState** prima di eliminare le entità nel modello Suppliers.You need to delete the derived hierarchy **SuppliersInState** before deleting the entities in the Suppliers model.  
  
4.  Selezionare **SuppliersInState** dall'elenco **Gerarchia derivata** e fare clic sul pulsante **X (Elimina)** sulla barra degli strumenti.  
  
5.  Fare clic **su OK** per confermare l'eliminazione.  
  
6.  Passare il mouse su **Gestisci** dal menu e fare clic su **Entità**.  
  
7.  Fare clic su **Fornitore** e quindi sul pulsante **Elimina (X)** sulla barra degli strumenti per eliminare l'entità. Fare clic **su OK** nelle finestre di messaggio.  
  
8.  Ripetere il passaggio precedente per eliminare l'entità **Stato.**  
  
9. Non chiudere **Master Data Manager**.  
  
10. Passare alla finestra di Excel con il file **Cleansed and Matched Suppliers.xls** aperto. Passare alla scheda **Foglio1** nella parte inferiore.  
  
11. Selezionare solo la **prima riga con intestazioni**. Non selezionare altre righe. Si desidera creare le entità in base alle colonne di Excel ma non si desidera caricare dati. Pertanto, selezionare solo la prima riga con le intestazioni.  
  
12. Fare clic su **Dati master** sulla barra dei menu.  
  
13. Fare clic su **Crea entità** sulla barra multifunzione.  
  
14. Nella finestra di dialogo **Gestisci connessioni,** se la connessione al **server MDS locale** non viene visualizzata in Connessioni **esistenti**, eseguire le operazioni seguenti:  
  
    1.  Selezionare **Crea una nuova connessione**e fare clic sul pulsante **Nuovo.**  
  
    2.  Nella finestra di dialogo Aggiungi nuova connessione digitare **Server MDS locale** per **Descrizione** e **\/http: /localhost/MDS** per **l'indirizzo del server MDS**, quindi fare clic **su OK** per chiudere la finestra di dialogo.  
  
15. Nella finestra di dialogo **Gestisci connessioni** selezionare **Server MDS locale** (`http://localhost/MDS`), fare clic su **Test** per verificare la connessione. Fare clic **su OK** nella finestra di messaggio.  
  
16. Fare clic su **Connetti** per creare una connessione al server MDS.  
  
17. Nella finestra di dialogo **Crea entità** eseguire le operazioni seguenti:  
  
    1.  Verificare che **L'intervallo** sia impostato su **1: 1**.  
  
    2.  Selezionare **Fornitori** per **Modello**.  
  
    3.  Selezionare **VERSION_1** per **Versione**.  
  
    4.  Digitare **Fornitore** per **Nuovo nome entità**.  
  
    5.  Selezionare **IDFornitore** per **Codice**.  
  
    6.  Selezionare **Nome fornitore** per **Nome**.  
  
    7.  Fare clic **su OK** per creare l'entità e chiudere la finestra di dialogo.  
  
18. Chiudere **Excel** e **non salvare** il file.  
  
19. In **Master Data Manager**, aggiornare il browser Internet e verificare che l'entità **Fornitore** sia visualizzata nell'elenco.  
  
20. Passare alla **home page** facendo clic su SQL Server **2012 Master Data Services** nella parte superiore.  
  
21. Verificare che il modello **Fornitori** sia selezionato per **Modello** e **VERSION_1** sia selezionato per **Versione**.  
  
22. Fare clic su **Esplora**. Si noti che l'entità **Supplier** con tutti gli attributi viene creata **senza valori**.  
  
## <a name="next-step"></a>passaggio successivo  
 [Attività 2 &#40;&#41; facoltativi: Creazione di una visualizzazione di sottoscrizione MDS tramite Master Data ManagerTask 2 to Optional&#41;: Creating a MDS Subscription View using Master Data Manager](../../2014/tutorials/task-2-optional-creating-a-mds-subscription-view-using-master-data-manager.md)  
  
  
