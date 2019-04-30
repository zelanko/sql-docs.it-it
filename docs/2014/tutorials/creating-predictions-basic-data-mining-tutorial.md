---
title: Creazione di stime (esercitazione di base di Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a8410ed2-bb98-4d51-a9eb-b239be1201c2
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b32ffb832baf12a72df6e32b07386f24448b3c35
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63285686"
---
# <a name="creating-predictions-basic-data-mining-tutorial"></a>Creazione di stime (Esercitazione di base sul data mining)
  Dopo aver testato l'accuratezza dei modelli di data mining e ha deciso che si è soddisfatti dei risultati, è quindi possibile generare stime tramite il generatore di Query di stima nel **stima modello di Data Mining** scheda modelli di Data Mining Finestra di progettazione.  
  
 Nel generatore delle query di stima sono disponibili tre viste. Con il **Design** e **Query** visualizzazioni, è possibile compilare ed esaminare la query. È quindi possibile eseguire la query e visualizzare i risultati nel **risultato** visualizzazione.  
  
 Tutte le query di stima utilizzano DMX, ovvero la forma abbreviata per il linguaggio Data Mining Extensions (DMX). La sintassi di DMX è simile a quella di T-SQL e viene utilizzata specificamente per le query sugli oggetti di data mining. Sebbene la sintassi DMX non sia complicata, usando un generatore di query come questo o in quello di [SQL Server Data Mining componente aggiuntivo per Office](../../2014/analysis-services/data-mining/sql-server-data-mining-add-ins-for-office.md), rende molto più semplice selezionare gli input e la compilazione di espressioni, pertanto è consigliabile che descrive le nozioni di base.  
  
## <a name="creating-the-query"></a>Creazione della query  
 Il primo passaggio per creare una query di stima consiste nel selezionare un modello di data mining e una tabella di input.  
  
#### <a name="to-select-a-model-and-input-table"></a>Per selezionare un modello e una tabella di input  
  
1.  Nel **stima modello di Data Mining** scheda della finestra di progettazione modelli di Data Mining, nelle **modello di Data Mining** fare clic su **Seleziona modello**.  
  
2.  Nel **Seleziona modello di Data Mining** finestra di dialogo passare attraverso l'albero per il **Targeted Mailing** strutturare, espandere la struttura, selezionare `TM_Decision_Tree`e quindi fare clic su **OK**.  
  
3.  Nel **Seleziona tabelle di Input** fare clic su **Seleziona tabella del Case**.  
  
4.  Nel **Seleziona tabella del** nella finestra di dialogo il **Zdroj dat** selezionare la vista origine dati [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)].  
  
5.  Nelle **nome tabella/vista**, selezionare la **ProspectiveBuyer (dbo)** tabella e quindi fare clic su **OK**.  
  
     Il `ProspectiveBuyer` tabella rispecchia maggiormente le **vTargetMail** tabella del case.  
  
## <a name="mapping-the-columns"></a>Mapping delle colonne  
 Dopo aver selezionato la tabella di input, il generatore delle query di stima crea un mapping predefinito tra il modello di data mining e la tabella di input in base ai nomi delle colonne. Almeno una colonna della struttura deve corrispondere a una colonna dei dati esterni.  
  
> [!IMPORTANT]  
>  I dati utilizzati per determinare l'accuratezza dei modelli devono contenere una colonna della quale è possibile eseguire il mapping alla colonna stimabile. Se tale colonna non esiste, è possibile crearne una con valori vuoti, ma deve contenere lo stesso tipo di dati della colonna stimabile.  
  
#### <a name="to-map-the-inputs-to-the-model"></a>Per eseguire il mapping degli input al modello  
  
1.  Fare doppio clic su linee che connettono il **modello di Data Mining** finestra per il **Seleziona tabella di Input** finestra e selezionare **Modifica connessioni**.  
  
     Si noti che non su tutte le colonne viene eseguito il mapping. Si aggiungeranno i mapping per diverse **le colonne della tabella**. Verrà inoltre generata una nuova colonna per la data di nascita in base alla colonna della data corrente in modo da ottenere una maggiore corrispondenza tra le colonne.  
  
2.  Sotto **colonna della tabella**, fare clic su di `Bike Buyer` cella e selezionare Prospectivebuyer dall'elenco a discesa.  
  
     Verrà eseguito il mapping della colonna stimabile [Bike Buyer] a una colonna della tabella di input.  
  
3.  Fare clic su **OK**.  
  
4.  Nelle **Esplora soluzioni**, fare doppio clic il **Targeted Mailing** vista origine dati e selezionare **Visualizza finestra di progettazione**.  
  
5.  La tabella ProspectiveBuyer, mouse e scegliere **nuovo calcolo denominato**.  
  
6.  Nel **Crea calcolo denominato** della finestra di dialogo per **nome di colonna**, tipo `calcAge`.  
  
7.  Per la **Description**, digitare **calcolare l'età in base alla data di nascita**.  
  
8.  Nel **espressione** , digitare `DATEDIFF(YYYY,[BirthDate],getdate())` e quindi fare clic su **OK**.  
  
     Poiché la tabella di input non contiene **età** colonna che corrisponde a quella nel modello, è possibile usare questa espressione per calcolare l'età del cliente dalla colonna BirthDate della tabella di input. Poiché **età** è stato identificato come più influenti colonna per la stima dell'acquisto di biciclette, deve esistere sia nel modello e della tabella di input.  
  
9. Progettazione modelli di Data Mining, selezionare la **stima modello di Data Mining** scheda e riaprire il **Modifica connessioni** finestra.  
  
10. Sotto **colonna della tabella**, fare clic sui **Age** cella e selezionare CalcAge dall'elenco a discesa.  
  
    > [!WARNING]  
    >  Se la colonna non viene visualizzata nell'elenco, potrebbe essere necessario aggiornare la definizione della vista origine dati caricata nella finestra di progettazione. A tale scopo, dal **File** dal menu **Salva tutto**, quindi chiudere e riaprire il progetto nella finestra di progettazione.  
  
11. Fare clic su **OK**.  
  
## <a name="designing-the-prediction-query"></a>Progettazione della query di stima  
  
1.  Il primo pulsante nella barra degli strumenti del **stima modello di Data Mining** scheda è la **passare alla progettazione consente di visualizzare / passa alla visualizzazione dei risultati / passa alla visualizzazione query** pulsante. Fare clic sulla freccia verso il basso su questo pulsante e selezionare **progettazione**.  
  
2.  Nella griglia al **stima modello di Data Mining** scheda, fare clic sulla cella nella prima riga vuota nel **origine** colonna e quindi selezionare **funzione di stima**.  
  
3.  Nel **funzione di stima** riga il **campo** colonna, selezionare `PredictProbability`.  
  
     Nel **Alias** colonna della stessa riga, digitare **probabilità del risultato**.  
  
4.  Dal **modello di Data Mining** finestra precedente, selezionare e trascinare [Bike Buyer] nella **criteri/argomento** cella.  
  
     Quando si let passa, [TM_Decision_Tree]. [Bike Buyer] viene visualizzato nei **criteri/argomento** cella.  
  
     In questo modo viene specificata la colonna di destinazione per la funzione `PredictProbability`. Per altre informazioni sulle funzioni, vedere [Data Mining Extensions &#40;DMX&#41; Function Reference](/sql/dmx/data-mining-extensions-dmx-function-reference).  
  
5.  Fare clic sulla riga vuota successiva nella **origine** colonna e quindi selezionare i modelli di data mining TM_Decision_Tree **.**  
  
6.  Nel `TM_Decision_Tree` riga di **campo** colonna, selezionare `Bike Buyer`.  
  
7.  Nel `TM_Decision_Tree` riga di **criteri/argomento** colonna, tipo `=1`.  
  
8.  Fare clic sulla riga vuota successiva nella **origine** colonna e quindi selezionare **tabella ProspectiveBuyer**.  
  
9. Nel `ProspectiveBuyer` riga di **campo** colonna, selezionare **ProspectiveBuyerKey**.  
  
     Verrà aggiunto un identificatore univoco alla query di stima che consente di identificare la probabilità di acquisto di una bicicletta da parte dei singoli clienti.  
  
10. Aggiungere altre cinque righe alla griglia. Per ogni riga, selezionare **tabella ProspectiveBuyer** come la **origine** e quindi aggiungere le colonne seguenti nel **campo** celle:  
  
    -   calcAge  
  
    -   LastName  
  
    -   FirstName  
  
    -   AddressLine1  
  
    -   AddressLine2  
  
 Eseguire infine la query e visualizzare i risultati.  
  
 Il **generatore Query di stima** include anche questi controlli:  
  
-   **Mostra** casella di controllo  
  
     Consente di rimuovere le clausole dalla query senza doverle eliminare dalla finestra di progettazione. Questa operazione può risultare utile quando si utilizzano query complesse e si desidera mantenere la sintassi senza dover copiare e incollare il codice DMX nella finestra.  
  
-   **Gruppo**  
  
     Inserisce una parentesi (sinistra) di apertura all'inizio della riga selezionata o inserisce una parentesi (destra) di chiusura alla fine della riga corrente.  
  
-   **AND/OR**  
  
     Inserisce l'operatore `AND` o l'operatore `OR` immediatamente dopo la funzione o la colonna corrente.  
  
#### <a name="to-run-the-query-and-view-results"></a>Per eseguire la query e visualizzare i risultati  
  
1.  Nel **stima modello di Data Mining** scheda, seleziona la **risultato** pulsante.  
  
2.  Dopo l'esecuzione della query e la visualizzazione dei risultati, è possibile rivedere i risultati.  
  
     Il **stima modello di Data Mining** scheda vengono visualizzate le informazioni di contatto dei potenziali clienti che saranno probabilmente acquirenti di biciclette. Il **probabilità del risultato** colonna indica la probabilità che la stima sia corretta. È possibile utilizzare questi risultati per determinare quali tra i clienti potenziali sono da considerare come potenziali destinatari di messaggi promozionali.  
  
3.  A questo punto, è possibile salvare i risultati. Sono disponibili tre opzioni:  
  
    -   Fare doppio clic su una riga di dati nei risultati e selezionare **copia** per salvare solo il valore (e sull'intestazione di colonna) negli Appunti.  
  
    -   Fare doppio clic su qualsiasi riga nei risultati e selezionare **copia tutto** per copiare l'intero set di risultati, incluse le intestazioni di colonna, negli Appunti.  
  
    -   Fare clic su **Salva risultati query** per salvare i risultati direttamente a un database, come indicato di seguito:  
  
        1.  Nel **Salva risultati Data Mining Query** nella finestra di dialogo selezionare un'origine dati oppure definire una nuova origine dati.  
  
        2.  Digitare un nome per la tabella in cui saranno contenuti i risultati della query.  
  
        3.  Usare l'opzione **Aggiungi a vista origine dati**, per creare la tabella e aggiungerla a una vista origine dati esistente. Ciò è utile se si desidera mantenere tutte le tabelle correlate per un modello, ad esempio dati di training, dati di origine di stima e query risultati aggiuntivo la stessa vista origine dati.  
  
        4.  Usare l'opzione **Sovrascrivi se esistente**, per aggiornare una tabella esistente con i risultati più recenti.  
  
             È necessario utilizzare l'opzione per sovrascrivere la tabella se sono state aggiunte tutte le colonne alla query di stima, modificati i nomi o i tipi di dati di tutte le colonne nella query di stima o se sono state eseguite tutte le istruzioni ALTER sulla tabella di destinazione.  
  
             Inoltre, se più colonne con lo stesso nome (ad esempio, il nome di colonna predefinito **espressione**) è necessario creare un alias per le colonne con nomi duplicati o verrà generato un errore durante il tentativo di salvare i risultati in SQL con la finestra di progettazione Server. Il motivo è che SQL Server non consente più colonne con lo stesso nome.  
  
             Per altre informazioni, vedere [salvare finestra di dialogo di Data Mining Query risultato &#40;visualizzazione stima modello di Data Mining&#41;](../../2014/analysis-services/save-data-mining-query-result-dialog-box-mining-model-prediction-view.md).  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Usando il drill-through sui dati della struttura &#40;esercitazione di base di Data Mining&#41;](../../2014/tutorials/using-drillthrough-on-structure-data-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Creare una query di stima usando Generatore di query di stima](../../2014/analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)  
  
  
