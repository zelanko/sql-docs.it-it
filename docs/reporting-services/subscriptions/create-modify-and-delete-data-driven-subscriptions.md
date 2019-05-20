---
title: Creare, modificare ed eliminare le sottoscrizioni guidate dai dati | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- query-based subscriptions [Reporting Services]
- queries [Reporting Services], data-driven subscriptions
- subscriptions [Reporting Services], data-driven
- data-driven subscriptions
ms.assetid: 0ba2093e-9393-4eb6-af06-9da10988cfaf
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: dc07797030f18527178c2041ccfd8c8732d8d47c
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65578247"
---
# <a name="create-modify-and-delete-data-driven-subscriptions"></a>Come creare, modificare ed eliminare le sottoscrizioni guidate dai dati
  Una sottoscrizione guidata dai dati è una sottoscrizione basata su query che recupera i valori dei dati utilizzati per l'elaborazione della sottoscrizione in fase di esecuzione. Quando la sottoscrizione viene attivata, viene elaborata una query per recuperare informazioni aggiornate su destinatari, opzioni di recapito di report, formati di rendering e impostazioni dei parametri. I risultati della query vengono combinati con la definizione della sottoscrizione per creare una sottoscrizione dinamica che utilizza i dati già gestiti dall'utente in un database dei dipendenti, un database dei clienti o altri database contenenti informazioni che possono essere utilizzate come dati del sottoscrittore.  
  
 Per creare una nuova sottoscrizione guidata dai dati o modificarne una esistente, utilizzare le pagine relative in Gestione report. Queste pagine consentono di eseguire in modo semplice i vari passaggi per la creazione o la modifica di una sottoscrizione. Per accedere a una sottoscrizione dopo averla creata, utilizzare la pagina Sottoscrizioni personali e l'elenco delle sottoscrizioni di un report. Per informazioni su come creare una sottoscrizione guidata dai dati, vedere [Creare una sottoscrizione guidata dai dati &#40;esercitazione su SSRS&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md).  
  
 Contenuto dell'argomento:  
  
-   [Gestione ed eliminazione di una sottoscrizione guidata dai dati](#bkmk_manage_and_delete)  
  
-   [Creazione e modifica di una sottoscrizione guidata dai dati](#bkmk_create_and_modify)  
  
-   [Definizione di una query che recupera le informazioni sulla sottoscrizione](#bkmk_define_query)  
  
-   [Esecuzione della sottoscrizione](#bkmk_run_subscription)  
  
##  <a name="bkmk_manage_and_delete"></a> Gestione ed eliminazione di una sottoscrizione guidata dai dati  
 Una sottoscrizione guidata dai dati in corso non può essere arrestata o eliminata tramite la pagina Gestisci processi di Gestione report. Per questa ragione, è vantaggioso utilizzare una pianificazione condivisa per attivare una sottoscrizione guidata dai dati. In questo modo, se si desidera impedire temporaneamente l'elaborazione di una sottoscrizione, è possibile sospendere la pianificazione che ne determina l'attivazione. Per altre informazioni, vedere [old_Creare e gestire sottoscrizioni per server di report in modalità nativa](https://msdn.microsoft.com/7f46cbdb-5102-4941-bca2-5e0ff9012c6b).  
  
 Per eliminare una sottoscrizione guidata dai dati, selezionarla nella pagina Sottoscrizioni personali o nella pagina Sottoscrizioni di un report e quindi fare clic su **Elimina**.  
  
 Per istruzioni sull'annullamento di una sottoscrizione guidata dai dati, vedere [Gestire un processo in esecuzione](../../reporting-services/subscriptions/manage-a-running-process.md).  
  
##  <a name="bkmk_create_and_modify"></a> Creazione e modifica di una sottoscrizione guidata dai dati  
 Per creare una sottoscrizione guidata dai dati, selezionare un report che utilizza credenziali archiviate o nessuna credenziale. Quando si crea la sottoscrizione guidata dai dati, considerare di utilizzare una convenzione di denominazione per il campo di descrizione in modo da poter facilmente differenziare le sottoscrizioni standard dalle sottoscrizioni guidate dai dati.  
  
#### <a name="to-create-a-data-driven-subscription-native-mode"></a>Per creare una sottoscrizione guidata dai dati (modalità nativa)  
  
1.  In Gestione report, passare alla cartella contenente il report, posizionare il puntatore del mouse sul report, aprire il menu delle opzioni e fare clic su **Gestisci**.  
  
2.  Fare clic sulla scheda **Sottoscrizioni** .  
  
3.  Fare clic sul pulsante **Nuova sottoscrizione guidata dai dati** .  
  
#### <a name="to-create-a-data-driven-subscription-sharepoint-mode"></a>Per creare una sottoscrizione guidata dai dati (modalità SharePoint)  
  
1.  Nella raccolta documenti di SharePoint, posizionare il puntatore del mouse sul report, aprire il menu delle opzioni e fare clic su **Gestisci sottoscrizioni**.  
  
2.  Fare clic su **Aggiungi sottoscrizione guidata dai dati**.  
  
#### <a name="to-modify-an-existing-data-driven-subscription-native-mode"></a>Per modificare una sottoscrizione guidata dai dati esistente (modalità nativa)  
  
1.  In Gestione report, passare alla cartella contenente il report, posizionare il puntatore del mouse sul report, aprire il menu delle opzioni e fare clic su **Gestisci**.  
  
2.  Fare clic sulla scheda **Sottoscrizioni** . In alternativa, fare clic sul collegamento **Sottoscrizioni personali** nella parte superiore di Gestione report.  
  
3.  Selezionare la sottoscrizione che si desidera modificare. L'icona seguente indica una sottoscrizione guidata dai dati: ![Icona della sottoscrizione guidata dai dati](../../reporting-services/subscriptions/media/hlp-16subscriptiondd.gif "Icona della sottoscrizione guidata dai dati")  
  
#### <a name="to-modify-an-existing-data-driven-subscription-sharepoint-mode"></a>Per modificare una sottoscrizione guidata dai dati esistente (modalità SharePoint)  
  
1.  Nella raccolta documenti di SharePoint, posizionare il puntatore del mouse sul report, aprire il menu delle opzioni e fare clic su **Gestisci sottoscrizioni**.  
  
2.  Selezionare la sottoscrizione che si desidera modificare.  
  
> [!NOTE]  
>  È possibile modificare qualsiasi valore già specificato. Tutti i valori vengono visualizzati come al momento della loro creazione, ad eccezione della password che viene utilizzata per accedere all'archivio dati del sottoscrittore. È infatti necessario immettere la password ogni volta che si modificano i valori nella seconda pagina o in una pagina successiva.  
  
 Prima di creare una sottoscrizione guidata dai dati, verificare che siano soddisfatti i requisiti seguenti:  
  
-   **Requisiti per i report**. Per poter recuperare i dati in fase di esecuzione, è necessario che per il report vengano utilizzate credenziali archiviate oppure nessuna credenziale. Per connettersi a un'origine dei dati esterna, non è possibile sottoscrivere un report che utilizza credenziali rappresentate o delegate. Le credenziali dell'utente che crea la sottoscrizione o ne è proprietario non saranno disponibili durante l'elaborazione della sottoscrizione. Le credenziali archiviate possono essere un account di Windows o un account utente del database. Per altre informazioni, vedere [Specificare le credenziali e le informazioni sulla connessione per le origini dati del report](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md).  
  
     Non è possibile sottoscrivere un report di Generatore report che utilizza come origine dei dati un modello contenente impostazioni di sicurezza degli elementi del modello. La restrizione riguarda solo i report che utilizzano la sicurezza degli elementi del modello.  
  
     Non è possibile creare una sottoscrizione guidata dai dati in un report che contiene l'espressione `User!UserID` .  
  
-   **Requisiti per i dati**. È necessario disporre di un'origine dei dati esterna accessibile che contenga i dati del sottoscrittore.  
  
-   **Requisiti per gli utenti**. L'autore della sottoscrizione deve disporre dell'autorizzazione per la gestione dei report e di tutte le sottoscrizioni. Per altre informazioni sulle autorizzazioni per attività a livello di elemento, vedere [Attività e autorizzazioni](../../reporting-services/security/tasks-and-permissions.md). L'autore deve inoltre disporre delle credenziali necessarie per l'accesso all'origine dei dati esterna contenente i dati del sottoscrittore.  
  
##  <a name="bkmk_define_query"></a> Definizione di una query che recupera le informazioni sulla sottoscrizione  
 In una sottoscrizione guidata dai dati è necessario specificare una query o un comando che recupera i dati del sottoscrittore. La query dovrebbe produrre una riga per ogni sottoscrittore. Se si utilizza l'estensione per il recapito tramite posta elettronica, la query dovrebbe restituire un alias di posta elettronica valido per ogni sottoscrittore. Il numero di recapiti effettuati si basa sul numero di righe restituite dalla query. Se il set di righe contiene 10.000 righe, significa che la sottoscrizione determina il recapito di 10.000 report.  
  
 Se l'elaborazione della query richiede tempi particolarmente lunghi, è possibile aumentare il valore di timeout per consentire il proseguimento delle operazioni di elaborazione.  
  
 In questo passaggio, è necessario che la query venga convalidata per poter continuare. L'operazione di convalida non determina l'elaborazione della query, ma solo la restituzione dell'elenco di tutte le colonne presenti nel set di righe, in modo che sia possibile fare riferimento alle colonne durante le successive operazioni di selezione. Se la query non viene convalidata, non è possibile proseguire. La query non viene convalidata se la sintassi della query non è corretta o la connessione all'origine dei dati non è valida. Utilizzare il pulsante **Indietro** per apportare correzioni all'origine dei dati.  
  
##  <a name="bkmk_run_subscription"></a> Esecuzione della sottoscrizione  
 È necessario specificare le condizioni per l'elaborazione della sottoscrizione. È possibile specificare una pianificazione oppure fare in modo che la sottoscrizione venga attivata in corrispondenza degli aggiornamenti a uno snapshot dell'esecuzione del report. Le modalità di elaborazione delle sottoscrizioni guidate dai dati sono uguali a quelle delle sottoscrizioni standard.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare e gestire sottoscrizioni per server di report in modalità nativa](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)   
 [Sottoscrizioni e recapito &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Gestione report &#40;modalità nativa SSRS&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [old_Creare e gestire sottoscrizioni per server di report in modalità nativa](https://msdn.microsoft.com/7f46cbdb-5102-4941-bca2-5e0ff9012c6b)   
 [Pagina Sottoscrizioni &#40;Gestione report&#41;](https://msdn.microsoft.com/library/cf3a6bd0-e0b2-4875-a532-63ef34cfa860)   
 [Pagina Sottoscrizioni personali &#40;Gestione report&#41;](https://msdn.microsoft.com/library/491a85a3-f323-4155-a0a8-de2779899995)  
  
  
