---
title: Rendering delle aree dati (Generatore report e SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 4f3b2c7d-3669-457f-899b-b758d1db3426
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 368b17a6ffe7355569a9d60509a9a2db61931fee
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65576435"
---
# <a name="rendering-data-regions-report-builder-and-ssrs"></a>Rendering delle aree dati (Generatore report e SSRS)
  Oltre ai comportamenti di rendering generali che si applicano a tutti gli elementi del report, le aree dati prevedono comportamenti aggiuntivi di paginazione e rendering. Le regole di rendering specifiche delle aree dati includono il modo in cui aumentano le dimensioni dell'area dati, la modalità di rendering di celle speciali, ad esempio la cella d'angolo o le celle di intestazione, e la modalità di rendering di un'area dati per la lettura da destra a sinistra. In questo argomento viene descritto il rendering delle varie parti di un'area dati.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="tablix-data-regions"></a>Aree dati Tablix  
 L'area dati Tablix, che consente di creare tabelle, matrici ed elenchi, viene visualizzata come una griglia composta da colonne e righe. L'intersezione di una riga e di una colonna corrisponde a una cella. Quando viene eseguito il rendering, questa cella può contenere dati o altri elementi del report, ad esempio immagini, rettangoli, caselle di testo o sottoreport. Le dimensioni di un'area dati Tablix possono aumentare in verticale e/o in orizzontale. Inoltre, le dimensioni della cella d'angolo, delle celle di intestazione e delle celle del corpo dell'area dati possono aumentare in base al rispettivo contenuto. Se l'area dati si estende in più pagine, gli elementi del report impostati per essere ripetuti con l'area dati vengono visualizzati in tutte le pagine in cui è visualizzata l'area dati. Per altre informazioni, vedere [Tabelle, matrici ed elenchi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md).  
  
### <a name="right-to-left"></a>Da destra a sinistra  
 Un'area dati Tablix impostata per la visualizzazione da destra a sinistra viene visualizzata con la relativa struttura come immagine speculare dell'area dati, se il rendering è stato eseguito da sinistra a destra. L'angolo dell'area dati viene visualizzato nell'angolo superiore destro. Se il report contiene colonne dinamiche, queste si espandono verso sinistra. Le impostazioni da destra a sinistra non influiscono sull'ordine dei dati nell'area dati. Le colonne vengono semplicemente disposte in un ordine diverso.  
  
### <a name="tablix-headers"></a>Intestazioni Tablix  
 Le intestazioni Tablix vengono visualizzate come un'intestazione di riga o un'intestazione di colonna, a seconda che la cella di intestazione appaia nella gerarchia dei gruppi di righe o di colonne. Se nel contenuto della cella di un'intestazione è presente un'interruzione di pagina logica, questa verrà ignorata. Le interruzioni di pagina logiche nei gruppi di colonne vengono ignorate.  
  
 Le interruzioni di pagina logiche nei gruppi non generano l'interruzione delle intestazioni dei gruppi esterni. Si supponga ad esempio che il report includa un gruppo esterno relativo al paese e un gruppo interno per la provincia. Se è presente un'interruzione di pagina logica tra le istanze del gruppo della provincia, il gruppo esterno, ovvero il paese, verrà visualizzato in entrambe le pagine del report.  
  
#### <a name="repeated-tablix-headers"></a>Intestazioni Tablix ripetute  
 Quando la proprietà RepeatWith è impostata nel riquadro **Proprietà** , gli elementi che non cambiano all'interno dell'area dati, ad esempio le intestazioni di colonna, vengono ripetuti in ogni pagina in cui viene visualizzata tale parte dell'area dati. Se, ad esempio, una riga di dati viene visualizzata nella pagina successiva e la proprietà Repeat With è impostata, le intestazioni di colonna verranno visualizzate anche nella pagina di cui è stato eseguito il rendering.  
  
### <a name="tablix-corner"></a>Angolo Tablix  
 L'angolo superiore sinistro è denominato angolo Tablix. L'angolo Tablix può contenere altri elementi del report ma, se nell'angolo vengono inserite interruzioni di pagina logiche, queste verranno ignorate quando verrà eseguito il rendering dell'area dati Tablix.  
  
### <a name="tablix-body"></a>Corpo Tablix  
 Il rendering del corpo Tablix, costituito da celle Tablix, viene eseguito in base alle regole di paginazione e ai comportamenti di rendering degli elementi del report. Per altre informazioni, vedere [Rendering degli elementi del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md).  
  
## <a name="chart-gauge-and-map-data-regions"></a>Aree dati di grafici, misuratori e mappe  
 Il comportamento delle aree dati di grafici, misuratori e mappe è simile a quello delle immagini quando ne viene eseguito il rendering e vengono visualizzate nel corpo del report. Ai valori nell'area dati è possibile che siano associate azioni, ad esempio il collegamento a un altro report o il passaggio a un segnalibro. È possibile eseguire il rendering anche di tali azioni, se il renderer lo supporta.  
  
## <a name="see-also"></a>Vedere anche  
 [Paginazione in Reporting Services &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Tipi di rendering &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [Funzionalità interattiva per estensioni per il rendering di report differenti &#40;Generatore report e SSRS&#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [Rendering degli elementi del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [Tabelle, matrici ed elenchi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Grafici &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Misuratori &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)  
  
  
