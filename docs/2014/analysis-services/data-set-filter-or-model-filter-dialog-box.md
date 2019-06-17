---
title: Filtro dei Set di dati o finestra di dialogo Filtro modello | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a9602174-b7e2-4e16-8ded-dfd8eb9264d7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 89ba538c3ac3dfd7a262e4ae17cb9ddd6cf7265c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66082606"
---
# <a name="data-set-filter-or-model-filter-dialog-box"></a>Finestra di dialogo Filtro dei set di dati o Filtro modello
  Questa finestra di dialogo consente di compilare i filtri che è possibile applicare a un set di dati.  Il set di dati può essere un set esterno utilizzato per eseguire il test o un set di dati di case per un modello di data mining. Il nome della finestra di dialogo varia a seconda che il filtro venga utilizzato per un set di dati esterno o per un modello di data mining.  
  
 Se si applica il filtro a un nuovo set di dati, il modello di data mining viene valutato solo con i case del set di dati che soddisfano le condizioni. Se si applica il filtro al modello di data mining stesso, il training e il test del modello vengono eseguiti solo con i case del set di dati di test esistente che soddisfano i criteri di filtro.  
  
-   La finestra di dialogo **Filtro dei set di dati** è disponibile dalla scheda **Selezione input** della finestra di progettazione **Grafico accuratezza modello di data mining** .  
  
-   La finestra di dialogo **Filtro modello** è disponibile dalla scheda **Modelli di data mining** della finestra di progettazione Data Mining.  
  
-   Nella griglia **Condizioni** sono contenute le colonne in cui è possibile specificare un nome di colonna o tabella, un operatore e i valori di destinazione. Mediante questa griglia sostanzialmente si crea una clausola WHERE.  
  
> [!TIP]  
>  Per eseguire il test dell'accuratezza su un subset di dati di training originali, è possibile aggiungere la vista origine dati usata per definire il set di training come dati di test esterni e aggiungere quindi condizioni nella griglia **Filtro dei set di dati**.  
  
 **Per ulteriori informazioni:** [Test e convalida &#40;Data mining&#41;](data-mining/testing-and-validation-data-mining.md)  
  
## <a name="options"></a>Opzioni  
 **Condizioni**  
 Consente di visualizzare nomi di tabelle seguiti da nomi di colonne con condizioni.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**And/Or**|Scegliere un operatore per eseguire il join di più condizioni.|  
|**Colonna della struttura di data mining**|Fare clic per selezionare un'origine dati, quindi fare clic sulle righe successive della griglia per aggiungere le colonne dall'origine dati.<br /><br /> La prima riga nella griglia specifica la vista origine dati. Dopo avere selezionato una vista origine dati, vengono visualizzate un'icona di tabella in **Colonna struttura di data mining** e la combinazione di tutti i criteri definiti per quell'origine dati nel campo **Valore** .<br /><br /> Dopo avere selezionato un'origine dati, nella casella **Colonna struttura di data mining** diventa disponibile un elenco a discesa di singole colonne dell'origine dati.|  
|**Operatore**|Selezionare un operatore dall'elenco.|  
|**Valore**|Per le tabelle, nel campo **Valore** viene visualizzata la combinazione di tutti i filtri applicati all'origine dati. È anche possibile scegliere la compilazione **(...)**  nella parte destra della casella di testo per aprire la **filtro** nella finestra di dialogo e compilare una condizione.|  
  
 **Espressione**  
 Consente di visualizzare il set di criteri compilato tramite la griglia.  
  
 **Modifica Query**  
 Consente di cambiare la modalità di modifica del filtro per poter specificare un'espressione di filtro direttamente nella casella di testo **Espressione** .  
  
> [!NOTE]  
>  Dopo avere apportato modifiche manuali all'espressione di filtro, non è possibile tornare alla modalità di modifica della griglia, persino dopo avere salvato l'espressione nella casella **Espressione filtro** della scheda **Selezione input** . Se si desidera compilare un'espressione tramite la griglia, è necessario prima eliminare l'espressione di filtro esistente e ripetere nuovamente l'operazione.  
  
 **Annulla modifiche Query**  
 Consente di ripristinare la griglia allo stato precedente e annullare qualsiasi modifica apportata all'espressione di filtro.  
  
## <a name="see-also"></a>Vedere anche  
 [Test e convalida le attività e procedure relative alla &#40;Data Mining&#41;](data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)   
 [Finestra di progettazione grafico accuratezza di data mining &#40;Data Mining&#41;](mining-accuracy-chart-designer-data-mining.md)  
  
  
