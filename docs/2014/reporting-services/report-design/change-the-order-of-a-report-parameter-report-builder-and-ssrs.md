---
title: Modificare l'ordine di un parametro del report (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: abd61e19-dba3-423c-a26c-e8bc43197d3f
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 41280d4021dae3c52ebd0e2d888108104ca7b01c
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56289169"
---
# <a name="change-the-order-of-a-report-parameter-report-builder-and-ssrs"></a>Modificare l'ordine di un parametro del report (Generatore report e SSRS)
  Modificare l'ordine dei parametri del report quando un parametro dipendente è elencato prima del parametro da cui dipende. L'ordine dei parametri è importante quando sono presenti parametri di propagazione o quando si desidera indicare il valore predefinito di un parametro prima che gli utenti scelgano i valori per altri parametri. Un parametro dipendente del report contiene un riferimento, nella query dei valori predefiniti o in quella dei valori validi, a un parametro di query che punta a un parametro del report successivo nell'elenco dei parametri contenuto nel riquadro dei dati del report.  
  
 L'ordine in cui i parametri vengono visualizzati sulla barra degli strumenti del visualizzatore di report è determinato dall'ordine dei parametri nel riquadro dei dati del report.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-the-order-of-report-parameters"></a>Per modificare l'ordine dei parametri del report  
  
1.  Nel riquadro dei dati del report espandere il nodo Parametri.  
  
2.  Fare clic su un parametro e utilizzare i pulsanti freccia Su e freccia Giù sulla barra degli strumenti del riquadro dei dati del report per spostare il parametro in una posizione superiore o inferiore nell'elenco. La figura seguente mostra il riquadro Dati report in Generatore report.  
  
     ![Riquadro dati report](../media/reportdatapane.png "riquadro dati Report")  
  
## <a name="see-also"></a>Vedere anche  
 [Parametri report &#40;Generatore report e Progettazione report&#41;](report-parameters-report-builder-and-report-designer.md)   
 [Guida di Generatore report per finestre di dialogo, riquadri e procedure guidate](../report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [Aggiunta di parametri di propagazione a un report &#40;Generatore report e SSRS&#41;](add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [Esercitazione: Aggiungere un parametro al Report &#40;Generatore Report&#41;](../tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [Aggiungere filtri per set di dati, aree dati e gruppi &#40;Generatore report e SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Riferimenti alla raccolta dei parametri &#40;Generatore report e SSRS&#41;](built-in-collections-parameters-collection-references-report-builder.md)  
  
  
