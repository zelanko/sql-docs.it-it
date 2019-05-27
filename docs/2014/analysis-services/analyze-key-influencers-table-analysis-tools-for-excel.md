---
title: Analizza fattori di influenza chiave (strumenti di analisi tabelle per Excel) | Microsoft Docs
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
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66062255"
---
# <a name="analyze-key-influencers-table-analysis-tools-for-excel"></a>Analizza fattori di influenza chiave (Strumenti di analisi tabelle per Excel)
  ![Pulsante analizza fattori di influenza chiave sulla barra multifunzione](media/tat-aki.gif "pulsante analizza fattori di influenza chiave sulla barra multifunzione")  
  
 Con il **analizza fattori di influenza chiave** strumento, si sceglie una colonna che contiene un risultato di destinazione e l'algoritmo determina quali fattori hanno influenzato maggiormente il risultato.  
  
 Lo strumento consente di creare nuove tabelle dati in cui sono segnalati i fattori associati a ogni risultato e di rappresentare graficamente la probabilità della relazione. Le tabelle possono essere filtrate in base a diversi fattori e risultati per esaminare i dati in maggiore dettaglio.  
  
 Consente inoltre di selezionare una coppia di risultati possibili per il confronto. Ad esempio, è possibile confrontare i diversi gruppi di consumer per individuare i fattori potenzialmente rilevanti per le decisioni.  
  
## <a name="using-the-analyze-key-influencers-tool"></a>Utilizzo dello strumento Analizza fattori di influenza chiave  
  
1.  Aprire una tabella di dati di Excel.  
  
2.  Nelle **strumenti tabella**via le **Analizza** sulla barra multifunzione, fare clic su **analizza fattori di influenza chiave.**  
  
3.  Selezionare la singola colonna di destinazione dell'analisi.  
  
4.  Facoltativamente, fare clic su **scegliere le colonne da utilizzare per l'analisi**. Nel **selezione colonne avanzata** finestra di dialogo scegliere le colonne che con maggiore possono contengono dati rilevanti. Per migliorare le prestazioni e l'accuratezza, deselezionare le colonne contenenti ID o nomi, in genere non significative per l'analisi dei modelli. Fare clic su **OK** per chiudere la **selezione colonne avanzata** nella finestra di dialogo.  
  
5.  Fare clic su **Esegui**.  
  
     Il **analizza fattori di influenza chiave** strumento esegue un'analisi dei dati per determinare le impostazioni ottimali e imposta automaticamente tutti i parametri.  
  
6.  Se non sono stati rilevati modelli, tramite la procedura guidata viene creato un nuovo foglio di lavoro contenente una descrizione del problema.  
  
7.  Se vengono rilevati modelli, tramite la procedura guidata viene creato un report in un nuovo foglio di lavoro in cui sono illustrati i modelli. Il report è denominato **fattori di influenza chiave per \<colonna >**. È possibile personalizzare il report come descritto nella procedura seguente.  
  
#### <a name="create-a-custom-report"></a>Creazione di un report personalizzato  
  
1.  Nel **analisi discriminante basata sui fattori di influenza chiave** finestra di dialogo scegliere i due valori che si desidera confrontare selezionandoli le **valore 1** e **valore 2** negli elenchi a discesa . Si potrebbero ad esempio confrontare gli acquirenti con coloro che non effettuano acquisti.  
  
2.  Fare clic su **aggiungere Report**.  
  
     Tramite la procedura guidata verrà creato un nuovo foglio di lavoro e verrà aggiunta una tabella per ogni coppia di fattori chiave confrontati.  
  
3.  Dopo avere effettuato i confronti, fare clic su **Chiudi**.  
  
## <a name="understanding-the-key-influencers-report"></a>Informazioni sul report dei fattori di influenza chiave  
 Dopo aver creato il modello di dati, il **analizza fattori di influenza chiave** lo strumento consente di creare report che consentono di esplorare e confrontare i fattori di influenza chiave.  
  
-   Il report a sinistra è quello generato per impostazione predefinita. Indica le stime più attendibili della colonna dei risultati (la variabile dipendente).  
  
-   Il report a destra è facoltativo ed è possibile crearlo confrontando due valori di risultati specifici. In questo report viene eseguito il confronto degli acquirenti e dei non acquirenti.  
  
-   Si noti che viene aggiunto un nuovo foglio di lavoro per ogni report creato. È possibile spostare le tabelle dopo averle create. Ai fini del confronto sono state posizionate affiancate.  
  
 ![DM13](media/dm13-tat-aki-report.gif "DM13")  
  
 **Impatto relativo**  
 La barra ombreggiata nel primo report indica l'attendibilità dell'associazione di questo attributo al risultato.  
  
 La lunghezza della barra indica la probabilità che il fattore contribuisca al risultato. Per questo motivo, a una maggiore lunghezza della barra ombreggiata corrisponde una maggiore attendibilità dell'associazione.  
  
 **Predilige**  
 Nel secondo report, i valori di destinazione confrontati sono elencati in due colonne insieme ai fattori correlati elencati in ordine di confidenza discendente.  
  
-   Il **blu** barra indica gli attributi che contribuiscono al risultato, "No" (= non è stata acquistata).  
  
-   Il **rosso** barra indica gli attributi che contribuiscono al risultato, "Yes" (= acquistato una bicicletta).  
  
 I colori della barra ombreggiata sono arbitrari e possono essere modificati impostando le opzioni per la progettazione di tabelle in Excel.  
  
 In un report in cui vengono contrapposti due valori, i fattori di influenza chiave vengono classificati nel secondo report in base all'impatto sui valori di destinazione.  
  
 Poiché tutti i grafici sono basati sulle tabelle di Excel, è possibile filtrare e ordinare in modo da concentrare l'attenzione su fattori o risultati specifici.  
  
## <a name="more-about-the-analyze-key-influencers-tool"></a>Ulteriori informazioni sullo strumento Analizza fattori di influenza chiave  
 Quando la **analizza fattori di influenza chiave** strumento analizza i dati, esegue le operazioni seguenti:  
  
-   Creazione di una struttura dei dati per l'archiviazione delle informazioni principali relative alla distribuzione dei dati.  
  
-   Creazione di un modello utilizzando l'algoritmo Microsoft Naïve Bayes.  
  
-   Creazione di stime che mettono in correlazione ogni colonna di dati con il risultato specificato.  
  
-   Utilizzo del punteggio di confidenza per ciascuna delle stime per identificare i fattori più influenti nella produzione del risultato previsto.  
  
-   Creazione di un report che descrive i fattori di influenza chiave, ordinati in base ai punteggi di confidenza.  
  
### <a name="requirements"></a>Requisiti  
 Se la colonna di destinazione contiene valori numerici continui, i valori numerici vengono automaticamente segmentati in gruppi. Tali raggruppamenti rappresentano cluster di case con caratteristiche simili. I valori numerici potrebbero tuttavia non essere divisi in gruppi semplici da usare. Ad esempio, il report potrebbe contenere un raggruppamento, ad esempio "\<12.85701", mentre gli utenti del report è in genere preferibile visualizzare raggruppamenti che utilizzano numeri interi, ad esempio 10-19, 29, 20 e così via.  
  
 Se si desidera raggruppare i dati numerici in un modo diverso, è necessario segmentare i dati nel modo desiderato prima di creare l'analisi. Ad esempio, è possibile usare la [Rietichettare](relabel-sql-server-data-mining-add-ins.md) strumento nel Client di Data Mining per Excel per creare una nuova etichetta di raggruppamento in una colonna separata e quindi utilizzare solo tale nuova colonna nell'analisi.  
  
### <a name="related-tools"></a>Strumenti correlati  
 Il **Data Mining** della barra multifunzione fornisce strumenti più avanzati, inclusa la possibilità di personalizzare modelli di data mining  
  
 Se si salva il modello usando il **analizza fattori di influenza chiave** strumento, è possibile usare il Client di Data Mining per esplorare il modello e analizzare le relazioni più dettagliatamente. Per informazioni, vedere [esplorazione di modelli in Excel &#40;componenti aggiuntivi Data Mining di SQL Server&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md). È inoltre possibile utilizzare Microsoft Office Visio per creare grafici e diagrammi per rappresentare le relazioni come cluster o come reti di dipendenze. Per altre informazioni, vedere [risoluzione dei problemi dei diagrammi di Data Mining di Visio Data &#40;componenti aggiuntivi Data Mining di SQL Server&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md).  
  
> [!NOTE]  
>  I modelli creati con Strumenti di analisi tabelle vengono eliminati quando si chiude il foglio di lavoro o si termina la connessione con il server [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. È pertanto possibile esplorare i modelli solo fino a quando la connessione rimane aperta. Se si chiude la connessione o il foglio di lavoro, non è inoltre possibile eseguire il rendering dei modelli in Visio.  
  
 Per altre informazioni sull'algoritmo utilizzato per il **analizza fattori di influenza chiave** dello strumento, vedere "Microsoft all'algoritmo Naive Bayes" nella documentazione Online di SQL Server.  
  
## <a name="see-also"></a>Vedere anche  
 [Strumenti di analisi tabelle per Excel](table-analysis-tools-for-excel.md)   
 [Creazione di un modello di data mining](creating-a-data-mining-model.md)  
  
  
