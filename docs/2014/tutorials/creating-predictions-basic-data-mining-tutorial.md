---
title: Creazione di stime (esercitazione di base sul data mining) | Microsoft Docs
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
ms.openlocfilehash: 456aec6c6b9d0d1a5d0ee1d9949507a37577130c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67597519"
---
# <a name="creating-predictions-basic-data-mining-tutorial"></a>Creazione di stime (Esercitazione di base sul data mining)
  Una volta verificata l'accuratezza dei modelli di data mining e si è deciso di ottenere risultati soddisfacenti, è possibile generare stime utilizzando la Generatore di query di stima nella scheda **Stima modello** di data mining di progettazione modelli di data mining.  
  
 Nel generatore delle query di stima sono disponibili tre viste. Con le visualizzazioni **progettazione** e **query** , è possibile compilare ed esaminare la query. È quindi possibile eseguire la query e **visualizzare i risultati nella visualizzazione risultati** .  
  
 Tutte le query di stima utilizzano DMX, ovvero la forma abbreviata per il linguaggio Data Mining Extensions (DMX). La sintassi di DMX è simile a quella di T-SQL e viene utilizzata specificamente per le query sugli oggetti di data mining. Sebbene la sintassi DMX non sia complicata, l'utilizzo di un generatore di query come questo o quello nel [SQL Server componenti aggiuntivi Data mining per Office](../../2014/analysis-services/data-mining/sql-server-data-mining-add-ins-for-office.md), rende molto più semplice selezionare gli input e le espressioni di compilazione, pertanto è consigliabile apprendere le nozioni di base.  
  
## <a name="creating-the-query"></a>Creazione della query  
 Il primo passaggio per creare una query di stima consiste nel selezionare un modello di data mining e una tabella di input.  
  
#### <a name="to-select-a-model-and-input-table"></a>Per selezionare un modello e una tabella di input  
  
1.  Nella scheda **Stima modello** di data mining di progettazione modelli di data mining fare clic su **Seleziona modello**nella casella **modello di data mining** .  
  
2.  Nella finestra di dialogo **Seleziona modello di data mining** spostarsi nell'albero fino alla struttura **Targeted Mailing** , espandere la struttura `TM_Decision_Tree`, selezionare, quindi fare clic su **OK**.  
  
3.  Nella casella **Seleziona tabella/** e di input fare clic su **Seleziona tabella del case**.  
  
4.  Nella finestra di dialogo **Seleziona tabella** selezionare la vista [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]origine dati nell'elenco **origine dati** .  
  
5.  In **nome tabella/vista**selezionare la tabella **ProspectiveBuyer (dbo)** , quindi fare clic su **OK**.  
  
     La `ProspectiveBuyer` tabella è molto simile alla tabella del case **vTargetMail** .  
  
## <a name="mapping-the-columns"></a>Mapping delle colonne  
 Dopo aver selezionato la tabella di input, il generatore delle query di stima crea un mapping predefinito tra il modello di data mining e la tabella di input in base ai nomi delle colonne. Almeno una colonna della struttura deve corrispondere a una colonna dei dati esterni.  
  
> [!IMPORTANT]  
>  I dati utilizzati per determinare l'accuratezza dei modelli devono contenere una colonna della quale è possibile eseguire il mapping alla colonna stimabile. Se tale colonna non esiste, è possibile crearne una con valori vuoti, ma deve contenere lo stesso tipo di dati della colonna stimabile.  
  
#### <a name="to-map-the-inputs-to-the-model"></a>Per eseguire il mapping degli input al modello  
  
1.  Fare clic con il pulsante destro del mouse sulle linee che connettono la finestra **modello di data mining** alla finestra **Seleziona tabella di input** e scegliere **modifica connessioni**.  
  
     Si noti che non su tutte le colonne viene eseguito il mapping. Si aggiungeranno i mapping per diverse **colonne della tabella**. Verrà inoltre generata una nuova colonna per la data di nascita in base alla colonna della data corrente in modo da ottenere una maggiore corrispondenza tra le colonne.  
  
2.  In **colonna tabella**fare clic sulla `Bike Buyer` cella e selezionare ProspectiveBuyer. Unknown nell'elenco a discesa.  
  
     Verrà eseguito il mapping della colonna stimabile [Bike Buyer] a una colonna della tabella di input.  
  
3.  Fare clic su **OK**.  
  
4.  In **Esplora soluzioni**fare clic con il pulsante destro del mouse sulla vista origine dati **mailing** diretto e scegliere **Visualizza finestra di progettazione**.  
  
5.  Fare clic con il pulsante destro del mouse sulla tabella ProspectiveBuyer e scegliere **nuovo calcolo denominato**.  
  
6.  Nella finestra di dialogo **Crea calcolo denominato** Digitare `calcAge`per **nome colonna**.  
  
7.  Per **Descrizione**digitare **Calculate Age in base alla data di nascita**.  
  
8.  Nella casella **espressione** Digitare `DATEDIFF(YYYY,[BirthDate],getdate())` , quindi fare clic su **OK**.  
  
     Poiché la tabella di input non dispone di una colonna **Age** corrispondente a quella del modello, è possibile utilizzare questa espressione per calcolare l'età del cliente dalla colonna Data di nascita nella tabella di input. Poiché **Age** è stato identificato come la colonna più influente per la stima dell'acquisto di biciclette, deve esistere sia nel modello che nella tabella di input.  
  
9. In Progettazione modelli di data mining selezionare la scheda **Stima modello di data mining** e riaprire la finestra **modifica connessioni** .  
  
10. In **colonna tabella**fare clic sulla cella **età** e selezionare ProspectiveBuyer. calci nell'elenco a discesa.  
  
    > [!WARNING]  
    >  Se la colonna non viene visualizzata nell'elenco, potrebbe essere necessario aggiornare la definizione della vista origine dati caricata nella finestra di progettazione. A tale scopo, scegliere **Salva tutto**dal menu **file** , quindi chiudere e riaprire il progetto nella finestra di progettazione.  
  
11. Fare clic su **OK**.  
  
## <a name="designing-the-prediction-query"></a>Progettazione della query di stima  
  
1.  Il primo pulsante della barra degli strumenti della scheda **Stima modello di data mining** è **passa alla visualizzazione progettazione/passa a visualizzazione risultati/passa al pulsante visualizzazione query** . Fare clic sulla freccia verso il basso in questo pulsante e selezionare **progetta**.  
  
2.  Nella griglia della scheda **Stima modello di data mining** fare clic sulla cella nella prima riga vuota della colonna **origine** , quindi selezionare **funzione di stima**.  
  
3.  Nella riga **funzione di stima** fare clic `PredictProbability`su nella colonna **campo** .  
  
     Nella colonna **alias** della stessa riga digitare **probabilità di risultato**.  
  
4.  Dalla finestra **modello di data mining** precedente, selezionare e trascinare [Bike Buyer] nella cella **criteri/argomento** .  
  
     Quando si lascia andare, [TM_Decision_Tree]. [Bike Buyer] viene visualizzato nella cella **criteri/argomento** .  
  
     In questo modo viene specificata la colonna di destinazione per la funzione `PredictProbability`. Per ulteriori informazioni sulle funzioni, vedere [Data Mining Extensions &#40;DMX&#41; Function Reference](/sql/dmx/data-mining-extensions-dmx-function-reference).  
  
5.  Fare clic sulla riga vuota successiva nella colonna **origine** , quindi selezionare **TM_Decision_Tree** modello di data mining.  
  
6.  Nella `TM_Decision_Tree` riga della colonna **campo** Selezionare `Bike Buyer`.  
  
7.  Nella `TM_Decision_Tree` riga, nella colonna **criteri/argomento** , digitare `=1`.  
  
8.  Fare clic sulla riga vuota successiva nella colonna **origine** , quindi selezionare la **tabella ProspectiveBuyer**.  
  
9. Nella `ProspectiveBuyer` riga della colonna **campo** Selezionare **ProspectiveBuyerKey**.  
  
     Verrà aggiunto un identificatore univoco alla query di stima che consente di identificare la probabilità di acquisto di una bicicletta da parte dei singoli clienti.  
  
10. Aggiungere altre cinque righe alla griglia. Per ogni riga selezionare **ProspectiveBuyer Table** come **origine** , quindi aggiungere le colonne seguenti nelle celle del **campo** :  
  
    -   calcAge  
  
    -   LastName  
  
    -   FirstName  
  
    -   AddressLine1  
  
    -   AddressLine2  
  
 Eseguire infine la query e visualizzare i risultati.  
  
 Il **Generatore di query di stima** include anche i controlli seguenti:  
  
-   Casella di controllo **Mostra**  
  
     Consente di rimuovere le clausole dalla query senza doverle eliminare dalla finestra di progettazione. Questa operazione può risultare utile quando si utilizzano query complesse e si desidera mantenere la sintassi senza dover copiare e incollare il codice DMX nella finestra.  
  
-   **Gruppo**  
  
     Inserisce una parentesi (sinistra) di apertura all'inizio della riga selezionata o inserisce una parentesi (destra) di chiusura alla fine della riga corrente.  
  
-   **E/O**  
  
     Inserisce l'operatore `AND` o l'operatore `OR` immediatamente dopo la funzione o la colonna corrente.  
  
#### <a name="to-run-the-query-and-view-results"></a>Per eseguire la query e visualizzare i risultati  
  
1.  Nella scheda **Stima modello di data mining** selezionare il pulsante **risultato** .  
  
2.  Dopo l'esecuzione della query e la visualizzazione dei risultati, è possibile rivedere i risultati.  
  
     Nella scheda **Stima modello di data mining** vengono visualizzate le informazioni di contatto per i potenziali clienti che probabilmente sono acquirenti di biciclette. La colonna **probabilità della colonna risultati** indica la probabilità che la stima sia corretta. È possibile utilizzare questi risultati per determinare quali tra i clienti potenziali sono da considerare come potenziali destinatari di messaggi promozionali.  
  
3.  A questo punto, è possibile salvare i risultati. Sono disponibili tre opzioni:  
  
    -   Fare clic con il pulsante destro del mouse su una riga di dati nei risultati e selezionare **copia** per salvare solo quel valore (e l'intestazione di colonna) negli Appunti.  
  
    -   Fare clic con il pulsante destro del mouse su una riga nei risultati e selezionare **copia tutto** per copiare negli Appunti l'intero set di risultati, incluse le intestazioni di colonna.  
  
    -   Fare clic su **Salva risultati query** per salvare i risultati direttamente in un database, come indicato di seguito:  
  
        1.  Nella finestra di dialogo **Salva risultati query di data mining** selezionare un'origine dati o definire una nuova origine dati.  
  
        2.  Digitare un nome per la tabella in cui saranno contenuti i risultati della query.  
  
        3.  Utilizzare l'opzione **Aggiungi a DSV**per creare la tabella e aggiungerla a una vista origine dati esistente. Questa opzione è utile se si desidera utilizzare tutte le tabelle correlate per un modello, ad esempio i dati di training, i dati di origine della stima e i risultati della query, nella stessa vista origine dati.  
  
        4.  Utilizzare l'opzione, **Sovrascrivi se esistente**, per aggiornare una tabella esistente con i risultati più recenti.  
  
             È necessario utilizzare l'opzione per sovrascrivere la tabella se sono state aggiunte tutte le colonne alla query di stima, modificati i nomi o i tipi di dati di tutte le colonne nella query di stima o se sono state eseguite tutte le istruzioni ALTER sulla tabella di destinazione.  
  
             Inoltre, se più colonne hanno lo stesso nome (ad esempio, l' **espressione**del nome di colonna predefinito), è necessario creare un alias per le colonne con nomi duplicati. in caso di errore, verrà generato un errore quando la finestra di progettazione tenterà di salvare i risultati in SQL Server. Il motivo è che SQL Server non consente più colonne con lo stesso nome.  
  
             Per ulteriori informazioni, vedere la [finestra di dialogo Salva risultati query di Data Mining &#40;visualizzazione Stima modello di data mining&#41;](../../2014/analysis-services/save-data-mining-query-result-dialog-box-mining-model-prediction-view.md).  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Utilizzo del drill-through sui dati della struttura &#40;esercitazione di base sul data mining&#41;](../../2014/tutorials/using-drillthrough-on-structure-data-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Creare una query di stima utilizzando Generatore query di stima](../../2014/analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)  
  
  
