---
title: Editor dei Form delle azioni drill-through (scheda azioni, Progettazione cubi) (Analysis Services - dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.actionexpression.drillthroughaction.f1
ms.assetid: 225fd818-b5ea-494f-b67b-66e09798274a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8589c743e926b6654cfba123ef7a47a85c0e95d3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62731713"
---
# <a name="drillthrough-action-form-editor-actions-tab-cube-designer-analysis-services---multidimensional-data"></a>Editor dei form delle azioni drill-through (scheda Azioni, Progettazione cubi) (Analysis Services - Dati multidimensionali)
  Usare il riquadro dell'**editor dei form delle azioni drill-through** nella scheda **Azioni** di Progettazione cubi per modificare l'azione drill-through selezionata nel riquadro **Libreria azioni**. Per altre informazioni sulle azioni drill-through, vedere [Azioni &#40;Analysis Services - Dati multidimensionali&41#;](multidimensional-models/actions-analysis-services-multidimensional-data.md).  
  
> [!NOTE]  
>  Le azioni drill-through non eseguono più il drill-down nell'archivio di dati sottostante. Le informazioni accessibili dalle azioni drill-through devono essere modellate all'interno del cubo utilizzando membri di dimensione o di gerarchia.  
  
## <a name="options"></a>Opzioni  
 **name**  
 Consente di digitare il nome dell'azione.  
  
 **Destinazione azione**  
 Espandere questa opzione per visualizzare la casella di riepilogo **Membri gruppo di misure** .  
  
 **Membri gruppo di misure**  
 Consente di selezionare il gruppo di misure al quale associare l'azione drill-through.  
  
 **Condizione (facoltativa)**  
 Immettere l'espressione MDX (Multidimensional Expressions) che descrive una condizione facoltativa, usata in combinazione con l'opzione **Membri gruppo di misure**, che consente di limitare ulteriormente la disponibilità dell'azione. L'espressione deve restituire un valore booleano il quale, se è True, indica che l'azione è disponibile.  
  
 Trascinare gli elementi selezionati dal riquadro **Strumenti di calcolo** alla casella di questa opzione per includere la sintassi MDX per l'elemento selezionato.  
  
 **Colonne drill-through**  
 Espandere questa opzione per visualizzare una griglia nella quale specificare gli attributi restituiti quando l'utente esegue l'azione.  
  
> [!NOTE]  
>  È possibile selezionare più di una dimensione, ma non è possibile utilizzare più di una volta una dimensione in un'azione drill-through.  
  
 La griglia include le colonne seguenti:  
  
|colonna|Descrizione|  
|------------|-----------------|  
|**Dimensions**|Consente di selezionare la dimensione utilizzata per restituire l'attributo. Selezionare MEASURES per eseguire il drill-through sulle misure.|  
|**Restituire colonne**|Consente di selezionare l'attributo o la misura dalla dimensione selezionata da restituire all'esecuzione dell'azione.|  
  
 **Proprietà aggiuntive**  
 Espandere questa opzione per visualizzare le opzioni **Impostazione predefinita**, **Numero massimo di righe**, **Chiamata**, **Applicazione**, **Descrizione**, **Didascalia**e **Didascalia MDX** .  
  
 **Default**  
 Selezionare **True** per includere l'azione drill-through attuale come azione predefinita. In caso contrario selezionare **False**.  
  
 Se il `RETURN` clausola viene omessa dal MDX `DRILLTHROUGH` istruzione eseguita da un'applicazione client, il [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] istanza valuta tutte le azioni di drill-through predefinite ed esegue il drill-through predefinita prima azione che restituisce un set non vuoto. Per altre informazioni su MDX `DRILLTHROUGH` istruzione, vedere [istruzione drill-through &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-drillthrough).  
  
> [!NOTE]  
>  Questa opzione viene utilizzata per garantire la compatibilità con le versioni precedenti.  
  
 **Numero massimo di righe**  
 Consente di digitare il numero massimo di righe che devono essere restituite dall'azione drill-through. Se si imposta questa opzione a zero o a un valore vuoto l'azione drill-through restituirà all'applicazione client tutte le righe recuperate.  
  
 **Chiamata**  
 Consente di selezionare l'impostazione che indica quando eseguire l'azione.  
  
> [!NOTE]  
>  Questa opzione costituisce solo un'indicazione per un'applicazione client relativa al momento in cui eseguire un'azione e non controlla direttamente la chiamata dell'azione.  
  
 Nella tabella seguente vengono descritte le impostazioni disponibili.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|Batch|L'azione deve essere eseguita come parte di un'operazione batch o di un'attività di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .|  
|Interattiva|L'azione viene eseguita in seguito alla chiamata dell'utente.|  
|Su apertura|L'azione viene eseguita quando il cubo viene aperto per la prima volta.|  
  
 **Applicazione**  
 Consente di digitare il nome dell'applicazione che può eseguire l'azione drill-through.  
  
 È inoltre possibile utilizzare questa opzione per identificare l'applicazione client che utilizza con maggiore frequenza questa azione, oltre a visualizzare icone appropriate accanto all'azione in un menu a comparsa.  
  
> [!NOTE]  
>  Questa opzione costituisce solo un'indicazione per un'applicazione client relativa a quale client deve eseguire un'azione e non controlla direttamente l'accesso all'azione. Nelle applicazioni devono essere nascoste le azioni associate ad altre applicazioni client.  
  
 **Descrizione**  
 Consente di digitare la descrizione facoltativa dell'azione.  
  
 **Caption**  
 Consente di digitare la didascalia da visualizzare per l'azione nell'applicazione client se l'opzione **Didascalia MDX** è impostata su **False**.  
  
 Consente di digitare l'espressione MDX che restituisce una stringa per la didascalia se l'opzione **Didascalia MDX** è impostata su **True**.  
  
 **Didascalia è MDX**  
 Selezionare **False** per indicare che **Didascalia** contiene una stringa letterale che rappresenta una didascalia da visualizzare per l'azione nell'applicazione client.  
  
 Selezionare **True** per indicare che **Didascalia** contiene un'espressione MDX che restituisce una stringa che rappresenta una didascalia da visualizzare per l'azione nell'applicazione client. L'espressione MDX deve essere risolta prima che l'azione venga restituita all'applicazione client.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a MDX &#40;Multidimensional Expressions&#41;](/sql/mdx/multidimensional-expressions-mdx-reference)   
 [Azioni &#40;Progettazione cubi&#41; &#40;Analysis Services - dati multidimensionali&#41;](actions-cube-designer-analysis-services-multidimensional-data.md)   
 [Sulla barra degli strumenti &#40;scheda azioni, Progettazione cubi&#41; &#40;Analysis Services - dati multidimensionali&#41;](toolbar-actions-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Libreria azioni &#40;scheda azioni, Progettazione cubi&#41; &#40;Analysis Services - dati multidimensionali&#41;](action-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [Strumenti di calcolo &#40;scheda azioni, Progettazione cubi&#41; &#40;Analysis Services - dati multidimensionali&#41;](calculation-tools-actions-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor dei Form delle azioni &#40;scheda azioni, Progettazione cubi&#41; &#40;Analysis Services - dati multidimensionali&#41;](action-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor dei Form delle azioni report &#40;scheda azioni, Progettazione cubi&#41; &#40;Analysis Services - dati multidimensionali&#41;](report-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)  
  
  
