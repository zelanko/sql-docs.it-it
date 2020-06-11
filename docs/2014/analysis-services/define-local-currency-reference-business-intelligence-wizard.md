---
title: Definizione riferimento valuta locale (configurazione guidata funzionalità di Business Intelligence) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.currencyconversion.localcurrency.f1
ms.assetid: 74993b0d-dfca-476b-acba-d66c593680a5
author: minewiskan
ms.author: owend
ms.openlocfilehash: 12a32140b2586b440fabcadc8385ab801963280a
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528837"
---
# <a name="define-local-currency-reference-business-intelligence-wizard"></a>Definizione associazioni valute locali (Configurazione guidata funzionalità di Business Intelligence)
  Usare la pagina **Definizione associazioni valute locali** per definire le valute locali per la funzionalità di conversione valuta che riguarda il tipo di conversione molti-a-molti o molti-a-uno specificato nella pagina **Selezione tipo di conversione** . Una valuta locale è la valuta in cui vengono archiviate le transazioni per le misure selezionate nella pagina **Selezione misure** .  
  
> [!NOTE]  
>  Questa pagina non viene visualizzata se la Configurazione guidata funzionalità di Business Intelligence viene avviata da Progettazione dimensioni oppure facendo clic con il pulsante destro del mouse su una dimensione in Esplora soluzioni in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Questa pagina non viene inoltre visualizzata se è stata selezionata l'opzione **One-to-Many** (Uno-a-molti) nella pagina **Selezione tipo di conversione** .  
  
## <a name="options"></a>Opzioni  
 **Identificatori nella tabella dei fatti**  
 Selezionare questa opzione per specificare un attributo che fornisce gli identificatori di valuta per le valute locali in una dimensione di tipo Valuta a cui fa riferimento la tabella dei fatti contenente le misure selezionate nella pagina **Selezione misure** . Una dimensione di tipo valuta in un oggetto la cui `Type` proprietà è impostata su *Currency*.  
  
 Utilizzare questa opzione quando è la transazione stessa a determinare la valuta corrente per la transazione. Nel database di esempio, ad esempio [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] , il gruppo di misure Internet Sales ha una relazione di tipo regolare con la dimensione di tipo valuta. La tabella dei fatti per tale gruppo di misure include una colonna chiave esterna che fa riferimento agli identificatori di valuta della tabella della dimensione.  
  
 **Dimensione e attributo di valuta a cui fanno riferimento i dati della tabella dei fatti**  
 Consente di selezionare l'attributo di valuta nella dimensione di tipo Valuta i cui membri rappresentano gli identificatori di valuta per le valute locali. Un attributo di valuta è uno la cui `Type` proprietà è impostata su *Currency*.  
  
> [!NOTE]  
>   Questa opzione non è disponibile se non è stata selezionata l'opzione **Identificatori nella tabella dei fatti** .  
  
 **Attributi nella tabella delle dimensioni**  
 Consente di specificare un attributo da una dimensione correlata al gruppo di misure che contiene gli identificatori di valuta per le valute locali.  
  
 Utilizzare questa opzione quando è la relazione tra una transazione e un'altra entità commerciale, ad esempio un percorso, a determinare la valuta locale per la transazione. Nel database di esempio, ad esempio [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] , il gruppo di misure Financial Reporting dispone di una relazione di dimensione di tipo riferimento con la dimensione di tipo valuta tramite la dimensione Organization. Cioè, la tabella dei fatti per il gruppo di misure Financial Reporting contiene una colonna chiave esterna che fa riferimento a membri nella tabella della dimensione per la dimensione Organization. Questa tabella della dimensione include a sua volta una colonna chiave esterna che fa riferimento agli identificatori di valuta nella tabella della dimensione per la dimensione di tipo Valuta.  
  
 **Attributo della dimensione che fa riferimento alla valuta**  
 Consente di selezionare l'attributo all'interno di una dimensione i cui membri fanno riferimento agli identificatori di valuta per la valuta locale.  
  
> [!NOTE]  
>   Questa opzione non è disponibile se non è stata selezionata l'opzione **Attributi nella tabella delle dimensioni** .  
  
## <a name="see-also"></a>Vedere anche  
 [Guida sensibile al contesto della configurazione guidata funzionalità di Business Intelligence](business-intelligence-wizard-f1-help.md)   
 [Progettazione cubi &#40;Analysis Services-Dati multidimensionali&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Progettazione dimensioni &#40;Analysis Services-Dati multidimensionali&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
