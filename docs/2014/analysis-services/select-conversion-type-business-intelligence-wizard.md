---
title: Selezionare il tipo di conversione (configurazione guidata Business Intelligence) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.currencyconversion.conversiontype.f1
ms.assetid: 2c664138-e8a1-4c47-8e7d-ee01c57e4692
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 97ab8896d13bfb19790148fb6f01bb8e054ab270
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62748083"
---
# <a name="select-conversion-type-business-intelligence-wizard"></a>Selezione tipo di conversione (Configurazione guidata funzionalità di Business Intelligence)
  Utilizzare la pagina **Selezione tipo di conversione** per definire le relazioni tra le valute locali e le valute report per le transazioni archiviate in più valute. Una valuta locale è la valuta in cui vengono archiviate le transazioni per le misure selezionate nella pagina **Selezione misure** . La valuta report è la valuta in cui vengono convertite le transazioni selezionate nella pagina **Selezione misure** .  
  
> [!NOTE]  
>  Questa pagina non viene visualizzata se la Configurazione guidata funzionalità di Business Intelligence viene avviata da Progettazione dimensioni oppure facendo clic con il pulsante destro del mouse su una dimensione in Esplora soluzioni in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
## <a name="options"></a>Opzioni  
 **Molti-a-molti**  
 Consente di archiviare le transazioni utilizzando le valute locali. La funzionalità di conversione di valuta converte le transazioni nella valuta pivot specificata nella pagina **Impostazione opzioni di conversione valuta** e quindi in una o più valute report diverse.  
  
 Se, ad esempio, si imposta la valuta pivot sul dollaro statunitense (USD), le transazioni possono venire archiviate nella tabella dei fatti in euro (EUR), dollari australiani (AUD) e peso messicani (MXN). Selezionando questa opzione le transazioni vengono prima convertite dalle valute locali specificate alla valuta pivot e quindi riconvertite dalla valuta pivot alle valute report specificate. Di conseguenza le transazioni possono essere archiviate nelle valute locali specificate e visualizzate sia nella valuta pivot specificata che in una delle valute report specificate nella pagina **Impostazione valute report** .  
  
 **Molti-a-uno**  
 Consente di archiviare le transazioni utilizzando le valute locali. La funzionalità di conversione di valuta converte le transazioni nella valuta pivot specificata nella pagina **Impostazione opzioni di conversione valuta** . La valuta pivot viene utilizzata come unica valuta report specificata.  
  
> [!NOTE]  
>  Se si seleziona questa opzione la pagina **Impostazione valute report** non viene visualizzata.  
  
 Se, ad esempio, si imposta la valuta pivot sul dollaro statunitense (USD), le transazioni possono venire archiviate nella tabella dei fatti in euro (EUR), dollari australiani (AUD) e peso messicani (MXN). Selezionando questa opzione le transazioni vengono convertite dalle valute locali specificate alla valuta pivot. Di conseguenza le transazioni possono essere archiviate nelle valute locali specificate e visualizzate nella valuta pivot specificata.  
  
 **Uno-a-molti**  
 Consente di archiviare le transazioni usando la valuta pivot specificata nella pagina **Impostazione opzioni di conversione valuta** , quindi in una o più valute report diverse.  
  
> [!NOTE]  
>  Se si seleziona questa opzione la pagina **Definizione associazioni valute locali** non viene visualizzata.  
  
 Se, ad esempio, si imposta la valuta pivot sul dollaro statunitense (USD), le transazioni vengono archiviate nella tabella dei fatti in questa valuta. Selezionando questa opzione le transazioni vengono convertite dalla valuta pivot alle valute report specificate. Di conseguenza le transazioni possono essere archiviate nella valuta pivot specificata e visualizzate sia nella valuta pivot specificata che in una delle valute report specificate nella pagina **Impostazione valute report** .  
  
## <a name="see-also"></a>Vedere anche  
 [Guida sensibile al contesto della Configurazione guidata funzionalità di Business Intelligence](business-intelligence-wizard-f1-help.md)   
 [Finestra di progettazione del cubo &#40;Analysis Services - dati multidimensionali&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Finestra di progettazione della dimensione &#40;Analysis Services - dati multidimensionali&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
