---
title: 'Esercitazione: Aggiunta di un grafico sparkline al report (Generatore report) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 18c90a36-48bf-4805-a960-2d1e8f00c2dc
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a543182d5c367be9cc1be875f05c1ab5d4c9bfcf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66099036"
---
# <a name="tutorial-add-a-sparkline-to-your-report-report-builder"></a>Esercitazione: Aggiungere un grafico sparkline al report (Generatore report)
  In questa esercitazione si creerà un report tabella semplice basato su dati di vendita di esempio, quindi si aggiungerà un grafico sparkline a una cella della tabella.  
  
 Una versione avanzata del report che verrà creato in questa esercitazione è disponibile come report di esempio di Generatore report di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Per ulteriori informazioni sul download di questo report di esempio e di altri, vedere [Generatore report report di esempio](https://go.microsoft.com/fwlink/?LinkId=184851). Nell'immagine seguente viene illustrato il report di esempio simile a quello che verrà creato.  
  
 ![rs_SparklineMatrixTutorial](../../2014/tutorials/media/rs-sparklinematrixtutorial.gif "rs_SparklineMatrixTutorial")  
  
 Il video [procedura: creare un sparkline in una tabella (video Generatore report)](https://technet.microsoft.com/bi/ff871942.aspx) illustra come creare un report simile con i grafici sparkline.  
  
##  <a name="BackToTop"></a>Cosa si apprenderà  
 In questa esercitazione si apprenderà come eseguire le operazioni seguenti:  
  
 1. [Creare un report con una tabella](#CreateTable)  
  
 2. [Creare una query in Creazione guidata tabella o matrice](#Query)  
  
 3. [Aggiungere un grafico sparkline alla tabella](#Sparkline)  
  
 4. [Allineare i grafici sparkline verticalmente e orizzontalmente](#AlignSparklines)  
  
### <a name="other-optional-steps"></a>Altri passaggi facoltativi  
 5. [Formattare i dati come valuta](#FormatCurrency)  
  
 6. [Formattare i dati come date](#FormatDates)  
  
 7. [Modificare la larghezza delle colonne](#Width)  
  
 8. [Aggiungere un titolo al report](#Title)  
  
 9. [Salva il report](#Save)  
  
 Tempo previsto per il completamento di questa esercitazione: 30 minuti.  
  
## <a name="requirements"></a>Requisiti  
 Per altre informazioni sui requisiti, vedere [Prerequisiti per le esercitazioni &#40;Generatore report&#41;](../reporting-services/report-builder-tutorials.md).  
  
##  <a name="CreateTable"></a>1. creare un report con una tabella  
  
#### <a name="to-create-a-report"></a>Per creare un report  
  
1.  Fare clic sul menu **Start**, scegliere **Programmi**, **Generatore report per Microsoft SQL Server 2012**e quindi fare clic su **Generatore report**.  
  
     Verrà visualizzata la finestra di dialogo **Introduzione** .  
  
    > [!NOTE]  
    >  Se la finestra di dialogo **Introduzione** non viene visualizzata, dal pulsante **Generatore report** fare clic su **nuovo**.  
  
2.  Nel riquadro sinistro verificare che sia selezionata l'opzione **Nuovo report** .  
  
3.  Nel riquadro destro fare clic su **Creazione guidata tabella o matrice**.  
  
4.  Nella pagina **Scegliere un set di dati** selezionare **Crea un set di dati**, quindi fare clic su **Avanti**. Verrà visualizzata la pagina **Scegliere una connessione a un'origine dei dati** .  
  
    > [!NOTE]  
    >  Per questa esercitazione non sono necessari dati specifici. È sufficiente una connessione a un database di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] . Se in **Connessioni a origini dati**è già disponibile una connessione all'origine dati, sarà possibile selezionarla e andare al passaggio 10. Per altre informazioni, vedere [Modalità alternative di acquisizione di una connessione dati &#40;Generatore report&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
5.  Fare clic su **Nuovo**. Verrà visualizzata la finestra di dialogo **Proprietà origine dati** .  
  
6.  In **Nome**digitare **Vendite prodotto**come nome per l'origine dati.  
  
7.  In **Select a connection type**(Seleziona un tipo di connessione), verificare che sia selezionato **Microsoft SQL Server** .  
  
8.  In **Stringa di connessione**digitare il testo seguente:  
  
     **Origine dati =\<nomeserver>**  
  
     L'espressione \<ServerName>, ad esempio Report001, specifica un computer in cui è installata un'istanza del SQL Server motore di database. Poiché i dati del report non vengono estratti da un database di SQL Server, non è necessario includere il nome di un database. Per analizzare la query viene utilizzato il database predefinito nel server specificato.  
  
9. Fare clic su **Credenziali**. Immettere le credenziali necessarie per accedere all'origine dati esterna.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     Verrà visualizzata di nuovo la pagina **Scegliere una connessione a un'origine dei dati** .  
  
11. Per verificare che la connessione all'origine dati avvenga correttamente, fare clic su **Test connessione**.  
  
     Verrà visualizzato il messaggio "Creazione connessione completata".  
  
12. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
13. Fare clic su **Avanti**.  
  
##  <a name="Query"></a>2. creare una query in creazione guidata tabella  
 In un report, è possibile utilizzare un set di dati condiviso che dispone di una query predefinita oppure è possibile creare un set di dati incorporato da utilizzare solo nel report. In questa esercitazione si creerà un set di dati incorporato.  
  
> [!NOTE]  
>  Nella query di questa esercitazione sono contenuti i valori dei dati in modo che non sia necessaria un'origine dati esterna. Tale condizione rende tuttavia la query piuttosto lunga. In una query di un ambiente aziendale non sarebbe incluso alcun dato. Questo esempio è solo a scopo illustrativo.  
  
#### <a name="to-create-a-query"></a>Per creare una query  
  
1.  Nella pagina **Progetta query** viene aperta la finestra Progettazione query relazionale. Per questa esercitazione si utilizzerà la finestra Progettazione query basata su testo.  
  
2.  Fare clic su **Modifica come testo**. Nella finestra Progettazione query basata su testo viene visualizzato il riquadro della query e il riquadro dei risultati.  
  
3.  Nella casella [!INCLUDE[tsql](../includes/tsql-md.md)] Query **incollare la query** seguente.  
  
    ```  
    SELECT CAST('2010-01-04' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2010-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Carrying Case' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2010-01-10' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Carrying Case' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2010-01-04' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Budget Movie-Maker' as Product, CAST(1056.00 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2010-01-05' AS date) as SalesDate,  'Accessories' as Subcategory,  
       'Slim Digital' as Product, CAST(1380.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2010-01-05' AS date) as SalesDate,'Accessories' as Subcategory,    
       'Budget Movie-Maker' as Product, CAST(780.00 AS money) AS Sales, 26 as Quantity  
    UNION SELECT CAST('2010-01-07' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3798.00 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2010-01-08' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(10400.00 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2010-01-09' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3000.00 AS money) AS Sales, 60 as Quantity  
    UNION SELECT CAST('2010-01-10' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(7234.50 AS money) AS Sales, 39 as Quantity  
    UNION SELECT CAST('2010-01-06' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Carrying Case' as Product, CAST(10836.00 AS money) AS Sales, 84 as Quantity  
    UNION SELECT CAST('2010-01-07' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(2550.00 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2010-01-04' AS date) as SalesDate, 'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2010-01-08' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'Slim Digital' as Product, CAST(18530.00 AS money) AS Sales, 34 as Quantity  
    UNION SELECT CAST('2010-01-06' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'Slim Digital' as Product, CAST(26576.00 AS money) AS Sales, 88 as Quantity  
    ```  
  
4.  Sulla barra degli strumenti Progettazione query fare clic su Esegui (**!**).  
  
     Viene eseguita la query e viene visualizzato il set di risultati per i campi **SalesDate**, **SubCategory**, **Product**, **Sales**e **Quantity**.  
  
5.  Fare clic su **Avanti**.  
  
6.  Nella pagina **Disponi campi** trascinare **Sales** in **Valori**.  
  
     Le **vendite** vengono aggregate dalla funzione Sum. Il valore è [Sum(Sales)].  
  
7.  Trascinare **Product** in **Gruppi di righe**.  
  
8.  Trascinare **SalesDate** in **Gruppi di colonne**.  
  
9. Fare clic su **Avanti**.  
  
10. Nella pagina **Scegliere il layout** , sotto **Opzioni**, verificare che la casella **Mostra subtotali e totali complessivi** sia selezionata.  
  
     Nel riquadro di anteprima della creazione guidata verrà visualizzata una tabella con tre righe. Quando si esegue il report, ogni riga viene visualizzata nel seguente modo:  
  
    1.  La prima riga verrà visualizzata una sola volta per la tabella per mostrare le intestazioni di colonna.  
  
    2.  La seconda riga verrà ripetuta una volta per ogni prodotto e conterrà il nome del prodotto, il totale per giorno e il totale della riga.  
  
    3.  La terza riga verrà visualizzata una sola volta per la tabella per visualizzare i totali complessivi.  
  
11. Fare clic su **Avanti**.  
  
12. Nel riquadro **Stili** della pagina **Scegliere uno stile** selezionare **Ardesia**.  
  
     Nel riquadro di anteprima viene visualizzato un esempio della tabella con lo stile selezionato.  
  
13. Fare clic su **Fine**.  
  
14. La tabella viene aggiunta all'area di progettazione. Nella tabella sono presenti tre colonne e altrettante righe.  
  
     Osservare il riquadro di raggruppamento. Se il riquadro Raggruppamento non è visualizzato, scegliere **Raggruppamento** dal menu **Visualizza**. Nel riquadro Gruppi di righe viene visualizzato un gruppo di righe, ovvero **Product**. Nel riquadro Gruppi di colonne viene visualizzato un gruppo di colonne, ovvero **SalesDate**. I dati dettaglio costituiscono tutti i dati recuperati dalla query del set di dati.  
  
15. Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
##  <a name="Sparkline"></a>3. aggiungere un sparkline  
  
#### <a name="to-add-a-sparkline-chart-to-a-table"></a>Per aggiungere un grafico sparkline a una tabella  
  
1.  Fare clic su **Progettazione** per tornare alla visualizzazione Struttura.  
  
2.  Selezionare la colonna Total nella tabella.  
  
3.  Fare clic con il pulsante destro del mouse, scegliere **Inserisci colonna**e fare clic su **A sinistra**.  
  
4.  Nella nuova colonna, fare clic con il pulsante destro del mouse sulla riga [Product], scegliere la scheda **Inserisci** barra multifunzione e quindi fare clic su **sparkline**.  
  
5.  Verificare che sia selezionato il primo sparkline nella riga della **colonna** e quindi fare clic su **OK**.  
  
6.  Fare clic sul grafico sparkline per visualizzare il riquadro Dati grafico.  
  
7.  Fare clic sul segno più (+) nella casella valori, quindi fare clic su **vendite**.  
  
     I valori nel campo **Sales** corrispondono ora ai valori per il grafico sparkline.  
  
8.  Fare clic sul segno più (+) nella casella gruppi di categorie e quindi fare clic su **SalesDate**.  
  
9. Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
     Si noti che sono presenti grafici sparkline in ogni riga della tabella, che tuttavia non sono corretti. Le barre nei grafici non sono allineate l'una all'altra. Nella seconda riga di dati sono presenti solo quattro barre; pertanto le barre risultano più ampie di quelle nella prima riga, che ne contiene sei. Non è possibile confrontare i valori di ogni prodotto per giorno. È necessario che le barre siano allineate.  
  
     Per ogni riga si noti inoltre che la barra più alta per la riga specifica corrisponde all'altezza della riga stessa. Anche questo è fuorviante perché i valori più grandi per ogni riga non sono uguali: il valore più grande per il produttore del budget è $10.400, ma il valore più grande per Slim Digital è $26.576-più del doppio delle dimensioni. Inoltre, le barre più grandi in quelle due righe hanno all'incirca la stessa altezza. L'altezza deve inoltre essere ridimensionata conformemente agli altri grafici sparkline.  
  
     ![rs_SprklineMtrxUnaligndBars](../../2014/tutorials/media/rs-sprklinemtrxunaligndbars.gif "rs_SprklineMtrxUnaligndBars")  
  
##  <a name="AlignSparklines"></a>4. allineare i grafici sparkline verticalmente e orizzontalmente  
 I grafici sparkline sono difficili da leggere quando non utilizzano tutte le stesse misurazioni. È necessario che vi sia corrispondenza tra gli assi orizzontale e verticale di ognuno.  
  
#### <a name="to-set-alignment-for-the-sparklines-in-the-table"></a>Per impostare l'allineamento per i grafici sparkline nella tabella  
  
1.  Fare clic su **Progettazione** per tornare alla visualizzazione Struttura.  
  
2.  Fare clic con il pulsante destro del mouse sul grafico sparkline e scegliere **Proprietà asse verticale**.  
  
3.  Selezionare la casella di controllo **Allinea assi in** .  
  
     Nell'elenco viene visualizzato Tablix1. Questa è l'unica opzione e consente di impostare l'altezza delle barre in ogni grafico sparkline rispetto alle altre.  
  
4.  Fare clic su **OK**.  
  
5.  Fare clic con il pulsante destro del mouse sul grafico sparkline e scegliere **Proprietà asse orizzontatale**.  
  
6.  Selezionare la casella di controllo **Allinea assi in** .  
  
     Nell'elenco viene visualizzato Tablix1. Questa è l'unica opzione e consente di impostare la larghezza delle barre in ogni grafico sparkline rispetto alle altre. Se sono presenti grafici sparkline con un numero inferiore di barre, in tali grafici saranno contenuti spazi vuoti per i dati mancanti.  
  
7.  Fare clic su **OK**.  
  
8.  Fare clic su **Esegui** per visualizzare l'anteprima del nuovo report.  
  
 Si noti che tutte le barre risultano ora allineate con le barre nelle altre righe.  
  
##  <a name="FormatCurrency"></a>5. (facoltativo) formattare i dati come valuta  
 Per impostazione predefinita, i dati di riepilogo per il campo **Sales** riportano un numero generico. È possibile formattare tale numero come valuta. Attivare o disattivare **Stili segnaposto** per visualizzare caselle di testo formattate e testo segnaposto come valori di esempio.  
  
#### <a name="to-format-a-currency-field"></a>Per formattare un campo di tipo valuta  
  
1.  Fare clic su **progettazione** per passare alla visualizzazione progettazione.  
  
2.  Fare clic sulla cella nella seconda riga (sotto la riga delle intestazioni di colonna) nella colonna **SalesDate** e trascinare per selezionare tutte le celle che `[Sum(Sales)]`contengono.  
  
3.  Nel gruppo **Numero** della scheda **Home** fare clic sul pulsante **Valuta** . Nelle celle i numeri vengono visualizzati nel formato di valuta.  
  
     Se la lingua delle impostazioni locali è Inglese (Stati Uniti), il testo di esempio predefinito sarà [**$12,345.00**]. Se non viene visualizzato un valore di valuta di esempio, fare clic su **Stili segnaposto** nel gruppo **numeri** , quindi fare clic su **valori di esempio**.  
  
4.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
 I valori di riepilogo per **Sales** vengono visualizzati come valuta.  
  
##  <a name="FormatDates"></a>6. (facoltativo) formattare i dati come date  
 Per impostazione predefinita, il campo **SalesDate** Visualizza le informazioni su data e ora. È possibile formattare tale campo in modo da visualizzare solo la data.  
  
#### <a name="to-format-a-date-field-as-the-default-format"></a>Per formattare un campo relativo alla data utilizzando il formato predefinito  
  
1.  Fare clic su **Progettazione** per tornare alla visualizzazione Struttura.  
  
2.  Fare clic sulla cella contenente `[SalesDate]`.  
  
3.  Sulla barra multifunzione, nella scheda **Home** , nel gruppo **numero** , selezionare **Data**nell'elenco a discesa.  
  
     Nella cella verrà visualizzata la data di esempio **[1/31/2000]**. Se non viene visualizzata una data di esempio, fare clic su **Stili segnaposto** nel gruppo **Numeri** , quindi fare clic su **Valori di esempio**.  
  
4.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
 I valori **SalesDate** vengono visualizzati nel formato di data predefinito.  
  
##  <a name="Width"></a>7. (facoltativo) modificare la larghezza delle colonne  
 Per impostazione predefinita, in ogni cella della tabella è contenuta una casella di testo. Una casella di testo si espande verso il basso per adattarsi al testo digitato quando la pagina viene sottoposta al rendering. Nel report visualizzabile, ogni riga si espande fino all'altezza della casella di testo visualizzabile più alta nella riga. L'altezza della riga nell'area di progettazione non ha alcun effetto sull'altezza della riga nel report visualizzabile.  
  
 Per ridurre la quantità di spazio verticale di ciascuna riga, espandere la larghezza della colonna per adattare su un'unica riga il contenuto previsto delle caselle di testo nella colonna.  
  
#### <a name="to-change-the-width-of-columns"></a>Per modificare la larghezza delle colonne  
  
1.  Fare clic su **Progettazione** per tornare alla visualizzazione Struttura.  
  
2.  Fare clic nella tabella in modo che vengano visualizzati gli handle di colonna e riga sopra e accanto alla tabella.  
  
     Le barre grigie lungo la parte superiore e laterale della tabella sono gli handle di riga e di colonna.  
  
3.  Posizionare il puntatore del mouse sulla riga tra gli handle di colonna in modo che il cursore assuma la forma di una doppia freccia. Trascinare le colonne fino a ottenere le dimensioni desiderate. Espandere, ad esempio, la colonna **Product** in modo da visualizzare il nome del prodotto su una riga.  
  
4.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
##  <a name="Title"></a>8. (facoltativo) aggiungere un titolo al report  
 Nella parte superiore del report viene visualizzato il titolo del report. È possibile posizionare il titolo del report in un'apposita intestazione oppure, se ne è privo, in una casella di testo nella parte superiore del corpo del report. In questa esercitazione sarà utilizzata la casella di testo che viene posizionata automaticamente nella parte superiore del corpo del report.  
  
 Il testo può essere ulteriormente migliorato applicando stili di carattere, dimensioni e colori diversi alle frasi e ai singoli caratteri del testo. Per altre informazioni, vedere [Formattare il testo in una casella di testo &#40;Generatore report e SSRS&#41;](report-design/format-text-in-a-text-box-report-builder-and-ssrs.md).  
  
#### <a name="to-add-a-report-title"></a>Per aggiungere il titolo di un report  
  
1.  Nell'area di progettazione fare clic su **Fare clic per aggiungere il titolo**.  
  
2.  Digitare **Vendite prodotto**, quindi fare clic all'esterno della casella di testo.  
  
3.  Fare clic con il pulsante destro del mouse sulla casella di testo che contiene **Vendite prodotto** , quindi fare clic su **Proprietà casella di testo**.  
  
4.  Nella finestra di dialogo **Proprietà casella di testo** fare clic su **Carattere**.  
  
5.  Nell'elenco **Dimensione** selezionare **18pt**.  
  
6.  Nell'elenco **colore** selezionare **Bordeaux**.  
  
7.  Selezionare **Grassetto**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="Save"></a>9. salvare il report  
 Salvare il report in un server di report o nel computer. Se il report non viene salvato nel server di report, non saranno disponibili alcune funzionalità di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , ad esempio le parti del report e i sottoreport.  
  
#### <a name="to-save-the-report-on-a-report-server"></a>Per salvare il report in un server di report  
  
1.  Dal pulsante **Generatore report** fare clic su **Salva con nome**.  
  
2.  Fare clic su **Siti e server recenti**.  
  
3.  Selezionare o digitare il nome del server di report per il quale si dispone delle autorizzazioni di salvataggio dei report.  
  
     Verrà visualizzato il messaggio "Connessione al server di report". Al termine della connessione, verrà visualizzato il contenuto della cartella di report specificata dall'amministratore del server di report come posizione predefinita per i report.  
  
4.  In **Nome**sostituire il nome predefinito con **Product Sales**.  
  
5.  Fare clic su **Salva**.  
  
 Il report verrà salvato sul server di report. Il nome del server di report al quale si è connessi verrà visualizzato sulla barra di stato nella parte inferiore della finestra.  
  
#### <a name="to-save-the-report-on-your-computer"></a>Per salvare il report nel computer  
  
1.  Dal pulsante **Generatore report** fare clic su **Salva con nome**.  
  
2.  Fare clic su **Desktop**, **Documenti**o **Risorse del computer**e selezionare la cartella in cui si vuole salvare il report.  
  
3.  In **Nome**sostituire il nome predefinito con **Product Sales**.  
  
4.  Fare clic su **Salva**.  
  
## <a name="next-steps"></a>Passaggi successivi  
 L'esercitazione sulla creazione di un report tabella con grafici sparkline è terminata. Per altre informazioni, vedere [Grafici sparkline e barre dei dati &#40;Generatore report e SSRS&#41;](report-design/sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Esercitazioni &#40;Generatore report&#41;](report-builder-tutorials.md)   
 [Generatore report in SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)  
  
  
