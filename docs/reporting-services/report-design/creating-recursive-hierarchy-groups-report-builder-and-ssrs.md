---
title: Creazione di gruppi di gerarchie ricorsive (Generatore report) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 06eccab6-4089-46e8-a84f-5bf3bbe0c23b
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a1674673e3c009815d04e3c4428244dfc29d0343
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "77078532"
---
# <a name="creating-recursive-hierarchy-groups-report-builder-and-ssrs"></a>Creazione di gruppi di gerarchie ricorsive (Generatore report e SSRS)
Per visualizzare dati ricorsivi in report impaginati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , dove la relazione tra padre e figlio è rappresentata mediante i campi del set di dati, impostare l'espressione di raggruppamento nell'area dati in base al campo figlio e la proprietà Parent in base al campo padre.  
  
 La visualizzazione di dati gerarchici è in genere utilizzata per gruppi di gerarchie ricorsive, ad esempio i dipendenti in un organigramma. Il set di dati include un elenco di dipendenti e responsabili, in cui i nomi dei responsabili sono visualizzati anche nell'elenco dei dipendenti.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="creating-recursive-hierarchies"></a>Creazione di gerarchie ricorsive  
 Per compilare una gerarchia ricorsiva in un'area dati Tablix è necessario impostare l'espressione di raggruppamento sul campo che specifica i dati figlio e la proprietà Parent del gruppo sul campo che specifica i dati padre. Ad esempio, per un set di dati che include campi ID dipendente e ID responsabile in cui i dipendenti sono subordinati ai responsabili, impostare l'espressione di raggruppamento su ID dipendente e la proprietà Parent su ID responsabile.  
  
 Un gruppo definito come gerarchia ricorsiva, ovvero un gruppo che usa la proprietà Parent, può includere una sola espressione di raggruppamento. È possibile usare la funzione **Level** nella spaziatura interna della casella di testo per applicare un rientro ai nomi dei dipendenti in base al relativo livello nella gerarchia.  
  
 Per altre informazioni, vedere [Aggiungere o eliminare un gruppo in un'area dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md) e [Creare un gruppo di gerarchie ricorsive &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/create-a-recursive-hierarchy-group-report-builder-and-ssrs.md).  
  
### <a name="aggregate-functions-that-support-recursion"></a>Funzioni di aggregazione che supportano la ricorsione  
 È possibile usare funzioni di aggregazione di Reporting Services che accettano il parametro *Recursive* per calcolare dati riepilogativi per una gerarchia ricorsiva. Nelle funzioni seguenti **Recursive** è accettato come parametro: [Sum](../../reporting-services/report-design/report-builder-functions-sum-function.md), [Avg](../../reporting-services/report-design/report-builder-functions-avg-function.md), [Count](../../reporting-services/report-design/report-builder-functions-count-function.md), [CountDistinct](../../reporting-services/report-design/report-builder-functions-countdistinct-function.md), [CountRows](../../reporting-services/report-design/report-builder-functions-countrows-function.md), [Max](../../reporting-services/report-design/report-builder-functions-max-function.md), [Min](../../reporting-services/report-design/report-builder-functions-min-function.md), [StDev](../../reporting-services/report-design/report-builder-functions-stdev-function.md), [StDevP](../../reporting-services/report-design/report-builder-functions-stdevp-function.md), [Sum](../../reporting-services/report-design/report-builder-functions-sum-function.md), [Var](../../reporting-services/report-design/report-builder-functions-var-function.md) e [VarP](../../reporting-services/report-design/report-builder-functions-varp-function.md). Per altre informazioni, vedere [Riferimento a funzioni di aggregazione &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle, matrici ed elenchi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Area dati Tablix &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [Riferimento a funzioni di aggregazione &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)   
 [Tabelle &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [Matrici &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [Elenchi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)    
 [Tabelle, matrici ed elenchi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
