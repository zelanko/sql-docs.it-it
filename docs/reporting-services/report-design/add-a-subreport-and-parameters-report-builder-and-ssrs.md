---
title: Aggiungere un sottoreport e i parametri (Generatore report) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- "10093"
- sql13.rtp.rptdesigner.subreportproperties.general.f1
ms.assetid: 94f960f8-a629-4f1e-8277-c3b8f0680d98
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a74ef0a64fb7d1a77f3e336f98aeaa245c4458d8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "77080674"
---
# <a name="add-a-subreport-and-parameters-report-builder-and-ssrs"></a>Aggiungere un sottoreport e di parametri (Generatore report e SSRS)
  Aggiungere sottoreport a un report quando si desidera creare un report principale in cui è possibile includere più report correlati. Un sottoreport rappresenta un riferimento a un altro report. Per correlare i report tramite valori dei dati, ad esempio per fare in modo che in più report vengano visualizzati i dati relativi allo stesso cliente, è necessario progettare come sottoreport un report con parametri, ovvero un report in cui sono visualizzati i dettagli relativi a un cliente specifico. Quando al report principale si aggiunge un sottoreport, è possibile specificare parametri da passare a quest'ultimo.  
  
 È inoltre possibile aggiungere sottoreport a righe o colonne dinamiche in una tabella oppure in una matrice. Quando il report principale viene elaborato, il sottoreport viene elaborato per ogni riga. In questo caso, è necessario valutare se sia possibile ottenere l'effetto desiderato utilizzando aree dati o aree dati annidate.  
  
 Per aggiungere un sottoreport a un report, è necessario prima creare il report che sarà utilizzato come sottoreport. Per altre informazioni sulla creazione del sottoreport, vedere [Sottoreport &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/subreports-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-subreport"></a>Per aggiungere un sottoreport  
  
1.  Fare clic su **Sottoreport** nella scheda **Inserisci**.  
  
2.  Nell'area di progettazione fare clic in un punto del report, quindi trascinare una casella fino alle dimensioni desiderate per il sottoreport. In alternativa, fare clic nell'area di progettazione per creare un sottoreport di dimensioni predefinite.  
  
3.  Fare clic con il pulsante destro del mouse sul sottoreport e quindi scegliere **Proprietà sottoreport**.  
  
4.  Nella finestra di dialogo **Proprietà sottoreport** digitare un nome nella casella di testo **Nome** o accettare il nome predefinito. Il nome deve essere univoco nel report. Per impostazione predefinita, viene assegnato un nome generale, ad esempio Subreport1 o Subreport2.  
  
5.  Nella casella **Utilizzare il report come sottoreport** fare clic su **Sfoglia**oppure digitare il nome del report. È preferibile fare clic su **Sfoglia** perché il percorso del sottoreport verrà specificato automaticamente. È possibile specificare il report in diversi modi. Per altre informazioni, vedere [Specifica di percorsi di elementi esterni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md).  
  
6.  (Facoltativo) Fare clic su **Sì** per **Ometti bordo sull'interruzione di pagina** per impedire che venga visualizzato un bordo a metà del sottoreport se si estende su più di una pagina.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-specify-parameters-to-pass-to-a-subreport"></a>Per specificare i parametri da passare a un sottoreport  
  
1.  Nella visualizzazione della struttura fare clic con il pulsante destro del mouse sul sottoreport e quindi scegliere **Proprietà sottoreport**.  
  
2.  Nella finestra di dialogo **Proprietà sottoreport** fare clic su **Parametri**.  
  
3.  Fare clic su **Aggiungi**. Alla griglia dei parametri verrà aggiunta una nuova riga.  
  
4.  Nella casella di testo **Nome** digitare il nome di un parametro nel sottoreport o sceglierlo dalla casella di riepilogo. Il nome deve corrispondere a un parametro del report e non al parametro di query nel sottoreport.  
  
5.  Nella casella di riepilogo **Valore** digitare o selezionare un valore da passare al sottoreport. È possibile specificare un testo statico o un'espressione che fa riferimento a un campo oppure a un altro oggetto nel report principale.  
  
    > [!NOTE]  
    >  In Generatore report, se un parametro non è presente nell'elenco **Parametri** e il sottoreport dispone di un valore predefinito, il sottoreport sarà elaborato correttamente.  
    >   
    >  In Progettazione report, tutti i parametri necessari per il sottoreport devono essere inclusi nell'elenco **Parametri** . Se non viene specificato un parametro obbligatorio, il sottoreport non verrà visualizzato correttamente nel report principale.  
  
6.  Ripetere i passaggi 3-5 per specificare un nome e un valore per ogni parametro del sottoreport.  
  
7.  Per eliminare un parametro di sottoreport, fare clic sul parametro nella griglia dei parametri e quindi fare clic su **Elimina**.  
  
8.  Per modificare l'ordine di un parametro di sottoreport, fare clic sul parametro e quindi sul pulsante freccia in su o freccia in giù.  
  
     La modifica dell'ordine di un parametro di sottoreport non comporta effetti sull'elaborazione del sottoreport.  
  
## <a name="see-also"></a>Vedere anche  
 [Sottoreport &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/subreports-report-builder-and-ssrs.md)   
 [Tipi di rendering &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)  
  
  
