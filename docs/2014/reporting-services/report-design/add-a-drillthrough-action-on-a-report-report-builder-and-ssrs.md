---
title: Aggiungere un'azione drill-through a un report (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 153729c4-d01e-4629-b78f-0cfd5a7f83da
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a345b0ed36fde93a3bc94ff4075233c6c24728af
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66106873"
---
# <a name="add-a-drillthrough-action-on-a-report-report-builder-and-ssrs"></a>Aggiungere un'azione drill-through a un report (Generatore report e SSRS)
  Il report visualizzato quando si fa clic sul collegamento nel report principale è noto come *report drill-through*. Questo collegamento drill-through consente un'azione drill-through.  
  
 I report drill-through devono essere pubblicati sullo stesso server di report del report principale, anche se in cartelle diverse. È possibile aggiungere un collegamento drill-through a qualsiasi elemento che dispone di una proprietà **Azione** , ad esempio una casella di testo, un'immagine o punti dati in un grafico.  
  
 Per aggiungere un collegamento drill-through a un report, è necessario prima creare il report drill-through cui collegare il report principale. Un report drill-through contiene in genere i dettagli su un elemento presente nel report di riepilogo originale e spesso parametri che consentono di filtrare il report in base ai parametri passati dal report principale. Per altre informazioni sulla creazione del report drill-through, vedere [Report drill-through &#40;Generatore report e SSRS&#41;](drillthrough-reports-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-drillthrough-action"></a>Per aggiungere un'azione drill-through  
  
1.  In visualizzazione Progettazione fare clic con il pulsante destro del mouse sulla casella di testo, sull'immagine o sul grafico cui si vuole aggiungere un collegamento e quindi scegliere **Proprietà**.  
  
2.  Nella finestra di dialogo **Proprietà** dell'elemento fare clic su **Azione**.  
  
3.  Selezionare **Vai al report**. Nella finestra di dialogo verranno visualizzate sezioni aggiuntive per questa opzione.  
  
4.  In **Specifica un report**fare clic su **Sfoglia** per individuare il report a cui si vuole passare oppure digitarne il nome. In alternativa, fare clic sul pulsante di espressione (**fx**) per creare un'espressione per il nome del report.  
  
     Il formato del percorso del report drill-through è diverso a seconda che sia attiva la modalità nativa o la modalità integrata SharePoint. Se si utilizza la funzionalità di esplorazione, viene fornito un percorso con il formato corretto. Per altre informazioni, vedere [Specifica di percorsi di elementi esterni &#40;Generatore report e SSRS&#41;](specifying-paths-to-external-items-report-builder-and-ssrs.md).  
  
     Se è necessario specificare parametri per il report drill-through, eseguire la procedura successiva.  
  
5.  In **Utilizzare i parametri seguenti per eseguire il report**fare clic su **Aggiungi**. Alla griglia dei parametri verrà aggiunta una nuova riga.  
  
    -   Nella casella di testo **Nome** fare clic sull'elenco a discesa o digitare il nome del parametro di report nel report drill-through.  
  
        > [!NOTE]  
        >  I nomi nell'elenco dei parametri devono corrispondere esattamente ai parametri previsti nel report di destinazione. I nomi di parametro devono presentare ad esempio la stessa combinazione di maiuscole e minuscole. Se i nomi non corrispondono o un parametro previsto non è presente nell'elenco, il report drill-through restituirà un errore.  
  
    -   In **Valore**digitare o selezionare il valore da passare al parametro nel report drill-through.  
  
        > [!NOTE]  
        >  I valori possono contenere un'espressione che restituisce un valore da passare al parametro del report. Le espressioni nell'elenco dei valori includono l'elenco dei campi per il report corrente.  
  
     Per informazioni su come nascondere i parametri nei report, vedere [Aggiungere, modificare o eliminare un parametro di report &#40;Generatore report e SSRS&#41;](add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md).  
  
6.  (Facoltativo) Per le caselle di testo, è utile indicare all'utente che il testo è un collegamento modificandone il colore e l'effetto nella scheda **Home** della barra multifunzione.  
  
7.  Per verificare il collegamento, eseguire il report e fare clic sull'elemento di report su cui è stato impostato il collegamento.  
  
## <a name="see-also"></a>Vedere anche  
 [Finestra di dialogo Proprietà azione &#40;Generatore report e SSRS&#41;](../action-properties-dialog-box-report-builder-and-ssrs.md)   
 [Formattazione dei punti dati di un grafico &#40;Generatore report e SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [Visualizzazione di descrizioni comandi in una serie &#40;Generatore report e SSRS&#41;](show-tooltips-on-a-series-report-builder-and-ssrs.md)  
  
  
