---
title: Esplorare dati e metadati in un cubo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 5faf2a9d-df39-465f-9c81-a00d5cd63f5a
author: minewiskan
ms.author: owend
ms.openlocfilehash: 371b515bbd548b544fba0125cf3d6b58b0098470
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544553"
---
# <a name="browse-data-and-metadata-in-cube"></a>Esplorare dati e metadati in un cubo
  Usare la scheda **Esplorazione** di Progettazione cubi per visualizzare i dati di un cubo. Questa vista può essere utilizzata per esaminare la struttura di un cubo e per controllare dati, calcoli, formattazione e sicurezza di oggetti di database. È possibile esaminare rapidamente un cubo quando gli utenti finali lo visualizzano negli strumenti di report o in altre applicazioni client. Quando si visualizzano dati del cubo, è possibile visualizzare dimensioni diverse, eseguire il drill-down dei membri, nonché eseguire sezionamenti tramite dimensioni.  
  
 Prima di visualizzare un cubo, è necessario elaborarlo e riconnetterlo. Al termine dell'elaborazione, aprire la scheda **Esplorazione** di Progettazione cubi. Sulla barra degli strumenti fare clic sul pulsante Riconnetti per aggiornare la connessione.  
  
 La scheda **esplorazione** dispone di tre riquadri: il riquadro dei metadati, il riquadro del filtro e il riquadro dati. Utilizzare il riquadro Metadati per esaminare la struttura del cubo nel formato albero. Usare il riquadro Filtro nella parte superiore della scheda **Esplorazione** per definire un qualsiasi sottocubo si voglia visualizzare. Utilizzare il riquadro Dati per visualizzare i set di risultati ed eseguire il drill-down tramite le gerarchie di dimensione.  
  
## <a name="setting-up-the-browser"></a>Configurazione di Esplorazione  
 Per preparare la visualizzazione di un cubo, è possibile specificare una prospettiva o una traduzione che si desidera utilizzare. Aggiungere misure e dimensioni al riquadro Dati e specificare tutti i filtri nel riquadro Filtro.  
  
##### <a name="specifying-a-perspective"></a>Specifica di una prospettiva  
 Usare l'elenco **Prospettiva** per scegliere una prospettiva da definire per il cubo. Le prospettive vengono definite nella scheda **Prospettive** di Progettazione cubi. Per passare a una prospettiva diversa, selezionare una qualsiasi prospettiva nell'elenco.  
  
##### <a name="specifying-a-translation"></a>Specifica di una traduzione  
 Usare l'elenco **Lingua** per scegliere una traduzione da definire per il cubo. Le traduzioni vengono definite nella relativa scheda di Progettazione cubi. **** La scheda **Esplorazione** visualizza inizialmente le didascalie per la lingua predefinita, specificata dalla proprietà **Lingua** del cubo. Per passare a una lingua diversa, selezionare una qualsiasi lingua nell'elenco.  
  
##### <a name="formatting-the-data-pane"></a>Formattazione del riquadro Dati  
 È possibile formattare didascalie e celle nel riquadro Dati. Fare clic con il pulsante destro del mouse sulle celle o didascalie selezionate che si vuole formattare e quindi fare clic su **Comandi e opzioni**. A seconda della selezione, nella finestra di dialogo **Comandi e opzioni** vengono visualizzate le impostazioni per **Formato**, **Filtra e raggruppa**, **Report**e **Comportamento**.  
  
## <a name="setting-up-the-data"></a>Configurazione dei dati  
  
##### <a name="adding-or-removing-measures"></a>Aggiunta o rimozione di misure  
 Trascinare le misure che si desidera visualizzare dal riquadro Metadati all'area dei dettagli del riquadro Dati, ossia il grande riquadro vuoto nella parte inferiore destra dell'area di lavoro. Quando si trascinano misure aggiuntive, queste vengono aggiunte come colonne. Una riga verticale indica la posizione in cui verrà rilasciata ciascuna misura aggiuntiva. Se si trascina la cartella **Misure** vengono rilasciate tutte le misure nell'area dei dettagli.  
  
 Per rimuovere una misura dall'area dei dettagli, trascinarla fuori del riquadro Dati o fare clic con il pulsante destro del mouse su di essa e quindi scegliere **Elimina** dal menu di scelta rapida.  
  
##### <a name="adding-or-removing-dimensions"></a>Aggiunta o rimozione di dimensioni  
 Trascinare le gerarchie o le dimensioni nelle aree di riga o di filtro.  
  
 Per usare più dimensioni, utilizzare la funzionalità Analizza in Excel. Analizza in Excel è un collegamento che avvia Excel se è installato nello stesso computer di [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Verrà aperta una cartella di lavoro in Excel contenente una connessione al database corrente e a un elenco campi tabella pivot precaricato con misure e dimensioni. Per altre informazioni, vedere [Analizza in Excel &#40;scheda Esplorazione, Progettazione cubi&#41; &#40;Analysis Services - Dati multidimensionali&#41;](../analyze-in-excel-browser-cube-designer-analysis-services-multidimensional-data.md).  
  
 Per rimuovere una dimensione, trascinarla fuori del riquadro Dati o fare clic con il pulsante destro del mouse su di essa e quindi scegliere **Elimina** dal menu di scelta rapida.  
  
##### <a name="adding-or-removing-filters"></a>Aggiunta o rimozione di filtri  
 È possibile utilizzare uno dei due metodi per aggiungere un filtro:  
  
-   Espandere una dimensione nel riquadro Metadati, quindi trascinare una gerarchia nel riquadro Filtro.  
  
     \- - oppure -  
  
-   Nella colonna **dimensione** del riquadro **filtro** fare clic **\<Select dimension>** e selezionare una dimensione nell'elenco, quindi fare clic **\<Select hierarchy>** nella colonna **gerarchia** e selezionare una gerarchia nell'elenco.  
  
 Dopo aver specificato la gerarchia, indicare l'operatore e l'espressione di filtro. Nella tabella seguente vengono descritti gli operatori e le espressioni di filtro.  
  
|Operatore|Espressione filtro|Descrizione|  
|--------------|-----------------------|-----------------|  
|Uguale|Uno o più membri|I valori devono essere uguali a un membro specificato.<br /><br /> Fornisce la selezione di più membri per le gerarchie di attributi, a eccezione delle gerarchie padre-figlio, e la selezione di un solo membro per le altre gerarchie.|  
|Diverso da|Uno o più membri|I valori devono essere diversi da un membro specificato.<br /><br /> Fornisce la selezione di più membri per le gerarchie di attributi, a eccezione delle gerarchie padre-figlio, e la selezione di un solo membro per le altre gerarchie.|  
|In|Uno o più set denominati|I valori devono trovarsi in un set denominato specificato.<br /><br /> Supportato solo per le gerarchie di attributi.|  
|Non incluso|Uno o più set denominati|I valori non devono trovarsi in un set denominato specificato.<br /><br /> Supportato solo per le gerarchie di attributi.|  
|Intervallo (inclusivo)|Uno o due membri di delimitazione di un intervallo|I valori devono essere compresi tra o uguali ai membri di delimitazione. Se i membri di delimitazione sono uguali o solo un membro viene specificato, non viene applicato alcun intervallo e tutti i valori sono consentiti.<br /><br /> Supportato solo per le gerarchie di attributi. L'intervallo deve trovarsi in un livello di una gerarchia. Gli intervalli non associati non sono attualmente supportati.|  
|Intervallo (esclusivo)|Uno o due membri di delimitazione di un intervallo|I valori devono essere compresi tra i membri di delimitazione. Se i membri di delimitazione sono uguali o solo un membro viene specificato, i valori devono essere maggiori o minori del membro di delimitazione.<br /><br /> Supportato solo per le gerarchie di attributi. L'intervallo deve trovarsi in un livello di una gerarchia. Gli intervalli non associati non sono attualmente supportati.|  
|MDX|Espressione MDX tramite cui viene restituito un set di membri|I valori devono trovarsi nel set di membri calcolato. Se si seleziona questa opzione viene visualizzata la finestra di dialogo **Generatore membri calcolati** per la creazione di espressioni MDX.|  
  
 Per gerarchie definite dall'utente in cui è possibile specificare più membri nell'espressione di filtro, tutti i membri specificati devono essere allo stesso livello e condividere lo stesso padre. Questa restrizione non viene applicata alle gerarchie padre-figlio.  
  
## <a name="working-with-data"></a>Utilizzo dei dati  
  
##### <a name="drilling-down-into-a-member"></a>Drill-down di un membro  
 Per eseguire il drill-down di un particolare membro, fare clic sul segno più (+) accanto al membro o fare doppio clic sul membro.  
  
##### <a name="slicing-through-cube-dimensions"></a>Sezionamento tramite dimensioni del cubo  
 Per filtrare i dati del cubo, fare clic sull'elenco a discesa sull'intestazione di colonna di livello superiore. È possibile espandere la gerarchia e selezionare o deselezionare un membro in un qualsiasi livello per mostrare o nascondere quest'ultimo e tutti i relativi discendenti. Deselezionare la casella di controllo accanto a **(Tutti)** per deselezionare tutti i membri nella gerarchia.  
  
 Dopo aver impostato questo filtro sulle dimensioni, è possibile attivare o disattivare quest'ultimo facendo clic con il pulsante destro del mouse in un punto qualsiasi del riquadro Dati e selezionando **Filtro automatico**.  
  
##### <a name="filtering-data"></a>Filtraggio dei dati  
 È possibile utilizzare l'area del filtro per definire un sottocubo in cui eseguire la ricerca. È possibile aggiungere un filtro facendo clic su una dimensione nel riquadro Filtro o espandendo una dimensione nel riquadro Metadati, quindi trascinando una gerarchia nella pagina Filtro. Successivamente specificare un **Operatore** e un' **Espressione filtro**.  
  
##### <a name="performing-actions"></a>Esecuzione di azioni  
 Mediante un triangolo viene contrassegnata una qualsiasi intestazione o cella nel riquadro Dati per la quale è disponibile un'azione. Potrebbe applicarsi a una dimensione, a un livello, a un membro o a una cella del cubo. Spostare il puntatore sull'oggetto dell'intestazione per visualizzare un elenco di azioni disponibili. Fare clic sul triangolo nella cella per visualizzare un menu e avviare il processo associato.  
  
 Per motivi di sicurezza, la scheda **Esplorazione** supporta solo le azioni seguenti:  
  
-   URL  
  
-   Set di righe  
  
-   Drill-through  
  
 Riga di comando, istruzioni e azioni proprietarie non sono supportate. Le azioni URL sono solo sicure quanto la pagina Web a cui si collegano.  
  
##### <a name="viewing-member-properties-and-cube-cell-information"></a>Visualizzazione di proprietà dei membri e informazioni sulle celle di cubi  
 Per visualizzare informazioni su un oggetto dimensione o sul valore di una cella, spostare il puntatore sulla cella.  
  
##### <a name="showing-or-hiding-empty-cells"></a>Mostrare o nascondere celle vuote  
 È possibile nascondere celle vuote nella griglia dati facendo clic su un punto qualsiasi nel riquadro Dati e selezionando **Mostra celle vuote**.  
  
  
