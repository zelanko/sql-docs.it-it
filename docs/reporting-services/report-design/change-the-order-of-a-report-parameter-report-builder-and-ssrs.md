---
title: Modificare l'ordine di un parametro del report (Generatore report) | Microsoft Docs
description: Informazioni su come modificare l'ordine dei parametri del report quando un parametro dipendente è elencato non in ordine in Generatore report.
ms.date: 08/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: abd61e19-dba3-423c-a26c-e8bc43197d3f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c2b93a9092991bdc5e7d177e8819303bc3474255
ms.sourcegitcommit: 02b22274da4a103760a376c4ddf26c4829018454
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/11/2020
ms.locfileid: "84681250"
---
# <a name="change-the-order-of-a-report-parameter-report-builder-and-ssrs"></a>Modificare l'ordine di un parametro del report (Generatore report e SSRS)
  Modificare l'ordine dei parametri del report quando un parametro dipendente è elencato prima del parametro da cui dipende. L'ordine dei parametri è importante quando sono presenti parametri di propagazione o quando si desidera indicare il valore predefinito di un parametro prima che gli utenti scelgano i valori per altri parametri. Un parametro dipendente del report contiene un riferimento, nella query dei valori predefiniti o in quella dei valori validi, a un parametro di query che punta a un parametro del report successivo nell'elenco dei parametri del riquadro dei **dati del report** .  
  
 L'ordine con cui i parametri vengono visualizzati nella barra degli strumenti del visualizzatore di report quando viene eseguito il report è determinato dall'ordine dei parametri nel riquadro dei **dati del report** e dalla posizione dei parametri nel riquadro dei parametri personalizzati. Per altre informazioni, vedere [Personalizzare il riquadro dei parametri in un report &#40;Generatore report&#41;](../../reporting-services/report-design/customize-the-parameters-pane-in-a-report-report-builder.md)  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-change-the-order-of-report-parameters"></a>Per modificare l'ordine dei parametri del report  
  
È possibile modificare l'ordine dei parametri del report eseguendo una delle operazioni seguenti:  
  
-   Fare clic su un parametro nel riquadro dei **dati del report** e usare i pulsanti freccia Su e freccia Giù per spostare il parametro in una posizione superiore o inferiore nell'elenco, come mostrato nell'immagine seguente.  Quando si modifica l'ordine del parametro del riquadro dei **dati del report** , viene modificata la posizione del parametro nel riquadro.  
  
     ![Modificare l'ordine dei parametri nel riquadro dei dati del report](../../reporting-services/report-design/media/ssrs-changeorderofparameters-reportdata.png "Modificare l'ordine dei parametri nel riquadro dei dati del report")  
  
-   Nel riquadro dei parametri trascinare il parametro in una nuova colonna o riga del riquadro. Quando si modifica la posizione del parametro nel riquadro, viene modificato l'ordine del parametro nel riquadro dei **dati del report** . Per altre informazioni sullo spostamento dei parametri nel riquadro, vedere [Personalizzare il riquadro dei parametri in un report &#40;Generatore report&#41;](../../reporting-services/report-design/customize-the-parameters-pane-in-a-report-report-builder.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Parametri report &#40;Generatore report e Progettazione report&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Aggiunta di parametri di propagazione a un report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [Esercitazione: Aggiungere un parametro al report &#40;Generatore report&#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [Aggiungere filtri per set di dati, aree dati e gruppi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Riferimenti alla raccolta dei parametri &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)  
  
  
