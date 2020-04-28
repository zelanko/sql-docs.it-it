---
title: Riquadro dei dati del report (Generatore report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10435"
helpviewer_keywords:
- Report Data pane
ms.assetid: 1492aa39-aeb1-4509-ab97-b9edd0901b7e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2a77024e62402cea0a37b945e0539274fee9a3c6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "78173330"
---
# <a name="report-data-pane-report-builder"></a>Riquadro dei dati del report (Generatore report)
  Usare il riquadro **Dati report** per visualizzare i parametri, le origini dati, i set di dati, le raccolte di campi e le immagini attualmente definiti nel report. Nel riquadro dei dati del report è riportata una visualizzazione gerarchica degli elementi che rappresentano i dati del report. I nodi di livello superiore rappresentano campi, parametri, immagini e riferimenti a origini dati predefiniti. Espandere ogni nodo per visualizzare gli elementi dei dati. Ad esempio, quando si espande il nodo di un'origine dati, verranno visualizzati i set di dati definiti per tale origine dati. Quando si espande un set di dati, verrà visualizzata la relativa raccolta di campi. Trascinare gli elementi nell'area di progettazione del report o nel riquadro Raggruppamento per collegare i dati agli elementi del report selezionati nella pagina del report. Per altre informazioni, vedere [Visualizzazione di progettazione report &#40;Generatore report&#41;](report-builder/report-design-view-report-builder.md).

## <a name="options"></a>Opzioni
 **Campi predefiniti** Rappresenta i campi di uso comune in un report, ad esempio il nome del report o il numero di pagina. Per altre informazioni, vedere [Raccolte predefinite nelle espressioni &#40;Generatore report e SSRS&#41;](report-design/built-in-collections-in-expressions-report-builder.md).

 **Parametri** di Rappresenta la raccolta di parametri del report, ognuno dei quali può essere a valore singolo o multivalore. Per ulteriori informazioni, vedere la pagina relativa al [Parametri report &#40;Generatore report e Progettazione report&#41;](report-design/report-parameters-report-builder-and-report-designer.md).

 **Immagini** di Rappresenta il set di immagini utilizzate nel report. Per altre informazioni, vedere [Immagini &#40;Generatore report e SSRS&#41;](report-design/images-report-builder-and-ssrs.md).

 **Origini dati** Rappresenta un'origine dati incorporata o un riferimento a un'origine dati condivisa. Tale origine indica un'origine di dati per il report. Un'origine dati è il nodo padre per la raccolta di set di dati che la utilizza. Per ulteriori informazioni, vedere [aggiungere dati a un Report &#40;Generatore report e SSRS&#41;](report-data/report-datasets-ssrs.md) e [connessioni dati, origini dati e stringhe di connessione in Generatore report](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md).

 **Set di impostazioni** Rappresenta i dati recuperati da un'origine dati eseguendo un comando, ad esempio una [!INCLUDE[tsql](../includes/tsql-md.md)] query che recupera i dati da un [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] database. Un set di dati è il nodo padre per la raccolta di campi specificati dalla query e include anche i campi calcolati. Generatore report supporta le Progettazione query che consentono di specificare una query. Per ulteriori informazioni, vedere [aggiungere dati a un Report &#40;Generatore report e SSRS&#41;](report-data/report-datasets-ssrs.md).

## <a name="see-also"></a>Vedere anche
 [Raccolta di campi del set di dati &#40;Generatore report e ssrs&#41;](report-data/dataset-fields-collection-report-builder-and-ssrs.md) [Generatore report guida per le finestre di dialogo, i riquadri e il riquadro di raggruppamento delle procedure guidate](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md) [Grouping Pane &#40;Report Builder&#41;](report-design/grouping-pane-report-builder.md) &#40;Generatore report&#41;la [ricerca, la visualizzazione e la gestione dei report &#40;Generatore report e SSRS &#41;](report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)


