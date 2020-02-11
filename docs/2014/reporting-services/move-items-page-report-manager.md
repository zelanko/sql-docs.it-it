---
title: Pagina Sposta elementi (Gestione report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: fc83b8d2-bc79-4b56-8970-34a1cbbcc176
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2f64a9e9efe180c2db776c38553403e5f7cdfac9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108219"
---
# <a name="move-items-page-report-manager"></a>Pagina Spostamento elementi (Gestione report)
  La pagina di spostamento degli elementi consente di spostare un report, una cartella o altri elementi in una nuova posizione nel server di report. È possibile digitare il percorso della nuova posizione oppure utilizzare una visualizzazione albero per selezionare una nuova posizione nello spazio dei nomi del server di report. Si possono spostare solo gli elementi per i quali si dispone delle autorizzazioni per lo spostamento e che sono archiviati nel server di report corrente.  
  
 Quando si sposta un elemento a cui un altro elemento fa riferimento, ad esempio un'origine dati condivisa o un modello a cui fanno riferimento molti report, le informazioni sul percorso dell'elemento vengono aggiornate automaticamente. Un'origine dati condivisa può pertanto essere spostata senza interrompere la connessione all'origine dati dei report e dei modelli che la utilizzano. Se si sposta un'origine dati condivisa o un modello in una cartella per la quale gli utenti non dispongono di autorizzazioni, gli utenti potranno comunque eseguire i report che fanno riferimento all'origine dati o al modello, ma l'elemento non sarà visibile nella gerarchia di cartelle.  
  
 In **Percorso**specificare il percorso completo della cartella, a partire dal nome della cartella radice. È possibile digitare il nome del percorso oppure utilizzare la visualizzazione albero per passare alla cartella desiderata.  
  
> [!NOTE]  
>  Non tutti gli elementi sono mobili. Non è possibile spostare cartelle riservate come Home, Report personali o Cartelle utenti. Non è inoltre possibile spostare la cronologia o gli snapshot dei report in posizioni diverse. La cronologia e gli snapshot sono sempre posizionati nello stesso percorso del report su cui si basano ed è possibile accedervi solo tramite il report associato.  
  
## <a name="navigation"></a>Navigazione  
 Utilizzare le procedure riportate di seguito per navigare fino a questo percorso nell'interfaccia utente.  
  
###### <a name="to-open-the-move-items-page-from-the-contents-page-in-details-view"></a>Per aprire la pagina di spostamento degli elementi dalla pagina Contenuto in Visualizzazione Dettagli  
  
1.  Aprire Gestione report e navigare fino alla cartella che contiene l'elemento che si desidera spostare. È possibile spostare anche elementi dalla home page di Gestione report.  
  
2.  Nella barra degli strumenti fare clic su **Visualizzazione Dettagli**.  
  
    > [!NOTE]  
    >  Se viene visualizzata solo la **visualizzazione riquadri**, si è già in **visualizzazione dettagli**.  
  
3.  Selezionare la casella accanto all'elemento, quindi fare clic su **Sposta** nella barra degli strumenti. È possibile selezionare più di una casella se si desidera spostare più elementi nello stesso percorso nuovo.  
  
###### <a name="to-open-the-move-items-page-from-the-contents-page-in-tiles-view"></a>Per aprire la pagina di spostamento degli elementi dalla pagina Contenuto in Visualizzazione Affiancata  
  
1.  Aprire Gestione report e navigare fino alla cartella che contiene l'elemento che si desidera spostare. È possibile spostare anche elementi dalla home page di Gestione report.  
  
2.  Nella barra degli strumenti fare clic su **Visualizzazione Affiancata**.  
  
    > [!NOTE]  
    >  Se viene visualizzata solo la **visualizzazione dettagli**, si è già in **visualizzazione affiancata**.  
  
3.  Passare con il puntatore del mouse su un elemento, quindi fare clic sulla freccia a discesa.  
  
4.  Nel menu a discesa fare clic su **Sposta**.  
  
###### <a name="to-open-the-move-items-page-from-the-general-properties-page-of-an-item"></a>Per aprire la pagina di spostamento degli elementi dalla pagina delle proprietà Generale di un elemento  
  
1.  Aprire Gestione report e navigare fino alla cartella che contiene l'elemento che si desidera spostare. È possibile spostare anche elementi dalla home page di Gestione report.  
  
2.  Passare con il puntatore del mouse su un elemento, quindi fare clic sulla freccia a discesa.  
  
3.  Scegliere **Gestisci**dal menu a discesa. Viene visualizzata la pagina delle proprietà Generale per l'elemento.  
  
4.  Sulla barra degli strumenti dell'elemento, fare clic su **Sposta**.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione report &#40;modalità nativa SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Pagina delle proprietà generale, cartelle &#40;Gestione report&#41;](../../2014/reporting-services/general-properties-page-folders-report-manager.md)   
 [Pagina delle proprietà generale, report &#40;Gestione report&#41;](../../2014/reporting-services/general-properties-page-reports-report-manager.md)   
 [Pagina delle proprietà generale, risorse &#40;Gestione report&#41;](../../2014/reporting-services/general-properties-page-resources-report-manager.md)   
 [Pagina delle proprietà generale, origini dati condivise &#40;Gestione report&#41;](../../2014/reporting-services/general-properties-page-shared-data-sources-report-manager.md)   
 [Guida sensibile al contesto di Gestione report](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
