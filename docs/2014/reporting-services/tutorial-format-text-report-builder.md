---
title: 'Esercitazione: Formattazione di testo (Generatore report) | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 67d8513e-8a70-464b-b87f-e91d010cfd82
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9e509fb84ffd35085e7930925fd71499a6c96c87
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62647535"
---
# <a name="tutorial-format-text-report-builder"></a>Esercitazione: Formattazione del testo (Generatore report)
  In questa esercitazione sarà possibile applicare una formattazione al testo in modi diversi. Dopo avere impostato l'origine dati e il set di dati per il report vuoto, sarà possibile scegliere i passaggi che si desidera esplorare.  
  
 Nell'immagine seguente viene illustrato un report simile a quello che verrà creato.  
  
 ![rs_FormatTextFinal](../../2014/tutorials/media/rs-formattextfinal.gif "rs_FormatTextFinal")  
  
 In un passaggio si introdurrà intenzionalmente un errore, in modo da comprenderne gli effetti. Si correggerà quindi l'errore per ottenere il risultato desiderato.  
  
 Una versione avanzata del report che verrà creato in questa esercitazione è disponibile come report di esempio di Generatore report di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Per altre informazioni sul download di questo report di esempio e ad altri utenti, vedere [Report di Generatore report di esempio](https://go.microsoft.com/fwlink/?LinkId=184851).  
  
##  <a name="BackToTop"></a> Lezioni dell'esercitazione  
  
### <a name="set-up-the-report"></a>Impostazione del report  
 1. [Creare un Report vuoto con dati di un set di dati e origine](#CreateReport)  
  
 2. [Aggiungere un campo all'area di progettazione Report (in modo non corretto e quindi correggendolo)](#AddField)  
  
 3. [Aggiungere una tabella all'area di progettazione Report](#AddTable)  
  
### <a name="pick-and-choose"></a>Effettuare una scelta  
 [Aggiungere un collegamento ipertestuale al Report](#AddHyperlink)  
  
 [Ruotare il testo nel Report](#RotateText)  
  
 [Visualizzazione di testo con formattazione HTML](#FormatHTML)  
  
 [Formattazione della valuta](#FormatCurrency)  
  
 [Salvare il Report](#Save)  
  
 Tempo stimato per completare questa esercitazione: 20 minuti.  
  
## <a name="requirements"></a>Requisiti  
 Per altre informazioni sui requisiti, vedere [Prerequisiti per le esercitazioni &#40;Generatore report&#41;](../reporting-services/report-builder-tutorials.md).  
  
##  <a name="CreateReport"></a> Creare un Report vuoto con dati di un set di dati e origine  
  
#### <a name="to-create-a-blank-report"></a>Per creare un report vuoto  
  
1.  Fare clic su **avviare**, scegliere **programmi**, scegliere [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)] **Generatore Report**, quindi fare clic su **Generatore Report**.  
  
    > [!NOTE]  
    >  Verrà visualizzata la finestra di dialogo **Riquadro attività iniziale** . In caso contrario, fare clic sul pulsante Generatore report, quindi su **Nuovo**.  
  
2.  Nel riquadro sinistro della finestra di dialogo **Riquadro attività iniziale** verificare che l'opzione **Nuovo report** sia selezionata.  
  
3.  Nel riquadro destro fare clic su **Report vuoto**.  
  
#### <a name="to-create-a-data-source"></a>Per creare un'origine dati  
  
1.  Nel riquadro dei dati del report fare clic su **Nuova**, quindi su **Origine dati**.  
  
2.  Nella casella **Nome** digitare: **TextDataSource**  
  
3.  Fare clic su **Usa una connessione incorporata nel report**.  
  
4.  Verificare che il tipo di connessione sia Microsoft SQL Server, quindi nella casella **Stringa di connessione** digitare: **Origine dati = \<nomeserver>**  
  
    > [!NOTE]  
    >  L'espressione \<servername >, ad esempio Report001, specifica un computer in cui è installata un'istanza del motore di Database SQL Server. Per questa esercitazione non sono necessari dati specifici. È sufficiente una connessione a un database di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] . Se in **Connessioni a origini dati** è già disponibile una connessione, è possibile selezionarla e passare alla procedura successiva, ovvero "Per creare un set di dati". Per altre informazioni, vedere [Modalità alternative di acquisizione di una connessione dati &#40;Generatore report&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-create-a-dataset"></a>Per creare un set di dati  
  
1.  Nel riquadro dei dati del report fare clic su **Nuovo**, quindi su **Set di dati**.  
  
2.  Verificare che l'origine dati sia **TextDataSource**.  
  
3.  Nella casella **Nome** digitare: **TextDataset.**  
  
4.  Verificare che il tipo di query **Testo** sia selezionato, quindi fare clic su **Progettazione query**.  
  
5.  Fare clic su **Modifica come testo**.  
  
6.  Incollare la query seguente nel relativo riquadro:  
  
    ```  
    SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13747.25 AS money) AS Sales, 55 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(9248.15 AS money) As Sales, 37 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1800.00 AS money) AS Sales, 24 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1125.00 AS money) AS Sales, 15 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,  'Lens Adapter' as Product, CAST(742.50 AS money) AS Sales, 11 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1417.50 AS money) AS Sales, 21 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13497.30 AS money) AS Sales, 54 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(11997.60 AS money) AS Sales, 48 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(10247.95 AS money) As Sales, 41 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Tripod' as Product, CAST(1200.00 AS money) AS Sales, 16 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(2025.00 AS money) AS Sales, 27 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1425.00 AS money) AS Sales, 19 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(887.50 AS money) AS Sales, 13 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Lens Adapter' as Product, CAST(607.50 AS money) AS Sales, 9 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1215.00 AS money) AS Sales, 18 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(10191.00 AS money) AS Sales, 79 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8772.00 AS money) AS Sales, 68 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(10578.00 AS money) AS Sales, 82 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(7218.10 AS money) AS Sales, 38 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory,'Digital' as Subcategory,'Slim Digital' as Product, CAST(9307.55 AS money) AS Sales, 49 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(3870.00 AS money) AS Sales, 30 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(5805.00 AS money) AS Sales, 45 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8643.00 AS money) AS Sales, 67 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(9877.40 AS money) AS Sales, 52 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(12536.70 AS money) AS Sales, 66 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(6648.25 AS money) AS Sales, 35 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    ```  
  
7.  Scegliere Esegui (**!**) per eseguire la query.  
  
     I risultati della query corrispondono ai dati disponibili per la visualizzazione nel report.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="AddField"></a> Aggiungere un campo all'area di progettazione Report  
 Se si desidera visualizzare un campo del set di dati in un report, è probabile che si scelga innanzitutto di trascinarlo direttamente nell'area di progettazione. In questo esercizio viene indicato perché questo modo di procedere non è corretto e quale operazione è invece necessario eseguire.  
  
#### <a name="to-add-a-field-to-the-report-and-get-the-wrong-result"></a>Per aggiungere un campo al report (e ottenere il risultato sbagliato)  
  
1.  Trascinare il campo **FullName** dal riquadro Dati report nell'area di progettazione.  
  
     Generatore report consente di creare una casella di testo con un'espressione rappresentata come \<Expr >.  
  
2.  Fare clic su **Esegui**.  
  
     Si noti che esiste un solo record, **Fernando Ross**, che rappresenta il primo record nella query in ordine alfabetico. Il campo non viene ripetuto per visualizzare gli altri record di tale campo.  
  
3.  Fare clic su **Progettazione** per tornare alla visualizzazione Struttura.  
  
4.  Selezionare l'espressione \<Expr > nella casella di testo.  
  
5.  Nel riquadro Proprietà della proprietà **Value** verrà visualizzato quanto segue (se il riquadro Proprietà non è visualizzato, selezionare **Proprietà** nella scheda **Visualizza**):  
  
    ```  
    =First(Fields!FullName.Value, "TextDataSet")  
    ```  
  
     La funzione `First` è progettata per recuperare solo il primo valore in un campo, così come è avvenuto.  
  
     Il trascinamento del campo direttamente nell'area di progettazione ha determinato la creazione di una casella di testo. Le caselle di testo non sono di per sé aree dati e pertanto non consentono di visualizzare i dati di un set di dati del report. Le caselle di testo incluse in aree dati, ad esempio tabelle, matrici ed elenchi, consentono invece di visualizzare dati.  
  
6.  Selezionare la casella di testo (se l'espressione è stata selezionata, premere ESC per selezionare la casella di testo), quindi premere CANC.  
  
#### <a name="to-add-a-field-to-the-report-and-get-the-right-result"></a>Per aggiungere un campo al report (e ottenere il risultato corretto)  
  
1.  Fare clic su **Elenco** nell'area **Aree dati** della scheda **Inserisci**sulla barra multifunzione . Fare clic nell'area di progettazione, quindi trascinare il mouse per creare una casella di circa 2 pollici (5 centimetri) di larghezza e 1 pollice (2,5 centimetri) di altezza.  
  
2.  Trascinare il campo **FullName** dal riquadro Dati report nella casella di riepilogo.  
  
     Questa volta Generatore report crea una casella di testo contenente l'espressione `[FullName]` .  
  
3.  Fare clic su **Esegui**.  
  
     Si noti che in questo caso le casella viene ripetuta per visualizzare tutti i record nella query.  
  
4.  Fare clic su **Progettazione** per tornare alla visualizzazione Struttura.  
  
5.  Selezionare l'espressione nella casella di testo.  
  
6.  Nel riquadro Proprietà della proprietà **Value** verrà visualizzato quanto segue:  
  
    ```  
    =Fields!FullName.Value  
    ```  
  
     Il trascinamento della casella di testo nell'area dati dell'elenco determina la visualizzazione dei dati inclusi nel set di dati.  
  
7.  Selezionare la casella di riepilogo e premere CANC.  
  
##  <a name="AddTable"></a> Aggiungere una tabella all'area di progettazione Report  
 Creare questa tabella in modo da disporre di un elemento in cui inserire i collegamenti ipertestuali e il testo ruotato.  
  
#### <a name="to-add-a-table-to-the-report"></a>Per aggiungere una tabella al report  
  
1.  Nel **inserire** menu, fare clic su **tabella**e quindi fare clic su **guidata tabella**.  
  
2.  Nel **scegliere un set di dati** pagina della procedura guidata nuova tabella o matrice, fare clic su **Scegli un set di dati esistente nel report o un set di dati condiviso**, fare clic su **TextDataset (in questo Report)**, quindi fare clic su **successiva**.  
  
3.  Nel **Disponi campi** pagina, trascinare il **Territory**, **LinkText**, e **prodotto** i campi a **gruppidirighe**, trascinare il **vendite** campo **valori**, quindi fare clic su **successivo**.  
  
4.  Nel **scegliere il layout** pagina, deseleziona le **Espandi/Comprimi gruppi** casella di controllo in modo che è possibile visualizzare l'intera tabella e quindi fare clic su **Avanti**.  
  
5.  Nel **scegliere uno stile** pagina, fare clic su **Slate**e quindi fare clic su **fine**.  
  
6.  Trascinare la tabella in modo da posizionarla sotto il blocco del titolo.  
  
7.  Fare clic su **Esegui**.  
  
     La tabella ha un aspetto corretto, ma dispone di due righe dei totali. Il **LinkText** campo non è necessaria una riga del totale.  
  
8.  Fare clic su **Progettazione** per tornare alla visualizzazione Struttura.  
  
9. Fare doppio clic su casella di testo che contiene `[LinkText]`, fare clic su **Dividi celle**.  
  
10. Selezionare la cella vuota sotto la `[LinkText]` cella, quindi tenere premuto il tasto MAIUSC e selezionare le due celle a destra: il **totale** cella il **prodotto** colonna e il `[Sum(Sales)]` cella il  **Vendite** colonna.  
  
11. Con queste tre celle selezionate, fare doppio clic su una delle celle e scegliere **Elimina riga**.  
  
12. Fare clic su **Esegui**.  
  
##  <a name="AddHyperlink"></a> Aggiungere un collegamento ipertestuale al Report  
 In questa sezione si aggiungerà un collegamento ipertestuale al testo incluso nella tabella creata nella sezione precedente.  
  
#### <a name="to-add-a-hyperlink-to-the-report"></a>Per aggiungere un collegamento ipertestuale al report  
  
1.  Fare clic su **Progettazione** per tornare alla visualizzazione Struttura.  
  
2.  Fare clic con il pulsante destro del mouse sulla cella contenente `[LinkText]`, quindi scegliere **Proprietà casella di testo**.  
  
3.  Nel **proprietà casella di testo** fare clic su **azione**.  
  
4.  Fare clic su **Vai a URL**.  
  
5.  Nel **selezionare un URL** fare clic su **[URL]**, quindi fare clic su **OK**.  
  
6.  Si noti che il testo non presenta alcuna differenza. È necessario renderlo simile al testo di un collegamento.  
  
7.  Selezionare `[LinkText]`.  
  
8.  Nel **Font** sezione del **Home** scheda, fare clic sui **sottolineato** pulsante e quindi fare clic sulla freccia giù accanto al **colore** pulsante, Fare clic su **blu**.  
  
9. Fare clic su **Esegui**.  
  
     L'aspetto del testo è ora simile a quello di un collegamento.  
  
10. Fare clic su un collegamento. Se il computer è connesso a Internet, in una finestra del browser verrà aperto un argomento della Guida di Generatore report.  
  
##  <a name="RotateText"></a> Ruotare il testo nel Report  
 In questa sezione si ruoterà parte del testo incluso nella tabella creata nelle sezioni precedenti.  
  
#### <a name="to-rotate-text"></a>Per ruotare il testo  
  
1.  Fare clic su **Progettazione** per tornare alla visualizzazione Struttura.  
  
2.  Fare clic nella cella che contiene `[Territory].`  
  
3.  Nella scheda **Home** della sezione **Carattere** fare clic sul pulsante **Grassetto** .  
  
4.  Se il riquadro Proprietà non è visualizzato, selezionare la casella di controllo **Proprietà** nella scheda **Vista** .  
  
5.  Individuare la proprietà WritingMode nel riquadro proprietà.  
  
    > [!NOTE]  
    >  Se le proprietà nel riquadro Proprietà sono organizzate in categorie, WritingMode si trova nella categoria **Localizzazione** . Assicurarsi di aver selezionato la cella e non il testo. WritingMode è una proprietà della casella di testo, non del testo.  
  
6.  Nella casella di riepilogo, fare clic su **Rotate270**.  
  
7.  Nel **Home** scheda il **paragrafo** fare clic sul **intermedio** e **Center** pulsanti per posizionare il testo al centro della cella entrambi verticalmente e orizzontalmente.  
  
8.  Fare clic su Esegui (**!**).  
  
 Il testo incluso nella cella `[Territory]` scorre ora verticalmente dal basso verso l'alto delle celle.  
  
##  <a name="FormatHTML"></a> Visualizzazione di testo con formattazione HTML  
  
#### <a name="to-display-text-formatted-as-html"></a>Per visualizzare testo formattato come HTML  
  
1.  Fare clic su **Progettazione** per passare alla visualizzazione Struttura.  
  
2.  Nella scheda **Inserisci** fare clic su **Casella di testo**, quindi nell'area di progettazione fare clic e trascinare il mouse per creare, sotto la tabella, una casella di testo di circa 10 centimetri di larghezza e 8 centimetri di altezza.  
  
3.  Copiare questo testo e incollarlo nella casella di testo:  
  
    ```  
    <h4>Limitations of cascading style sheet attributes</h4>  
          <p>Only a basic set of <b>cascading style sheet (CSS)</b> attributes are defined:</p>  
          <ul><li>  
              text-align, text-indent  
            </li><li>  
              font-family, font-size  
            </li><li>  
              color  
            </li><li>  
              padding, padding-bottom, padding-top, padding-right, padding-left  
            </li><li>  
              font-weight  
            </li></ul>  
    ```  
  
4.  Selezionare tutto il testo presente nella casella di testo.  
  
     Poiché questa è una proprietà del testo e non della casella di testo, in una casella di testo è possibile avere una combinazione di testo normale e di testo in cui vengono utilizzati tag HTML come stili.  
  
5.  Fare clic con il pulsante destro del mouse su tutto il testo selezionato, quindi scegliere **Proprietà testo**.  
  
6.  Nel **generali** nella pagina **tipo di Markup**, fare clic su **HTML - interpreta tag HTML come stili**.  
  
7.  Fare clic su **OK**.  
  
8.  Fare clic su Esegui (**!**) per visualizzare l'anteprima del report.  
  
 Il testo nella casella di testo viene visualizzato come un'intestazione, un paragrafo e un elenco puntato.  
  
##  <a name="FormatCurrency"></a> Formattazione della valuta  
  
#### <a name="to-format-numbers-as-currency"></a>Per formattare i numeri come valuta  
  
1.  Fare clic su **Progettazione** per passare alla visualizzazione Struttura.  
  
2.  Fare clic sulla cella prima cella tabella contenente `[Sum(Sales)]`, tenere premuto MAIUSC e fare clic sull'ultima cella della tabella contenente `[Sum(Sales)]`.  
  
3.  Nel gruppo **Numero** della scheda **Home** fare clic sul pulsante **Valuta** .  
  
4.  (Facoltativo) Nel **Home** nella scheda il **numero** raggruppare, fare clic il **stili segnaposto** pulsante e fare clic su **valori di esempio** per vedere come i numeri verranno da formattare.  
  
5.  (Facoltativo) Nel gruppo **Numero** della scheda **Home** fare clic due volte sul pulsante **Diminuisci decimali** per visualizzare le cifre in dollari senza centesimi.  
  
6.  Fare clic su Esegui (**!**) per visualizzare l'anteprima del report.  
  
 Nel report verranno visualizzati i dati formattati che rendono più facile la lettura.  
  
##  <a name="Save"></a> Salvare il Report  
 È possibile salvare i report in un server di report, in una raccolta di SharePoint o nel computer locale.  
  
 In questa esercitazione il report verrà salvato in un server di report. Se non si dispone dell'accesso a un server di report, sarà possibile salvare il report nel computer locale.  
  
#### <a name="to-save-the-report-on-a-report-server"></a>Per salvare il report in un server di report  
  
1.  Fare clic sul pulsante **Generatore report** , quindi su **Salva con nome**.  
  
2.  Fare clic su **Siti e server recenti**.  
  
3.  Selezionare o digitare il nome del server di report per il quale si dispone delle autorizzazioni di salvataggio dei report.  
  
     Verrà visualizzato il messaggio "Connessione al server di report". Al termine della connessione, verrà visualizzato il contenuto della cartella di report specificata dall'amministratore del server di report come posizione predefinita per i report.  
  
4.  In **Nome**sostituire il nome predefinito con un nome a scelta.  
  
5.  Fare clic su **Salva**.  
  
 Il report verrà salvato sul server di report. Il nome del server di report al quale si è connessi verrà visualizzato sulla barra di stato nella parte inferiore della finestra.  
  
#### <a name="to-save-the-report-on-your-computer"></a>Per salvare il report nel computer  
  
1.  Fare clic sul pulsante **Generatore report** , quindi su **Salva con nome**.  
  
2.  Fare clic su **Desktop**, **Documenti**o **Risorse del computer**, quindi selezionare la cartella in cui si desidera salvare il report.  
  
3.  In **Nome**sostituire il nome predefinito con un nome a scelta.  
  
4.  Fare clic su **Salva**.  
  
## <a name="next-steps"></a>Passaggi successivi  
 Esistono diversi modi per formattare il testo in Generatore Report [esercitazione: Creazione di un Report in formato libero &#40;Generatore Report&#41; ](../reporting-services/tutorial-creating-a-free-form-report-report-builder.md) include più esempi.  
  
## <a name="see-also"></a>Vedere anche  
 [Esercitazioni su &#40;Generatore Report&#41;](report-builder-tutorials.md)   
 [Formattazione degli elementi del report &#40;Generatore report e SSRS&#41;](report-design/formatting-report-items-report-builder-and-ssrs.md)   
 [Generatore report in SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)  
  
  
