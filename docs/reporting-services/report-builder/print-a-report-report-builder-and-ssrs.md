---
title: Stampare un report (Generatore report e SSRS) | Microsoft Docs
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: b96936c9-c387-41a9-8c19-6eb325769ffd
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 67d9e057b7ed307377e59172948d56d92c45e7f3
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65581173"
---
# <a name="print-a-report-report-builder-and-ssrs"></a>Stampare un report (Generatore report e SSRS)
  Dopo avere salvato un report in un server di report, è possibile visualizzarlo e stamparlo da un browser, dal portale Web di Reporting Services o da qualsiasi applicazione usata per visualizzare un report esportato. Prima di salvare un report, è possibile stamparlo durante l'anteprima.  
  
 Quando si stampa un report, è possibile specificare le dimensioni della pagina da utilizzare. Le dimensioni del foglio determinano il numero di pagine del report e la quantità di dati contenuta in ogni pagina. Il formato della carta influisce solo sui report visualizzati con i renderer di interruzioni di pagina manuali: PDF, immagine e stampa. L'impostazione del formato della carta non influisce su altri renderer. Per altre informazioni, vedere [Tipi di rendering  &#40;Generatore report e SSRS &#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md).  
  
 Dalla barra degli strumenti del visualizzatore di report nel portale Web di Reporting Services o in un'anteprima in Generatore report è possibile esportare un report in un renderer di interruzione di pagina manuale oppure fare clic sul pulsante Stampa per stampare una copia del report. Potrebbe essere necessario impostare il formato della carta o altre proprietà di impostazione pagina. Usare la finestra di dialogo **Proprietà report** per modificare le proprietà di impostazione della pagina, tra cui il formato della carta.  
  
 È possibile specificare i margini della pagina di stampa in due modi diversi, ovvero in modalità di progettazione e in modalità di esecuzione.  
  
-   **Modalità progettazione.** Quando si impostano i margini della pagina in modalità di progettazione, queste impostazioni vengono salvate nella definizione del report quando si salva il report.  
  
-   **Modalità esecuzione.** Quando si impostano i margini della pagina in modalità di esecuzione, queste informazioni non vengono salvate nella definizione del report. La volta successiva che si stampa il report, verranno utilizzate le impostazioni della definizione del report, a meno che non si indichino nuovamente i margini di stampa.  
  
    > [!NOTE]  
    >  I margini di stampa non vengono visualizzati nelle modalità di progettazione o esecuzione. Non c'è relazione tra l'area dell'area di progettazione e l'area di stampa del report. Per vedere i margini di stampa, in modalità di esecuzione fare clic su Layout di stampa nella scheda **Esegui** sulla barra multifunzione.  
  
 Per altre informazioni sul paginazione dei report, vedere [Paginazione in Reporting Services &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-print-a-report-in-report-builder"></a>Per stampare un report in Generatore report  
  
1.  Aprire un report.  
  
2.  Nella scheda Home fare clic su **Esegui**.  
  
3.  (Facoltativo) Fare clic su **Layout di stampa** per visualizzare un'anteprima del report prima di stamparlo.  
  
4.  (Facoltativo) Fare clic su **Imposta pagina** per impostare la carta, l'orientamento e i margini.  
  
    > [!NOTE]  
    >  I valori predefiniti di tali voci provengono dalle proprietà del report impostate in visualizzazione Progettazione. I valori impostati nella finestra di dialogo **Imposta pagina** sono validi solo per la sessione corrente. Quando il report viene chiuso e poi riaperto, verranno ripristinati i valori predefiniti.  
  
5.  Fare clic su **Stampa**.  
  
6.  Nella finestra di dialogo **Stampa** selezionare una stampante e specificare altre opzioni di stampa.  
  
### <a name="to-print-a-report-from-a-web-browser-application"></a>Per stampare un report da un'applicazione browser  
  
1.  Nel portale web di Reporting Services passare al report da stampare. quindi aprirlo.  
  
3.  Fare clic su **Stampa**sulla barra degli strumenti nella parte superiore del report.  
  
    > [!NOTE]  
    >  Quando si stampa per la prima volta un report in formato HTML, per il server di report viene richiesta l'installazione di un controllo ActiveX utilizzato per la stampa. È necessario installare e configurare il controllo per poter stampare.  
  
4.  Nella finestra di dialogo **Stampa** selezionare una stampante e fare clic su **Stampa**.  
  
### <a name="to-print-a-report-from-other-applications"></a>Per stampare un report da altre applicazioni  
  
1.  Nel portale web di Reporting Services passare al report da stampare. quindi aprirlo.  
  
2.  Selezionare un formato di rendering sulla barra degli strumenti nella parte superiore del report, quindi fare clic su **Esporta**. Il report verrà aperto nell'applicazione di visualizzazione corrispondente al formato di rendering selezionato.  
  
     Ad esempio, se si seleziona il formato PDF, il report verrà aperto in Adobe Acrobat Reader.  
  
3.  Scegliere **Stampa** dal menu **File**del programma in uso.  
  
### <a name="to-change-paper-size"></a>Per modificare il formato della carta  
  
1.  Fare clic con il pulsante destro del mouse al di fuori del corpo del report e scegliere **Proprietà report**.  
  
2.  Selezionare un valore dall'elenco **Formato carta**in **Imposta pagina** . Verranno popolate le proprietà **Larghezza** e **Altezza** . È anche possibile specificare un formato personalizzato digitando valori numerici nelle caselle **Larghezza** e **Altezza** . [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  I valori relativi alle dimensioni sono calcolati in base all'unità di misura predefinita specificata dall'utente nelle impostazioni locali. Per specificare un'unità di misura diversa, digitare un identificatore di unità fisica, ad esempio cm, mm, pt o pc, dopo il valore numerico.  
  
### <a name="to-set-page-margins-in-design-mode"></a>Per impostare i margini della pagina in modalità di progettazione  
  
-   Fare clic con il pulsante destro del mouse sull'area blu intorno all'area di progettazione, scegliere **Proprietà report**, quindi fare clic sulla pagina **Imposta pagina** .  
  
### <a name="to-set-page-margins-in-run-mode"></a>Per impostare i margini della pagina in modalità di esecuzione  
  
-   Fare clic su **Imposta pagina** nella scheda **Esegui** .  
  
## <a name="see-also"></a>Vedere anche  
 [Stampa di report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)   
 [Esportare report &#40;Generatore Report e SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [Finestra di dialogo Proprietà report, Imposta pagina &#40;Generatore report&#41;](https://msdn.microsoft.com/library/eb3b5d01-7b82-4808-a58b-9e096742f8c6)   
 [Visualizzazione di progettazione report &#40;Generatore report&#41;](../../reporting-services/report-builder/report-design-view-report-builder.md)  
  
  
