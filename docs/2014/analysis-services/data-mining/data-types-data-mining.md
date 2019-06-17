---
title: I tipi di dati (Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data types [data mining]
- columns [data mining], data types
- data mining [Analysis Services], data types
ms.assetid: 4af5b7db-790b-459c-b2b4-00f0cf6b5ce4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fc810f56d552fa17cb027598a25bde114a696375
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66084796"
---
# <a name="data-types-data-mining"></a>Tipi di dati (data mining)
  Quando si crea un modello di data mining o una struttura di data mining in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], è necessario definire i tipi di dati per ogni colonna della struttura. Il tipo di dati indica al motore di data mining se i dati presenti nell'origine dati sono numerici o di testo e il modo in cui devono essere elaborati. Se nei dati di origine ad esempio sono contenuti dati numerici, è possibile specificare se i numeri devono essere considerati come numeri interi o se devono essere utilizzate posizioni decimali.  
  
 Ogni tipo di dati supporta uno o più tipi di contenuto. Se si imposta il tipo di contenuto, è possibile personalizzare le modalità di elaborazione o di calcolo dei dati presenti nella colonna nel modello di data mining.  
  
 Se ad esempio in una colonna sono presenti dati numerici, è possibile scegliere di gestirli come tipi di dati numerici o di testo. Se si sceglie il tipo di dati numerico, è possibile impostare numerosi tipi di contenuto diversi, ovvero discretizzare i numeri o gestirli come valori continui. Per un elenco di tutti i tipi di contenuto, vedere [Tipi di contenuto &#40;Data mining&#41;](content-types-data-mining.md).  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] supporta i tipi di dati riportati di seguito per le colonne della struttura di data mining:  
  
|Tipo di dati|Tipi di contenuto supportati|  
|---------------|-----------------------------|  
|`Text`|Cyclical, Discrete, Discretized, Key Sequence, Ordered, Sequence|  
|`Long`|Continuous, Cyclical, Discrete, Discretized, Key, Key Sequence, Key Time, Ordered, Sequence, Time<br /><br /> Classified|  
|`Boolean`|Cyclical, Discrete, Ordered|  
|`Double`|Continuous, Cyclical, Discrete, Discretized, Key, Key Sequence, Key Time, Ordered, Sequence, Time<br /><br /> Classified|  
|`Date`|Continuous, Cyclical, Discrete, Discretized, Key, Key Sequence, Key Time, Ordered|  
  
> [!NOTE]  
>  I tipi di contenuto Time e Sequence sono supportati solo da algoritmi di terze parti. I tipi di contenuto Cyclical e Ordered sono supportati, ma la maggior parte degli algoritmi li tratta come valori discreti e non esegue un'elaborazione speciale.  
  
## <a name="specifying-a-data-type"></a>Specifica di un tipo di dati  
 Se si crea il modello di data mining direttamente tramite DMX (Data Mining Extensions), è possibile definire il tipo di dati per ogni colonna in modo analogo a come si definisce il modello e in Analysis Services verrà creata contemporaneamente la struttura di data mining corrispondente ai tipi di dati specificati. Se si crea il modello di data mining o la struttura di data mining tramite una procedura guidata, in Analysis Services viene indicato un tipo di dati oppure è possibile scegliere un tipo di dati da un elenco.  
  
## <a name="changing-a-data-type"></a>Modifica di un tipo di dati  
 Se si modifica il tipo di dati di una colonna, è necessario rielaborare sempre la struttura di data mining e qualsiasi modello di data mining basato su tale struttura. Se si modifica il tipo di dati, in alcuni casi tale colonna non può più essere utilizzata in un modello particolare. In una situazione di questo tipo in Analysis Services verrà generato un errore quando si rielabora il modello oppure verrà rielaborato il modello senza la colonna specifica.  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di contenuto &#40;Data mining&#41;](content-types-data-mining.md)   
 [Tipi di contenuto &#40;DMX&#41;](/sql/dmx/content-types-dmx)   
 [Algoritmi di data mining &#40;Analysis Services - Data mining&#41;](data-mining-algorithms-analysis-services-data-mining.md)   
 [Strutture di data mining &#40;Analysis Services - Data mining&#41;](mining-structures-analysis-services-data-mining.md)   
 [Tipi di dati &#40;DMX&#41;](/sql/dmx/data-types-dmx)   
 [Colonne del modello di data mining](mining-model-columns.md)   
 [Colonne della struttura di data mining](mining-structure-columns.md)  
  
  
