---
title: Programmazione di Data Mining di Analysis Services | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1b4068d012b64cb4fc5352ed11c8576a38d6d6c4
ms.sourcegitcommit: 603d5ef9b45c2f111d36d11864dc032917e4a321
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/08/2019
ms.locfileid: "65450120"
---
# <a name="data-mining-programming"></a>Programmazione di data mining
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

  Se gli strumenti e i visualizzatori predefiniti disponibili in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] non soddisfano i propri requisiti, è possibile estendere le funzionalità di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mediante la codifica di estensioni personalizzate. Questo approccio rende disponibili due opzioni:  
  
-   **XMLA**  
  
     [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] supporta XML for Analysis (XMLA) come protocollo per la comunicazione con applicazioni client. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] supporta comandi aggiuntivi che estendono la specifica XML for Analysis.  
  
     Poiché [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilizza XMLA per la definizione dei dati, la manipolazione dei dati e il supporto del controllo dei dati, è possibile creare strutture di data mining e modelli di data mining tramite gli strumenti visivi forniti da [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], quindi estendere gli oggetti di data mining creati tramite script DMX (Data Mining Extensions) e ASSL (Analysis Services Scripting Language).  
  
     È possibile creare e modificare completamente oggetti di data mining negli script XMLA ed eseguire query di stima sui modelli a livello di codice dalle applicazioni personalizzate.  
  
-   **Analysis Management Objects (AMO)**  
  
     [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] include inoltre un framework completo che consente ai provider di data mining di terze parti di integrare gli oggetti di data mining in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
     È possibile creare le strutture e i modelli di data mining tramite AMO. Vedere gli esempi seguenti in CodePlex:  
  
    -   Visualizzatore AMO  
  
         Si connette all'istanza di SSAS specificata e restituisce un elenco di tutti gli oggetti server e delle relative proprietà, inclusa la struttura di data mining e i modelli di data mining.  
  
    -   AMO Simple Sample  
  
         AS Simple Sample illustra l'accesso a livello di codice alla maggior parte degli oggetti principali e dimostra la visualizzazione dei metadati e l'accesso ai valori negli oggetti.  
  
         L'esempio illustra inoltre come creare ed elaborare una struttura e un modello di data mining, nonché sfogliare un modello di data mining esistente.  
  
-   **DMX**  
  
     È possibile utilizzare DMX per incapsulare istruzioni di comando, query di stima e query sui metadati e per restituire i risultati in un formato tabulare, presupponendo che sia stata creata una connessione a un server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
## <a name="in-this-section"></a>In questa sezione  
 [OLE DB per Data Mining](data-mining-programming-ole-db.md)  
 Vengono descritte le aggiunte alla specifica per il supporto di data mining e dati multidimensionali, ovvero nuovi set di righe e colonne dello schema e linguaggio DMX (Data Mining Extensions) per la creazione e la gestione di strutture di data mining.  
  
## <a name="related-reference"></a>Riferimenti correlati  
 [Sviluppo con ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/developing-with-adomd-net)  
 Viene fornita un'introduzione agli oggetti di programmazione client e server ADOMD.NET.  
  
 [Sviluppo con Analysis Management Objects &#40;AMO&#41;](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo)  
 Viene fornita un'introduzione alla libreria di programmazione AMO.  
  
 [Sviluppo con Analysis Services Scripting Language &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)  
 Viene fornita un'introduzione a XML for Analysis (XMLA) e alle relative estensioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Documentazione per gli sviluppatori di Analysis Services](../analysis-services-developer-documentation.md)   
 [Guida di riferimento a DMX &#40;Data Mining Extensions&#41;](../../dmx/data-mining-extensions-dmx-reference.md)  
  
  
