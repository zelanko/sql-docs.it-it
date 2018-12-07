---
title: Creare e gestire sottoscrizioni per server di report in modalità nativa | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- standard subscriptions [Reporting Services]
- subscriptions [Reporting Services], standard
ms.assetid: 5ab1c661-9bfa-434a-b315-faac34ed12b1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cc5d22756ce35acb3469dbf385a5a21e3c969ef0
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52400904"
---
# <a name="create-and-manage-subscriptions-for-native-mode-report-servers"></a>Creare e gestire sottoscrizioni per server di report in modalità nativa
  Il termine sottoscrizione standard si riferisce alla sottoscrizione creata dai singoli utenti che desiderano che un report venga recapitato tramite posta elettronica o a una cartella condivisa. In questo argomento vengono fornite informazioni sulle sottoscrizioni standard che vengono create e gestite dai singoli utenti. Le sottoscrizioni guidate dai dati prevedono procedure e requisiti diversi e sono illustrate in un altro argomento. Per altre informazioni, vedere [Come creare, modificare ed eliminare le sottoscrizioni guidate dai dati](../../reporting-services/subscriptions/create-modify-and-delete-data-driven-subscriptions.md)  
  
 **Contenuto dell'argomento:**  
  
-   [Requisiti generali per le sottoscrizioni](#bkmk_create_subscription)  
  
-   [Per creare una sottoscrizione con recapito tramite condivisione file](#bkmk_create_fileshare_subscription)  
  
-   [Per creare una sottoscrizione con recapito tramite posta elettronica](#bkmk_create_email_subscription)  
  
-   [Per modificare una sottoscrizione](#bkmk_modify_subscription)  
  
-   [Per eliminare una sottoscrizione](#bkmk_delete_subscription)  
  
##  <a name="bkmk_create_subscription"></a> Requisiti generali per le sottoscrizioni  
 Il contenuto in questo argomento spiega come creare sottoscrizioni in un server di report in modalità nativa utilizzando Gestione report [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Dopo avere definito una sottoscrizione, è possibile accedervi in Gestione report tramite la pagina Sottoscrizioni personali oppure la scheda **Sottoscrizioni** di un report specifico.  
  
 [Creare e gestire sottoscrizioni per server di report in modalità SharePoint](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md) illustra come usare le pagine dell'applicazione in un sito di SharePoint per sottoscrivere report in un server di report in modalità SharePoint.  
  
-   Per utilizzare il recapito tramite posta elettronica, è necessario che il server di report sia configurato per una connessione tramite un server SMTP o gateway prima di creare la sottoscrizione.  
  
-   Per utilizzare il recapito tramite condivisione file, è necessario aver già definito la cartella di destinazione. Per altre informazioni, vedere [Configurare un server di report per il recapito tramite posta elettronica (Gestione configurazione SSRS)](https://msdn.microsoft.com/b838f970-d11a-4239-b164-8d11f4581d83).  
  
 Per sottoscrivere un report, è necessario che l'origine dati del report sia configurata per l'utilizzo di credenziali archiviate o di nessuna credenziale. Per altre informazioni, vedere [Archiviare le credenziali in un'origine dati di Reporting Services](../../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md). Se non le utilizza, il pulsante **Nuova sottoscrizione** non è disponibile.  
  
 In questo argomento non viene illustrato come creare una sottoscrizione guidata dai dati. Per istruzioni sulla creazione di una sottoscrizione guidata dai dati, vedere [Creare una sottoscrizione guidata dai dati &#40;esercitazione su SSRS&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md) o la Guida online per la pagina Creazione di una sottoscrizione guidata dai dati in Gestione report.  
  
###  <a name="bkmk_create_fileshare_subscription"></a> Per creare una sottoscrizione con recapito tramite condivisione file  
  
1.  Avviare [Gestione report &#40;modalità nativa SSRS&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
2.  Passare al report che si vuole sottoscrivere. Fare clic sul menu del report e fare clic su **Sottoscrivi**.  
  
     ![menu report](../../reporting-services/subscriptions/media/ssrs-report-menu-report-manager.png "menu report")  
  
3.  **Descrizione**: digitare una descrizione per il report composta da un massimo di 512 caratteri.  
  
4.  **Proprietario**: il campo del proprietario viene impostato sull'utente corrente per impostazione predefinita e non può essere modificato quando si crea la sottoscrizione. Dopo aver salvato la sottoscrizione, tuttavia, è possibile modificare le proprietà di sottoscrizione, tra cui il proprietario e la descrizione.  
  
5.  **Recapito**: selezionare **Condivisione file di Windows**.  
  
6.  **Nome file**: digitare un nome di file per il report.  
  
7.  **Aggiungi estensione file alla creazione del file**: questa opzione consente di aggiungere un'estensione di tre caratteri al nome del file. L'estensione del file dipende dal formato di output del report selezionato.  
  
8.  **Percorso**: digitare il percorso UNC (Universal Naming Convention) di una cartella esistente a cui si vuole che vengano recapitati i report, ad esempio \\\\<nomeserver\>\\<reportpersonali\>. Includere due barre rovesciate all'inizio del percorso e non specificare una barra rovesciata finale.  
  
     ![sottoscrizione di condivisione di file](../../reporting-services/subscriptions/media/ssrs-file-share-subscription.png "sottoscrizione di condivisione di file")  
  
9. **Formato di rendering**: selezionare un formato di output del report per il recapito del file. Selezionare un formato corrispondente all'applicazione desktop che verrà utilizzata per aprire il report. Evitare formati che non eseguono il rendering del report in un singolo flusso o che introducono elementi di interattività non supportati in un file statico, ad esempio il formato HTML 4.0.  
  
10. **Credenziali**: selezionare questa opzione per usare l'account di condivisione file o le credenziali di un utente di Windows specifico. L'opzione **Usa l'account di condivisione file** è disabilitata se l'amministratore dei report non ha configurato un account di condivisione file. Per altre informazioni, vedere [Impostazioni di sottoscrizione e un account di condivisione file &#40;Gestione configurazione&#41;](../../reporting-services/install-windows/subscription-settings-and-a-file-share-account-configuration-manager.md). Nelle caselle di testo **Nome utente** e **Password** specificare le credenziali richieste per accedere alla condivisione file usando il formato *\<dominio>*\\*\<nome utente>* per il nome utente.  
  
11. **Opzioni sovrascrittura**:  
  
    -   **Non sovrascrivere il file se esiste una versione precedente**, il recapito non verrà eseguito in presenza di un file esistente.  
  
    -   **Incrementa nomi dei file man mano che vengono aggiunte nuove versioni**, il server di report aggiunge un numero al nome del file per distinguerlo dai file esistenti con lo stesso nome.  
  
12. **Pianificazione**: specificare quando si vuole che il report venga recapitato:  
  
    -   Per pianificare un recapito, fare clic su **Quando viene completata l'esecuzione pianificata del report** , quindi sul pulsante **Seleziona pianificazione** . Verrà aperta una pagina di pianificazione.  
  
    -   Per selezionare una pianificazione condivisa per cui sono già stabilite la data, l'ora e le informazioni sull'occorrenza da utilizzare, fare clic su **In base a una pianificazione condivisa**, quindi selezionare la pianificazione da utilizzare.  
  
    -   Per recapitare il report quando lo snapshot di un report viene aggiornato con una versione più recente, fare clic su**Quando il contenuto del report viene aggiornato**. Se si sottoscrive un report che recupera dati a intervalli programmati, la pianificazione utilizzata per aggiornare i dati determina il momento dell'elaborazione della sottoscrizione.  
  
        > [!NOTE]  
        >  Questa opzione è disponibile solo per gli snapshot già associati a una pianificazione di aggiornamento.  
  
13. Per i report con parametri, specificare i parametri da utilizzare per il report di questa sottoscrizione. I parametri possono essere diversi da quelli utilizzati per l'esecuzione del report su richiesta o in altre operazioni pianificate.  
  
 Il report viene recapitato come file statico. Se include funzionalità interattive, ad esempio collegamenti a righe e colonne aggiuntive, tali funzionalità non saranno disponibili.  
  
###  <a name="bkmk_create_email_subscription"></a> Per creare una sottoscrizione con recapito tramite posta elettronica  
  
1.  Avviare [Gestione report &#40;modalità nativa SSRS&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
2.  Passare al report che si vuole sottoscrivere. Fare clic sul menu del report e fare clic su **Sottoscrivi**.  
  
     ![menu report](../../reporting-services/subscriptions/media/ssrs-report-menu-report-manager.png "menu report")  
  
3.  **Descrizione**: digitare una descrizione per il report composta da un massimo di 512 caratteri.  
  
4.  **Proprietario**: il campo del proprietario viene impostato sull'utente corrente per impostazione predefinita e non può essere modificato quando si crea la sottoscrizione. Dopo aver salvato la sottoscrizione, tuttavia, è possibile modificare le proprietà di sottoscrizione, tra cui il proprietario e la descrizione.  
  
5.  **Recapito**: selezionare **Messaggio di posta elettronica**. Se l'opzione **Messaggio di posta elettronica** non è disponibile, il server di report non è stato configurato per le sottoscrizioni tramite posta elettronica. Vedere [Configurare un server di report per il recapito tramite posta elettronica (Gestione configurazione SSRS)](https://msdn.microsoft.com/b838f970-d11a-4239-b164-8d11f4581d83)  
  
6.  **A**: il nome del destinatario nel campo A viene compilato automaticamente con l'account utente di dominio. Verificare che il formato sia [nome utente]@[dominio.com]. Le impostazioni di configurazione del server di report determinano se il campo **A** : viene compilato con l'account utente corrente. Per altre informazioni sulla modifica delle impostazioni di configurazione di indirizzi di posta elettronica, vedere [Configurare un server di report per il recapito tramite posta elettronica (Gestione configurazione SSRS)](https://msdn.microsoft.com/b838f970-d11a-4239-b164-8d11f4581d83).  
  
    > [!NOTE]  
    >  A seconda delle autorizzazioni, può essere possibile digitare l'indirizzo di posta elettronica cui si desidera recapitare il report. Per specificare più indirizzi di posta elettronica, separarli con un punto e virgola (;). È anche possibile digitare indirizzi di posta elettronica supplementari nelle caselle di testo **Cc**, **Ccn**e **Risposta** . A questo fine è necessario disporre dell'autorizzazione per la gestione di tutte le sottoscrizioni.  
  
7.  **Oggetto**: l'impostazione predefinita è "@ReportName eseguito alle ore @ExecutionTime". È possibile modificare l'oggetto ma si noti che @ReportName e @ExecutionTime sono le uniche variabili globali supportate nel campo **Oggetto**.  
  
8.  Selezionare le opzioni di recapito come segue:  
  
    -   **Includi report**: selezionare questa opzione per incorporare o allegare una copia del report. Il formato del report dipende dal formato di output di rendering selezionato. Non selezionare questa opzione se si ritiene che le dimensioni del report possano essere superiori al limite impostato per il sistema di posta elettronica.  
  
    -   **Includi collegamento**: selezionare questa opzione per includere l'URL del report nel corpo del messaggio di posta elettronica.  
  
    > [!NOTE]  
    >  Se entrambe le opzioni vengono deselezionate, verrà inviato solo il testo della notifica nella riga Oggetto.  
  
9. Selezionare un formato di rendering dalla casella di riepilogo **Formato di rendering** . Questa opzione è disponibile se viene selezionato **Includi report** per incorporare o allegare una copia del report.  
  
    -   Per incorporare il report nel corpo del messaggio di posta elettronica, selezionare **Archivio Web**.  
  
    -   Per inviare il report come allegato, selezionare uno degli altri formati di rendering.  
  
10. Selezionare una priorità dall'elenco di riepilogo **Priorità** . In [!INCLUDE[msCoName](../../includes/msconame-md.md)] Exchange questa impostazione consente di specificare un flag per il livello di importanza del messaggio di posta elettronica.  
  
11. Specificare quando si desidera che il report venga recapitato:  
  
    -   Per pianificare un'ora per il recapito, fare clic su **Quando viene completata l'esecuzione pianificata del report** , quindi su **Seleziona pianificazione**. Verrà aperta una pagina di pianificazione.  
  
    -   Per selezionare una pianificazione condivisa per cui sono già stabilite la data, l'ora e le informazioni sull'occorrenza da utilizzare, fare clic su **In base a una pianificazione condivisa**, quindi selezionare la pianificazione da utilizzare.  
  
    -   Per recapitare il report quando lo snapshot di un report viene aggiornato con una versione più recente, fare clic su**Quando il contenuto del report viene aggiornato**. Se si sottoscrive un report che recupera dati a intervalli programmati, la pianificazione utilizzata per aggiornare i dati determina il momento dell'elaborazione della sottoscrizione.  
  
    > [!NOTE]  
    >  Questa opzione è disponibile solo per gli snapshot già associati a una pianificazione di aggiornamento.  
  
12. Per i report con parametri, specificare i parametri da utilizzare per il report di questa sottoscrizione. I parametri specificati possono essere diversi da quelli utilizzati per l'esecuzione del report su richiesta o in altre operazioni pianificate.  
  
##  <a name="bkmk_modify_subscription"></a> Per modificare una sottoscrizione  
 Una sottoscrizione può essere modificata in qualsiasi momento. Se si modifica una sottoscrizione mentre viene elaborata, le impostazioni aggiornate vengono usato solo se vengono salvate nel server di report prima che l'estensione per il recapito riceva i dati della sottoscrizione. In caso contrario, vengono utilizzate le impostazioni esistenti.  
  
 L'utente che crea una sottoscrizione diventa automaticamente il proprietario di tale sottoscrizione e può pertanto modificarla o eliminarla. È possibile modificare il proprietario del report dalla pagina delle proprietà di sottoscrizione oppure è possibile modificare la proprietà a livello di codice. Per ulteriori informazioni, vedere quanto segue:  
  
-   [Usare PowerShell per modificare ed elencare i proprietari di sottoscrizioni di Reporting Services ed eseguire una sottoscrizione](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)  
  
-   <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A>  
  
 Per individuare una sottoscrizione, utilizzare la pagina **Sottoscrizioni personali** oppure visualizzare le definizioni della sottoscrizione associate a un report. Non è possibile individuare una sottoscrizione eseguendo ricerche dirette o altri tipi di ricerche, ad esempio in base al nome del proprietario, al trigger, alle informazioni sullo stato e così via.  
  
 Le sottoscrizioni possono inoltre essere modificate o eliminate dagli amministratori del server di report.  
  
> [!NOTE]  
>  Un amministratore del server di report non può gestire da un'unica posizione tutte le sottoscrizioni individuali che sono utilizzate in un determinato server di report. Può tuttavia accedere a ogni sottoscrizione per modificarla o eliminarla.  
  
##  <a name="bkmk_delete_subscription"></a> Per eliminare una sottoscrizione  
 Per eliminare una sottoscrizione  
  
1.  Avviare [Gestione report &#40;modalità nativa SSRS&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
2.  In Gestione report fare clic su **Sottoscrizioni personali** sulla barra degli strumenti e passare alla sottoscrizione da modificare o eliminare.  
  
3.  Aprire il menu del report e fare clic su **Elimina**.  
  
     ![menu report](../../reporting-services/subscriptions/media/ssrs-report-menu-report-manager.png "menu report")  
  
 Per annullare una sottoscrizione in corso di elaborazione nel server di report, vedere [Gestire un processo in esecuzione](../../reporting-services/subscriptions/manage-a-running-process.md).  
  
 Se si vuole interrompere una sottoscrizione e non si riesce a individuarla, prendere nota del nome del report che si riceve e cercare il report usando il nome come criterio di ricerca. Dopo aver ottenuto l'accesso al report, sarà possibile annullare la propria sottoscrizione. Se non è possibile individuarla, la sottoscrizione potrebbe essere guidata dai dati. Per ulteriori informazioni, rivolgersi all'amministratore del server di report.  
  
 Una sottoscrizione viene eliminata automaticamente quando viene eliminato il report a cui è associata. Se la sottoscrizione viene eliminata durante l'elaborazione, viene arrestata se l'operazione di eliminazione viene eseguita prima che l'estensione per il recapito riceva i dati della sottoscrizione. In caso contrario, l'elaborazione verrà portata a termine.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare e gestire sottoscrizioni per server di report in modalità SharePoint](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)   
 [Usare PowerShell per modificare ed elencare i proprietari di sottoscrizioni di Reporting Services ed eseguire una sottoscrizione](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)   
 [Data-Driven Subscriptions](../../reporting-services/subscriptions/data-driven-subscriptions.md)   
 [Sottoscrizioni e recapito &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Gestione report &#40;modalità nativa SSRS&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [Usare Sottoscrizioni personali &#40;server di report in modalità nativa&#41;](../../reporting-services/subscriptions/use-my-subscriptions-native-mode-report-server.md)  
  
  
