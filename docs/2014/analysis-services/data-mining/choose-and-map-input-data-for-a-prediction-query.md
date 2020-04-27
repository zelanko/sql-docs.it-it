---
title: Scegliere ed eseguire il mapping dei dati di input per una query di stima | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- tables [Analysis Services], prediction queries
- Mining Model Prediction [Analysis Services], input tables
ms.assetid: 00d330a0-879d-4da0-9f29-53c288116f4d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 89eaf3b59f6d779a01168b00d51acbee1e96ca7e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66085852"
---
# <a name="choose-and-map-input-data-for-a-prediction-query"></a>Scegliere ed eseguire il mapping di dati di input per una query di stima
  Quando si creano stime da un modello di data mining, generalmente si procede inserendo nuovi dati nel modello. (L'eccezione è rappresentata dai modelli Time Series che eseguono stime unicamente in base ai dati cronologici.) Per fornire al modello nuovi dati, è necessario assicurarsi che i dati siano disponibili in una vista origine dati. Se si sa in anticipo quali dati si utilizzeranno per la stima, è possibile includerli nella vista origine dati utilizzata per la creazione del modello. In caso contrario, potrebbe essere necessario creare una nuova vista origine dati. Per altre informazioni, vedere [Viste origine dati in modelli multidimensionali](../multidimensional-models/data-source-views-in-multidimensional-models.md).  
  
 È talvolta possibile che i dati necessari siano contenuti in più di una tabella in un join uno-a-molti. È il caso dei dati utilizzati per i modelli di associazione o Sequence Clustering che utilizzano una tabella del case collegata a una tabella nidificata che contiene i dettagli sul prodotto o la transazione. Se il modello utilizza una struttura di tabelle del case nidificate, i dati utilizzati per la stima devono anch'essi presentare una struttura di tabelle del case nidificate.  
  
> [!WARNING]  
>  Non è possibile aggiungere nuove colonne né eseguire il mapping di colonne che si trovano in una vista origine dati diversa. La vista origine dati selezionata deve contenere tutte le colonne necessarie per la query di stima.  
  
 Dopo avere identificato le tabelle che contengono i dati che si utilizzeranno per le stime, è necessario eseguire il mapping delle colonne nei dati esterni alle colonne nel modello di data mining. Ad esempio, se il modello elabora una stima del comportamento di acquisto del cliente in base ai dati demografici e alle risposte ai sondaggi, i dati di input devono contiene informazioni che generalmente corrispondono al contenuto del modello. Non è necessario disporre di dati corrispondenti per ogni singola colonna, ovviamente maggiore sarà il numero di colonne corrispondenti, migliore sarà il risultato. Se si tenta di eseguire il mapping di colonne con tipi di dati diversi, è possibile che si verifichi un errore. In quel caso, è possibile definire un calcolo denominato nella vista origine dati per eseguire il cast o la conversione dei nuovi dati della colonna al tipo di dati richiesto dal modello. Per ulteriori informazioni, vedere [definire calcoli denominati in una vista origine dati &#40;Analysis Services&#41;](../multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md).  
  
 Quando si scelgono i dati da utilizzare per la stima, è possibile che venga eseguito il mapping automatico delle colonne dell'origine dati selezionata alle colonne del modello di data mining, in base alla somiglianza del nome e al tipo di dati corrispondente. È possibile utilizzare la finestra di dialogo **Modifica mapping** in **Stima modello di data mining** per cambiare le colonne di cui è stato eseguito il mapping, eliminare i mapping non appropriati o creare nuovi mapping per le colonne esistenti. L'area di progettazione **Stima modello di data mining** supporta anche il trascinamento delle connessioni selezionate.  
  
-   Per creare una nuova connessione, selezionare una colonna nella tabella **Modello di data mining** e trascinarla nella colonna corrispondente della tabella **Seleziona tabelle di input** .  
  
-   Per rimuovere una connessione, selezionare la linea di connessione e premere CANC.  
  
 Nella procedura seguente viene illustrata la modifica dei join creati tra la tabella del case e una tabella nidificata utilizzate come input di una query di stima utilizzando la finestra di dialogo **Specifica join nidificato** .  
  
### <a name="select-an-input-table"></a>Selezionare una tabella di input  
  
1.  Nella tabella **Seleziona tabelle di input** della scheda **Grafico accuratezza modello di data mining** di Progettazione modelli di data mining in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]fare clic su **Seleziona tabella del case**.  
  
     Verrà visualizzata la finestra di dialogo **Seleziona tabella** , in cui è possibile selezionare la tabella contenente i dati su cui basare le query.  
  
2.  Nella finestra di dialogo **Seleziona tabella** selezionare un'origine dati nell'elenco **Origine dati** .  
  
3.  In **Nome tabella/vista**selezionare la tabella contenente i dati che si vogliono usare per testare i modelli.  
  
4.  Fare clic su **OK**.  
  
     Verrà automaticamente eseguito il mapping tra le colonne della struttura di data mining e le colonne con lo stesso nome contenute nella tabella di input.  
  
### <a name="change-the-way-that-input-data-is-mapped-to-the-model"></a>Modificare la modalità di mapping dei dati di input al modello  
  
1.  In Progettazione modelli di data mining in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]selezionare la scheda **Stima modello di data mining** .  
  
2.  Scegliere **Modifica connessioni** dal menu **Modello di data mining**.  
  
     Verrà visualizzata la finestra di dialogo **Modifica mapping** . In questa finestra di dialogo la colonna **Colonna modello di data mining** riporta le colonne della struttura di data mining selezionata. La colonna **Colonna tabella** riporta le colonne nell'origine dati esterna scelta nella finestra di dialogo **Seleziona tabelle di input** . Sulle colonne dell'origine dati esterna viene eseguito il mapping a quelle del modello di data mining.  
  
3.  In **Colonna tabella**selezionare la riga che corrisponde alla colonna del modello di data mining a cui si desidera effettuare il mapping.  
  
4.  Selezionare una nuova colonna dall'elenco di colonne disponibili nell'origine dati esterna. Selezionare la voce vuota dell'elenco per eliminare il mapping delle colonne.  
  
5.  Fare clic su **OK**.  
  
     I nuovi mapping delle colonne verranno visualizzati nella finestra di progettazione.  
  
### <a name="remove-a-relationship-between-input-tables"></a>Rimuovere una relazione tra tabelle di input  
  
1.  Nella tabella **Seleziona tabelle di input** della scheda **Stima modello di data mining** in Progettazione modelli di data mining di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]fare clic su **Modifica join**.  
  
     Verrà visualizzata la finestra di dialogo **Specifica join nidificato** .  
  
2.  Selezionare una relazione.  
  
3.  Fare clic su **Rimuovi relazione**.  
  
4.  Fare clic su **OK**.  
  
     Verrà rimossa la relazione tra la tabella del case e la tabella nidificata.  
  
### <a name="create-a-new-relationship-between-input-tables"></a>Creare una nuova relazione tra tabelle di input  
  
1.  Nella tabella **Seleziona tabelle di input** della scheda **Stima modello di data mining** in Progettazione modelli di data mining fare clic su **Modifica join**.  
  
     Verrà visualizzata la finestra di dialogo **Specifica join nidificato** .  
  
2.  Fare clic su **Aggiungi relazione**.  
  
     Verrà visualizzata la finestra di dialogo **Crea relazione** .  
  
3.  Selezionare la colonna chiave della tabella nidificata in **Colonne di origine**.  
  
4.  Selezionare la colonna chiave della tabella del case in **Colonne di destinazione**.  
  
5.  Fare clic su **OK** nella finestra di dialogo **Crea relazione** .  
  
6.  Fare clic su **OK** nella finestra di dialogo **Specifica join nidificato** .  
  
     È stata creata una nuova relazione tra la tabella del case e la tabella nidificata.  
  
### <a name="add-a-nested-table-to-the-input-tables-of-a-prediction-query"></a>Aggiungere una tabella nidificata alle tabelle di input di una query di stima  
  
1.  Nella scheda **Stima modello di data mining** in Progettazione modelli di data mining fare clic su **Seleziona tabella del case** per aprire la finestra di dialogo **Seleziona tabella** .  
  
    > [!NOTE]  
    >  Non è possibile aggiungere una tabella nidificata agli input a meno che non sia stata specificata una tabella del case. Per utilizzare una tabella è necessario che il modello di data mining utilizzato per la stima utilizzi anch'esso una tabella nidificata.  
  
2.  Nella finestra di dialogo **Seleziona tabella** selezionare un'origine dati dall'elenco **Origine dati** , quindi selezionare la tabella nella vista origine dati in cui sono contenuti i dati del case. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  Fare clic su **Seleziona tabella nidificata** per aprire la finestra di dialogo **Seleziona tabella** .  
  
4.  Nella finestra di dialogo **Seleziona tabella** selezionare un'origine dati dall'elenco **Origine dati** , quindi selezionare la tabella nella vista origine dati in cui sono contenuti i dati nidificati. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Se esiste già una relazione, viene eseguito il mapping automatico tra le colonne del modello di data mining e le colonne con lo stesso nome della tabella di input. È possibile modificare la relazione tra la tabella nidificata e la tabella del case facendo clic su **Modifica join**, che consente di aprire la finestra di dialogo **Crea relazione** .  
  
## <a name="see-also"></a>Vedi anche  
 [Query di stima &#40;Data Mining&#41;](prediction-queries-data-mining.md)  
  
  
