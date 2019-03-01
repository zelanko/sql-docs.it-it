---
title: Aggiungere un collegamento ipertestuale a un URL (Generatore report e SSRS) | Microsoft Docs
ms.date: 09/07/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: d3392c0b-7b62-4d27-bc04-2bd0c5487d08
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7dcd5d57b3b5452a9d14b8951cc8f8d6572f452d
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56288949"
---
# <a name="add-a-hyperlink-to-a-url-report-builder-and-ssrs"></a>Aggiungere un collegamento ipertestuale a un URL (Generatore report e SSRS)
Informazioni su come aggiungere azioni con collegamento ipertestuale a caselle di testo, immagini, grafici e misuratori in report impaginati di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]  . I collegamenti possono indirizzare ad altri report, a segnalibri di un report o a URL statici o dinamici. 

 È possibile aggiungere un collegamento ipertestuale a qualsiasi elemento che dispone di una proprietà **Azione** , ad esempio una casella di testo, un'immagine o una serie calcolata in un grafico. Quando l'utente fa clic sul tale elemento del report, viene eseguita l'azione definita.  
  
*   È possibile **aggiungere un collegamento ipertestuale che aprirà un browser con URL** specificato. Il collegamento ipertestuale può essere un URL statico o un'espressione che restituisce un URL. Se in un database è disponibile un campo contenente URL, sarà possibile usare tale campo nell'espressione per ottenere un elenco dinamico di collegamenti ipertestuali nel report. Assicurarsi che i lettori del report hanno accesso all'URL indicato.  
   
*  È inoltre possibile **specificare URL per creare drill-through** ai report in qualsiasi server di report per i quali gli utenti dispongono di autorizzazione di visualizzazione, usando richieste di URL inviate al server di report. È ad esempio possibile specificare un report e nascondere la mappa documento agli utenti quando visualizzano il report per la prima volta. Per altre informazioni, vedere [Accesso con URL &#40;SSRS&#41;](../../reporting-services/url-access-ssrs.md) e [Specifica di percorsi di elementi esterni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md).
 
 *  È possibile **aggiungere un segnalibro a un punto specifico** dello stesso report. 
  
Provare ad aggiungere collegamenti ipertestuali con i dati di esempio forniti in [Esercitazione: Formattazione di testo &#40;Generatore report&#41;](../../reporting-services/tutorial-format-text-report-builder.md).  
  
> [!NOTE]  
>  I collegamenti associati ai campi del set di dati possono essere esposti ad alterazioni per finalità dannose. Per altre informazioni, vedere [Garantire la sicurezza di report e risorse](../../reporting-services/security/secure-reports-and-resources.md).  
  
## <a name="to-add-a-hyperlink-and"></a>Per aggiungere un collegamento ipertestuale e...   
  
1.  Nella visualizzazione Progettazione report fare clic con il pulsante destro del mouse sulla casella di testo, sull'immagine o sul grafico a cui si desidera aggiungere un collegamento, quindi scegliere **Proprietà**.  
  
2.  Nella finestra di dialogo Proprietà fare clic sulla scheda **Azione** . Continuare a leggere per informazioni sulle opzioni disponibili.  

## <a name="-add-drillthrough-to-another-report"></a>... aggiungere un drill-through a un altro report

1. Nella scheda **Azione** selezionare **Vai al report**. 

2. Specificare il report di destinazione e i parametri da usare. I nomi dei parametri devono corrispondere ai parametri definiti per il report di destinazione. 

3. Usare i pulsanti **Aggiungi** ed **Elimina** per aggiungere e rimuovere parametri e le frecce SU e GIÙ per ordinare l'elenco di parametri.

4.  Digitare o selezionare un **Valore** da passare per il parametro denominato nel report drill-through. Fare clic sul pulsante Espressione (fx) per modificare l'espressione.

5. Selezionare **Ometti** per impedire l'esecuzione del parametro. Per impostazione predefinita, questa casella di controllo è deselezionata e non è attiva. Per selezionare la casella di controllo, fare clic sul pulsante Espressione (fx) e digitare True o creare un'espressione. La casella di controllo viene selezionata quando si fa clic su **OK** nella finestra di dialogo Espressione.
  
   Per altre informazioni, vedere [Aggiungere un'azione drill-through a un report](../../reporting-services/report-design/add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md) . 
   
6. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
   
## <a name="-add-a-bookmark"></a>...aggiungere un segnalibro

È possibile inserire collegamenti a segnalibri in una posizione del report corrente. Per creare un collegamento a un segnalibro, è prima necessario impostare la proprietà **Segnalibro** di un elemento del report. Per impostare la proprietà **Segnalibro** , selezionare un elemento del report e nel riquadro Proprietà digitare un valore o un'espressione per l'ID del segnalibro, ad esempio SalesChart o 5TopSales.

1. Nella scheda **Azione** selezionare **Vai al segnalibro**. 

2. Digitare o selezionare l'ID del segnalibro del report a cui passare. Fare clic sul pulsante Espressione (fx) per modificare l'espressione. 

   L'ID del segnalibro può essere un ID statico oppure un'espressione che restituisce l'ID di un segnalibro. L'espressione può includere un campo contenente un ID del segnalibro.
   
   Per altre informazioni, vedere [Aggiungere un segnalibro a un report](../../reporting-services/report-design/add-a-bookmark-to-a-report-report-builder-and-ssrs.md) .
   
3. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="-add-a-hyperlink"></a>... aggiungere un collegamento ipertestuale 
  
1. Nella scheda **Azione** selezionare **Vai a URL**. Nella finestra di dialogo verrà visualizzata una sezione aggiuntiva per questa opzione.  
  
4.  In **Selezionare un URL**digitare o selezionare un URL o un'espressione che restituisca un URL oppure fare clic sulla freccia a discesa e selezionare il nome di un campo contenente un URL. 

    Per un elemento pubblicato in un server di report configurato per la modalità nativa, utilizzare un percorso completo o relativo. Ad esempio, `https://<servername>/images/image1.jpg`. 
    
    Per un elemento pubblicato in un server di report configurato per la modalità integrata SharePoint, utilizzare un URL completo. Ad esempio, `https://<SharePointservername>/<site>/Documents/images/image1.jpg`.
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="after-you-add-a-hyperlink"></a>Dopo aver aggiunto un collegamento ipertestuale
  
1.  (Facoltativo) Il testo non viene formattato automaticamente come collegamento. Per il testo è utile modificare il colore e l'effetto del testo per indicare che si tratta di un collegamento. È possibile, ad esempio, modificare il colore in blu e sottolineare il testo nella sezione **Carattere** nella scheda Home della barra multifunzione.  
  
7.  Per verificare il collegamento,fare clic **Esegui** per visualizzare il report in anteprima, quindi fare clic sull'elemento di report su cui è stato impostato il collegamento.  
  
## <a name="see-also"></a>Vedere anche  
 [Ordinamento interattivo, mappe documento e collegamenti &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [Creare una mappa documento &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/create-a-document-map-report-builder-and-ssrs.md)  
  
  
