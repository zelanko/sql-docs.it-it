---
title: 'Attività 1 (prerequisito): Rimozione dei dati fornitore in MDS | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 6f0a4287-7fd4-4f18-b7e4-a5191a9d4a3c
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 19e402f1b74f72ce962aaa95f5f48794ffb7c154
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63222516"
---
# <a name="task-1-prerequisite-removing-supplier-data-in-mds"></a>Attività 1 (prerequisito): Rimozione dei dati fornitore in MDS
  In questa attività vengono rimossi i dati fornitore archiviati in MDS. È stato caricato i dati manualmente usando **componente aggiuntivo MDS per Excel** nella lezione precedente. Tramite il pacchetto SSIS creato durante questa lezione i dati vengono caricati automaticamente in MDS. Pertanto, prima di testare il pacchetto SSIS, è necessario rimuovere i dati fornitore da MDS, la gerarchia derivata, le entità Supplier e State e creare l'entità Supplier senza alcun dato.  
  
1.  Avvio veloce **gestione dati Master** passando a **http://localhost/MDS** o il sito Web e dell'applicazione specificato durante la configurazione di MDS. Se il **gestione dati Master** aperto, fare clic su **SQL Server 2012 Master Data Services** nella parte superiore per passare al **home page di**.  
  
2.  Fare clic su **Amministrazione sistema** nel **le attività amministrative** sezione.  
  
3.  Posizionare il mouse sopra **Manage** del menu e fare clic su **gerarchie derivate**. È necessario eliminare la gerarchia derivata **SuppliersInState** prima di eliminare le entità nel **Suppliers** modello.  
  
4.  Selezionare **SuppliersInState** dalle **gerarchia derivata** elenco e fare clic su **X (Elimina)** pulsante sulla barra degli strumenti.  
  
5.  Fare clic su **OK** per confermare l'eliminazione.  
  
6.  Posizionare il mouse sopra **Manage** del menu e fare clic su **entità**.  
  
7.  Fare clic su **Supplier** e fare clic su **Elimina (X)** sulla barra degli strumenti per eliminare l'entità. Fare clic su **OK** nelle finestre di messaggio.  
  
8.  Ripetere il passaggio precedente per eliminare **stato** entità.  
  
9. Non chiudere **gestione dati Master**.  
  
10. Passare alla finestra di Excel che dispone **Cleansed and Matched Suppliers. xls** file aperto. Passare al **Sheet1** scheda nella parte inferiore.  
  
11. Selezionare solo le **prima di tutto di riga con intestazioni**. Non selezionare nessun'altra riga. Si desidera creare entità basate sulle colonne di Excel senza caricare alcun dato. Pertanto, selezionare solo la prima riga con le intestazioni.  
  
12. Fare clic su **dati Master** nella barra dei menu.  
  
13. Fare clic su **Crea entità** dalla barra multifunzione.  
  
14. Nelle **Gestisci connessioni** finestra di dialogo, se non è possibile visualizzare la connessione al **server MDS locale** sotto **connessioni esistenti**, eseguire le operazioni seguenti:  
  
    1.  Selezionare **creare una nuova connessione**, fare clic su **New** pulsante.  
  
    2.  Nella finestra di dialogo Aggiungi nuova connessione, digitare **Server MDS locale** per **descrizione** e **http://localhost/MDS** per **indirizzo server MDS**, Fare clic su **OK** per chiudere la finestra di dialogo.  
  
15. Nelle **Gestisci connessioni** finestra di dialogo **Server MDS locale** (http://localhost/MDS), fare clic su **testare** per testare la connessione. Fare clic su **OK** nella finestra di messaggio.  
  
16. Fare clic su **Connect** per stabilire una connessione al server MDS.  
  
17. Nel **Crea entità** dialogo casella, eseguire le operazioni seguenti:  
  
    1.  Verificare che **Range** è impostata su **$1: $1**.  
  
    2.  Selezionare **Suppliers** per **modello**.  
  
    3.  Selezionare **VERSION_1** per **versione**.  
  
    4.  Tipo di **Supplier** per **Nome nuova entità**.  
  
    5.  Selezionare **SupplierID** per **codice**.  
  
    6.  Selezionare **Supplier Name** per **nome**.  
  
    7.  Fare clic su **OK** per creare l'entità e chiudere la finestra di dialogo.  
  
18. Chiusura **Excel** e **non salvare** il file.  
  
19. Nelle **gestione dati Master**, aggiornare il browser internet e verificare che **Supplier** entità viene visualizzata nell'elenco.  
  
20. Passare al **homepage** facendo clic **SQL Server 2012 Master Data Services** nella parte superiore.  
  
21. Verificare che **Suppliers** modello selezionato per **Model** e **VERSION_1** sia selezionato per **versione**.  
  
22. Fare clic su **Esplora**. Si noti che il **Supplier** entità con tutti gli attributi viene creata con **senza valori**.  
  
## <a name="next-step"></a>Passaggio successivo  
 [Attività 2 &#40;facoltativo&#41;: Creazione di viste sottoscrizioni MDS tramite Gestione dati Master](../../2014/tutorials/task-2-optional-creating-a-mds-subscription-view-using-master-data-manager.md)  
  
  
