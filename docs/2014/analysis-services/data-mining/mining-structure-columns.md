---
title: Colonne della struttura di data mining | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], structure
- mining structures [Analysis Services], columns
- data sources [Analysis Services], mining structure columns
- columns [data mining], mining structure columns
ms.assetid: 20cbf433-70d1-4b61-a462-41a8435b27b4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1c843a74b831315c98deda9a9d6fb0c3a463bc5c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66083409"
---
# <a name="mining-structure-columns"></a>Colonne della struttura di data mining
  In una struttura di data mining si definiscono le colonne al momento della creazione della struttura, scegliendo colonne di dati esterni e specificando quindi la modalità di utilizzo dei dati per la modellazione. Pertanto, le colonne della struttura di data mining non sono semplici copie dei dati di un'origine dati, ma definiscono la modalità in cui i dati dell'origine devono essere utilizzati dal modello di data mining. È possibile assegnare proprietà che determinano come vengono discretizzati i dati, proprietà che descrivono come sono distribuiti i valori dei dati  
  
 Le colonne della struttura di data mining sono state progettate in modo da risultare flessibili ed estensibili, in quanto ogni algoritmo utilizzato per compilare un modello di data mining può utilizzare colonne diverse della struttura allo scopo di interpretare i dati. Anziché disporre di un set di dati per ogni modello, è possibile utilizzare una sola struttura di data mining e le colonne che contiene per personalizzare i dati per ciascun modello.  
  
## <a name="defining-mining-structure-columns"></a>Definizione di colonne della struttura di data mining  
 I tipi di dati di base e di contenuto che definiscono le colonne della struttura derivano dall'origine dati utilizzata per creare la struttura. È possibile modificare queste impostazioni all'interno della struttura di data mining, nonché impostare i flag di modellazione e la distribuzione per le colonne continue.  
  
 La definizione di una colonna della struttura di data mining deve contenere le informazioni seguenti:  
  
-   **ID**: nome univoco della colonna, spesso identico al nome. Non è possibile modificare questo elemento dopo avere creato la struttura di data mining, mentre è possibile modificare il nome.  
  
-   **Nome**: nome o alias per la colonna.  
  
-   **Content**: enumerazione che descrive se i dati sono discreti o continui.  
  
-   **Tipo**: enumerazione che indica il tipo di dati generale.  
  
-   **Distribution**: enumerazione che descrive la distribuzione prevista dei valori. Una distribuzione viene inclusa se la colonna è continua.  
  
-   **Flag di modellazione**: enumerazione che indica come gestire i valori mancanti e così via. È anche possibile definire flag di modellazione nel modello di data mining, ma i flag del modello sono diversi da quelli utilizzati nelle colonne della struttura.  
  
-   **Bindings**: proprietà che specificano i dati di origine.  
  
 Gli algoritmi di terze parti possono includere inoltre proprietà personalizzate che è possibile definire nella colonna della struttura di data mining.  
  
 Per altre informazioni sulla struttura e il modello di data mining, vedere [Strutture di data mining &#40;Analysis Services - Data mining&#41;](mining-structures-analysis-services-data-mining.md).  
  
## <a name="related-content"></a>Contenuto correlato  
 Per ulteriori informazioni su come definire e utilizzare le colonne della struttura di data mining, vedere gli argomenti seguenti:  
  
|Argomento|Collegamenti|  
|-----------|-----------|  
|Vengono descritti i tipi di dati che è possibile utilizzare per definire una colonna della struttura di data mining.|[Tipi di dati &#40;&#41;di data mining](data-types-data-mining.md)|  
|Vengono descritti i tipi di contenuto disponibili per ogni tipo di dati contenuto in una colonna della struttura di data mining. I tipi di contenuto sono dipendenti dal tipo di dati. Il tipo di contenuto è assegnato a livello del modello e determina la modalità di utilizzo dei dati della colonna nel modello.|[Tipi di contenuto &#40;&#41;di data mining](content-types-data-mining.md)|  
|Viene introdotto il concetto di tabelle nidificate e viene illustrato in che modo è possibile aggiungere le tabelle nidificate all'origine dati come colonne della struttura di data mining.|[Colonne classificate &#40;&#41;di data mining](classified-columns-data-mining.md)|  
|Vengono elencate e illustrate le proprietà di distribuzione che è possibile impostare in una colonna della struttura di data mining per specificare la distribuzione prevista di valori nella colonna.|[Distribuzioni di colonne &#40;&#41;di data mining](column-distributions-data-mining.md)|  
|Viene illustrato il concetto di discretizzazione (talvolta definito *suddivisione in contenitori*) e vengono descritti i metodi forniti in Analysis Services per discretizzare dati numerici continui.|[Metodi di discretizzazione &#40;&#41;di data mining](discretization-methods-data-mining.md)|  
|Vengono descritti i flag di modellazione che è possibile impostare in una colonna della struttura di data mining.|[Flag di modellazione &#40;data mining&#41;](modeling-flags-data-mining.md)|  
|Vengono descritte le colonne classificate, un tipo speciale di colonna, che è possibile utilizzare per correlare una colonna della struttura di data mining a un'altra.|[Colonne classificate &#40;&#41;di data mining](classified-columns-data-mining.md)|  
|Vengono fornite informazioni sull'aggiunta e la modifica delle colonne della struttura di data mining.|[Attività e procedure relative alla struttura di data mining](mining-structure-tasks-and-how-tos.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Strutture di data mining &#40;Analysis Services-&#41;di data mining](mining-structures-analysis-services-data-mining.md)   
 [Colonne del modello di data mining](mining-model-columns.md)  
  
  
