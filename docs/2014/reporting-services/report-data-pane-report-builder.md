---
title: Segnalare il riquadro dei dati (Generatore Report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10435"
helpviewer_keywords:
- Report Data pane
ms.assetid: 1492aa39-aeb1-4509-ab97-b9edd0901b7e
author: maggiesmsft
ms.author: maghan
manager: kfile
ms.openlocfilehash: b73080811e001b67ea52e3cbc9572eb014162e68
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56010352"
---
# <a name="report-data-pane-report-builder"></a>Riquadro dei dati del report (Generatore report)
  Usare il riquadro **Dati report** per visualizzare i parametri, le origini dati, i set di dati, le raccolte di campi e le immagini attualmente definiti nel report. Nel riquadro dei dati del report è riportata una visualizzazione gerarchica degli elementi che rappresentano i dati del report. I nodi di livello superiore rappresentano campi, parametri, immagini e riferimenti a origini dati predefiniti. Espandere ogni nodo per visualizzare gli elementi dei dati. Ad esempio, quando si espande il nodo di un'origine dati, verranno visualizzati i set di dati definiti per tale origine dati. Quando si espande un set di dati, verrà visualizzata la relativa raccolta di campi. Trascinare gli elementi nell'area di progettazione del report o nel riquadro Raggruppamento per collegare i dati agli elementi del report selezionati nella pagina del report. Per altre informazioni, vedere [Visualizzazione di progettazione report &#40;Generatore report&#41;](report-builder/report-design-view-report-builder.md).  
  
## <a name="options"></a>Opzioni  
 **Campi predefiniti**  
 Rappresenta campi di uso comune in un report, ad esempio il nome del report o il numero di pagina. Per altre informazioni, vedere [Raccolte predefinite nelle espressioni &#40;Generatore report e SSRS&#41;](report-design/built-in-collections-in-expressions-report-builder.md).  
  
 **Parametri**  
 Rappresenta la raccolta dei parametri del report, che possono essere a valore singolo o multivalore. Per ulteriori informazioni, vedere la pagina relativa al [Parametri report &#40;Generatore report e Progettazione report&#41;](report-design/report-parameters-report-builder-and-report-designer.md).  
  
 **Immagini**  
 Rappresenta il set di immagini utilizzato nel report. Per altre informazioni, vedere [Immagini &#40;Generatore report e SSRS&#41;](report-design/images-report-builder-and-ssrs.md).  
  
 **Origini dei dati**  
 Rappresenta un'origine dati incorporata o un riferimento a un'origine dati condivisa. Tale origine indica un'origine di dati per il report. Un'origine dati è il nodo padre per la raccolta di set di dati che la utilizza. Per altre informazioni, vedere [aggiungere dati a un Report &#40;Generatore Report e SSRS&#41; ](report-data/report-datasets-ssrs.md) e [connessioni dati, origini dati e stringhe di connessione in Generatore Report](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
 **Set di dati**  
 Rappresenta i dati recuperati da un'origine dati eseguendo un comando, ad esempio una query [!INCLUDE[tsql](../includes/tsql-md.md)] che recupera i dati da un database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Un set di dati è il nodo padre per la raccolta di campi specificati dalla query e include anche i campi calcolati. Generatore report supporta le Progettazione query che consentono di specificare una query. Per altre informazioni, vedere [aggiungere dati a un Report &#40;Generatore Report e SSRS&#41;](report-data/report-datasets-ssrs.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Raccolta di campi del set di dati &#40;Generatore report e SSRS&#41;](report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [Guida di Generatore report per finestre di dialogo, riquadri e procedure guidate](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [Riquadro di raggruppamento &#40;Generatore report&#41;](report-design/grouping-pane-report-builder.md)   
 [Ricerca, visualizzazione e gestione dei report &#40;Generatore report e SSRS&#41;](report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
