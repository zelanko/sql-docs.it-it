---
title: Scegliere la colonna da utilizzare per il test di un modello di data mining | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- columns [data mining], predictable mining columns
- Mining Accuracy Chart [Analysis Services], columns
- predictable mining columns [Analysis Services]
ms.assetid: c6a8f23a-da21-4f31-9521-99460d624649
author: minewiskan
ms.author: owend
ms.openlocfilehash: 8f0d8a59ac40364a9e28c1bc52b49d04a785bd3a
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84524877"
---
# <a name="choose-the-column-to-use-for-testing-a-mining-model"></a>Scegliere la colonna da utilizzare per il test di un modello di data mining
  Prima di poter misurare l'accuratezza di un modello di data mining, è necessario decidere quale risultato si desidera valutare. La maggior parte dei modelli di data mining richiede che si scelga almeno una colonna da utilizzare come attributo stimabile quando si crea il modello. Pertanto, quando si testa l'accuratezza del modello, è in genere necessario selezionare quell'attributo da testare.  
  
 Nell'elenco seguente vengono descritte alcune considerazioni aggiuntive relative alla scelta dell'attributo stimabile da utilizzare nel test:  
  
-   Alcuni tipi di modelli di data mining possono prevedere più attributi, ad esempio reti neurali, che consentono di esplorare le relazioni tra molti attributi.  
  
-   Altri tipi di modelli di data mining, ad esempio i modelli di clustering, non dispongono necessariamente di un attributo stimabile. Non è possibile testare i modelli di clustering a meno che non dispongano di un attributo stimabile.  
  
-   Per creare un grafico a dispersione o misurare l'accuratezza di un modello di regressione è necessario scegliere un attributo stimabile continuo come risultato. In questo caso, non è possibile specificare un valore di destinazione. Se si crea qualsiasi grafico diverso da un grafico a dispersione, anche la colonna della struttura di data mining sottostante deve avere un tipo di contenuto **Discreto** o **Discretizzato**.  
  
-   Se si sceglie un attributo discreto come risultato stimabile, è anche possibile specificare un valore di destinazione oppure lasciare vuoto il campo **Valore stima** . Se si include un **valore di stima**, il grafico misurerà solo l'efficacia del modello alla stima del valore di destinazione. Se non si specifica un risultato di destinazione, il modello viene misurato per l'accuratezza alla stima di tutti i risultati.  
  
-   Se si desidera includere più modelli e confrontarli in un singolo grafico di accuratezza, tutti i modelli devono utilizzare la stessa colonna stimabile.  
  
-   Quando si crea un report di convalida incrociata, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] analizza automaticamente tutti i modelli che includono lo stesso attributo stimabile.  
  
-   Quando l'opzione **Sincronizza colonne e valori di stima**è selezionata, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] seleziona automaticamente le colonne stimabili che hanno gli stessi nomi e tipi di dati corrispondenti. Se le colonne non soddisfano questi criteri, è possibile disabilitare questa opzione e scegliere manualmente una colonna stimabile. Potrebbe essere necessario eseguire questa operazione per il test del modello con un set di dati esterni che dispone di colonne diverse rispetto al modello. Se tuttavia si sceglie una colonna con il tipo di dati errato si verificherà un errore o si otterranno risultati non corretti.  
  
### <a name="specify-the-outcome-to-predict"></a>Specificare il risultato da stimare  
  
1.  Fare doppio clic sulla struttura di data mining per aprirla in Progettazione modelli di data mining.  
  
2.  Selezionare la scheda **Grafico di accuratezza modello di data mining** .  
  
3.  Selezionare la scheda **Selezione input** .  
  
4.  In **Nome colonna stimabile** nella scheda **Selezione input**selezionare una colonna stimabile per ogni modello incluso nel grafico.  
  
     Le colonne del modello di data mining disponibili nella casella **Nome colonna stimabile** sono limitate solo a quelle con il tipo di utilizzo impostato su **Stima** o **Solo stima**.  
  
5.  Se si vuole determinare il livello di accuratezza per un modello, è necessario selezionare un risultato specifico da misurare nell'elenco **Valore stima** .  
  
## <a name="see-also"></a>Vedere anche  
 [Scegliere ed eseguire il mapping dei dati di test del modello](choose-and-map-model-testing-data.md)   
 [Scegliere un tipo di grafico di accuratezza e impostare le opzioni del grafico](choose-an-accuracy-chart-type-and-set-chart-options.md)  
  
  
