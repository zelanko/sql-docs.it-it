---
title: Scheda selezione (vista grafico di accuratezza Data Mining) di input | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.accuracychart.columnmapping.f1
ms.assetid: f8b1193c-5c86-4c7e-8e35-158d293184fa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3fb4771c7345eb270e91a377d2755a25606f9a93
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66080419"
---
# <a name="input-selection-tab-mining-accuracy-chart-view"></a>Scheda Selezione input (vista Grafico accuratezza modello di data mining)
  Usare la scheda **Selezione input** della finestra di progettazione **Grafico accuratezza modello di data mining** per specificare l'origine dati usata per eseguire il test del modello e compilare il grafico di accuratezza.  
  
 **Per ulteriori informazioni:** [Test e convalida &#40;Data mining&#41;](data-mining/testing-and-validation-data-mining.md)  
  
## <a name="options"></a>Opzioni  
 **Sincronizza colonne**  **e valori di stima**  
 Selezionare questa opzione per coordinare gli attributi stimabili della griglia in modo che, se il nome è diverso, vengono derivati dalla stessa colonna della struttura di data mining stimabile utilizzata durante il training del modello.  
  
 **Nota** Questa opzione è selezionata per impostazione predefinita. Deselezionare questa casella di controllo solo se si è certi che due colonne della struttura di data mining derivano dalla stessa origine relazionale o multidimensionale sottostante e che contengono gli stessi stati o sono state discretizzate nello stesso modo.  
  
 **Selezionare le colonne modello di data mining stimabile da visualizzare nel grafico di accuratezza**  
 Griglia contenente colonne che consentono di controllare i modelli inclusi nel grafico di accuratezza e controllarne la modalità di utilizzo.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**Mostra**|Consente di selezionare la casella accanto al nome di ogni colonna stimabile nel modello di data mining che si desidera visualizzare nel grafico.<br /><br /> Se il grafico è troppo complesso per essere visualizzato in modo semplice, deselezionare la casella accanto a una o più colonne per semplificare il grafico.<br /><br /> Nota: A meno che non sia selezionata almeno una colonna, è possibile creare un grafico di accuratezza.|  
|**Modello di data mining**|Consente di visualizzare l'elenco di modelli di data mining contenuti nella struttura di data mining.|  
|**Nome colonna stimabile**|Consente di selezionare una colonna stimabile contenuta nei modelli di data mining utilizzati per la creazione del grafico di accuratezza.|  
|**Valore stima**|Consente di selezionare un valore per la colonna stimabile. Se non si seleziona alcun valore, il grafico di accuratezza stimerà il livello di accuratezza dell'esecuzione da parte del modello per tutti gli stati della colonna stimabile.|  
  
 **Seleziona set di dati da utilizzare per il grafico di accuratezza**  
 Gruppo di tre opzioni per la specifica dei dati del test di accuratezza.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**Utilizza test case del modello di data mining**|Consente di utilizzare il set di testing creato durante la partizione della struttura di data mining e di applicare il filtro definito sul modello. Per informazioni sui filtri dei modelli, vedere [Filters for Mining Models &#40;Analysis Services - Data Mining&#41;](data-mining/mining-models-analysis-services-data-mining.md)|  
|**Utilizza test case della struttura di data mining**|Consente di utilizzare il set di testing creato durante la partizione della struttura di data mining.|  
|**Specifica un set di dati diverso**|Consente di specificare una tabella di una vista origine dati esistente da utilizzare come un set di dati di test.|  
  
## <a name="filtering-options"></a>Opzioni di filtro  
 Se si seleziona l'opzione **Specifica un set di dati diverso**, è possibile definire una vista origine dati e creare filtri da applicare a questi dati. Quando si crea un filtro, sostanzialmente si crea una clausola WHERE nella query che restituisce i dati di test dalla vista origine dati.  
  
 **Nota** Non è possibile specificare un filtro sul modello di data mining tramite la scheda **Selezione input** . Per creare un filtro del modello, fare clic sulla scheda **Modelli di data mining** e modificare le proprietà del modello.  
  
 Se non è stato creato un set di dati di controllo per il test durante la definizione della struttura di data mining, è possibile selezionare questa opzione e specificare quindi la vista origine dati iniziale come set di test. Grazie a questa soluzione alternativa, è anche possibile impostare filtri sul set di dati originali.  
  
 **Impostazione Mapping colonne**  
 Consente di aprire la finestra di dialogo **Impostazione mapping colonne**, in cui è possibile selezionare l'origine dati, specificare il case e le tabelle annidate nonché eseguire il mapping di colonne di dati esterne alle colonne della struttura di data mining.  
  
 Per altre informazioni, vedere [Finestra di dialogo Impostazione mapping colonne &#40;Grafico accuratezza modello di data mining&#41;](specify-column-mapping-dialog-box-mining-accuracy-chart.md).  
  
 **Espressione filtro**  
 Consente di visualizzare la condizione di filtro compilata tramite gli editor di filtri.  
  
 **Apri Editor filtri**  
 Consente di aprire la finestra di dialogo **Filtro dei set di dati** , in cui è possibile selezionare le tabelle esterne e impostare le condizioni sulle colonne delle tabelle del case e la finestra di dialogo **Filtro** in cui è possibile compilare condizioni che si applicano alle singole colonne della tabella selezionata o alle colonne delle tabelle annidate.  
  
## <a name="see-also"></a>Vedere anche  
 [Test e convalida le attività e procedure relative alla &#40;Data Mining&#41;](data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)   
 [Finestra di progettazione grafico accuratezza di data mining &#40;Data Mining&#41;](mining-accuracy-chart-designer-data-mining.md)   
 [Applicare un filtro a un modello di Data Mining](data-mining/apply-a-filter-to-a-mining-model.md)   
 [Filtri per i modelli di data mining &#40;Analysis Services - Data mining&#41;](data-mining/mining-models-analysis-services-data-mining.md)  
  
  
