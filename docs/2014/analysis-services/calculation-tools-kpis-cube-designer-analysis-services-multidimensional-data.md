---
title: Strumenti di calcolo (scheda KPI, Progettazione cubi) (Analysis Services-Dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.kpisview.calculationtoolspane.f1
ms.assetid: c030c725-7763-4c23-9988-4b274a88fc31
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ecd16965c81ccb091d70320bd91c56112d3c15a0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66088264"
---
# <a name="calculation-tools-kpis-tab-cube-designer-analysis-services---multidimensional-data"></a>Strumenti di calcolo (scheda KPI, Progettazione cubi) (Analysis Services - Dati multidimensionali)
  Usare il riquadro **Strumenti di calcolo** della scheda **KPI** in Progettazione cubi per esaminare i metadati, le funzioni e i modelli disponibili per gli indicatori di prestazioni chiave (KPI).  
  
> [!NOTE]  
>  Questo riquadro viene visualizzato solo in visualizzazione Form.  
  
## <a name="options"></a>Opzioni  
 **Metadati**  
 Consente di visualizzare i metadati relativi al cubo selezionato.  
  
 Trascinare un elemento selezionato nel riquadro **Editor form KPI** per includere la sintassi MDX (Multidimensional Expression) per questo elemento in corrispondenza del percorso specificato nel riquadro.  
  
 **Funzioni**  
 Consente di visualizzare le funzioni disponibili per espressioni e condizioni.  
  
 Trascinare un elemento selezionato nel riquadro **Editor form KPI** per includere la sintassi MDX per questo elemento in corrispondenza della posizione specificata nel riquadro.  
  
> [!NOTE]  
>  In modalità progetto, tramite la finestra di dialogo **Strumenti di calcolo** è possibile leggere le informazioni relative all'opzione da un file XML denominato MDXFunctions.xml, incluso in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. In modalità online, le informazioni relative all'opzione vengono recuperate dal set di righe dello schema MDSCHEMA_FUNCTIONS relativo all'istanza.  
  
 **Modelli**  
 Consente di visualizzare i modelli predefiniti disponibili per gli indicatori KPI.  
  
 Trascinare un elemento selezionato nel riquadro **Editor form KPI** per includere la sintassi MDX per questo elemento in corrispondenza della posizione specificata nel riquadro.  
  
## <a name="context-menu"></a>Menu di scelta rapida  
 Nel menu di scelta rapida che viene visualizzato quando si fa clic con il pulsante destro del mouse su un elemento del riquadro **Strumenti di calcolo** sono disponibili le opzioni seguenti:  
  
 **Copia**  
 Selezionare questa opzione per copiare negli Appunti l'elemento specificato in **Metadati** o **Funzioni** .  
  
> [!NOTE]  
>  Questa opzione non viene visualizzata se si seleziona **modelli** .  
  
> [!NOTE]  
>  Questa opzione è disabilitata se non è possibile copiare il membro selezionato, ad esempio la cartella **set** di una dimensione visualizzata in **metadati** o la cartella del gruppo di funzioni per una funzione visualizzata in **funzioni**.  
  
 **Filtra membri**  
 Selezionare questa opzione per visualizzare la finestra di dialogo **Filtra membri** e filtrare i membri visualizzati per l'elemento selezionato in **Metadati**. Per altre informazioni sulla finestra di dialogo **Filtra membri** vedere [Finestra di dialogo Filtra membri &#40;Analysis Services - Dati multidimensionali&#41;](filter-members-dialog-box-analysis-services-multidimensional-data.md).  
  
> [!NOTE]  
>  Questa opzione viene visualizzata solo se si seleziona **metadati** .  
  
> [!NOTE]  
>  Questa opzione è abilitata solo se nei **metadati**è selezionato un livello per un attributo.  
  
 **Aggiungi modello**  
 Selezionare questa opzione per aggiungere un nuovo membro calcolato, set denominato o comando script in base al modello selezionato nello script del cubo e visualizzare il riquadro **Editor form KPI** in visualizzazione Form.  
  
> [!NOTE]  
>  Questa opzione viene visualizzata solo se si seleziona **metadati** .  
  
## <a name="see-also"></a>Vedere anche  
 [Progettazione cubi &#40;Analysis Services-Dati multidimensionali&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Indicatori KPI &#40;Progettazione cubi&#41; &#40;Analysis Services Dati multidimensionali&#41;](kpis-cube-designer-analysis-services-multidimensional-data.md)   
 [Barra degli strumenti &#40;scheda KPI, Progettazione cubi&#41; &#40;Analysis Services Dati multidimensionali&#41;](toolbar-kpis-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Libreria KPI &#40;scheda KPI, Progettazione cubi&#41; &#40;Analysis Services Dati multidimensionali&#41;](kpi-organizer-kpis-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor form KPI &#40;scheda KPI, Progettazione cubi&#41; &#40;Analysis Services Dati multidimensionali&#41;](kpi-form-editor-kpis-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Visualizzatore KPI &#40;scheda KPI, Progettazione cubi&#41; &#40;Analysis Services Dati multidimensionali&#41;](kpi-browser-kpis-tab-cube-designer-analysis-services-multidimensional-data.md)  
  
  
