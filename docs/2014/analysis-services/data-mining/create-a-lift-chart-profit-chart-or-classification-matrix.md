---
title: Creare un grafico di accuratezza, un grafico dei profitti o una matrice di classificazione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Mining Accuracy Chart [Analysis Services], mining structures
ms.assetid: aa3d052f-58a9-4417-8e7a-5e6feb562af0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e183c1e25aa81b05c897674fc5c9f4a2dd8d0c5b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62718138"
---
# <a name="create-a-lift-chart-profit-chart-or-classification-matrix"></a>Creare un grafico di accuratezza, un grafico dei profitti o una matrice di classificazione
  È possibile creare un grafico di accuratezza per un modello di data mining di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in cinque passaggi fondamentali:  
  
-   Selezionare la struttura di data mining che contiene i modelli di data mining da confrontare.  
  
-   Selezionare i modelli di data mining da aggiungere al grafico.  
  
-   Specificare un'origine di dati di testing da utilizzare nella generazione del grafico.  
  
-   Scegliere il tipo di grafico.  
  
-   Configurare le opzioni del grafico.  
  
 Questi passaggi di base sono identici per il grafico di accuratezza, il grafico di profitti e la matrice di classificazione. Nelle procedure seguenti vengono descritti i passaggi per configurare le opzioni di base per questi tipi di grafico. Per altre informazioni su come creare un report di convalida incrociata, vedere [Misure nel report di convalida incrociata](measures-in-the-cross-validation-report.md).  
  
### <a name="open-the-mining-structure-in-the-accuracy-chart-designer"></a>Aprire la struttura di data mining nella Finestra di progettazione Grafico di accuratezza  
  
1.  Aprire Progettazione modelli di data mining in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  In Esplora soluzioni fare doppio clic sulla struttura che contiene il modello o i modelli di data mining.  
  
3.  Fare clic sulla scheda **Grafico accuratezza modello di data mining** .  
  
### <a name="select-mining-models-for-inclusion-in-the-chart"></a>Selezionare i modelli di data mining da includere nel grafico  
  
1.  Nella scheda **Grafico accuratezza modello di data mining** di Progettazione modelli di data mining in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]fare clic sulla scheda **Selezione input** .  
  
     Nell'elenco verranno visualizzati tutti i modelli presenti nella struttura corrente con lo stesso attributo stimabile.  
  
2.  Selezionare la casella **Mostra** per ogni modello da includere nel grafico.  
  
3.  Fare clic sulla casella di testo **Nome colonna stimabile** e selezionare il nome di una colonna stimabile nell'elenco. Tutti i modelli inclusi in un grafico devono avere la stessa colonna stimabile.  
  
4.  Se si confrontano due modelli e le colonne stimabili contengono valori o tipi di dati diversi, deselezionare la casella **Sincronizza colonne e valori di stima** per forzare un confronto.  
  
    > [!NOTE]  
    >  Se la casella **Sincronizza colonne e valori di stima** è selezionata, verranno analizzati i dati nelle colonne stimabili del modello e i dati di test e verrà effettuato il tentativo di trovare la migliore corrispondenza. Pertanto, non deselezionare la casella a meno che non sia assolutamente necessario per forzare un confronto delle colonne.  
  
5.  Fare clic sulla casella di testo **Valore stima** e selezionare un valore nell'elenco. Se la colonna stimabile è un tipo di dati continuo, è necessario digitare un valore nella casella di testo.  
  
     Per altre informazioni, vedere [Scegliere la colonna da usare per il test di un modello di data mining](choose-the-column-to-use-for-testing-a-mining-model.md).  
  
### <a name="select-testing-data"></a>Selezionare i dati di test  
  
1.  Nella scheda **Selezione input** della scheda **Grafico accuratezza modello di data mining** specificare l'origine dei dati che verranno usati per generare il grafico selezionando una delle opzioni del gruppo **Seleziona set di dati da utilizzare per il grafico di accuratezza**.  
  
    -   Selezionare l'opzione **Usa test case del modello di data mining**se si intende usare il subset di case definiti tramite l'intersezione dei test case della struttura di data mining ed eventuali filtri applicati durante la creazione del modello.  
  
    -   Selezionare l'opzione **Usa test case della struttura di data mining**per usare il set completo di test case definiti come parte del set di dati di controllo delle strutture di data mining.  
  
    -   Selezionare l'opzione **Specifica un set di dati diverso**se si vuole usare dati esterni.  Il set di dati deve essere disponibile come vista origine dati.   Fare clic su Sfoglia (**...** ) pulsante per scegliere le tabelle di dati da utilizzare per il grafico di accuratezza. Per altre informazioni, vedere [Scegliere ed eseguire il mapping dei dati di test del modello](choose-and-map-model-testing-data.md).  
  
         Se si utilizza un set di dati esterno, è possibile scegliere di filtrare il set di dati di input. Per altre informazioni, vedere [Applicare filtri ai dati di test del modello](apply-filters-to-model-testing-data.md).  
  
> [!NOTE]  
>  Non è possibile creare un filtro sui test case del modello o sui test case della struttura di data mining nella scheda **Selezione input** . Per creare un filtro sul modello di data mining, modificare la proprietà Filter del modello. Per altre informazioni, vedere [Applicare un filtro a un modello di data mining](apply-a-filter-to-a-mining-model.md).  
  
### <a name="configure-chart-settings-and-generate-the-chart"></a>Configurare le impostazioni e generare il grafico  
  
1.  Nella scheda **Grafico accuratezza modello di data mining** fare clic sulla scheda relativa al grafico da creare.  
  
2.  Per un **grafico di accuratezza**, fare clic sulla scheda **Grafico di accuratezza** . Il grafico viene generato automaticamente in base al modello, agli attributi stimabili e ai dati di input selezionati.  
  
3.  Per una **matrice di classificazione**, fare clic sulla scheda **Matrice di classificazione** . Non sono necessarie ulteriori impostazioni. Il grafico viene generato automaticamente in base al modello e ai dati di input selezionati.  
  
4.  Per un **grafico dei profitti**, fare clic sulla scheda **Grafico di accuratezza** . Selezionare **Grafico profitti** nell'elenco a discesa **Tipo di grafico**.  
  
     Immettere le impostazioni seguenti nella finestra di dialogo **Impostazioni grafico profitti** .  
  
     **Popolazione**  
     Numero di case del set di dati che si desidera utilizzare per la creazione del grafico di accuratezza.  
  
     Il modello sceglie sempre i case in ordine di probabilità decrescente. Ciò significa che, se si desidera valutare i potenziali clienti e si sceglie un numero che rappresenta solo metà dei record nel database dei clienti, il modello misurerà l'accuratezza nel subset di case più adatti al modello.  
  
     Ciò è dovuto al fatto che quando il modello viene utilizzato per generare un mailing o creare una campagna, verrà utilizzata la probabilità di stima associata a ogni case per individuare solo i clienti la cui risposta sarà positiva in base alla probabilità più alta.  
  
     **Costi fissi**  
     Costi fissi associati al problema aziendale.  
  
     Nel caso di una soluzione di mailing diretto, i costi fissi potrebbero essere correlati alla configurazione di una stampante per la copertura dei costi iniziali necessari per la preparazione del mailing promozionale.  
  
     Tali costi si applicano una volta all'intera popolazione di destinazione.  
  
     **Costi singolo contatto**  
     Costi extra in aggiunta ai costi fissi che possono essere associati al contatto di ogni cliente, È possibile, ad esempio, immettere i costi di affrancatura per un mailing promozionale o per l'esecuzione di telefonate.  
  
     Tali costi devono essere identici per l'intera popolazione di destinazione. Ogni valore viene moltiplicato per il numero di case di destinazione.  
  
     **Ricavi per singolo contatto**  
     Importo dei ricavi associati a ogni vendita effettuata.  
  
## <a name="see-also"></a>Vedere anche  
 [Grafico di accuratezza &#40;Analysis Services - Data mining&#41;](lift-chart-analysis-services-data-mining.md)   
 [Matrice di classificazione &#40;Analysis Services - Data mining&#41;](classification-matrix-analysis-services-data-mining.md)  
  
  
