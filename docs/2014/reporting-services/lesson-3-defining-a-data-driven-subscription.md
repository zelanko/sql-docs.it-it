---
title: 'Lesson 3: Defining a Data-Driven Subscription (Lezione 3: Definizione di una sottoscrizione guidata dai dati) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 89197b9b-7502-4fe2-bea3-ed7943eebf3b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ee51a19d1dc169d2ae784d8a44403e021ff8b665
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108513"
---
# <a name="lesson-3-defining-a-data-driven-subscription"></a>Lesson 3: Defining a Data-Driven Subscription
  In questa lezione verranno utilizzate le pagine di sottoscrizione guidate dai dati per connettersi a un'origine dei dati di sottoscrizione, verrà compilata una query che recupera i dati di sottoscrizione e sarà eseguito il mapping tra il set di risultati e le opzioni di recapito e del report.  
  
> [!NOTE]  
>  Prima di iniziare, verificare che il servizio [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent sia in esecuzione. Se non è in esecuzione, non è possibile salvare la sottoscrizione.  
  
 In questa lezione si presuppone che le lezioni 1 e 2 siano state completate e che l'origine dati del report utilizzi credenziali archiviate.  Per altre informazioni, vedere [Lezione 2: Modifica delle proprietà dell'origine dei dati del report](../reporting-services/lesson-2-modifying-the-report-data-source-properties.md)  
  
 In questo argomento  
  
-   [Avviare la creazione guidata sottoscrizione guidata dai dati](#bkmk_startwizard)  
  
-   [Passaggio 1: Definire una descrizione](#bkmk_definesubscription)  
  
-   [Passaggio 2: Definire una connessione all'origine dati del Sottoscrittore](#bkmk_defineconnectiontosubscriber)  
  
-   [Passaggio 3: Definire una query per il recupero dei dati del Sottoscrittore](#bkmk_definequery)  
  
-   [Passaggio 4: Impostare le opzioni di recapito](#bkmk_set_deliveryoptions)  
  
-   [Passaggio 5: Configurare un valore del parametro per variare l'output del report](#bkmk_configure_parameter)  
  
-   [Passaggio 6: Per pianificare una sottoscrizione](#bkmk_schedule_subscription)  
  
##  <a name="bkmk_startwizard"></a>Avviare la creazione guidata sottoscrizione guidata dai dati  
  
1.  In Gestione report fare clic su **Home**e passare alla cartella contenente il report **Ordini vendita** .  
  
2.  Nel menu di scelta rapida del report fare clic su **Gestisci**, quindi fare clic sulla scheda **Sottoscrizioni** .  
  
3.  Fare clic su **nuova sottoscrizione guidata dai dati**. Se il pulsante non è visualizzato, non si dispone delle autorizzazioni di Gestione contenuto.  
  
##  <a name="bkmk_definesubscription"></a>Passaggio 1: definire una descrizione  
  
1.  Digitare **Recapito ordine di vendita** nella descrizione.  
  
2.  Selezionare **Condivisione file di Windows** per **Specificare la modalità di notifica ai destinatari**.  
  
3.  Selezionare **Specificare solo per questa sottoscrizione**, quindi fare clic su **Avanti**.  
  
##  <a name="bkmk_defineconnectiontosubscriber"></a>Passaggio 2: definire una connessione all'origine dati del Sottoscrittore  
  
1.  Selezionare **Microsoft SQL Server** come tipo di origine dei dati.  
  
2.  In Stringa di connessione digitare la stringa di connessione seguente:  
  
    ```  
    data source=localhost; initial catalog=Subscribers  
    ```  
  
    > [!NOTE]  
    >  Subscribers è il database creato nella lezione 1.  
  
3.  Fare clic su **Credenziali archiviate in modo protetto nel server di report**.  
  
4.  In **Nome utente** e **Password**digitare nome utente e password per il dominio. In **Nome utente**specificare sia il dominio che l'account utente.  
  
    > [!NOTE]  
    >  Le credenziali utilizzate per connettersi a un'origine dati del Sottoscrittore non vengono restituite a [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]. Se in seguito si modifica la sottoscrizione, sarà necessario immettere nuovamente la password utilizzata per la connessione all'origine dei dati.  
  
5.  Selezionare **Usa come credenziali di Windows per la connessione all'origine dei dati**e quindi fare clic su **Avanti**.  
  
##  <a name="bkmk_definequery"></a>Passaggio 3: definire una query per recuperare i dati del Sottoscrittore  
  
1.  Nella casella della query digitare la query seguente:  
  
    ```  
    Select * from OrderInfo  
    ```  
  
2.  Specificare un timeout di 30 secondi.  
  
3.  Fare clic su **Convalida**e quindi su **Avanti**.  
  
##  <a name="bkmk_set_deliveryoptions"></a>Passaggio 4: impostare le opzioni di recapito  
  
1.  Per **Nome file**selezionare **Estrai il valore dal database**. Selezionare il campo **Ordine**.  
  
2.  Per **Percorso**selezionare **Specificare un valore statico**. In Valore impostazione digitare il nome di una condivisione file pubblica per la quale si dispone di autorizzazioni di scrittura, ad esempio `\\mycomputer\public\myreports`.  
  
3.  Per **Formato di rendering**selezionare **Estrai il valore dal database**. Selezionare **Formato**.  
  
4.  Per **Modalità scrittura**selezionare **Specificare un valore statico** e scegliere **Incremento automatico**.  
  
5.  Per **Estensione file**selezionare **Specificare un valore statico** e scegliere **True**.  
  
6.  Per **Nome utente**selezionare **Specificare un valore statico**. Digitare l'account utente di dominio. Immetterlo nel formato `<domain>\<account>`. L'account utente deve disporre delle autorizzazioni per il percorso configurato nei passaggi precedenti.  
  
7.  Per **Password**selezionare **Specificare un valore statico**. Digitare la password. Prestare attenzione quando si digita la password poiché non viene convalidata durante la procedura guidata.  
  
8.  Fare clic su **Avanti**.  
  
##  <a name="bkmk_configure_parameter"></a>Passaggio 5: configurare un valore di parametro per l'output del report  
  
1.  Per **OrderNumber**selezionare **Estrai il valore dal database**. In Valore selezionare **Ordine**. Fare clic su **Avanti**.  
  
##  <a name="bkmk_schedule_subscription"></a>Passaggio 6: per pianificare una sottoscrizione  
  
1.  Fare clic su **In base a una pianificazione creata per questa sottoscrizione**, quindi fare clic su **Avanti**.  
  
2.  In **Dettagli pianificazione**fare clic su **Singola occorrenza**.  
  
3.  Specificare un'ora di inizio posticipata di alcuni minuti rispetto all'ora corrente.  
  
4.  Fare clic su **Fine**.  
  
## <a name="next-steps"></a>Passaggi successivi  
 Quando la sottoscrizione viene eseguita, nella condivisione file specificata vengono recapitati quattro file di report, uno per ogni ordine nell'origine dati *Sottoscrittori* . Ogni recapito deve essere univoco in termini di dati (che devono essere specifici dell'ordine), di formato di visualizzazione e di formato di file. È possibile aprire tutti i report dalla cartella condivisa per verificare che ogni versione sia personalizzata in base alle opzioni di sottoscrizione definite.  
  
 ![Elenco di file creati dalla sottoscrizione](../../2014/tutorials/media/ssrs-tutorial-datadriven-subscription-filelist.gif "Elenco di file creati dalla sottoscrizione")  
  
 La pagina di sottoscrizione in Gestione report conterrà la data dell' **Ultima esecuzione** e lo **Stato** della sottoscrizione.  
  
> [!NOTE]  
>  Aggiornare la pagina dopo l'esecuzione della sottoscrizione per visualizzare le informazioni aggiornate.  
  
 ![Risultati della sottoscrizione in Gestione report](../../2014/tutorials/media/ssrs-tutorial-datadriven-subscription-status-reportmanager.gif "Risultati della sottoscrizione in Gestione report")  
  
 Questo passaggio conclude l'esercitazione relativa alla definizione di una sottoscrizione guidata dai dati. Per ulteriori informazioni sulle altre [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] esercitazioni, vedere [Reporting Services esercitazioni &#40;&#41;SSRS ](../reporting-services/reporting-services-tutorials-ssrs.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di una sottoscrizione guidata dai dati &#40;esercitazione su SSRS&#41;](../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)   
 [Sottoscrizioni e recapito &#40;Reporting Services&#41;](subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Data-Driven Subscriptions](subscriptions/data-driven-subscriptions.md)   
 [Creazione, modifica ed eliminazione di una sottoscrizione guidata dai dati](subscriptions/create-modify-and-delete-data-driven-subscriptions.md)   
 [Utilizzare un'origine dati esterna per i dati del Sottoscrittore &#40;sottoscrizione guidata dai dati&#41;](subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)  
  
  
