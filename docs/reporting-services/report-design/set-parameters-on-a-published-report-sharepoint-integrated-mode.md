---
title: Impostare i parametri in un report pubblicato - Modalità integrata SharePoint | Microsoft Docs
description: Informazioni su come impostare parametri ed eseguire un report con parametri, nella definizione del report o dopo la pubblicazione di questo, in Generatore report.
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
helpviewer_keywords:
- SharePoint integration [Reporting Services], content management
- report parameters [Reporting Services]
ms.assetid: dec5d985-a6c1-4dd8-8a66-a848e89a2e18
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a04058cc679d7697f2526c85b8b6526e8ea4a8ce
ms.sourcegitcommit: 02b22274da4a103760a376c4ddf26c4829018454
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/11/2020
ms.locfileid: "84681220"
---
# <a name="set-parameters-on-a-published-report---sharepoint-integrated-mode"></a>Impostare i parametri in un report pubblicato - Modalità integrata SharePoint
  Un report con parametri è un report che accetta valori di input, che verranno utilizzati per filtrare i dati durante l'esecuzione del report. I parametri vengono definiti al momento della creazione del report. A seconda di come sono definiti i parametri nella definizione del report, un report può accettare un solo valore, più valori o valori dinamici, che cambiano in risposta a una selezione precedente. Se ad esempio si sceglie una categoria di prodotti, la selezione successiva dovrà essere un prodotto specifico di tale categoria. Un parametro può avere un valore predefinito, che può essere utilizzato per eseguire automaticamente una versione filtrata del report o essere sostituito da un altro valore.  
  
 Tali proprietà possono essere impostate nella definizione del report o dopo la pubblicazione di quest'ultimo. Sebbene sia possibile modificare alcune proprietà dei parametri in un report pubblicato per cambiare il valore e le proprietà di visualizzazione, non è possibile modificare il tipo di dati o il nome di un parametro. Il tipo di dati e il nome del parametro possono essere modificati solo dall'autore del report nella definizione di quest'ultimo.  
  
 Per eseguire un report con parametri, è in genere necessario conoscere i valori da digitare, sebbene un report possa includere elenchi a discesa di valori validi tra cui scegliere.  
  
 Per impostare le proprietà dei parametri per un report pubblicato, è necessario disporre dell'autorizzazione Modifica elementi per il report. È possibile modificare alcune o tutte le proprietà dei parametri per un report che viene eseguito da un sito di SharePoint. Non è possibile personalizzare un report salvando una combinazione di valori dei parametri da utilizzare più volte. Tutti i valori predefiniti specificati vengono utilizzati da tutti gli utenti che aprono il report.  
  
 Se il report è incorporato in una web part Visualizzatore report configurata per visualizzare sempre tale report, impostare le proprietà nella web part Visualizzatore report. Per altre informazioni, vedere [Aggiungere la web part Visualizzatore di report a una pagina Web &#40;Reporting Services in modalità integrata SharePoint&#41;](../../reporting-services/report-server-sharepoint/add-the-report-viewer-web-part-to-a-web-page.md).  
  
### <a name="to-run-a-parameterized-report"></a>Per eseguire un report con parametri  
  
1.  Aprire la raccolta che contiene il report.  
  
2.  Fare clic sul nome del report. È necessario sapere in anticipo quali report dispongono di parametri. Non sono disponibili elementi di identificazione visivi che indichino la presenza di parametri per il report.  
  
3.  All'apertura del report, specificare i parametri da utilizzare. Il riquadro Parametri potrebbe risultare visibile, compresso o nascosto a seconda delle proprietà impostate nella web part Visualizzatore report.  
  
    1.  Se il riquadro Parametri è visibile, scegliere un valore per ogni parametro.  
  
    2.  Se è visualizzata una sottile striscia colorata disposta lungo il report e con una freccia al centro, significa che il riquadro Parametri è compresso. È possibile fare clic sulla freccia per espanderlo.  
  
    3.  Se il riquadro Parametri è nascosto, non è possibile specificare un valore.  
  
4.  Fare clic su **Applica** nella parte inferiore del riquadro Parametri per eseguire il report.  
  
     A volte la combinazione di valori specificata non restituisce i risultati previsti. Se non si ottengono le informazioni desiderate, potrebbe essere necessario richiedere all'autore di modificare il report.  
  
5.  Fare clic su **OK**.  
  
### <a name="to-set-parameter-properties"></a>Per impostare le proprietà dei parametri  
  
1.  Aprire la raccolta o la cartella che contiene il report.  
  
2.  Selezionare il report e fare clic sulla freccia verso il basso.  
  
3.  Fare clic su **Gestisci parametri**. Se il report contiene parametri, nella pagina visualizzata verranno elencati tutti i parametri. Per ogni parametro, nell'elenco sono indicati il nome, il tipo di dati, il valore predefinito e lo stato di visualizzazione nel riquadro dei parametri all'apertura del report.  
  
4.  Per modificare le impostazioni per un parametro, fare clic sul nome del parametro nell'elenco.  
  
5.  In Valore predefinito immettere un valore per il parametro. Poiché tale valore non verrà convalidato, verificare che il valore specificato sia appropriato per il report.  
  
    1.  Scegliere **Usa espressione del valore specificata nella definizione del report** se si vuole usare il valore predefinito impostato al momento della creazione del report. Se nella definizione del report non è disponibile un valore predefinito, questa opzione risulterà non disponibile.  
  
    2.  Scegliere **Ignora valore predefinito del report** se si vuole specificare un valore sostitutivo per il valore predefinito della definizione del report. Facoltativamente, per i parametri del report che accettano valori Null, è possibile selezionare la casella di controllo **Null** per impedire l'applicazione di filtri in base a questi parametri.  
  
    3.  Scegliere **Per il parametro non è specificato alcun valore predefinito** se si vuole che ogni utente specifichi un valore prima dell'elaborazione del report. Se si seleziona tale opzione, sarà necessario specificare anche le impostazioni di visualizzazione per richiedere all'utente di immettere un valore.  
  
     Si noti che, se tutti i parametri hanno un valore predefinito, al momento dell'apertura il report verrà automaticamente eseguito utilizzando tali valori. Se tuttavia il riquadro dei parametri è visualizzato, gli utenti possono ignorare il valore predefinito ed eseguire di nuovo il report.  
  
6.  Impostare le opzioni di visualizzazione per determinare se il parametro è visibile o meno.  
  
    1.  Per visualizzare il parametro nella pagina, selezionare **Richiesta all'utente** . È possibile specificare il testo della richiesta visualizzato in un campo per offrire una breve indicazione relativa al formato o al tipo di dati che l'utente deve specificare.  
  
    2.  Selezionare **Nascosto** se si usa un valore predefinito e non si vuole visualizzare il parametro nel riquadro Parametri.  
  
    3.  Selezionare **Interno** se si usa un valore predefinito e non si vuole che il parametro venga visualizzato nel riquadro Parametri o nelle pagine della sottoscrizione.  
  
7.  Fare clic su **Applica**.  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni di riferimento sulle autorizzazioni relative a elenchi e siti di SharePoint per gli elementi del server di report](../../reporting-services/security/sharepoint-site-and-list-permission-reference-for-report-server-items.md)  
  
  
