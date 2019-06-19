---
title: Editor dei Form delle azioni report (scheda azioni, Progettazione cubi) (Analysis Services - dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.actionexpression.reportaction.f1
ms.assetid: cebfdd07-e376-46d6-86ef-b6f816a2f360
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eeb3df670097c0d511a9f5b779b6705f40a5e897
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66070303"
---
# <a name="report-action-form-editor-actions-tab-cube-designer-analysis-services---multidimensional-data"></a>Editor dei form delle azioni report (scheda Azioni, Progettazione cubi) (Analysis Services - Dati multidimensionali)
  Usare il riquadro **Editor dei form delle azioni report** nella scheda **Azioni** in Progettazione cubi per modificare l'azione del report selezionata nel riquadro **Libreria azioni**.  
  
## <a name="options"></a>Opzioni  
 **Name**  
 Consente di digitare il nome dell'azione.  
  
 **Destinazione azione**  
 Espandere la finestra per visualizzare le opzioni **Tipo di destinazione** e **Oggetti di destinazione** .  
  
 **Tipo di destinazione**  
 Consente di selezionare il tipo di oggetto a cui associare l'azione. Il server restituisce al client solo le azioni del tipo specificato relative all'oggetto. L'azione è disponibile per il client se il valore di **Condizione** viene soddisfatto e se sono selezionati gli oggetti specificati nella tabella seguente.  
  
|Value|Oggetto selezionato|  
|-----------|---------------------|  
|Membri dell'attributo|In **Oggetto di destinazione**è selezionato un membro dell'attributo da un livello basato sull'attributo.<br /><br /> Nota: Altre gerarchie utente che usano l'attributo selezionato ereditano l'azione del report.|  
|Celle|In **Oggetto di destinazione** è selezionato il set denominato. Selezionare **Tutte le celle** per selezionare tutte le celle del cubo.|  
|Cube|In **Oggetto di destinazione** è selezionato il cubo. Selezionare CURRENTCUBE per utilizzare il cubo corrente.<br /><br /> Nota: Uso di CURRENTCUBE garantisce maggiore portabilità nel caso in cui il cubo venga rinominato o l'azione copiata in altri cubi. È consigliabile utilizzare CURRENTCUBE per rappresentare il cubo corrente.|  
|Membri della dimensione|In **Oggetto di destinazione** è selezionato un membro della dimensione.|  
|Gerarchia|In **Oggetto di destinazione** è selezionata la gerarchia.|  
|Membri della gerarchia|In **Oggetto di destinazione** è selezionato un membro della gerarchia.|  
|Level|In **Oggetto di destinazione** è selezionato il livello.|  
|Membri del livello|In **Oggetto di destinazione** è selezionato un membro del livello.|  
  
 **Oggetto di destinazione**  
 Consente di selezionare l'oggetto a cui associare l'azione. L'istanza di [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] restituisce al client solo le azioni applicabili all'oggetto selezionato. L'elenco degli oggetti disponibili è vincolato dall'opzione selezionata in **Tipo di destinazione**.  
  
 **Condizione (facoltativa)**  
 Consente di immettere l'espressione MDX (Multidimensional Expression) che descrive una condizione facoltativa, usata insieme a **Oggetto di destinazione**, per vincolare ulteriormente la disponibilità dell'azione. L'espressione deve restituire un valore booleano il quale, se è True, indica che l'azione è disponibile.  
  
 Trascinare gli elementi selezionati dal riquadro **Strumenti di calcolo** alla casella di questa opzione per includere la sintassi MDX per l'elemento selezionato.  
  
 **Server di report**  
 Espandere la finestra per visualizzare le opzioni **Nome server**, **Percorso server**e **Formato report** .  
  
 **Nome server**  
 Digitare il nome dell'istanza di [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] in cui l'azione esegue il report.  
  
 **Percorso server**  
 Consente di digitare il percorso del report nell'istanza di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Ad esempio, digitare **Vendite/VenditeAnnualiPerCategoria**.  
  
 **Formato report**  
 Consente di selezionare il formato in cui viene restituito il report. Nella tabella seguente vengono descritti i formati disponibili.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|HTML5|Il report viene restituito in un formato conforme a HTML 5.0.|  
|HTML3|Il report viene restituito in un formato conforme a HTML 3.2.|  
|Excel|Il report viene restituito come file di cartella di lavoro (XLS) di [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Excel.|  
|PDF|Il report viene restituito come file Adobe PDF con estensione pdf.|  
  
 **Parametri (facoltativi)**  
 Espandere la finestra per visualizzare una griglia in cui è possibile immettere i parametri del report specificati in **Report**. La griglia include le colonne seguenti:  
  
|colonna|Descrizione|  
|------------|-----------------|  
|**Nome parametro**|Consente di digitare il nome del parametro del report da passare al report.|  
|**Valore parametro**|Consente di digitare il valore del parametro del report da passare al report.<br /><br /> Fare clic sul pulsante con i puntini di sospensione ( **...** ) per visualizzare la finestra di dialogo **Generatore MDX** e creare un'espressione MDX che restituisca il valore del parametro del report. Per altre informazioni sulla finestra di dialogo **Generatore MDX**, vedere [Generatore MDX &#40;Analysis Services - Dati multidimensionali&#41;](mdx-builder-analysis-services-multidimensional-data.md).<br /><br /> Se il parametro è impostato su un'espressione MDX, tale espressione viene valutata quando l'azione viene eseguita, altrimenti viene passata al report senza alcuna modifica.|  
  
 **Proprietà aggiuntive**  
 Espandere la finestra per visualizzare le opzioni **Chiamata**, **Applicazione**, **Descrizione**, **Didascalia**e **Didascalia MDX** .  
  
 **Chiamata**  
 Consente di selezionare l'impostazione che indica quando eseguire l'azione.  
  
> [!NOTE]  
>  Questa opzione costituisce solo un'indicazione per un'applicazione client relativa al momento in cui eseguire un'azione e non controlla direttamente la chiamata dell'azione.  
  
 Nella tabella seguente vengono descritte le impostazioni disponibili.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|Batch|L'azione deve essere eseguita nell'ambito di un'operazione batch o di un'attività di [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .|  
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
  
 Digitare l'espressione MDX che restituisce una stringa per la didascalia se l'opzione **Didascalia MDX** è impostata su **True**.  
  
 **Didascalia MDX**  
 Selezionare **False** per indicare che **Didascalia** contiene una stringa letterale che rappresenta una didascalia da visualizzare per l'azione nell'applicazione client.  
  
 Selezionare **True** per indicare che **Didascalia** contiene un'espressione MDX che restituisce una stringa che rappresenta una didascalia da visualizzare per l'azione nell'applicazione client. L'espressione MDX deve essere risolta prima che l'azione venga restituita all'applicazione client.  
  
## <a name="see-also"></a>Vedere anche  
 [Azioni &#40;Progettazione cubi&#41; &#40;Analysis Services - dati multidimensionali&#41;](actions-cube-designer-analysis-services-multidimensional-data.md)   
 [Sulla barra degli strumenti &#40;scheda azioni, Progettazione cubi&#41; &#40;Analysis Services - dati multidimensionali&#41;](toolbar-actions-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Libreria azioni &#40;scheda azioni, Progettazione cubi&#41; &#40;Analysis Services - dati multidimensionali&#41;](action-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [Strumenti di calcolo &#40;scheda azioni, Progettazione cubi&#41; &#40;Analysis Services - dati multidimensionali&#41;](calculation-tools-actions-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor dei Form delle azioni &#40;scheda azioni, Progettazione cubi&#41; &#40;Analysis Services - dati multidimensionali&#41;](action-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor dei Form delle azioni drill-through &#40;scheda azioni, Progettazione cubi&#41; &#40;Analysis Services - dati multidimensionali&#41;](drillthrough-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)  
  
  
