---
title: Utilizzare il drill-through dai visualizzatori modello | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: e5e065ad-c688-4c2c-8c82-7f3038e04915
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ebb910af4a9c01784fb74195ad6eed0f7f96db71
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66082841"
---
# <a name="use-drillthrough-from-the-model-viewers"></a>Utilizzare il drill-through dai visualizzatori modello
  A seconda del tipo di modello, è possibile utilizzare il drill-through dai visualizzatori nella scheda **Visualizzatore modello di data mining** di Progettazione modelli di data mining per esplorare i case utilizzati nel modello di data mining o per visualizzare colonne aggiuntive nella struttura di data mining. Sebbene molti tipi di modello non supportino il drill-through perché gli schemi del modello non possono essere collegati direttamente a case specifici, i tipi di modello seguenti supportano il drill-through.  
  
 Ricordare che è necessario abilitare il drill-through per il modello e disporre delle autorizzazioni appropriate. L'opzione di drill-through deve invece essere disabilitata se il modello si trova in uno stato non elaborato, indipendentemente dal fatto che il modello sia stato elaborato o meno in precedenza e disponga di contenuto. Per recuperare i dati del case del modello tramite il drill-through, la cache della struttura e del modello deve essere quella corrente.  
  
### <a name="use-drillthrough-in-the-microsoft-tree-viewer"></a>Utilizzare il drill-through nel Visualizzatore Microsoft Decision Trees  
  
1.  In Progettazione modello di data mining selezionare un modello di albero delle decisioni e selezionare **Esplora modello** per aprire il modello nel **Visualizzare Microsoft Decision Trees**. In SQL Server Management Studio fare clic con il pulsante destro del mouse sul modello e selezionare **Sfoglia**  
  
2.  Fare clic con il pulsante destro del mouse su qualsiasi nodo del grafico dell'albero e selezionare **Drill-through**.  
  
3.  Selezionare una delle opzioni seguenti: **Solo colonne modello** o **Colonne struttura e modello**. Se non si dispone delle autorizzazioni necessarie, è possibile che un'opzione non sia disponibile.  
  
4.  Verrà visualizzata la finestra di dialogo **Drill-through** contenente i dati del case e/o i dati della struttura. La barra del titolo della finestra di dialogo contiene inoltre una descrizione del nodo da cui è stata eseguita la query drill-through.  
  
5.  Fare clic con il pulsante destro del mouse in qualsiasi punto nei risultati e selezionare **Copia tutto** per salvare i risultati negli Appunti.  
  
### <a name="use-drillthrough-in-the-microsoft-cluster-viewer"></a>Utilizzare il drill-through nel Visualizzatore Microsoft Clustering  
  
1.  In Progettazione modello di data mining selezionare un modello di clustering e selezionare **Esplora modello** per aprire il modello nel **Visualizzare Microsoft Clustering**. In SQL Server Management Studio fare clic con il pulsante destro del mouse sul modello e selezionare **Sfoglia**.  
  
2.  Nella scheda **Cluster** fare clic con il pulsante destro del mouse su un nodo qualsiasi.  
  
3.  Selezionare **Drill-through**, quindi scegliere una delle opzioni seguenti: **Solo colonne modello** o **Colonne struttura e modello**. Se non si dispone delle autorizzazioni necessarie, è possibile che un'opzione non sia disponibile.  
  
4.  Verrà visualizzata la finestra di dialogo **Drill-through** contenente i dati del case e/o i dati della struttura. La barra del titolo della finestra di dialogo contiene inoltre una descrizione del cluster per i case.  
  
5.  Fare clic con il pulsante destro del mouse in qualsiasi punto nei risultati e selezionare **Copia tutto** per salvare i risultati negli Appunti.  
  
### <a name="use-drillthrough-in-the-microsoft-association-rules-viewer"></a>Utilizzare il drill-through nel Visualizzatore Microsoft Association Rules  
  
1.  In Progettazione modello di data mining selezionare un modello di associazione e selezionare **Esplora modello** per aprire il modello nel **Visualizzare Microsoft Association Rules**. In SQL Server Management Studio fare clic con il pulsante destro del mouse sul modello e selezionare **Sfoglia**  
  
2.  Nella scheda **Regole** fare clic con il pulsante destro del mouse sulla riga di una regola. Nella scheda **Set di elementi** fare clic su una riga che contiene un set di elementi.  
  
3.  Selezionare **Drill-through**, quindi scegliere una delle opzioni seguenti: **Solo colonne modello** o **Colonne struttura e modello**. Se non si dispone delle autorizzazioni necessarie, è possibile che un'opzione non sia disponibile.  
  
4.  Verrà visualizzata la finestra di dialogo **Drill-through** contenente i dati del case e/o i dati della struttura. La barra del titolo della finestra di dialogo contiene inoltre una descrizione del nome della regola.  
  
5.  Fare clic con il pulsante destro del mouse in qualsiasi punto nei risultati e selezionare **Copia tutto** per salvare i risultati dei case completi negli Appunti. È anche possibile selezionare **Copia** per copiare soltanto il case selezionato. Se il modello contiene una colonna di una tabella nidificata, verrà incollato solo il nome della colonna della tabella nidificata. Per recuperare i valori dei dati all'interno della colonna della tabella nidificata per ogni case, è necessario creare una query sul contenuto del modello.  
  
### <a name="use-drillthrough-in-the-microsoft-sequence-cluster-viewer"></a>Utilizzare il drill-through nel Visualizzatore Microsoft Sequence Clustering  
  
1.  In Progettazione modello di data mining selezionare un modello di clustering e selezionare **Esplora modello** per aprire il modello nel **Visualizzare Microsoft Clustering**. In SQL Server Management Studio fare clic con il pulsante destro del mouse sul modello e selezionare **Sfoglia**.  
  
2.  Nella scheda **Diagramma dei cluster**fare clic con il pulsante destro del mouse su qualsiasi nodo che rappresenta un cluster. Nella scheda **Profili cluster** fare clic in qualsiasi punto di un profilo cluster o nel cluster che rappresenta il popolamento totale del modello.  
  
3.  Selezionare **Drill-through**, quindi scegliere una delle opzioni seguenti: **Solo colonne modello** o **Colonne struttura e modello**. Se non si dispone delle autorizzazioni necessarie, è possibile che un'opzione non sia disponibile.  
  
4.  Verrà visualizzata la finestra di dialogo **Drill-through** contenente i dati del case e/o i dati della struttura. La barra del titolo della finestra di dialogo contiene inoltre una descrizione del cluster per i case.  
  
5.  Fare clic con il pulsante destro del mouse in qualsiasi punto nei risultati e selezionare **Copia tutto** per salvare i risultati negli Appunti. Se il modello contiene una colonna di una tabella nidificata, verrà incollato solo il nome della colonna della tabella nidificata. Per recuperare i valori dei dati all'interno della colonna della tabella nidificata per ogni case, è necessario creare una query sul contenuto del modello.  
  
## <a name="see-also"></a>Vedi anche  
 [Attività e procedure relative al Visualizzatore modello di data mining](mining-model-viewer-tasks-and-how-tos.md)   
 [Drill-through sui modelli di data mining](drillthrough-on-mining-models.md)   
 [Drill-through sulle strutture di data mining](drillthrough-on-mining-structures.md)  
  
  
