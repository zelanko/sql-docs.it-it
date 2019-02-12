---
title: Creare una mappa documento (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: c200a97b-67f2-499f-8374-3ed1ebe3f33c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6b65d798c2de3cfe4b1fd14f50ea0dbb68bd624a
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56026512"
---
# <a name="create-a-document-map-report-builder-and-ssrs"></a>Creare una mappa documento (Generatore report e SSRS)
  Una mappa documento offre un set di collegamenti a elementi di report in un report visualizzabile. Quando si visualizza un report che include una mappa documento, accanto al report viene visualizzato un riquadro distinto. Gli utenti possono fare clic sui collegamenti della mappa documento per passare alla pagina del report in cui viene visualizzato l'elemento specifico. Le sezioni del report e i gruppi sono disposti in una gerarchia di collegamenti. Se si fa clic sugli elementi nella mappa documento, il report viene aggiornato e viene visualizzata l'area del report corrispondente all'elemento nella mappa documento.  
  
 Per aggiungere collegamenti alla mappa documento, impostare la proprietà `DocumentMapLabel` dell'elemento del report sul testo creato o su un'espressione che restituisca il testo da visualizzare nella mappa documento. A quest'ultima è possibile inoltre aggiungere i valori univoci per una tabella o un gruppo di matrici. Per un gruppo basato su un colore, ad esempio, ogni colore univoco rappresenta un collegamento alla pagina del report in cui viene visualizzata l'istanza del gruppo per il colore specifico.  
  
 È inoltre possibile creare un URL di un report in cui viene ignorata la visualizzazione della mappa documento, in modo che sia possibile eseguire il report senza visualizzare la mappa documento e successivamente fare clic sul pulsante **Mostra/Nascondi mappa documento** sulla barra degli strumenti del visualizzatore di report per attivare e disattivare la visualizzazione.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="DocMapRenderExtensions"></a> Mappe documento ed estensioni per il rendering  
 La mappa documento è destinata all'uso nell'estensione per il rendering HTML, ad esempio in Anteprima e nel Visualizzatore report. Altre estensioni per il rendering usano modalità diverse per organizzare una mappa documento:  
  
-   Con l'estensione per il rendering PDF, una mappa documento viene visualizzata come riquadro Segnalibri.  
  
-   Con l'estensione per il rendering Excel, una mappa documento viene visualizzata come foglio di lavoro denominato che include una gerarchia di collegamenti. Le sezioni del report vengono visualizzate in fogli di lavoro distinti inclusi nella mappa documento nella stessa cartella di lavoro.  
  
-   In Word è inclusa una mappa documento come sommario.  
  
-   In Atom, TIFF, XML e CSV le mappe documento vengono ignorate.  
  
 Per altre informazioni, vedere [Funzionalità interattiva per estensioni per il rendering di report differenti &#40;Generatore report e SSRS&#41;](../report-builder/interactive-functionality-different-report-rendering-extensions.md).  
  
##  <a name="AddRptItemToMap"></a>   
#### <a name="to-add-a-report-item-to-a-document-map"></a>Per aggiungere un elemento del report a una mappa documento  
  
1.  In visualizzazione Progettazione fare clic sull'elemento del report, ad esempio una tabella, una matrice o un misuratore, che si desidera aggiungere alla mappa documento. Le proprietà dell'elemento di report verranno visualizzate nel riquadro Proprietà.  
  
    > [!NOTE]  
    >  Per selezionare un'area dati Tablix, fare clic in una cella per visualizzare gli handle di riga e di colonna, quindi fare clic sull'handle d'angolo.  
  
2.  Nel riquadro proprietà, digitare il testo che si desidera visualizzare nella mappa documento nel `DocumentMapLabel` proprietà, oppure immettere un'espressione che restituisca un'etichetta. Digitare ad esempio **SalesChart**.  
  
    > [!NOTE]  
    >  Se il riquadro Proprietà non è visualizzato, nel gruppo **Mostra/Nascondi** della scheda **Visualizza** selezionare **Proprietà**.  
  
3.  Ripetere i passaggi 1 e 2 per ogni elemento di report da visualizzare nella mappa documento.  
  
4.  Fare clic su **Esegui**. Verrà avviata l'esecuzione del report e nella mappa documento verranno visualizzate le etichette create. Fare clic su un collegamento qualsiasi per passare alla pagina del report in cui è presente l'elemento specifico.  
  
 
  
##  <a name="AddUniqueValuesToMap"></a>   
#### <a name="to-add-unique-group-values-to-a-document-map"></a>Per aggiungere valori di gruppo univoci a una mappa documento  
  
1.  In visualizzazione Progettazione selezionare la tabella, la matrice o l'elenco che contiene il gruppo che si desidera visualizzare nella mappa documento. Nel riquadro di raggruppamento verranno visualizzati i gruppi di righe e di colonne.  
  
2.  Nel riquadro Gruppi di righe fare clic con il pulsante destro del mouse sul gruppo, quindi scegliere **Modifica gruppo**. Verrà visualizzata la scheda **Generale** della finestra di dialogo **Proprietà gruppo Tablix** .  
  
3.  Fare clic su **Avanzate**.  
  
4.  Nella casella di riepilogo **Mappa documento** digitare o selezionare un'espressione corrispondente all'espressione di raggruppamento.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  Ripetere i passaggi da 1 a 4 per ogni gruppo che si desidera visualizzare nella mappa documento.  
  
7.  Fare clic su **Esegui**. Verrà avviata l'esecuzione del report e nella mappa documento verranno visualizzati i valori dei gruppi. Fare clic su un collegamento qualsiasi per passare alla pagina del report in cui è presente l'elemento specifico.  
  
 
  
##  <a name="HideMapWhenViewRpt"></a>   
#### <a name="to-hide-the-document-map-when-you-view-a-report"></a>Per nascondere la mappa documento quando si visualizza un report  
  
1.  In Gestione report selezionare il report in cui è presente la mappa documento.  
  
     Per i report di esempio [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] , l'URL seguente specifica il report denominato Product Catalog.  
  
    ```  
    http://localhost/Reports/Pages/Report.aspx?ItemPath=%2fAdventureWorks2012+Sample+Reports%2fProduct+Catalog  
    ```  
  
2.  Copiare il percorso del report nel server. Nell'esempio il percorso del report è `%2fAdventureWorks2012+Sample+Reports%2fProduct+Catalog`.  
  
3.  Creare un nuovo URL con i tre componenti seguenti:  
  
    -   Visualizzatore di report nel server di report `http://localhost/ReportServer/Pages/ReportViewer.aspx?`  
  
    -   Nome del report copiato nel passaggio 1, ad esempio `%2fAdventureWorks2012+Sample+Reports%2fProduct+Catalog`  
  
    -   Parametri relativi alle informazioni sul dispositivo che specificano la disattivazione della visualizzazione della mappa documento `&rs%3aCommand=Render&rc%3aFormat=HTML4.0&rc%3aDocMap=False`  
  
     L'URL seguente è costituito da questi tre componenti aggiunti nell'ordine in cui vengono elencati.  
  
    ```  
    http://localhost/ReportServer/Pages/ReportViewer.aspx?  
    %2fAdventureWorks2012+Sample+Reports%2fProduct+Catalog  
    &rs%3aCommand=Render&rc%3aFormat=HTML4.0&rc%3aDocMap=False  
    ```  
  
     Per usare questo URL, copiarlo e rimuovere tutte le interruzioni di riga.  
  
4.  Incollare l'URL in Gestione report, quindi premere INVIO. Verrà avviata l'esecuzione del report e la mappa documento verrà nascosta.  
  
> [!NOTE]  
>  Per altre informazioni sul download di report di esempio, vedere la pagina relativa ai [report di esempio per Generatore report e Progettazione report](https://go.microsoft.com/fwlink/?LinkId=198283) di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
>   
>  Per altre informazioni, vedere "Accesso con URL" nella [documentazione relativa a Reporting Services](https://go.microsoft.com/fwlink/?linkid=121312) inclusa nella documentazione online di SQL Server.  
  
 
  
## <a name="see-also"></a>Vedere anche  
 [Ricerca e visualizzazione dei report in Gestione Report &#40;Report e SSRS&#41;](../report-builder/finding-and-viewing-reports-in-the-web-portal-report-builder-and-ssrs.md)  
  
  
