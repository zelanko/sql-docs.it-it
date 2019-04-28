---
title: Riquadro dei dati del report
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.prod: reporting-services-2014, sql-server-2014
ms.prod_service: reporting-services-native, reporting-services-sharepoint
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: 1ea9335986fa58159bd7bb71fc7d32ac7f655feb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62721444"
---
# <a name="report-data-pane-in-sql-server-reporting-services-ssrs"></a>Riquadro dei dati del report in SQL Server Reporting Services (SSRS)

  Usare il riquadro **Dati report** per visualizzare i parametri, le origini dati, i set di dati, le raccolte di campi e le immagini attualmente definiti nel report. Nel riquadro dei dati del report è riportata una visualizzazione gerarchica degli elementi che rappresentano i dati del report. I nodi di livello superiore rappresentano campi, parametri, immagini e riferimenti a origini dati predefiniti. Espandere ogni nodo per visualizzare gli elementi dei dati. Ad esempio, quando si espande il nodo di un'origine dati, verranno visualizzati i set di dati definiti per tale origine dati. Quando si espande un set di dati, verrà visualizzata la relativa raccolta di campi. Trascinare gli elementi nell'area di progettazione del report per collegare i dati a elementi del report nella pagina.  
  
## <a name="options"></a>Opzioni

 **Campi predefiniti**  
 Rappresenta i campi disponibili in Reporting Services comunemente utilizzati in un report, ad esempio il nome o il numero di pagina. Per altre informazioni, vedere [Raccolte predefinite nelle espressioni &#40;Generatore report e SSRS&#41;](../report-design/built-in-collections-in-expressions-report-builder.md).  
  
 **Parametri**  
 Rappresenta la raccolta dei parametri del report, che possono essere a valore singolo o multivalore. Per ulteriori informazioni, vedere la pagina relativa al [Parametri report &#40;Generatore report e Progettazione report&#41;](../report-design/report-parameters-report-builder-and-report-designer.md).  
  
 **Immagini**  
 Rappresenta il set di immagini utilizzato nel report. Per altre informazioni, vedere [Immagini &#40;Generatore report e SSRS&#41;](../report-design/images-report-builder-and-ssrs.md).  
  
 **Origine dati**  
 Rappresenta un singolo riferimento a un'origine dati incorporata o condivisa. In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]le origini dati condivise vengono visualizzate nella cartella Origini dati condivise in Esplora soluzioni. Un'origine dati specifica uno dei tipi di origine dati supportati da Reporting Services. L'origine dati rappresenta il nodo padre per la raccolta di set di dati basati su di essa. Per altre informazioni, vedere [connessioni dati, origini dati e stringhe di connessione in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) .  
  
 **Set di dati**  
 Rappresenta un singolo set di dati. Il set di dati corrisponde al nodo padre per la raccolta di campi specificati dalla query, inclusi eventuali campi calcolati. Reporting Services supporta le finestre di progettazione query che consentono di specificare una query. Per altre informazioni, vedere [aggiungere dati a un Report &#40;Generatore Report e SSRS&#41; ](report-datasets-ssrs.md) e [strumenti di progettazione Query nella finestra di progettazione di Report SQL Server Data Tools &#40;SSRS&#41;](query-design-tools-ssrs.md).  
  
## <a name="next-steps"></a>Passaggi successivi

 - [Raccolta di campi del set di dati &#40;Generatore report e SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)
 - [Riquadro di raggruppamento](../tools/grouping-pane.md)