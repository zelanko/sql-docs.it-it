---
title: Selezione metodo di creazione (creazione guidata dimensione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.dimensiondefinition.f1
ms.assetid: 291b0b2d-a03a-4df6-82f7-90ad92d4d1cf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d44afc5bb4c352a2cb5dfd39030a52db990e3a0b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66069600"
---
# <a name="select-creation-method-dimension-wizard"></a>Seleziona metodo di creazione (Creazione guidata dimensione)
  Usare la pagina **Seleziona metodo di creazione** per scegliere la modalità di creazione della dimensione.  
  
 **Per aprire la Creazione guidata dimensione.**  
  
-   In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]fare clic con il pulsante destro del mouse sulla cartella **Dimensioni**in **Esplora soluzioni** per scegliere un progetto di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , quindi fare clic su **Nuova dimensione**.  
  
## <a name="options"></a>Opzioni  
 **Utilizza una tabella esistente**  
 Creare una dimensione da una o più tabelle in un'origine dati. Gli attributi disponibili per la dimensione dipenderanno dalla struttura dei dati nella tabella.  
  
 Per altre informazioni, vedere [Creare una dimensione utilizzando una tabella esistente](multidimensional-models/create-a-dimension-by-using-an-existing-table.md).  
  
 **Genera una tabella dei tempi nell'origine dei dati**  
 Creare una tabella dei tempi nell'origine dei dati sottostanti, quindi utilizzare tale tabella per creare una dimensione temporale. Utilizzare questa opzione quando non esiste tale tabella e non si vuole utilizzare uno script per crearne una. La nuova tabella dei tempi conterrà i dati per l'intervallo di dati, gli attributi e i calendari specificati nella procedura guidata.  
  
> [!NOTE]  
>  Per utilizzare questa opzione, si deve disporre delle autorizzazioni per creare gli oggetti nell'origine dei dati sottostante. Se non si hanno le autorizzazioni per creare oggetti sull'origine dati, provare a usare in alternativa l'opzione **Genera una tabella dei tempi nel server** .  
  
 Per altre informazioni, vedere [Create a Time Dimension by Generating a Time Table](multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md)(Creare una dimensione temporale generando una tabella dei tempi).  
  
 **Genera una tabella dei tempi nel server**  
 Crea una tabella dei tempi direttamente nel server, quindi utilizzare tale tabella per creare una dimensione temporale. Utilizzare questa opzione se non si dispone delle autorizzazioni per creare oggetti nell'origine dati sottostante. La nuova dimensione temporale conterrà i dati per l'intervallo di dati, gli attributi e i calendari che si specificano nella procedura guidata.  
  
 Per altre informazioni, vedere [Create a Time Dimension by Generating a Time Table](multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md)(Creare una dimensione temporale generando una tabella dei tempi).  
  
 **Genera una tabella diversa dalla tabella dei tempi nell'origine dati**  
 Progetta la dimensione senza un'origine dati relazionale sottostante, quindi genera lo schema necessario per l'origine dati. Questo approccio è noto come modellizzazione dall'alto in basso.  
  
> [!NOTE]  
>  Per utilizzare questa opzione, si deve disporre delle autorizzazioni per creare gli oggetti nell'origine dei dati sottostante.  
  
 È possibile compilare la dimensione con o senza un modello. Per creare la dimensione con un modello, selezionare il modello dall'elenco **Modello** .  
  
 Per altre informazioni, vedere [Creare una dimensione generando una tabella non temporale nell'origine dati](multidimensional-models/create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md).  
  
 **Modello**  
 Selezionare il modello che si desidera utilizzare per creare la dimensione. I modelli offrono un set completo di definizioni di attributi e gerarchie orientate ad applicazioni aziendali specifiche.  
  
> [!NOTE]  
>  Questa opzione è disponibile solo quando l'opzione **Genera una tabella diversa dalla tabella dei tempi nell'origine dati** è stata selezionata.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida sensibile al contesto della creazione guidata dimensione](dimension-wizard-f1-help.md)   
 [Dimensioni &#40;Analysis Services Dati multidimensionali&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [Dimensioni nei modelli multidimensionali](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
