---
title: Stampare un report (Reporting Services in modalità SharePoint) | Microsoft Docs
description: Se un server di report viene eseguito in modalità SharePoint, è possibile stampare un report da un'applicazione Web di SharePoint da un sito di SharePoint, da un browser o da un'applicazione di destinazione.
ms.date: 05/14/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
helpviewer_keywords:
- printing reports, SharePoint Web application
- printing reports
ms.assetid: 026784f7-8cb4-4351-93ee-230b2ab0f8f5
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: eb3511714f893e4513c8a5ba1c215807003e6534
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "80290812"
---
# <a name="print-a-report-reporting-services-in-sharepoint-mode"></a>Stampare un report (Reporting Services in modalità SharePoint)
  In un server di report in esecuzione in SharePoint è possibile stampare un report da un'applicazione Web di SharePoint nei tre modi seguenti:  
  
-   **Da un sito di SharePoint** Scegliere **Stampa** dal menu **Azioni** visualizzato sulla barra degli strumenti per i report all'apertura del report. In questo modo si accede alla funzionalità di stampa di Reporting Services, che include una finestra di dialogo **Stampa** standard in cui è possibile selezionare una stampante, specificare pagine e margini, nonché visualizzare un'anteprima del report. Tale caratteristica di stampa può essere utilizzata in sostituzione del comando Stampa del menu File del browser. Quando si stampa un report in questo modo, il report viene stampato come è stato progettato, senza gli elementi aggiuntivi presenti nella stampa delle pagine Web.  
  
-   **Da un browser** Le caratteristiche di stampa dei browser forniscono risultati ottimali con i report in formato HTML che occupano una singola pagina. Le pagine stampate da un browser includono in genere tutti gli elementi visivi presenti nella pagina Web, più le informazioni dell'intestazione e del piè di pagina che identificano la pagina o il sito Web. Quando si esegue la stampa da un browser, viene stampato solo il contenuto della finestra corrente. Se il report è lungo, il browser ne stamperà solo una parte (in genere la prima pagina).  
  
-   **Da un'applicazione di destinazione** È possibile esportare un report per usare le caratteristiche di stampa di un'applicazione di destinazione, ad esempio Microsoft Office Excel o Adobe Acrobat Reader. Alcuni formati di applicazione, ad esempio TIFF o PDF, sono particolarmente adatti per la stampa dei report a più pagine. Dopo l'esportazione di un report in un'applicazione desktop, è possibile utilizzare tutte le caratteristiche di stampa specializzate offerte dall'applicazione. Per esportare un report, scegliere **Esporta** dal menu **Azioni** che viene visualizzato sulla barra degli strumenti per i report all'apertura del report.  
  
> [!NOTE]  
>  Per stampare un report, è necessario disporre delle autorizzazioni necessarie per visualizzarlo.  
  
 Per ottenere risultati ottimali in caso di stampa di un report da una pagina Web, usare il comando **Stampa** del menu **Azioni** . L'azione **Stampa** è associata a un controllo client di stampa che viene scaricato dal server di report. Il download viene eseguito solo la prima volta che si sceglie il comando **Stampa**.  
  
 Un report può essere progettato espressamente per l'output di stampa o per un formato di applicazione specifico. Poiché l'impaginazione viene implementata in modi diversi per formati di applicazione diversi, non sempre è possibile ottenere un output di stampa ottimale per tutti i report in tutti i formati di esportazione. Diversamente dai report progettati per l'output su stampante, le pagine dei report su schermo possono adattarsi a quantità variabili di dati. Le dimensioni delle pagine dei report che includono una tabella, ad esempio, possono aumentare in direzione orizzontale o verticale quando l'utente espande le righe o le colonne. Se si stampa un report con dimensioni variabili, i risultati di stampa saranno diversi a seconda che la matrice sia stata espansa o meno. Per la maggior parte dei report esportati, la stampa include tutti gli elementi visibili, esattamente come sono visualizzati sullo schermo.  
  
### <a name="how-to-print-reports-from-the-actions-menu"></a>Come stampare report dal menu Azioni  
  
1.  quindi aprirlo.  
  
2.  Scegliere **Stampa** dal menu **Azioni**. Se il menu **Azioni** non è visualizzato, significa che la barra degli strumenti per i report è nascosta e non è possibile usarne le caratteristiche. Se il menu **Azioni** è visualizzato ma il comando **Stampa** non è disponibile, significa che la funzionalità di stampa è stata disabilitata nel server di report e non può essere usata.  
  
3.  Nella finestra di dialogo **Stampa** selezionare la stampante e le impostazioni che si vogliono usare e quindi fare clic su **OK**.  
  
     Per modificare le impostazioni predefinite, fare clic sul pulsante **Proprietà** . Le dimensioni della pagina sono determinate dall'altezza e dalla larghezza predefinite delle pagine specificate nella definizione del report. L'entità delle modifiche che è possibile apportare alle dimensioni delle pagine dipende dalle funzionalità della stampante utilizzata.  
  
     Per visualizzare il report prima della stampa, fare clic sul pulsante **Anteprima** . Verrà aperta la prima pagina del report in una finestra di anteprima distinta. Se il rendering del report viene eseguito sul server di report, saranno disponibili alcune pagine aggiuntive. Il rendering dell'anteprima di un report viene eseguito in formato EMF. È possibile passare alla pagina precedente o successiva fino ad arrivare all'ultima pagina, in cui il pulsante **Successiva** risulta disabilitato. Per modificare i margini di stampa nella pagina di anteprima, fare clic sul pulsante **Margini** . Verrà visualizzata la finestra di dialogo **Margini** . Configurare i margini superiore, inferiore, destro e sinistro e quindi fare clic su **OK**. La finestra di dialogo verrà chiusa e le impostazioni verranno archiviate per l'anteprima del rendering e la stampa.  
  
## <a name="see-also"></a>Vedere anche  
 [Abilitare e disabilitare la stampa sul lato client per Reporting Services](../../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md)  
  
  
