---
title: Analizzare i fattori di influenza chiave (strumenti di analisi tabelle per Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- key influencers
- factor analysis
ms.assetid: 54d7b4ce-7b79-407a-985c-aa655ad19280
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: df6622abc3a507d917aefd2a8a5a1bf9505a2622
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66062255"
---
# <a name="analyze-key-influencers-table-analysis-tools-for-excel"></a>Analizza fattori di influenza chiave (Strumenti di analisi tabelle per Excel)
  ![Pulsante Analizza fattori di influenza chiave sulla barra multifunzione](media/tat-aki.gif "Pulsante Analizza fattori di influenza chiave sulla barra multifunzione")  
  
 Con lo strumento **Analizza fattori di influenza chiave** , è possibile scegliere una colonna che contiene un risultato di destinazione e l'algoritmo determina quali fattori hanno influenzato maggiormente il risultato.  
  
 Lo strumento consente di creare nuove tabelle dati in cui sono segnalati i fattori associati a ogni risultato e di rappresentare graficamente la probabilità della relazione. Le tabelle possono essere filtrate in base a diversi fattori e risultati per esaminare i dati in maggiore dettaglio.  
  
 Consente inoltre di selezionare una coppia di risultati possibili per il confronto. Ad esempio, è possibile confrontare i diversi gruppi di consumer per individuare i fattori potenzialmente rilevanti per le decisioni.  
  
## <a name="using-the-analyze-key-influencers-tool"></a>Utilizzo dello strumento Analizza fattori di influenza chiave  
  
1.  Aprire una tabella di dati di Excel.  
  
2.  In **Strumenti tabella**, sulla barra multifunzione **analizza** fare clic su **Analizza fattori di influenza chiave.**  
  
3.  Selezionare la singola colonna di destinazione dell'analisi.  
  
4.  Facoltativamente, fare clic su **Scegli le colonne da utilizzare per l'analisi**. Nella finestra di dialogo **Selezione colonne avanzate** scegliere le colonne che con maggiore probabilità contengono dati rilevanti. Per migliorare le prestazioni e l'accuratezza, deselezionare le colonne contenenti ID o nomi, in genere non significative per l'analisi dei modelli. Fare clic su **OK** per chiudere la finestra di dialogo **Selezione colonne avanzate** .  
  
5.  Fare clic su **Esegui**.  
  
     Lo strumento **Analizza fattori di influenza chiave** consente di eseguire un'analisi dei dati per determinare le impostazioni ottimali e di impostare automaticamente tutti i parametri.  
  
6.  Se non sono stati rilevati modelli, tramite la procedura guidata viene creato un nuovo foglio di lavoro contenente una descrizione del problema.  
  
7.  Se vengono rilevati modelli, tramite la procedura guidata viene creato un report in un nuovo foglio di lavoro in cui sono illustrati i modelli. Il report è denominato **fattori di influenza chiave \<per la colonna>**. È possibile personalizzare il report come descritto nella procedura seguente.  
  
#### <a name="create-a-custom-report"></a>Creare un report personalizzato  
  
1.  Nella finestra di dialogo analisi **discriminante basata sui fattori di influenza chiave** scegliere i due valori che si desidera confrontare selezionando gli elenchi a discesa **valore 1** e **valore 2** . Si potrebbero ad esempio confrontare gli acquirenti con coloro che non effettuano acquisti.  
  
2.  Fare clic su **Aggiungi report**.  
  
     Tramite la procedura guidata verrà creato un nuovo foglio di lavoro e verrà aggiunta una tabella per ogni coppia di fattori chiave confrontati.  
  
3.  Al termine dell'esecuzione di confronti, fare clic su **Chiudi**.  
  
## <a name="understanding-the-key-influencers-report"></a>Informazioni sul report dei fattori di influenza chiave  
 Una volta creato il modello di dati, lo strumento **Analizza fattori di influenza chiave** crea report che consentono di esplorare e confrontare i fattori di influenza chiave.  
  
-   Il report a sinistra è quello generato per impostazione predefinita. Indica le stime più attendibili della colonna dei risultati (la variabile dipendente).  
  
-   Il report a destra è facoltativo ed è possibile crearlo confrontando due valori di risultati specifici. In questo report viene eseguito il confronto degli acquirenti e dei non acquirenti.  
  
-   Si noti che viene aggiunto un nuovo foglio di lavoro per ogni report creato. È possibile spostare le tabelle dopo averle create. Ai fini del confronto sono state posizionate affiancate.  
  
 ![DM13](media/dm13-tat-aki-report.gif "DM13")  
  
 **Impatto relativo**  
 La barra ombreggiata nel primo report indica l'attendibilità dell'associazione di questo attributo al risultato.  
  
 La lunghezza della barra indica la probabilità che il fattore contribuisca al risultato. Per questo motivo, a una maggiore lunghezza della barra ombreggiata corrisponde una maggiore attendibilità dell'associazione.  
  
 **Predilige**  
 Nel secondo report, i valori di destinazione confrontati sono elencati in due colonne insieme ai fattori correlati elencati in ordine di confidenza discendente.  
  
-   La barra **blu** indica gli attributi che contribuiscono al risultato, ovvero "No" (= non è stato acquistato).  
  
-   La barra **rossa** Mostra gli attributi che contribuiscono al risultato, ovvero "Sì" (= acquistato una bicicletta).  
  
 I colori della barra ombreggiata sono arbitrari e possono essere modificati impostando le opzioni per la progettazione di tabelle in Excel.  
  
 In un report in cui vengono contrapposti due valori, i fattori di influenza chiave vengono classificati nel secondo report in base all'impatto sui valori di destinazione.  
  
 Poiché tutti i grafici sono basati sulle tabelle di Excel, è possibile filtrare e ordinare in modo da concentrare l'attenzione su fattori o risultati specifici.  
  
## <a name="more-about-the-analyze-key-influencers-tool"></a>Ulteriori informazioni sullo strumento Analizza fattori di influenza chiave  
 Quando lo strumento **Analizza fattori di influenza chiave** analizza i dati, esegue le operazioni seguenti:  
  
-   Creazione di una struttura dei dati per l'archiviazione delle informazioni principali relative alla distribuzione dei dati.  
  
-   Creazione di un modello utilizzando l'algoritmo Microsoft Naïve Bayes.  
  
-   Creazione di stime che mettono in correlazione ogni colonna di dati con il risultato specificato.  
  
-   Utilizzo del punteggio di confidenza per ciascuna delle stime per identificare i fattori più influenti nella produzione del risultato previsto.  
  
-   Creazione di un report che descrive i fattori di influenza chiave, ordinati in base ai punteggi di confidenza.  
  
### <a name="requirements"></a>Requisiti  
 Se la colonna di destinazione contiene valori numerici continui, i valori numerici vengono automaticamente segmentati in gruppi. Tali raggruppamenti rappresentano cluster di case con caratteristiche simili. I valori numerici potrebbero tuttavia non essere divisi in gruppi semplici da usare. Ad esempio, il report potrebbe contenere un raggruppamento, ad esempio "\<12,85701", mentre gli utenti del report in genere vogliono visualizzare i raggruppamenti che utilizzano numeri interi, ad esempio 10-19, 20-29 e così via.  
  
 Se si desidera raggruppare i dati numerici in un modo diverso, è necessario segmentare i dati nel modo desiderato prima di creare l'analisi. È ad esempio possibile utilizzare lo strumento modifica [etichette](relabel-sql-server-data-mining-add-ins.md) nel client di data mining per Excel per creare una nuova etichetta di raggruppamento in una colonna separata e quindi utilizzare solo tale nuova colonna nell'analisi.  
  
### <a name="related-tools"></a>Strumenti correlati  
 La barra multifunzione **data mining** fornisce strumenti più avanzati, inclusa la possibilità di personalizzare modelli di data mining  
  
 Se si salva il modello utilizzando lo strumento **Analizza fattori di influenza chiave** , è possibile utilizzare il client di data mining per esplorare il modello ed esplorare le relazioni in modo più dettagliato. Per informazioni, vedere [esplorazione di modelli in Excel &#40;SQL Server componenti aggiuntivi Data Mining&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md). È inoltre possibile utilizzare Microsoft Office Visio per creare grafici e diagrammi per rappresentare le relazioni come cluster o come reti di dipendenze. Per ulteriori informazioni, vedere [risoluzione dei problemi relativi ai diagrammi di data mining di Visio &#40;SQL Server componenti aggiuntivi Data mining&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md).  
  
> [!NOTE]  
>  I modelli creati con Strumenti di analisi tabelle vengono eliminati quando si chiude il foglio di lavoro o si termina la connessione con il server [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. È pertanto possibile esplorare i modelli solo fino a quando la connessione rimane aperta. Se si chiude la connessione o il foglio di lavoro, non è inoltre possibile eseguire il rendering dei modelli in Visio.  
  
 Per ulteriori informazioni sull'algoritmo utilizzato dallo strumento **Analizza fattori di influenza chiave** , vedere l'argomento relativo all'algoritmo Microsoft Naive Bayes in documentazione online di SQL Server.  
  
## <a name="see-also"></a>Vedere anche  
 [Strumenti di analisi tabelle per Excel](table-analysis-tools-for-excel.md)   
 [Creazione di un modello di data mining](creating-a-data-mining-model.md)  
  
  
