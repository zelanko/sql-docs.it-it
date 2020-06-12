---
title: Query e filtro (scheda Esplorazione, Progettazione cubi) (Analysis Services-Dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.browsecube.filterpane.f1
ms.assetid: f5cf0bb1-3afb-4856-a2ef-614deb4e7e49
author: minewiskan
ms.author: owend
ms.openlocfilehash: aa501e2a5b23f32fbd10d244788b1e6e938e938b
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84539733"
---
# <a name="query-and-filter-browser-tab-cube-designer-analysis-services---multidimensional-data"></a>Query e filtro (scheda Esplorazione, Progettazione cubi) (Analysis Services - Dati multidimensionali)
  In questa area della scheda **Esplorazione** in Progettazione cubi è presente un'area della query e del filtro che consente di scegliere dati del cubo da utilizzare nell'esplorazione o nelle query. È possibile aggiungere tutti gli oggetti cubo desiderati, quindi visualizzare i risultati nell'area dei dati o esportare i risultati in un report tramite Analizza in Excel per verificare come verranno visualizzati i dati agli utenti finali.  
  
> [!WARNING]  
>  Quando si utilizzano i dati in questa area, per impostazione predefinita in **Esplorazione** viene utilizzata la modalità di progettazione grafica. È tuttavia possibile modificare la query direttamente tramite MDX, facendo clic sull'interruttore **Modalità progettazione** . Quando si esegue questa operazione, il riquadro che consente di progettare filtri sulle dimensioni viene nascosto. Se si desidera aggiungere un filtro, è possibile tornare alla modalità di progettazione grafica.  
  
 Per impostazione predefinita, vengono utilizzate le credenziali dell'utente corrente, non quelle specificate nella pagina **Impostazioni di rappresentazione** , per la connessione all'origine dati quando viene eseguita una query. È tuttavia possibile modificare anche il contesto utente per la query o il report facendo clic su **Cambia utente** sulla **Barra degli strumenti**.  
  
## <a name="options"></a>Opzioni  
 **Dimensione**  
 Consente di selezionare la dimensione in base a cui sezionare il sottocubo.  
  
 **Gerarchia**  
 Consente di selezionare la gerarchia in base a cui sezionare il sottocubo.  
  
 **Operatore**  
 Consente di selezionare l'operatore che definisce il modo in cui l'espressione contenuta in **Espressione filtro** viene applicata alla gerarchia selezionata. Nella tabella seguente vengono descritti gli operatori disponibili.  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|**Uguale**|I risultati sono limitati al set definito in **Espressione filtro**.|  
|**Diverso da**|I risultati sono limitati ai membri esclusi dal set definito in **Espressione filtro**.|  
|**In**|I risultati sono limitati al set denominato scelto in **Espressione filtro**.|  
|**Non incluso**|I risultati sono limitati ai membri esclusi dal set denominato scelto in **Espressione filtro**.|  
|**Contiene**|I risultati sono limitati ai membri i cui nomi contengono la stringa inclusa in **Espressione filtro**.|  
|**Inizia con**|I risultati sono limitati ai membri i cui nomi iniziano con la stringa inclusa in **Espressione filtro**.|  
|**Intervallo (inclusivo)**|I risultati sono limitati all'intervallo scelto in **Espressione filtro**.|  
|**Intervallo (esclusivo)**|I risultati sono limitati ai membri esclusi dall'intervallo scelto in **Espressione filtro**.|  
|**MDX**|I risultati sono limitati al set di espressioni MDX incluso in **Espressione filtro**.|  
  
 **Espressione filtro**  
 Consente di digitare l'espressione che deve essere valutata da **Operatore**, che limita i risultati da visualizzare.  
  
> [!NOTE]  
>  Questo campo rappresenta un elemento dinamico per l'immissione di dati, che cambia aspetto per riflettere i tipi di dati necessari per l'operatore selezionato.  
  
## <a name="see-also"></a>Vedere anche  
 [Progettazione cubi &#40;Analysis Services-Dati multidimensionali&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Progettazione cubi &#40;browser&#41; &#40;Analysis Services Dati multidimensionali&#41;](browser-cube-designer-analysis-services-multidimensional-data.md)   
 [Barra degli strumenti &#40;scheda Esplorazione, Progettazione cubi&#41; &#40;Analysis Services Dati multidimensionali&#41;](toolbar-browser-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Analizza in Excel &#40;scheda Esplorazione, Progettazione cubi&#41; &#40;Analysis Services Dati multidimensionali&#41;](analyze-in-excel-browser-cube-designer-analysis-services-multidimensional-data.md)   
 [Scheda Esplorazione &#40;metadati, Progettazione cubi&#41; &#40;Analysis Services Dati multidimensionali&#41;](metadata-browser-tab-cube-designer-analysis-services-multidimensional-data.md)  
  
  
