---
title: Creare, modificare ed eliminare sottoscrizioni Standard (Reporting Services in modalità nativa) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- standard subscriptions [Reporting Services]
- subscriptions [Reporting Services], standard
ms.assetid: 5ab1c661-9bfa-434a-b315-faac34ed12b1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bd1404868213820d3ba3fc6d2715f7a8ae1c6716
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62511090"
---
# <a name="create-modify-and-delete-standard-subscriptions-reporting-services-in-native-mode"></a>Creare, modificare ed eliminare sottoscrizioni standard (Reporting Services in modalità nativa)
  Il termine sottoscrizione standard si riferisce alla sottoscrizione creata dai singoli utenti che desiderano che un report venga recapitato tramite posta elettronica o a una cartella condivisa. Una sottoscrizione standard viene sempre definita tramite il report su cui si basa.  
  
 L'utente che crea una sottoscrizione diventa automaticamente il proprietario di tale sottoscrizione e può pertanto modificarla o eliminarla.  
  
> [!NOTE]  
>  A partire da [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], è possibile trasferire la proprietà di una sottoscrizione a livello di programmazione. Non è disponibile alcuna interfaccia utente da utilizzare per trasferire la proprietà delle sottoscrizioni. Per altre informazioni, vedere <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A>  
  
 A seconda delle impostazioni del file di configurazione **RSReportServer.config** , potrebbe essere possibile aggiungere altri utenti a una sottoscrizione. Un responsabile potrebbe ad esempio aggiungere gli indirizzi di posta elettronica dei propri subalterni in modo che possano ricevere una copia del report. Questa funzionalità è supportata se il campo A: è visibile durante la definizione delle singole sottoscrizioni. Per altre informazioni, vedere [configurare un Server di Report per il recapito tramite posta elettronica &#40;Gestione configurazione SSRS&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md).  
  
 In questo argomento vengono fornite informazioni sulle sottoscrizioni standard che vengono create e gestite dai singoli utenti. Le sottoscrizioni guidate dai dati prevedono procedure e requisiti diversi e sono illustrate in un altro argomento. Per altre informazioni, vedere [creare, modificare ed eliminare una sottoscrizione guidata dai dati](data-driven-subscriptions.md).  
  
 Contenuto dell'argomento:  
  
-   [Per creare una sottoscrizione](#bkmk_create_subscription)  
  
-   [Per creare una sottoscrizione con recapito tramite condivisione file](#bkmk_create_fileshare_subscription)  
  
-   [Per creare una sottoscrizione con recapito tramite posta elettronica](#bkmk_create_email_subscription)  
  
-   [Per modificare una sottoscrizione](#bkmk_modify_subscription)  
  
-   [Per eliminare una sottoscrizione](#bkmk_delete_subscription)  
  
##  <a name="bkmk_create_subscription"></a> Per creare una sottoscrizione  
 Per creare una sottoscrizione, scegliere lo strumento e l'approccio validi per la distribuzione del server di report:  
  
-   Il contenuto in questo argomento spiega come creare sottoscrizioni in un server di report in modalità nativa utilizzando Gestione report [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Dopo avere definito una sottoscrizione, è possibile accedervi in Gestione report tramite la pagina Sottoscrizioni personali oppure la scheda **Sottoscrizioni** di un report specifico.  
  
-   [Creare e gestire sottoscrizioni per server di Report in modalità SharePoint](create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md) spiega come usare le pagine dell'applicazione in un sito di SharePoint per sottoscrivere report in un server di report eseguito in modalità integrata SharePoint.  
  
 In questo argomento vengono fornite le istruzioni per creare una sottoscrizione con recapito tramite posta elettronica e una sottoscrizione con recapito tramite condivisione file.  
  
-   Per utilizzare il recapito tramite posta elettronica, è necessario che il server di report sia configurato per una connessione tramite un server SMTP o gateway prima di creare la sottoscrizione.  
  
-   Per utilizzare il recapito tramite condivisione file, è necessario aver già definito la cartella di destinazione. Per altre informazioni, vedere [configurare un Server di Report per il recapito tramite posta elettronica &#40;Gestione configurazione SSRS&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md).  
  
 Per sottoscrivere un report, è necessario che l'origine dati del report sia configurata per l'utilizzo di credenziali archiviate o di nessuna credenziale. Per altre informazioni, vedere [Archiviare le credenziali in un'origine dati di Reporting Services](../report-data/store-credentials-in-a-reporting-services-data-source.md). Se non le utilizza, il pulsante **Nuova sottoscrizione** non è disponibile.  
  
 In questo argomento non viene illustrato come creare una sottoscrizione guidata dai dati. Per istruzioni sulla creazione di una sottoscrizione guidata dai dati, vedere [Creare una sottoscrizione guidata dai dati &#40;esercitazione su SSRS&#41;](../create-a-data-driven-subscription-ssrs-tutorial.md) o la Guida online per la pagina Creazione di una sottoscrizione guidata dai dati in Gestione report.  
  
###  <a name="bkmk_create_fileshare_subscription"></a> Per creare una sottoscrizione con recapito tramite condivisione file  
  
1.  Avviare [Gestione report &#40;modalità nativa SSRS&#41;](../report-manager-ssrs-native-mode.md).  
  
2.  Nella pagina **Contenuto** di Gestione report passare al report che si desidera sottoscrivere. Fare clic sul report per aprirlo.  
  
3.  Fare clic sulla scheda **Sottoscrizioni** e quindi fare clic su **Nuova sottoscrizione**.  
  
4.  In **Recapito**selezionare **Condivisione file di Windows**.  
  
5.  In **Nome file**digitare un nome di file per il report.  
  
6.  Selezionare l'opzione **Aggiungi estensione file alla creazione del file**. Questa opzione consente di specificare un'estensione di tre caratteri per il nome del file. L'estensione del file dipende dal formato di output del report selezionato.  
  
7.  Nel **tracciato** testo, digitare un percorso Universal Naming Convention (UNC) per una cartella esistente in cui si desidera recapitare il report (ad esempio, \\ \\< servername\>\\< MyReports\>). Includere due barre rovesciate all'inizio del percorso e non specificare una barra rovesciata finale.  
  
8.  In Formato di rendering selezionare un formato di output del report per il recapito del file. Selezionare un formato corrispondente all'applicazione desktop che verrà utilizzata per aprire il report. Evitare formati che non eseguono il rendering del report in un singolo flusso o che introducono elementi di interattività non supportati in un file statico, ad esempio il formato HTML 4.0.  
  
9. Nelle caselle di testo **Nome utente** e **Password** specificare le credenziali richieste per accedere alla condivisione file usando il formato *\<dominio>*\\*\<nome utente>* per il nome utente.  
  
10. Specificare le opzioni di sovrascrittura. Se si fa clic su **Non sovrascrivere il file se esiste una versione precedente**il recapito non verrà eseguito in presenza di un file esistente. Se si seleziona **Incrementa nomi dei file man mano che vengono aggiunte nuove versioni**, il server di report aggiunge un numero al nome del file per distinguerlo dai file esistenti con lo stesso nome.  
  
11. Specificare quando si desidera che il report venga recapitato:  
  
    -   Per pianificare un recapito, fare clic su **Quando viene completata l'esecuzione pianificata del report** , quindi sul pulsante **Seleziona pianificazione** . Verrà aperta una pagina di pianificazione.  
  
    -   Per selezionare una pianificazione condivisa per cui sono già stabilite la data, l'ora e le informazioni sull'occorrenza da utilizzare, fare clic su **In base a una pianificazione condivisa**, quindi selezionare la pianificazione da utilizzare.  
  
    -   Per recapitare il report quando lo snapshot di un report viene aggiornato con una versione più recente, fare clic su**Quando il contenuto del report viene aggiornato**. Se si sottoscrive un report che recupera dati a intervalli programmati, la pianificazione utilizzata per aggiornare i dati determina il momento dell'elaborazione della sottoscrizione.  
  
        > [!NOTE]  
        >  Questa opzione è disponibile solo per gli snapshot già associati a una pianificazione di aggiornamento.  
  
12. Per i report con parametri, specificare i parametri da utilizzare per il report di questa sottoscrizione. I parametri possono essere diversi da quelli utilizzati per l'esecuzione del report su richiesta o in altre operazioni pianificate.  
  
 Il report viene recapitato come file statico. Se include funzionalità interattive, ad esempio collegamenti a righe e colonne aggiuntive, tali funzionalità non saranno disponibili.  
  
###  <a name="bkmk_create_email_subscription"></a> Per creare una sottoscrizione con recapito tramite posta elettronica  
  
1.  Nella pagina **Contenuto** di Gestione report passare al report che si desidera sottoscrivere. Fare clic sul report per aprirlo.  
  
2.  Fare clic sulla scheda **Sottoscrizioni** e quindi fare clic su **Nuova sottoscrizione**.  
  
3.  In **Recapito**selezionare **Messaggio di posta elettronica**. Se questo tipo di recapito non è disponibile, il server di report non è stato configurato per le sottoscrizioni tramite posta elettronica.  
  
4.  Nella casella di testo **A** il nome del destinatario nel campo A: viene riempito automaticamente con l'account utente di dominio. Le impostazioni di configurazione del server di report determinano se il campo **A** viene riempito con l'account utente corrente. Per altre informazioni sulla modifica di indirizzi di posta elettronica impostazioni di configurazione, vedere [configurare un Server di Report per il recapito tramite posta elettronica &#40;Gestione configurazione SSRS&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md).  
  
    > [!NOTE]  
    >  A seconda delle autorizzazioni, può essere possibile digitare l'indirizzo di posta elettronica cui si desidera recapitare il report. Per specificare più indirizzi di posta elettronica, separarli con un punto e virgola (;). È anche possibile digitare indirizzi di posta elettronica supplementari nelle caselle di testo **Cc**, **Ccn**e **Risposta** . A questo fine è necessario disporre dell'autorizzazione per la gestione di tutte le sottoscrizioni.  
  
5.  Selezionare le opzioni di recapito come segue:  
  
    -   Per incorporare o allegare una copia del report, selezionare **Includi report**. Il formato del report dipende dal formato di output di rendering selezionato. Non selezionare questa opzione se si ritiene che le dimensioni del report possano essere superiori al limite impostato per il sistema di posta elettronica.  
  
    -   Selezionare **Includi collegamento**per includere l'URL del report nel corpo del messaggio di posta elettronica.  
  
    > [!NOTE]  
    >  Se entrambe le opzioni vengono deselezionate, verrà inviato solo il testo della notifica nella riga Oggetto.  
  
6.  Selezionare un formato di rendering dalla casella di riepilogo **Formato di rendering** . Questa opzione è disponibile se viene selezionato **Includi report** per incorporare o allegare una copia del report.  
  
    -   Per incorporare il report nel corpo del messaggio di posta elettronica, selezionare **Archivio Web**.  
  
    -   Per inviare il report come allegato, selezionare uno degli altri formati di rendering.  
  
7.  Selezionare una priorità dall'elenco di riepilogo **Priorità** . In [!INCLUDE[msCoName](../../includes/msconame-md.md)] Exchange questa impostazione consente di specificare un flag per il livello di importanza del messaggio di posta elettronica.  
  
8.  Specificare quando si desidera che il report venga recapitato:  
  
    -   Per pianificare un'ora per il recapito, fare clic su **Quando viene completata l'esecuzione pianificata del report** , quindi su **Seleziona pianificazione**. Verrà aperta una pagina di pianificazione.  
  
    -   Per selezionare una pianificazione condivisa per cui sono già stabilite la data, l'ora e le informazioni sull'occorrenza da utilizzare, fare clic su **In base a una pianificazione condivisa**, quindi selezionare la pianificazione da utilizzare.  
  
    -   Per recapitare il report quando lo snapshot di un report viene aggiornato con una versione più recente, fare clic su**Quando il contenuto del report viene aggiornato**. Se si sottoscrive un report che recupera dati a intervalli programmati, la pianificazione utilizzata per aggiornare i dati determina il momento dell'elaborazione della sottoscrizione.  
  
    > [!NOTE]  
    >  Questa opzione è disponibile solo per gli snapshot già associati a una pianificazione di aggiornamento.  
  
9. Per i report con parametri, specificare i parametri da utilizzare per il report di questa sottoscrizione. I parametri specificati possono essere diversi da quelli utilizzati per l'esecuzione del report su richiesta o in altre operazioni pianificate.  
  
##  <a name="bkmk_modify_subscription"></a> Per modificare una sottoscrizione  
 Una sottoscrizione può essere modificata in qualsiasi momento. Se si modifica una sottoscrizione mentre viene elaborata, le impostazioni aggiornate vengono utilizzate solo se vengono salvate nel database del server di report prima che l'estensione per il recapito riceva i dati della sottoscrizione. In caso contrario, vengono utilizzate le impostazioni esistenti.  
  
 Per individuare una sottoscrizione, utilizzare la pagina **Sottoscrizioni personali** oppure visualizzare le definizioni della sottoscrizione associate a un report. Non è possibile individuare una sottoscrizione eseguendo ricerche dirette o altri tipi di ricerche, ad esempio in base al nome del proprietario, al trigger, alle informazioni sullo stato e così via.  
  
 Le sottoscrizioni possono inoltre essere modificate o eliminate dagli amministratori del server di report.  
  
> [!NOTE]  
>  Un amministratore del server di report non può gestire da un'unica posizione tutte le sottoscrizioni individuali che sono utilizzate in un determinato server di report. Può tuttavia accedere a ogni sottoscrizione per modificarla o eliminarla.  
  
##  <a name="bkmk_delete_subscription"></a> Per eliminare una sottoscrizione  
 Per eliminare una sottoscrizione  
  
1.  Avviare [Gestione report &#40;modalità nativa SSRS&#41;](../report-manager-ssrs-native-mode.md).  
  
2.  In Gestione report fare clic su **Sottoscrizioni personali** sulla barra degli strumenti principale e passare alla sottoscrizione che si desidera modificare o eliminare.  
  
3.  In alternativa, nella scheda **Sottoscrizioni** di un report aperto individuare la sottoscrizione che si desidera modificare o eliminare. Eseguire una delle operazioni seguenti:  
  
    1.  Per modificare una sottoscrizione, fare clic su **Modifica**.  
  
    2.  Per eliminare una sottoscrizione, selezionare la casella di controllo accanto alla sottoscrizione e quindi fare clic su **Elimina**.  
  
 In questo argomento non vengono fornite informazioni sulle modalità di annullamento di una sottoscrizione in corso di elaborazione nel server di report. Per altre informazioni sull'annullamento di sottoscrizioni, vedere [gestire un processo in esecuzione](manage-a-running-process.md)  
  
 Se si desidera interrompere una sottoscrizione e non si riesce a individuarla in modo semplice, annotare il nome del report che si riceve e cercare il report utilizzando il nome come criterio di ricerca. Dopo aver ottenuto l'accesso al report, sarà possibile annullare la propria sottoscrizione. Se non è possibile individuarla, la sottoscrizione potrebbe essere guidata dai dati. Per ulteriori informazioni, rivolgersi all'amministratore del server di report.  
  
 Una sottoscrizione viene eliminata automaticamente quando viene eliminato il report a cui è associata. Se la sottoscrizione viene eliminata durante l'elaborazione, viene arrestata se l'operazione di eliminazione viene eseguita prima che l'estensione per il recapito riceva i dati della sottoscrizione. In caso contrario, l'elaborazione verrà portata a termine.  
  
## <a name="see-also"></a>Vedere anche  
 [Attività e autorizzazioni](../security/tasks-and-permissions.md)   
 [Create and Manage Subscriptions for SharePoint Mode Report Servers](create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)   
 [Creare e gestire sottoscrizioni per server di report in modalità nativa](../create-manage-subscriptions-native-mode-report-servers.md)   
 [Data-Driven Subscriptions](data-driven-subscriptions.md)   
 [Sottoscrizioni e recapito &#40;Reporting Services&#41;](subscriptions-and-delivery-reporting-services.md)   
 [Gestione report &#40;modalità nativa SSRS&#41;](../report-manager-ssrs-native-mode.md)   
 [Usare Sottoscrizioni personali](use-my-subscriptions-native-mode-report-server.md)  
  
  
