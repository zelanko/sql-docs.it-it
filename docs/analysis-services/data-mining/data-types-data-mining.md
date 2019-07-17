---
title: I tipi di dati (Data Mining) | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4b62c9a4ebc9caf9875a1e5b6aef987bf0b4fa8a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68183359"
---
# <a name="data-types-data-mining"></a>Tipi di dati (data mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Quando si crea un modello di data mining o una struttura di data mining in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], è necessario definire i tipi di dati per ogni colonna della struttura. Il tipo di dati indica al motore di analisi se i dati presenti nell'origine dati sono numerici o di testo e il modo in cui devono essere elaborati. Se nei dati di origine ad esempio sono contenuti dati numerici, è possibile specificare se i numeri devono essere considerati come numeri interi o se devono essere utilizzate posizioni decimali.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] supporta i tipi di dati riportati di seguito per le colonne della struttura di data mining:  
  
|Tipo di dati|Tipi di contenuto supportati|  
|---------------|-----------------------------|  
|**per**|Cyclical, Discrete, Discretized, Key Sequence, Ordered, Sequence|  
|**Long**|Continuous, Cyclical, Discrete, Discretized, Key, Key Sequence, Key Time, Ordered, Sequence, Time<br /><br /> Classified|  
|**Boolean**|Cyclical, Discrete, Ordered|  
|**Double**|Continuous, Cyclical, Discrete, Discretized, Key, Key Sequence, Key Time, Ordered, Sequence, Time<br /><br /> Classified|  
|**Data**|Continuous, Cyclical, Discrete, Discretized, Key, Key Sequence, Key Time, Ordered|  
  
> [!NOTE]  
>  I tipi di contenuto Time e Sequence sono supportati solo da algoritmi di terze parti. I tipi di contenuto Cyclical e Ordered sono supportati, ma la maggior parte degli algoritmi li tratta come valori discreti e non esegue un'elaborazione speciale.  
  
 La tabella indica anche i *tipi di contenuto* supportati per ogni tipo di dati.  
  
 Il tipo di contenuto è specifico per il data mining e consente di personalizzare le modalità di elaborazione o di calcolo dei dati nel modello di data mining. Anche se la colonna contiene numeri, ad esempio, potrebbe essere necessario modellarli come valori discreti. Se la colonna contiene numeri, è anche possibile specificare che sono suddivisi in contenitori o discretizzati o che il modello deve gestirli come valori continui. Il tipo di contenuto può quindi avere un notevole effetto sul modello. Per un elenco di tutti i tipi di contenuto, vedere [Tipi di contenuto &#40;Data mining&#41;](../../analysis-services/data-mining/content-types-data-mining.md).  
  
> [!NOTE]  
>  In altri sistemi di apprendimento automatico potrebbero essere usati i termini *dati nominali*, *fattori* o *categorie*, *dati ordinali*o *dati sequenziali*. In generale, questi corrispondono ai tipi di contenuto. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il tipo di dati specifica solo il tipo di valore per l'archiviazione, non il relativo uso nel modello.  
  
## <a name="specifying-a-data-type"></a>Specifica di un tipo di dati  
 Se si crea il modello di data mining direttamente tramite DMX (Data Mining Extensions), è possibile definire il tipo di dati per ogni colonna in modo analogo a come si definisce il modello e in Analysis Services verrà creata contemporaneamente la struttura di data mining corrispondente ai tipi di dati specificati. Se si crea il modello di data mining o la struttura di data mining tramite una procedura guidata, in Analysis Services viene indicato un tipo di dati oppure è possibile scegliere un tipo di dati da un elenco.  
  
## <a name="changing-a-data-type"></a>Modifica di un tipo di dati  
 Se si modifica il tipo di dati di una colonna, è necessario rielaborare sempre la struttura di data mining e qualsiasi modello di data mining basato su tale struttura. Se si modifica il tipo di dati, in alcuni casi tale colonna non può più essere utilizzata in un modello particolare. In una situazione di questo tipo in Analysis Services verrà generato un errore quando si rielabora il modello oppure verrà rielaborato il modello senza la colonna specifica.  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di contenuto &#40;Data mining&#41;](../../analysis-services/data-mining/content-types-data-mining.md)   
 [Tipi di contenuto &#40;DMX&#41;](../../dmx/content-types-dmx.md)   
 [Algoritmi di data mining &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Strutture di data mining &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Tipi di dati &#40;DMX&#41;](../../dmx/data-types-dmx.md)   
 [Colonne del modello di data mining](../../analysis-services/data-mining/mining-model-columns.md)   
 [Colonne della struttura di data mining](../../analysis-services/data-mining/mining-structure-columns.md)  
  
  
