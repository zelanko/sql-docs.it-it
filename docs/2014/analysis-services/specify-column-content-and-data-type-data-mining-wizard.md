---
title: Impostazione tipo di dati e contenuto delle colonne (creazione guidata modello di data mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0634be64-4c38-4381-9b19-fe9a5889306c
author: minewiskan
ms.author: owend
ms.openlocfilehash: f23bc2e0f21f15c0af1a26d64e528c65632d75a2
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940422"
---
# <a name="specify-column-content-and-data-type-data-mining-wizard"></a>Impostazione tipo di contenuto e dati delle colonne (Creazione guidata modello di data mining)
  Usare la pagina **Impostazione tipo di contenuto e dati delle colonne** per specificare l'uso e il tipo di dati di ogni colonna selezionata nella pagina precedente della procedura guidata. Per ignorare la colonna, fare clic su **Indietro** per tornare alla pagina **Impostazione dati di training**e deselezionare tutte le caselle di controllo.  
  
 L'utilizzo di una colonna indica l'utilizzo dei dati nel modello. Una colonna può essere utilizzata come una chiave per identificare una serie, come un valore di input da utilizzare nelle analisi o come valore da stimare. Le colonne possono essere utilizzate sia per la stima che per l'input.  
  
 Il tipo di dati specifica dettagli aggiuntivi sul tipo di dati contenuto nella colonna e sull'utilizzo dei dati durante il training. Alcuni tipi di contenuto richiedono un tipo di dati specifico e viceversa. Potrebbe anche essere necessario specificare un particolare tipo di dati a seconda dell'algoritmo utilizzato durante la creazione del modello di data mining. Per informazioni sui tipi di contenuto e i tipi di dati nei modelli e nelle strutture di data mining, vedere [Tipi di contenuto &#40;Data Mining&#41;](data-mining/content-types-data-mining.md).  
  
 **Per altre informazioni:** [Strutture di data mining &#40;Analysis Services - Data mining&#41;](data-mining/mining-structures-analysis-services-data-mining.md), [Colonne del modello di data mining](data-mining/mining-model-columns.md), [Creazione guidata modello di data mining &#40;Analysis Services - Data mining&#41;](data-mining/data-mining-wizard-analysis-services-data-mining.md), [Creare una struttura di data mining relazionale](data-mining/create-a-relational-mining-structure.md)  
  
## <a name="options"></a>Opzioni  
 **Struttura modello di data mining**  
 Consente di visualizzare le colonne dalle viste e dalle tabelle nidificate selezionate nella pagina precedente della procedura guidata.  
  
 **Colonne**  
 Consente di visualizzare l'elenco delle colonne.  
  
 **Tipo di contenuto**  
 Consente di specificare il tipo di contenuto della colonna Se nella pagina precedente della procedura guidata è stato specificato che la colonna è una chiave, sono disponibili i seguenti valori:  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|Chiave|Consente di specificare che la colonna contiene un identificatore univoco per la serie di casi.|  
|Key Sequence|Consente di specificare che la colonna contiene un identificatore di sequenza.|  
|Chiave temporale|Consente di specificare che la colonna contiene una data o un altro numero continuo univoco utilizzato per identificare una data o una serie temporale.|  
  
 Se si seleziona la colonna come colonna non chiave, sono disponibili i seguenti valori a seconda del tipo di dati:  
  
|Opzione|Description|  
|------------|-----------------|  
|Continua|Consente di specificare che la colonna contiene valori numerici continui.|  
|Discretizzato|Consente di specificare che la colonna contiene valori numerici discretizzati o che possono essere trattati come valori discreti.|  
|Discrete|Consente di specificare che la colonna contiene testo o altri valori non numerici.|  
  
 **Tipo di dati**  
 Consente di specificare il tipo di dati della colonna.  
  
 Sono disponibili i valori seguenti.  
  
-   `Boolean`  
  
-   `Date`  
  
-   `Double`  
  
-   `Long`  
  
-   `Text`  
  
 **Detect**  
 Consente di analizzare un esempio di dati in tutte le colonne numeriche. Consente di sostituire i valori **Tipo di contenuto** con un tipo di contenuto consigliato.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida sensibile al contesto della creazione guidata modello di data mining &#40;Analysis Services-&#41;di data mining](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [Suggerisci colonne correlate &#40;creazione guidata modello di data mining&#41;](suggest-related-columns-data-mining-wizard.md)   
 [Impostazione tipi di tabella &#40;creazione guidata modello di data mining&#41;](specify-table-types-data-mining-wizard.md)   
 [Specificare il tipo di dati e il contenuto della colonna &#40;creazione guidata modello di data mining&#41;](specify-the-column-s-content-and-data-type-data-mining-wizard.md)  
  
  
