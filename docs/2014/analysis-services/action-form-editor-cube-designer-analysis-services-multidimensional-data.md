---
title: Editor dei Form delle azioni (scheda azioni, Progettazione cubi) (Analysis Services - dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.actionexpression.action.f1
ms.assetid: c363a29b-6099-473c-9625-460cc15b3d95
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f7c0a9b232a30fbaa4358bf9b23eb28ff16d79b2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66062963"
---
# <a name="action-form-editor-actions-tab-cube-designer-analysis-services---multidimensional-data"></a>Editor dei form delle azioni (scheda Azioni, Progettazione cubi) (Analysis Services - Dati multidimensionali)
  Usare il riquadro dell'editor dei form delle azioni della scheda **Azioni** in Progettazione cubi per creare e modificare azioni standard.  
  
## <a name="options"></a>Opzioni  
 **Name**  
 Consente di digitare il nome dell'azione.  
  
 **Destinazione azione**  
 Espandere la finestra per visualizzare le opzioni **Tipo di destinazione** e **Oggetti di destinazione** .  
  
 **Tipo di destinazione**  
 Consente di selezionare il tipo di oggetto a cui associare l'azione. Il server restituisce al client solo le azioni del tipo specificato relative all'oggetto. L'azione è disponibile per il client se il valore di **Condizione** viene soddisfatto e se sono selezionati gli oggetti specificati nella tabella seguente.  
  
|Value|Oggetto selezionato|  
|-----------|---------------------|  
|Membri dell'attributo|Un membro è selezionato da un livello basato sull'attributo in **Oggetto di destinazione**.|  
|Celle|In **Oggetto di destinazione** è selezionato il set denominato. Selezionare **Tutte le celle** per selezionare tutte le celle del cubo.|  
|Cube|In **Oggetto di destinazione** è selezionato il cubo. Selezionare CURRENTCUBE per utilizzare il cubo corrente.<br /><br /> Nota: Uso di CURRENTCUBE garantisce maggiore portabilità nel caso in cui il cubo venga rinominato o l'azione copiata in altri cubi. È consigliabile utilizzare CURRENTCUBE per rappresentare il cubo corrente.|  
|Membri della dimensione|In **Oggetto di destinazione** è selezionato un membro della dimensione.|  
|Gerarchia|In **Oggetto di destinazione** è selezionata la gerarchia.|  
|Membri della gerarchia|In **Oggetto di destinazione** è selezionato un membro della gerarchia.|  
|Level|In **Oggetto di destinazione** è selezionato il livello.|  
|Membri del livello|In **Oggetto di destinazione** è selezionato un membro del livello.|  
  
 **Oggetto di destinazione**  
 Consente di selezionare l'oggetto a cui associare l'azione. L'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] restituisce nel client solo le azioni applicabili all'oggetto selezionato. L'elenco degli oggetti disponibili è vincolato dall'opzione selezionata in **Tipo di destinazione**.  
  
 **Condizione (facoltativa)**  
 Consente di immettere l'espressione MDX (Multidimensional Expression) che descrive una condizione facoltativa, usata insieme a **Oggetto di destinazione**, per vincolare ulteriormente la disponibilità dell'azione. L'espressione deve restituire un valore booleano il quale, se è True, indica che l'azione è disponibile.  
  
 Trascinare gli elementi selezionati dal riquadro **Strumenti di calcolo** alla casella di questa opzione per includere la sintassi MDX per l'elemento selezionato.  
  
 **Contenuto azione**  
 Espandere per visualizzare le opzioni **Tipo** ed **Espressione azione** .  
  
 **Tipo**  
 Consente di selezionare il tipo di azione da intraprendere quando l'azione viene eseguita. Sono disponibili i tipi di azione seguenti:  
  
|Value|Descrizione|  
|-----------|-----------------|  
|Set di dati|Restituisce un'istruzione MDX che rappresenta un set di dati multidimensionale e deve essere eseguita e visualizzata dall'applicazione client.|  
|Proprietario|Restituisce una stringa sul proprietario che può essere interpretata dalle applicazioni client associate all'impostazione **Applicazione** relativa a questa azione.|  
|Set di righe|Restituisce un'istruzione MDX che rappresenta un set di righe tabulare e deve essere eseguita e visualizzata dall'applicazione client.|  
|.|Restituisce una stringa di comando che deve essere eseguita dall'applicazione client.|  
|URL|Restituisce un URL a cui accedere da un'applicazione client, in genere tramite un browser Internet.|  
  
 Per altre informazioni sui tipi di azione, vedere [Azioni &#40;Analysis Services - Dati multidimensionali&#41;](multidimensional-models/actions-analysis-services-multidimensional-data.md).  
  
 **Espressione azione**  
 Consente di digitare l'espressione MDX che restituisce la stringa restituita dall'azione nell'applicazione client per l'esecuzione.  
  
 **Proprietà aggiuntive**  
 Espandere la finestra per visualizzare le opzioni **Chiamata**, **Applicazione**, **Descrizione**, **Didascalia**e **Didascalia MDX** .  
  
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
 Consente di digitare il nome dell'applicazione in grado di interpretare la stringa restituita da **Espressione azione**.  
  
 È inoltre possibile utilizzare questa opzione per identificare l'applicazione client che utilizza con maggiore frequenza questa azione, oltre a visualizzare icone appropriate accanto all'azione in un menu a comparsa.  
  
> [!NOTE]  
>  Questa opzione costituisce solo un'indicazione per un'applicazione client relativa a quale client deve eseguire un'azione e non controlla direttamente l'accesso all'azione. Nelle applicazioni devono essere nascoste le azioni associate ad altre applicazioni client.  
  
 **Descrizione**  
 Consente di digitare la descrizione facoltativa dell'azione.  
  
 **Caption**  
 Consente di digitare la didascalia da visualizzare per l'azione nell'applicazione client se l'opzione **Didascalia MDX** è impostata su **False**.  
  
 Consente di digitare l'espressione MDX che restituisce una stringa per la didascalia se l'opzione **Didascalia MDX** è impostata su **True**.  
  
 **Didascalia MDX**  
 Selezionare **False** per indicare che **Didascalia** contiene una stringa letterale che rappresenta una didascalia da visualizzare per l'azione nell'applicazione client.  
  
 Selezionare **True** per indicare che **Didascalia** contiene un'espressione MDX che restituisce una stringa che rappresenta una didascalia da visualizzare per l'azione nell'applicazione client. L'espressione MDX deve essere risolta prima che l'azione venga restituita all'applicazione client.  
  
## <a name="see-also"></a>Vedere anche  
 [Azioni &#40;Progettazione cubi&#41; &#40;Analysis Services - dati multidimensionali&#41;](actions-cube-designer-analysis-services-multidimensional-data.md)   
 [Sulla barra degli strumenti &#40;scheda azioni, Progettazione cubi&#41; &#40;Analysis Services - dati multidimensionali&#41;](toolbar-actions-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Libreria azioni &#40;scheda azioni, Progettazione cubi&#41; &#40;Analysis Services - dati multidimensionali&#41;](action-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [Strumenti di calcolo &#40;scheda azioni, Progettazione cubi&#41; &#40;Analysis Services - dati multidimensionali&#41;](calculation-tools-actions-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor dei Form delle azioni drill-through &#40;scheda azioni, Progettazione cubi&#41; &#40;Analysis Services - dati multidimensionali&#41;](drillthrough-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor dei Form delle azioni report &#40;scheda azioni, Progettazione cubi&#41; &#40;Analysis Services - dati multidimensionali&#41;](report-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)  
  
  
