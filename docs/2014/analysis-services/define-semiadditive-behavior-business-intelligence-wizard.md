---
title: Definire il comportamento di funzioni semiadditive (configurazione guidata funzionalità di Business Intelligence) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.semiadditivememberdetection.f1
ms.assetid: e57080ba-ce96-40f8-bca7-6701d1725b3c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 161e2cb9dd9eeae4f2ed369b77ab0799ae12a33a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66081997"
---
# <a name="define-semiadditive-behavior-business-intelligence-wizard"></a>Definizione funzioni semiadditive (Configurazione guidata funzionalità di Business Intelligence)
  La pagina **Definizione funzioni semiadditive** consente di attivare o disattivare le funzioni semiadditive sulle misure. Tali funzioni determinano le modalità di aggregazione in base a una dimensione temporale delle misure contenute in un cubo.  
  
> [!NOTE]  
>  Ad eccezione di LastChild disponibile nell'edizione Standard, le funzioni semiadditive sono disponibili solo in Business Intelligence o nelle edizioni Enterprise. Inoltre, poiché le funzioni semiadditive vengono definite solo sulle misure e non sulle dimensioni, questa pagina non verrà visualizzata nella Configurazione guidata funzionalità di Business Intelligence se avviata da Progettazione dimensioni oppure facendo clic con il pulsante destro del mouse su una dimensione in Esplora soluzioni in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
## <a name="options"></a>Opzioni  
 **Disattiva il comportamento di funzioni semiadditive**  
 Consente di disabilitare le funzioni semiadditive in tutte le misure contenute nel cubo.  
  
 **La procedura guidata ha rilevato \<il nome della dimensione> dimensione di tipo conti, che contiene membri funzioni semiadditive. Il server aggrega i membri di questa dimensione in base al comportamento funzioni semiadditive specificato per ogni tipo di conto.**  
 Abilita le funzioni semiadditive per le dimensioni di tipo Conti che contengono membri semiadditivi. Se si seleziona questa opzione, le funzioni di aggregazione vengono impostate per tutti i gruppi di misure che fanno riferimento alla dimensione di tipo Conti in `ByAccount`.  
  
 Per altre informazioni sulle dimensioni di tipo Conti, vedere [Creare un conto finanziario della dimensione di tipo padre-figlio](multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md).  
  
 **Definisci funzioni semiadditive per singole misure**  
 Abilita le funzioni semiadditive e specifica la funzione di aggregazione semiadditiva per misure specifiche. La funzione di aggregazione viene applicata a tutte le dimensioni a cui fa riferimento il gruppo di misure che contiene la misura.  
  
 **Misure**  
 Consente di visualizzare il nome di una misura contenuta nel cubo.  
  
 **Funzioni semiadditive (funzione)**  
 Consente di selezionare la funzione di aggregazione per la misura selezionata. Nella tabella seguente vengono elencate le funzioni di aggregazioni disponibili.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**AverageOfChildren**|Aggregazione eseguita restituendo la media degli elementi figlio della misura.|  
|`ByAccount`|Aggregazione eseguita mediante la funzione di aggregazione associata al tipo di conto specificato di un attributo in una dimensione di tipo Conti.|  
|`Count`|Aggregazione eseguita mediante la funzione `Count`.|  
|`DistinctCount`|Aggregazione eseguita mediante la funzione `DistinctCount`.|  
|**FirstChild**|Aggregazione eseguita restituendo il primo membro figlio della misura in base a una dimensione temporale.|  
|**FirstNonEmpty**|Aggregazione eseguita restituendo il primo membro non vuoto della misura in base a una dimensione temporale.|  
|**LastChild**|Aggregazione eseguita restituendo l'ultimo membro figlio della misura in base a una dimensione temporale.|  
|**LastNonEmpty**|Aggregazione eseguita restituendo l'ultimo membro non vuoto della misura in base a una dimensione temporale.|  
|`Max`|Aggregazione eseguita mediante la funzione `Max`.|  
|`Min`|Aggregazione eseguita mediante la funzione `Min`.|  
|**Nessuno**|Aggregazione non eseguita.|  
|`Sum`|Aggregazione eseguita mediante la funzione `Sum`.|  
  
> [!NOTE]  
>  Le selezioni effettuate per questa opzione vengono applicate solo se **Definisci funzioni semiadditive per singole misure** è selezionato.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida sensibile al contesto della configurazione guidata funzionalità di Business Intelligence](business-intelligence-wizard-f1-help.md)   
 [Progettazione cubi &#40;Analysis Services-Dati multidimensionali&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Progettazione dimensioni &#40;Analysis Services-Dati multidimensionali&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
