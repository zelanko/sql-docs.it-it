---
title: Aggiungere un collegamento ipertestuale a un URL (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: d3392c0b-7b62-4d27-bc04-2bd0c5487d08
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6fa7b0d32a62e5e2d729e05c88b892ccaffc0fc2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66106821"
---
# <a name="add-a-hyperlink-to-a-url-report-builder-and-ssrs"></a>Aggiungere un collegamento ipertestuale a un URL (Generatore report e SSRS)
  È possibile aggiungere un collegamento ipertestuale a un elemento di report quando si desidera che gli utenti siano in grado di fare clic su un collegamento in un report e aprire una finestra del browser relativa all'URL specificato. Un collegamento ipertestuale può essere un URL statico o un'espressione che restituisce un URL. Se in un database è disponibile un campo contenente URL, sarà possibile usare tale campo nell'espressione per ottenere un elenco dinamico di collegamenti ipertestuali nel report. È possibile aggiungere collegamenti ipertestuali a caselle di testo, immagini, grafici e misuratori. È necessario garantire che l'utente acceda all'URL specificato.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 È inoltre possibile specificare URL ai report in qualsiasi server di report per la cui visualizzazione gli utenti dispongono delle autorizzazioni usando richieste di URL inviate al server di report. È ad esempio possibile specificare un report e nascondere la mappa documento agli utenti quando visualizzano il report per la prima volta. Per altre informazioni, vedere [Accesso con URL &#40;SSRS&#41;](../url-access-ssrs.md) della [Documentazione relativa a Reporting Services](https://go.microsoft.com/fwlink/?linkid=121312) inclusa nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 È possibile aggiungere un collegamento ipertestuale a un URL in qualsiasi elemento che dispone di una proprietà **Azione** , ad esempio una casella di testo, un'immagine o una serie calcolata in un grafico. Quando l'utente fa clic sul tale elemento del report, viene eseguita l'azione definita. Per altre informazioni, vedere [Finestra di dialogo Proprietà azione &#40;Generatore report e SSRS&#41;](../action-properties-dialog-box-report-builder-and-ssrs.md) e [Specifica di percorsi di elementi esterni &#40;Generatore report e SSRS&#41;](specifying-paths-to-external-items-report-builder-and-ssrs.md).  
  
 Per iniziare rapidamente, vedere [Esercitazione: Formattazione di testo &#40;Generatore report&#41;](../tutorial-format-text-report-builder.md).  
  
> [!NOTE]  
>  I collegamenti associati ai campi del set di dati possono essere esposti ad alterazioni per finalità dannose. Per altre informazioni, vedere [Garantire la sicurezza di report e risorse](../security/secure-reports-and-resources.md) nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]documentazione online[ di ](https://go.microsoft.com/fwlink/?LinkId=154888) sul sito msdn.microsoft.com.  
  
### <a name="to-add-a-hyperlink"></a>Per aggiungere un collegamento ipertestuale  
  
1.  Nella visualizzazione Progettazione report fare clic con il pulsante destro del mouse sulla casella di testo, sull'immagine o sul grafico a cui si desidera aggiungere un collegamento, quindi scegliere **Proprietà**.  
  
2.  Nella finestra di dialogo Proprietà fare clic su **Azione**.  
  
3.  Selezionare **Vai a URL**. Nella finestra di dialogo verrà visualizzata una sezione aggiuntiva per questa opzione.  
  
4.  In **Selezionare un URL**digitare o selezionare un URL o un'espressione che restituisca un URL oppure fare clic sulla freccia a discesa e selezionare il nome di un campo contenente un URL.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  (Facoltativo) Il testo non viene formattato automaticamente come collegamento. Per il testo è utile modificare il colore e l'effetto del testo per indicare che si tratta di un collegamento. È possibile, ad esempio, modificare il colore in blu e sottolineare il testo nella sezione **Carattere** nella scheda Home della barra multifunzione.  
  
7.  Per verificare il collegamento,fare clic **Esegui** per visualizzare il report in anteprima, quindi fare clic sull'elemento di report su cui è stato impostato il collegamento.  
  
## <a name="see-also"></a>Vedere anche  
 [Ordinamento interattivo, mappe documento e collegamenti &#40;Generatore report e SSRS&#41;](interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [Creare una mappa documento &#40;Generatore report e SSRS&#41;](create-a-document-map-report-builder-and-ssrs.md)  
  
  
