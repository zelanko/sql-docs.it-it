---
title: Ricerca e visualizzazione dei report in Gestione Report (Generatore Report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 8556807e-f2e2-4a7b-bb1b-ac5ea1872e51
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 22d183aa8ddbad06b0dc949bfe1780f360eb96ba
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66107870"
---
# <a name="finding-and-viewing-reports-in-report-manager-report-builder-and-ssrs"></a>Ricerca e visualizzazione di report in Gestione report (Generatore report e SSRS)
  Gestione report è uno strumento basato sul Web in cui sono disponibili funzionalità per la visualizzazione e la gestione dei report. Fa parte di un'installazione del server di report. Per aprire Gestione report, digitare l'URL relativo in una finestra del browser. Per informazioni sui requisiti del browser, vedere [Planning for Reporting Services e supporto Browser per Power View &#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md). Per ulteriori informazioni sulla configurazione di un URL di Gestione report nel server di report, rivolgersi all'amministratore di sistema. Per altre informazioni, vedere [Configurare Gestione report &#40;modalità nativa&#41;](../report-server/configure-web-portal.md).  
  
 Le autorizzazioni che l'amministratore di sistema ha impostato sul server di report determinano gli elementi che vengono visualizzati quando si utilizza Gestione report. Le autorizzazioni vengono concesse tramite un'assegnazione di ruolo. Per individuare e visualizzare report, è necessario disporre di un'assegnazione di ruolo che includa l'attività Visualizzazione di report. Per individuare un report in un server di report, cercarlo in base al nome o alla descrizione oppure esplorare le cartelle del server di report. È possibile cercare o individuare solo report pubblicati o caricati nel server di report. Per altre informazioni su come eseguire la ricerca di un report, vedere [Ricerca di report e altri elementi &#40;Generatore report e SSRS&#41;](searching-for-reports-and-other-items-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="navigating-the-folder-hierarchy-in-report-manager"></a>Navigazione della gerarchia delle cartelle in Gestione report  
 Per individuare i report che si desidera eseguire, è possibile utilizzare la Home page, visualizzata automaticamente quando si avvia Gestione report e quando si apre una qualsiasi cartella nella gerarchia delle cartelle. Nella Home page vengono visualizzati solo gli elementi per i quali si dispone delle autorizzazioni per la visualizzazione. Il percorso delle cartelle viene invece indicato come sequenza di collegamenti nella parte superiore della Home page. I nomi delle cartelle sono elencati in sequenza a partire dalla cartella radice (Home). Quando si apre un'altra cartella, il nome di tale cartella viene aggiunto al percorso indicato nella parte superiore della pagina. **(1)** nell'immagine illustrata di seguito. Se si apre un report, anche il nome del report viene aggiunto al percorso della cartella.  
  
 ![Barra multifunzione e navigazione in Gestione report](../media/rs-reportmanager-ribbon.gif "Barra multifunzione e navigazione in Gestione report")  
Barra multifunzione di Gestione report  
  
 Per navigare in una gerarchia di cartelle, utilizzare le tecniche seguenti:  
  
-   Per visualizzare il contenuto di una cartella, fare clic sul nome della cartella nella pagina Home page. Verrà aperta la pagina della cartella in cui è visualizzato il contenuto della cartella.  
  
-   Per esplorare un livello inferiore della gerarchia di cartelle, aprire una sottocartella della cartella corrente. Le cartelle possono contenere report, risorse, origini dei dati condivise e altre cartelle. È possibile fare clic sull'icona di una cartella per aprirla e visualizzare il contenuto del livello immediatamente inferiore della gerarchia.  
  
-   Per tornare a un livello superiore della gerarchia di cartelle, nella sequenza di collegamenti nella parte superiore della pagina fare clic sul nome della cartella di cui si desidera visualizzare il contenuto. **(1)** nell'immagine precedente.  
  
## <a name="opening-a-report"></a>Apertura di un report  
 Dopo avere individuato un report, fare clic sul nome per aprirlo. Il report, di cui viene eseguito il rendering in formato HTML, viene visualizzato nella pagina Contenuto in Gestione report. I report vengono sempre memorizzati nella cache per ogni sessione del browser. Ciò significa che se si apre un report è in genere possibile tornarvi tramite il pulsante **Indietro** . Questa possibilità è disponibile anche se sono stati richiesti nome utente e password per l'esecuzione del report. Un report visualizzabile viene quindi chiuso effettivamente solo quando si chiude il browser.  
  
 Non tutti i report visibili nella gerarchia delle cartelle sono immediatamente accessibili. Per alcuni report potrebbe essere richiesta l'immissione di nome utente e password per verificare se l'utente può accedere all'origine dati per il report. Per altre informazioni sull'apertura di report in Gestione Report, vedere [Aprire e chiudere un report &#40;Gestione report&#41;](../reports/open-and-close-a-report-report-manager.md).  
  
 È inoltre possibile individuare e aprire un report direttamente dal server di report in Generatore report. Per altre informazioni, vedere [Ricerca di report e altri elementi &#40;Generatore report e SSRS&#41;](searching-for-reports-and-other-items-report-builder-and-ssrs.md).  
  
## <a name="to-search-for-a-items"></a>Per cercare elementi  
  
-   Per cercare elementi in Gestione report, digitare una stringa di ricerca nella casella di testo **Cerca** nella parte superiore della pagina. **(2)** nell'immagine precedente. Le ricerche iniziano dal nodo principale della gerarchia di cartelle e proseguono in ogni ramo. Se non si dispone delle autorizzazioni per l'accesso a un ramo specifico, questo viene ignorato. Questa regola è valida per le cartelle Report personali appartenenti ad altri utenti e per altre cartelle che in genere non sono disponibili. Nei risultati delle ricerche sono inclusi solo i report e gli elementi che l'utente che esegue la ricerca è autorizzato a visualizzare.  
  
-   Per cercare un elemento in base al nome o alla descrizione, specificare tutto il testo per il quale si desidera trovare una corrispondenza o solo parte di esso. La stringa di ricerca non supporta la distinzione tra maiuscole e minuscole. Non è possibile usare operatori di ricerca quali i segni di addizione (+) o di sottrazione (–) per includere o escludere i criteri di ricerca.  
  
-   Per cercare testo specifico all'interno di un report, utilizzare la barra degli strumenti nella parte superiore del report.  
  
## <a name="see-also"></a>Vedere anche  
 [Ricerca di report e altri elementi &#40;Generatore report e SSRS&#41;](searching-for-reports-and-other-items-report-builder-and-ssrs.md)   
 [Ricerca, visualizzazione e gestione dei report &#40;Generatore report SSRS&#41;](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
