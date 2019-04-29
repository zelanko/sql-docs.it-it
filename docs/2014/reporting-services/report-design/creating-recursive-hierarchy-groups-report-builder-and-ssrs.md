---
title: Creazione di gruppi di gerarchie ricorsive (Generatore Report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 06eccab6-4089-46e8-a84f-5bf3bbe0c23b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 92412bbde8a1032b34264ca254560f31704281e8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63135576"
---
# <a name="creating-recursive-hierarchy-groups-report-builder-and-ssrs"></a>Creazione di gruppi di gerarchie ricorsive (Generatore Report e SSRS)
  Per visualizzare dati ricorsivi dove la relazione tra padre e figlio è rappresentata dai campi del set di dati, è possibile impostare l'espressione di gruppo di nell'area dati in base al campo figlio e impostare la proprietà Parent in base al campo padre.  
  
 Visualizzazione gerarchica dei dati è un utilizzo comune per gruppi di gerarchie ricorsive, ad esempio, i dipendenti in un organigramma. Il set di dati include un elenco di dipendenti e responsabili, in cui i nomi di gestione vengono anche visualizzati nell'elenco dei dipendenti.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="creating-recursive-hierarchies"></a>Creazione di gerarchie ricorsive  
 Per compilare una gerarchia ricorsiva in un'area dati tablix, è necessario impostare l'espressione di raggruppamento sul campo che specifica i dati figlio e la proprietà Parent del gruppo sul campo che specifica i dati padre. Ad esempio, per un set di dati che include campi ID dipendente e ID responsabile in cui i dipendenti sono subordinati ai responsabili, impostare l'espressione di raggruppamento su ID dipendente e la proprietà Parent su gestione ID.  
  
 Un gruppo definito come gerarchia ricorsiva (vale a dire, un gruppo che usa la proprietà Parent) può avere solo un'espressione di raggruppamento. È possibile utilizzare la funzione `Level` nel riempimento della casella di testo per applicare un rientro ai nomi dei dipendenti in base al relativo livello nella gerarchia.  
  
 Per altre informazioni, vedere [aggiungere o eliminare un gruppo in un'area dati &#40;Generatore Report e SSRS&#41; ](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md) e [creare un gruppo di gerarchie ricorsive &#40;Generatore Report e SSRS&#41;](create-a-recursive-hierarchy-group-report-builder-and-ssrs.md).  
  
### <a name="aggregate-functions-that-support-recursion"></a>Funzioni di aggregazione che supportano la ricorsione  
 È possibile usare funzioni di aggregazione di Reporting Services che accettano il parametro *ricorsiva* per calcolare dati riepilogativi per una gerarchia ricorsiva. Le funzioni seguenti accettano `Recursive` come parametro: [Somma](report-builder-functions-sum-function.md), [Avg](report-builder-functions-avg-function.md), [conteggio](report-builder-functions-count-function.md), [CountDistinct](report-builder-functions-countdistinct-function.md), [CountRows](report-builder-functions-countrows-function.md), [Max](report-builder-functions-max-function.md), [Min](report-builder-functions-min-function.md), [StDev](report-builder-functions-stdev-function.md), [StDevP](report-builder-functions-stdevp-function.md), [Sum](report-builder-functions-sum-function.md), [Var](report-builder-functions-var-function.md), e [VarP](report-builder-functions-varp-function.md) . Per altre informazioni, vedere [riferimento a funzioni di aggregazione &#40;Generatore Report e SSRS&#41;](report-builder-functions-aggregate-functions-reference.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Le tabelle, matrici ed elenchi &#40;Report e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Un'area dati Tablix &#40;Report e SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [Riferimento a funzioni di aggregazione &#40;Report e SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)   
 [Le tabelle &#40;Report e SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [Le matrici &#40;Report e SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [Sono elencati &#40;Report e SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Le tabelle, matrici ed elenchi &#40;Report e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
