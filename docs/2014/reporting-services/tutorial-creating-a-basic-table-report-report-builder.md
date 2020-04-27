---
title: 'Esercitazione: Creazione di un report tabella semplice (Generatore report) | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: d9e30521-f8ae-4c45-89c3-d40727f622f7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 93213609abbc3e274cc61207d02b3828f9b90d7d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66099028"
---
# <a name="tutorial-creating-a-basic-table-report-report-builder"></a>Esercitazione: Creazione di un report tabella semplice (Generatore report)
  In questa esercitazione viene illustrato come creare un report tabella semplice basato sui dati di vendita di esempio. Nell'illustrazione seguente viene mostrato il report che verrà creato.  
  
 ![rs_CreateBasicReportTutorial](../../2014/tutorials/media/rs-createbasicreporttutorial.gif "rs_CreateBasicReportTutorial")  
  
##  <a name="what-you-will-learn"></a><a name="BackToTop"></a>Cosa si apprenderà  
 In questa esercitazione verranno illustrate le operazioni seguenti:  
  
1.  [Creare un nuovo report dal Riquadro attività iniziale](#CreateTable)  
  
    1.  [Specificare una connessione dati in Creazione guidata tabella](#DataConnection)  
  
    2.  [Creare una query in Creazione guidata tabella](#Query)  
  
    3.  [Organizzare dati in gruppi in Creazione guidata tabella](#Groups)  
  
    4.  [Aggiungere le righe Subtotale e Totale in Creazione guidata tabella](#Subtotals)  
  
    5.  [Scegliere uno stile in Creazione guidata tabella](#Style)  
  
2.  [Formattare i dati come valuta](#FormatCurrency)  
  
3.  [Formattare i dati come data](#FormatDate)  
  
4.  [Modificare la larghezza delle colonne](#Width)  
  
5.  [Aggiungere un titolo al report](#Title)  
  
6.  [Salva il report](#Save)  
  
7.  [Esportare il report](#Export)  
  
 Il tempo stimato per il completare l'esercitazione è di 20 minuti.  
  
## <a name="requirements"></a>Requisiti  
 Per altre informazioni sui requisiti, vedere [Prerequisiti per le esercitazioni &#40;Generatore report&#41;](../reporting-services/report-builder-tutorials.md).  
  
##  <a name="1-create-a-new-report-from-getting-started"></a><a name="CreateTable"></a>1. creare un nuovo report da Introduzione  
 Creare un report tabella dalla finestra di dialogo **Introduzione** . Sono disponibili due modalità: progettazione report e progettazione del set di dati condivisa. Nella modalità progettazione report si specificano i dati nel riquadro dei dati del report e il layout del report nell'area di progettazione. Nella modalità progettazione del set di dati condivisa, si creano query del set di dati da condividere con altri. In questa esercitazione si utilizzerà modalità progettazione report.  
  
#### <a name="to-create-a-new-report"></a>Per creare un nuovo report  
  
1.  Fare clic sul menu **Start**, scegliere **Programmi**, **Generatore report per Microsoft SQL Server 2012**e quindi fare clic su **Generatore report**.  
  
     Verrà visualizzata la finestra di dialogo **Attività iniziali**.  
  
    > [!NOTE]  
    >  Se la finestra di dialogo **Introduzione** non viene visualizzata, dal pulsante **Generatore report** fare clic su **nuovo**.  
  
2.  Nel riquadro sinistro verificare che sia selezionata l'opzione **Nuovo report** .  
  
3.  Nel riquadro destro verificare che sia selezionata **Creazione guidata tabella o matrice** .  
  
##  <a name="1a-specify-a-data-connection-in-the-table-wizard"></a><a name="DataConnection"></a>1a. Specificare una connessione dati in Creazione guidata tabella  
 Una connessione dati contiene le informazioni necessarie per connettersi a un'origine dati esterna, ad esempio un database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . In genere, le informazioni di connessione e il tipo di credenziali da utilizzare vengono fornite dal proprietario dell'origine dati. Per specificare una connessione dati, è possibile utilizzare un'origine dati condivisa dal server di report o creare un'origine dati incorporata che sia utilizzata solo in questo report.  
  
 In questa esercitazione si utilizzerà un'origine dati incorporata. Per altre informazioni sull'uso di un'origine dati condivisa, vedere [Modalità alternative di acquisizione di una connessione dati &#40;Generatore report&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
#### <a name="to-create-an-embedded-data-source"></a>Per creare un'origine dati incorporata  
  
1.  Nella pagina **Scegliere un set di dati** selezionare **Crea un set di dati**, quindi fare clic su **Avanti**. Verrà visualizzata la pagina **Scegliere una connessione a un'origine dei dati** .  
  
2.  Fare clic su **New**. Verrà visualizzata la finestra di dialogo **Proprietà origine dati** .  
  
3.  In **nome**digitare **vendite prodotto** un nome per l'origine dati.  
  
4.  In **Select a connection type**(Seleziona un tipo di connessione), verificare che sia selezionato **Microsoft SQL Server** .  
  
5.  In **stringa di connessione**Digitare il testo seguente, dove * \<nomeserver>* è il nome di un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
    ```  
    Data Source=<servername>  
    ```  
  
     Poiché verrà utilizzata una query che contiene i dati anziché recuperarli da un database, la stringa di connessione non include il nome del database. Per altre informazioni, vedere [Prerequisiti per le esercitazioni &#40;Generatore report&#41;](../reporting-services/report-builder-tutorials.md).  
  
6.  Fare clic su **Credenziali**. Immettere le credenziali necessarie per accedere all'origine dati esterna.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     Verrà visualizzata di nuovo la pagina **Scegliere una connessione a un'origine dei dati** .  
  
8.  Per verificare che la connessione all'origine dati avvenga correttamente, fare clic su **Test connessione**.  
  
     Verrà visualizzato il messaggio "Creazione connessione completata".  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. Fare clic su **Avanti**.  
  
##  <a name="1b-create-a-query-in-the-table-wizard"></a><a name="Query"></a>1b. Creare una query in Creazione guidata tabella  
 In un report, è possibile utilizzare un set di dati condiviso che dispone di una query predefinita oppure è possibile creare un set di dati incorporato da utilizzare solo nel report. In questa esercitazione si creerà un set di dati incorporato.  
  
> [!NOTE]  
>  Nella query di questa esercitazione sono contenuti i valori dei dati in modo che non sia necessaria un'origine dati esterna. Tale condizione rende tuttavia la query piuttosto lunga. In una query di un ambiente aziendale non sarebbe incluso alcun dato. Questo esempio è solo a scopo illustrativo.  
  
#### <a name="to-create-a-query"></a>Per creare una query  
  
1.  Nella pagina **Progetta query** si apre la finestra Progettazione query relazionale. Per questa esercitazione si utilizzerà la finestra Progettazione query basata su testo.  
  
     Fare clic su **modifica come testo**. Nella finestra Progettazione query basata su testo viene visualizzato il riquadro della query e il riquadro dei risultati.  
  
2.  Nella casella [!INCLUDE[tsql](../includes/tsql-md.md)] Query **incollare la query** seguente.  
  
    ```  
    SELECT CAST('2009-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Carrying Case' as Product, CAST(9924.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-11' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Mini Battery Charger' as Product, CAST(1056.00 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Accessories' as Subcategory,  
       'Telephoto Conversion Lens' as Product, CAST(1380.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,'Accessories' as Subcategory,    
       'USB Cable' as Product, CAST(780.00 AS money) AS Sales, 26 as Quantity  
    UNION SELECT CAST('2009-01-08' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3798.00 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2009-01-09' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Business Videographer' as Product, CAST(10400.00 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2009-01-10' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Social Videographer' as Product, CAST(3000.00 AS money) AS Sales, 60 as Quantity  
    UNION SELECT CAST('2009-01-11' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Advanced Digital' as Product, CAST(7234.50 AS money) AS Sales, 39 as Quantity  
    UNION SELECT CAST('2009-01-07' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Compact Digital' as Product, CAST(10836.00 AS money) AS Sales, 84 as Quantity  
    UNION SELECT CAST('2009-01-08' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Consumer Digital' as Product, CAST(2550.00 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2009-01-09' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'SLR Camera 35mm' as Product, CAST(18530.00 AS money) AS Sales, 34 as Quantity  
    UNION SELECT CAST('2009-01-07' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'SLR Camera' as Product, CAST(26576.00 AS money) AS Sales, 88 as Quantity  
  
    ```  
  
3.  Sulla barra degli strumenti Progettazione query fare clic su **Esegui** (**!**).  
  
     La query viene eseguita e viene visualizzato il set di risultati per il campi SalesDate, Subcategory, Product, Sales e Quantity.  
  
     Nel set di risultati le intestazioni di colonna sono basate sui nomi nella query. Nel set di dati, le intestazioni di colonna diventano i nomi dei campi e vengono salvate nel report. Al termine della procedura guidata, è possibile utilizzare il riquadro dei dati del report per esaminare la raccolta dei campi del set di dati.  
  
4.  Fare clic su **Avanti**.  
  
##  <a name="1c-organize-data-into-groups-in-the-table-wizard"></a><a name="Groups"></a>1C. Organizzare dati in gruppi in Creazione guidata tabella  
 Quando si selezionano dei campi da raggruppare, si progetta una tabella con righe e colonne che visualizzano dati dettagliati e dati aggregati.  
  
#### <a name="to-organize-data-into-groups"></a>Per organizzare i dati in gruppi  
  
1.  Nella pagina **Disponi campi** trascinare Product in **valori**.  
  
2.  Trascinare Quantity in **Valori** e posizionarlo sotto Product.  
  
     Quantity viene aggregata automaticamente dalla funzione Sum, l'aggregazione predefinita per i campi numerici. Il valore è [Sum(Quantity)].  
  
     È possibile aprire l'elenco a discesa per visualizzare le altre funzioni di aggregazione disponibili. Non modificare la funzione di aggregazione.  
  
3.  Trascinare Sales in **Valori** e posizionarlo sotto [Sum(Quantity)].  
  
     Il campo Sales viene aggregato mediante la funzione Sum. Il valore è [Sum(Sales)].  
  
     Nei passaggi 1, 2 e 3 sono specificati i dati da visualizzare nella tabella.  
  
4.  Trascinare SalesDate in **Gruppi di righe**.  
  
5.  Trascinare Subcategory in **Gruppi di righe** e posizionarlo sotto SalesDate.  
  
     I passaggi 4 e 5 consentono di organizzare i valori per i campi prima in base alla data, quindi in base alla sottocategoria del prodotto per quella data.  
  
6.  Fare clic su **Avanti**.  
  
##  <a name="1d-add-subtotal-and-total-rows-in-the-table-wizard"></a><a name="Subtotals"></a>1D. Aggiungere le righe Subtotale e Totale in Creazione guidata tabella  
 Dopo avere creato dei gruppi, è possibile aggiungere e formattare delle righe nelle quali visualizzare valori di aggregazione per i campi. È possibile scegliere se mostrare tutti i dati o lasciare che sia l'utente a espandere e comprimere in modo interattivo i dati raggruppati.  
  
#### <a name="to-add-subtotals-and-totals"></a>Per aggiungere subtotali e totali  
  
1.  Nella pagina **scegliere il layout** , in **Opzioni**, verificare che sia selezionata l'opzione **Mostra subtotali e totali** complessivi.  
  
2.  Verificare che l'opzione **Bloccato, subtotale sotto** sia selezionata.  
  
     Nel riquadro di anteprima della creazione guidata viene visualizzata una tabella con cinque righe. Quando si esegue il report, ogni riga viene visualizzata nel seguente modo:  
  
    1.  La prima riga si ripete una volta per la tabella per mostrare le intestazioni di colonna.  
  
    2.  La seconda riga si ripete una volta per ogni voce nell'ordine di vendita e contiene il nome di prodotto, la quantità dell'ordine e il totale della riga.  
  
    3.  La terza riga si ripete una volta per ogni ordine di vendita per visualizzare i subtotali di ciascun ordine.  
  
    4.  La quarta riga si ripete una volta per ogni data dell'ordine per visualizzare i subtotali di ciascun giorno.  
  
    5.  La quinta riga si ripete una volta per la tabella per visualizzare i totali complessivi.  
  
3.  Deselezionare l'opzione **Espandi/comprimi gruppi**. Nel report creato in questa esercitazione non viene utilizzata la funzionalità drill-down che consente all'utente di espandere una gerarchia di gruppo padre per visualizzare le righe del gruppo figlio e le righe di dettaglio.  
  
4.  Fare clic su **Avanti**.  
  
##  <a name="1e-choose-a-style-in-the-table-wizard"></a><a name="Style"></a>1e. Scegliere uno stile in Creazione guidata tabella  
 Uno stile specifica lo stile del carattere, il set di colori e uno stile del bordo.  
  
#### <a name="to-specify-a-table-style"></a>Per specificare uno stile della tabella  
  
1.  Nella pagina **scegliere uno stile** , nel riquadro Stili, selezionare oceano.  
  
     Nel riquadro di anteprima viene visualizzato un esempio della tabella con lo stile selezionato.  
  
2.  Facoltativamente, fare clic sugli altri stili per vederli applicati all'esempio.  
  
3.  Fare clic su **Fine**.  
  
 La tabella viene aggiunta all'area di progettazione. La tabella dispone di 5 colonne e 5 righe. Nel riquadro Gruppi di righe sono visualizzati tre gruppi di righe: SalesDate, Subcategory e Details. I dati dettaglio costituiscono tutti i dati recuperati dalla query del set di dati.  
  
##  <a name="2-format-data-as-currency"></a><a name="FormatCurrency"></a>2. formattare i dati come valuta  
 Per impostazione predefinita, i dati di riepilogo del campo Sales riportano un numero generico. È possibile formattare tale numero come valuta. Attivare o disattivare **Stili segnaposto** per visualizzare caselle di testo formattate e testo segnaposto come valori di esempio.  
  
#### <a name="to-format-a-currency-field"></a>Per formattare un campo di tipo valuta  
  
1.  Fare clic su **progettazione** per passare alla visualizzazione progettazione.  
  
2.  Fare clic sulla cella nella seconda riga (sotto la riga delle intestazioni di colonna) della colonna Sales e trascinare verso il basso per selezionare tutte le celle che contengono `[Sum(Sales)]`.  
  
3.  Nel gruppo **Numero** della scheda **Home** fare clic sul pulsante **Valuta** . Nelle celle i numeri vengono visualizzati nel formato di valuta.  
  
     Se la lingua delle impostazioni locali è Inglese (Stati Uniti), il testo di esempio predefinito sarà [**$12,345.00**]. Se non viene visualizzato un valore di valuta di esempio, fare clic su **Stili segnaposto** nel gruppo **numeri** , quindi fare clic su **valori di esempio**.  
  
4.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
 I valori di riepilogo per Sales vengono visualizzati come valuta.  
  
##  <a name="3-format-data-as-date"></a><a name="FormatDate"></a>3. formattare i dati come data  
 Per impostazione predefinita, nel campo SalesDate vengono visualizzate sia la data che l'ora. È possibile formattare tale campo in modo da visualizzare solo la data.  
  
#### <a name="to-format-a-date-field-as-the-default-format"></a>Per formattare un campo relativo alla data utilizzando il formato predefinito  
  
1.  Fare clic su **Progettazione** per tornare alla visualizzazione Struttura.  
  
2.  Fare clic sulla cella contenente `[SalesDate]`.  
  
3.  Sulla barra multifunzione, nella scheda **Home** , nel gruppo **numero** , selezionare **Data**nell'elenco a discesa.  
  
     Nella cella viene visualizzata la data di esempio **[1/31/2000]**. Se non viene visualizzata una data di esempio, fare clic su **Stili segnaposto** nel gruppo **Numeri** , quindi fare clic su **Valori di esempio**.  
  
4.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
 I valori SalesDate vengono visualizzati nel formato di data predefinito.  
  
#### <a name="to-change-the-date-format-to-a-custom-format"></a>Per modificare il formato della data in un formato personalizzato  
  
1.  Fare clic su **Progettazione** per tornare alla visualizzazione Struttura.  
  
2.  Fare clic sulla cella contenente `[SalesDate]`.  
  
3.  Nel gruppo **numero** della scheda **Home** fare clic sul pulsante di avvio della finestra di dialogo.  
  
     Il pulsante di avvio è la piccola freccia visualizzata nell'angolo a destra del gruppo. Viene aperta la finestra di dialogo **Proprietà casella di testo** .  
  
4.  Nel riquadro Categoria verificare che sia selezionata l'opzione **Data** .  
  
5.  Nel riquadro **Tipo** selezionare **31 gennaio 2000**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     Nella cella viene visualizzata la data di esempio **[31 gennaio 2000]**.  
  
7.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
 Il valore SalesDate viene visualizzato con il nome anziché il numero del mese.  
  
##  <a name="4-change-column-widths"></a><a name="Width"></a>4. modificare la larghezza delle colonne  
 Per impostazione predefinita, in ogni cella della tabella è contenuta una casella di testo. Una casella di testo si espande verso il basso per adattarsi al testo digitato quando la pagina viene sottoposta al rendering. Nel report visualizzabile, ogni riga si espande fino all'altezza della casella di testo visualizzabile più alta nella riga. L'altezza della riga nell'area di progettazione non ha alcun effetto sull'altezza della riga nel report visualizzabile.  
  
 Per ridurre la quantità di spazio verticale di ciascuna riga, espandere la larghezza della colonna per adattare su un'unica riga il contenuto previsto delle caselle di testo nella colonna.  
  
#### <a name="to-change-the-width-of-table-columns"></a>Per modificare la larghezza delle colonne della tabella  
  
1.  Fare clic su **Progettazione** per tornare alla visualizzazione Struttura.  
  
2.  Fare clic nella tabella in modo che vengano visualizzati gli handle di colonna e riga sopra e accanto alla tabella.  
  
     Le barre grigie lungo la parte superiore e laterale della tabella sono gli handle di riga e di colonna.  
  
3.  Posizionare il puntatore del mouse sulla riga tra gli handle di colonna in modo che il cursore assuma la forma di una doppia freccia. Trascinare le colonne fino a ottenere le dimensioni desiderate. Espandere, ad esempio, la colonna Prodotto in modo da visualizzare il nome di prodotto su una riga.  
  
4.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
##  <a name="5-add-a-report-title"></a><a name="Title"></a>5. aggiungere un titolo al report  
 Nella parte superiore del report viene visualizzato il titolo del report. È possibile posizionare il titolo del report in un'apposita intestazione oppure, se ne è privo, in una casella di testo nella parte superiore del corpo del report. In questa esercitazione sarà utilizzata la casella di testo che viene posizionata automaticamente nella parte superiore del corpo del report.  
  
 Il testo può essere ulteriormente migliorato applicando stili di carattere, dimensioni e colori diversi alle frasi e ai singoli caratteri del testo. Per altre informazioni, vedere [Formattare il testo in una casella di testo &#40;Generatore report e SSRS&#41;](report-design/format-text-in-a-text-box-report-builder-and-ssrs.md).  
  
#### <a name="to-add-a-report-title"></a>Per aggiungere il titolo di un report  
  
1.  Nell'area di progettazione fare clic su **Fare clic per aggiungere il titolo**.  
  
2.  Digitare **Vendite prodotto**, quindi fare clic all'esterno della casella di testo.  
  
3.  Fare clic con il pulsante destro del mouse sulla casella di testo che contiene **Vendite prodotto** , quindi fare clic su **Proprietà casella di testo**.  
  
4.  Nella finestra di dialogo **Proprietà casella di testo** fare clic su **Carattere**.  
  
5.  Nell'elenco **Dimensione** selezionare **18pt**.  
  
6.  Nell'elenco **Colore** selezionare **Blu fiordaliso**.  
  
7.  Selezionare **Grassetto**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="6-save-the-report"></a><a name="Save"></a>6. salvare il report  
 Salvare il report in un server di report o nel computer. Se il report non viene salvato nel server di report, non saranno disponibili alcune funzionalità di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , ad esempio le parti del report e i sottoreport.  
  
#### <a name="to-save-the-report-on-a-report-server"></a>Per salvare il report in un server di report  
  
1.  Fare clic sul pulsante **Generatore report** , quindi su **Salva con nome**.  
  
2.  Fare clic su **Siti e server recenti**.  
  
3.  Selezionare o digitare il nome del server di report per il quale si dispone delle autorizzazioni di salvataggio dei report.  
  
     Verrà visualizzato il messaggio "Connessione al server di report". Al termine della connessione, verrà visualizzato il contenuto della cartella di report specificata dall'amministratore del server di report come posizione predefinita per i report.  
  
4.  In **Nome**sostituire il nome predefinito con **Product Sales**.  
  
5.  Fare clic su **Save**.  
  
 Il report verrà salvato sul server di report. Il nome del server di report al quale si è connessi verrà visualizzato sulla barra di stato nella parte inferiore della finestra.  
  
#### <a name="to-save-the-report-on-your-computer"></a>Per salvare il report nel computer  
  
1.  Fare clic sul pulsante **Generatore report** , quindi su **Salva con nome**.  
  
2.  Fare clic su **Desktop**, **Documenti**o **Risorse del computer**e selezionare la cartella in cui si vuole salvare il report.  
  
3.  In **Nome**sostituire il nome predefinito con **Product Sales**.  
  
4.  Fare clic su **Save**.  
  
##  <a name="7-export-the-report"></a><a name="Export"></a>7. esportare il report  
 I report possono essere esportati in formati differenti quali Microsoft Excel e CSV. Per ulteriori informazioni, vedere [esportazione di report &#40;Generatore report e SSRS&#41;](report-builder/export-reports-report-builder-and-ssrs.md).  
  
 In questa esercitazione, si esporterà il report in Excel e si imposterà una proprietà nel report per fornire un nome personalizzato per la scheda della cartella di lavoro.  
  
#### <a name="to-specify-the-workbook-tab-name"></a>Per specificare il nome della scheda della cartella di lavoro  
  
1.  Fare clic su **Progettazione** per tornare alla visualizzazione Struttura.  
  
2.  Fare clic in un punto qualsiasi all'esterno del report.  
  
3.  . Nel riquadro Proprietà individuare la proprietà InitialPageName e digitare **vendite prodotto Excel**.  
  
    > [!NOTE]  
    >  Se il riquadro proprietà non è visibile, fare clic sulla scheda Visualizza sulla barra multifunzione, quindi fare clic su **Proprietà**.  
  
#### <a name="to-export-a-report-to-excel"></a>Per esportare un report in Excel  
  
1.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
2.  . Sulla barra multifunzione fare clic su **Esporta**, quindi su **Excel**.  
  
     Verrà aperta la finestra di dialogo **Salva con nome**.  
  
3.  Passare alla cartella **documenti** .  
  
4.  Nella casella di testo **nome file** digitare **vendite prodotto Excel**.  
  
5.  Verificare che il tipo di file sia **cartella di lavoro di Excel**.  
  
6.  Fare clic su **Save**.  
  
#### <a name="to-view-the-report-in-excel"></a>Per visualizzare il report in Excel  
  
1.  Aprire la cartella **documenti** e fare doppio clic su **vendite prodotto Excel. xlsx**.  
  
2.  Verificare che il nome della scheda della cartella di lavoro sia **Vendite prodotto Excel**.  
  
## <a name="next-steps"></a>Passaggi successivi  
 La procedura dettagliata per la creazione di un report tabella semplice è terminata. Per altre informazioni sulle tabelle, vedere [Tabelle, matrici ed elenchi &#40;Generatore report e SSRS&#41;](report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Esercitazioni &#40;Generatore report&#41;](report-builder-tutorials.md)   
 [Generatore report in SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)  
  
  
