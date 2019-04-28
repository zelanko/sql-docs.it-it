---
title: Strumenti di calcolo (scheda calcoli, Progettazione cubi) (Analysis Services - dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.calculationsview.calculationtoolspane.f1
ms.assetid: b1aa8a1a-6532-45d2-8f53-d3e211d7197a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 61aed2ac785c628d7a67df39af13aaf0a7c74914
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62681115"
---
# <a name="calculation-tools-calculations-tab-cube-designer-analysis-services---multidimensional-data"></a>Strumenti di calcolo (scheda Calcoli, Progettazione cubi) (Analysis Services - Dati multidimensionali)
  Utilizzare il riquadro **Strumenti di calcolo** della scheda **Calcoli** in Progettazione cubi per analizzare i metadati, le funzioni e i modelli da utilizzare per i calcoli.  
  
## <a name="options"></a>Opzioni  
 **Metadati**  
 Consente di visualizzare i metadati relativi al cubo selezionato.  
  
 Trascinare l'elemento selezionato nel riquadro Editor dello script, Editor form membro calcolato o Editor form set denominato per includere la sintassi MDX (Multidimensional Expressions) per questo elemento in corrispondenza della posizione selezionata nel riquadro.  
  
 **Funzioni**  
 Consente di visualizzare le funzioni disponibili per espressioni e condizioni.  
  
 Trascinare l'elemento selezionato nel riquadro **Editor dello script**, **Editor form membro calcolato**o **Editor form set denominato** per includere la sintassi MDX per questo elemento in corrispondenza della posizione selezionata nel riquadro.  
  
> [!NOTE]  
>  In modalità progetto, tramite la finestra di dialogo **Strumenti di calcolo** è possibile leggere le informazioni relative all'opzione da un file XML denominato MDXFunctions.xml, incluso in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. In modalità online, le informazioni relative all'opzione vengono recuperate dal set di righe dello schema MDSCHEMA_FUNCTIONS relativo all'istanza.  
  
 **Modelli**  
 Consente di visualizzare i modelli predefiniti disponibili per i membri calcolati, i set denominati e i comandi di script.  
  
 Trascinare l'elemento selezionato nel riquadro **Editor dello script**, **Editor form membro calcolato**o **Editor form set denominato** per includere la sintassi MDX per questo elemento in corrispondenza della posizione selezionata nel riquadro.  
  
## <a name="context-menu"></a>Menu di scelta rapida  
 Nel menu di scelta rapida che viene visualizzato quando si fa clic con il pulsante destro del mouse su un elemento del riquadro **Strumenti di calcolo** sono disponibili le opzioni seguenti:  
  
 **Copia**  
 Selezionare questa opzione per copiare negli Appunti l'elemento specificato in **Metadati** o **Funzioni** .  
  
> [!NOTE]  
>  Questa opzione non viene visualizzata se si seleziona **Modelli** .  
  
> [!NOTE]  
>  Questa opzione è disabilitata se non è possibile copiare il membro selezionato, ad esempio la cartella **Set** di una dimensione visualizzata in **Metadati** o la cartella del gruppo di funzioni relativa alla funzione visualizzata in **Funzioni**.  
  
 **Filtra membri**  
 Selezionare questa opzione per visualizzare la finestra di dialogo **Filtra membri** e filtrare i membri visualizzati per l'elemento selezionato in **Metadati**. Per altre informazioni sulla finestra di dialogo **Filtra membri** vedere [Finestra di dialogo Filtra membri &#40;Analysis Services - Dati multidimensionali&#41;](filter-members-dialog-box-analysis-services-multidimensional-data.md).  
  
> [!NOTE]  
>  Questa opzione viene visualizzata solo se si seleziona **Metadati** .  
  
> [!NOTE]  
>  Questa opzione è attivata solo se si seleziona un livello per un attributo in **Metadati**.  
  
 **Aggiungi modello**  
 Selezionare questa opzione per aggiungere allo script del cubo un nuovo membro calcolato, set denominato o comando di script basato sul modello selezionato e visualizzare **Editor dello script**, **Editor form membro calcolato**o **Editor form set denominato** a seconda del comando (in visualizzazione Form) o scorrere il contenuto del riquadro **Editor dello script** fino alla posizione del comando nello script del cubo (in visualizzazione Script).  
  
> [!NOTE]  
>  Questa opzione viene visualizzata solo se si seleziona **Metadati** .  
  
## <a name="see-also"></a>Vedere anche  
 [Finestra di progettazione del cubo &#40;Analysis Services - dati multidimensionali&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Sulla barra degli strumenti &#40;scheda calcoli, Progettazione cubi&#41; &#40;Analysis Services - dati multidimensionali&#41;](toolbar-calculations-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Libreria script &#40;scheda calcoli, Progettazione cubi&#41; &#40;Analysis Services - dati multidimensionali&#41;](script-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor Form membro calcolato &#40;scheda calcoli, Progettazione cubi&#41; &#40;Analysis Services - dati multidimensionali&#41;](calculated-member-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor Form Set denominato &#40;scheda calcoli, Progettazione cubi&#41; &#40;Analysis Services - dati multidimensionali&#41;](named-set-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor di script &#40;scheda calcoli, Progettazione cubi&#41; &#40;Analysis Services - dati multidimensionali&#41;](script-editor-calculations-cube-designer-analysis-services-multidimensional-data.md)   
 [Calcoli &#40;Progettazione cubi&#41; &#40;Analysis Services - dati multidimensionali&#41;](calculations-cube-designer-analysis-services-multidimensional-data.md)  
  
  
