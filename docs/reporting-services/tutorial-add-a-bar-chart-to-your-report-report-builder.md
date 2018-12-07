---
title: 'Esercitazione: Aggiungere un grafico a barre al report (Generatore report) | Microsoft Docs'
ms.date: 06/15/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 6956ebd6-0217-4087-a4fa-5cc1c3804691
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8e6855a7a6a47021a635e12b2c53515ed20aa6f4
ms.sourcegitcommit: c7febcaff4a51a899bc775a86e764ac60aab22eb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/30/2018
ms.locfileid: "52712442"
---
# <a name="tutorial-add-a-bar-chart-to-your-report-report-builder"></a>Esercitazione: Aggiungere un grafico a barre al report (Generatore report)
In questa esercitazione viene usata una procedura guidata di [!INCLUDE[ssRBnoversion_md](../includes/ssrbnoversion.md)] per creare un grafico a barre in un report impaginato di [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] . Successivamente si aggiungerà un filtro e si migliorerà il grafico. 

In un grafico a barre i dati delle categorie vengono visualizzati orizzontalmente per gli scopi seguenti:  
  
-   Migliorare la leggibilità dei nomi di categoria lunghi.  
-   Migliorare la comprensibilità delle ore tracciate come valori.   
-   Confrontare il valore relativo di più serie.  
  
L'illustrazione seguente visualizza il grafico a barre che verrà creato con le attività di vendita del 2014 e del 2015 relative ai primi cinque venditori, ordinate dal valore più alto al valore più basso delle vendite del 2015.  
  
![report-generatore-barra-grafico](../reporting-services/media/report-builder-bar-chart.png) 
  
 
> [!NOTE]  
> In questa esercitazione, i passaggi per la procedura guidata sono consolidati in un'unica procedura. Per istruzioni dettagliate su come selezionare un server di report, creare un set di dati e scegliere un'origine dati, vedere la prima esercitazione di questa serie: [Esercitazione: Creazione di un report di tabelle semplici &#40;Generatore report&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
Tempo previsto per il completamento di questa esercitazione: 15 minuti.  
  
## <a name="requirements"></a>Requisiti  
Per altre informazioni sui requisiti, vedere [Prerequisiti per le esercitazioni &#40;Generatore report&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="Chart"></a>1. Creare un report grafico da Creazione guidata grafico  
Nella quale si crea un set di dati incorporato, si sceglie un'origine dati condivisa e si crea un grafico a barre tramite la Creazione guidata grafico.  
  
> [!NOTE]  
> Nella query di questa esercitazione sono contenuti i valori dei dati in modo che non sia necessaria un'origine dati esterna. Tale condizione rende tuttavia la query piuttosto lunga. In una query di un ambiente aziendale non sarebbe incluso alcun dato. Questo esempio è solo a scopo illustrativo.  
  
1.  [Avviare Generatore report](../reporting-services/report-builder/start-report-builder.md) dal portale Web di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , dal server di report in modalità integrata SharePoint oppure dal computer.  
  
     Verrà visualizzata la finestra di dialogo **Riquadro attività iniziale** .  
  
     ![Attività iniziale Generatore report](../reporting-services/media/rb-getstarted.png "Attività iniziale Generatore report")  
  
     Se non viene visualizzata la finestra di dialogo **Riquadro attività iniziale** , fare clic su **File** >**Nuovo**. La finestra di dialogo **Nuovo report o set di dati** include all'incirca lo stesso contenuto della finestra di dialogo **Riquadro attività iniziale** . 
      
2.  Nel riquadro sinistro verificare che sia selezionata l'opzione **Nuovo report** .  
  
3.  Nel riquadro di destra fare clic su **Creazione guidata grafico**.  
  
4.  Nella pagina **Scegliere un set di dati** fare clic su **Crea un set di dati**e fare clic su **Avanti**.  
  
5.  Nella pagina **Scegliere una connessione a un'origine dati** selezionare un'origine dati esistente o individuare il server di report, quindi selezionare un'origine dati e fare clic su **Avanti**. Potrebbe essere necessario immettere un nome utente e una password.  
  
    > [!NOTE]  
    > L'origine dati scelta non ha importanza purché si disponga delle autorizzazioni appropriate. Non verranno recuperati dati dall'origine dati. Per altre informazioni, vedere [Modalità alternative di acquisizione di una connessione dati &#40;Generatore report&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
6.  Nella pagina **Progetta query** fare clic su **Modifica come testo**.  
  
7.  Incollare la query seguente nel relativo riquadro:  
  
    ```  
    SELECT 'Luis' as FirstName, 'Alverca' as LastName, CAST(170000.00 AS money) AS SalesYear2015, CAST(150000. AS money) AS SalesYear2014  
    UNION SELECT 'Jeffrey' as FirstName, 'Zeng' as LastName, CAST(210000. AS money) AS SalesYear2015, CAST(190000. AS money) AS SalesYear2014  
    UNION SELECT 'Houman' as FirstName, 'Pournasseh' as LastName, CAST(150000. AS money) AS SalesYear2015, CAST(180000. AS money) AS SalesYear2014  
    UNION SELECT 'Robin' as FirstName, 'Wood' as LastName, CAST(75000. AS money) AS SalesYear2015, CAST(175000. AS money) AS SalesYear2014  
    UNION SELECT 'Daniela' as FirstName, 'Guaita' as LastName,  CAST(170000. AS money) AS SalesYear2015, CAST(175000. AS money) AS SalesYear2014  
    UNION SELECT 'John' as FirstName, 'Yokim' as LastName, CAST(160000. AS money) AS SalesYear2015, CAST(195000. AS money) AS SalesYear2014  
    UNION SELECT 'Delphine' as FirstName, 'Ribaute' as LastName, CAST(180000. AS money) AS SalesYear2015, CAST(205000. AS money) AS SalesYear2014  
    UNION SELECT 'Robert' as FirstName, 'Hernady' as LastName, CAST(140000. AS money) AS SalesYear2015, CAST(180000. AS money) AS SalesYear2014  
    UNION SELECT 'Tanja' as FirstName, 'Plate' as LastName, CAST(150000. AS money) AS SalesYear2015, CAST(160000. AS money) AS SalesYear2014  
    UNION SELECT 'David' as FirstName, 'Bradley' as LastName, CAST(210000. AS money) AS SalesYear2015, CAST(180000. AS money) AS SalesYear2014  
    UNION SELECT 'Michal' as FirstName, 'Jaworski' as LastName, CAST(175000. AS money) AS SalesYear2015, CAST(220000. AS money) AS SalesYear2014  
    UNION SELECT 'Chris' as FirstName, 'Ashton' as LastName, CAST(195000. AS money) AS SalesYear2015, CAST(205000. AS money) AS SalesYear2014  
    UNION SELECT 'Pongsiri' as FirstName, 'Hirunyanitiwatna' as LastName, CAST(175000. AS money) AS SalesYear2015, CAST(215000. AS money) AS SalesYear2014  
    UNION SELECT 'Brian' as FirstName, 'Burke' as LastName, CAST(187000. AS money) AS SalesYear2015, CAST(207000. AS money) AS SalesYear2014  
    ```  
  
8.  (Facoltativo) Fare clic sul pulsante Esegui (**!**) per visualizzare i dati sui quali verrà basato il grafico.  
  
9. Scegliere **Avanti**.  
  
## <a name="ChartType"></a>2. Creare un grafico a barre  
 
1.  L'istogramma è il tipo di grafico predefinito nella pagina **Scegliere un tipo di grafico** .  
  
2.  Fare clic su **Barre**, quindi su **Avanti**.  
  
    Nella pagina **Disponi campi del grafico** il riquadro **Campi disponibili** include quattro campi: FirstName, LastName, SalesYear2015 e SalesYear2014.  
  
3.  Trascinare LastName nel riquadro Categorie.  
  
4.  Trascinare SalesYear2015 nel riquadro Valori. SalesYear2015 rappresenta l'importo totale delle vendite di ogni venditore per l'anno 2015. Nel riquadro Valori viene visualizzato `[Sum(SalesYear2015)]` perché nel grafico viene mostrata l'aggregazione per ogni prodotto.  
  
5.  Trascinare SalesYear2014 nel riquadro Valori sotto SalesYear2015. SalesYear2014 rappresenta l'importo totale delle vendite di ogni venditore per l'anno 2014.  
  
6.  Scegliere **Avanti**.  
  
7.  Fare clic su **Fine**.  
  
    Il grafico verrà aggiunto all'area di progettazione. Si noti che il nuovo grafico a barre include solo dati rappresentativi. La legenda include Cognome A, Cognome B, ecc. e non il nome reale delle persone, solo per dare un'idea dell'aspetto del report. 
  
9. Fare clic sul grafico per visualizzarne gli handle. Trascinare l'angolo inferiore destro del grafico per ingrandirlo. L'area di progettazione viene ingrandita man mano che viene trascinata. 
  
10. Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
Il grafico a barre visualizza le vendite di ogni venditore per il 2014 e 2015. La lunghezza della barra corrisponde al totale delle vendite.  
  
## <a name="AllValues"></a>3. Visualizzare tutti i nomi sull'asse verticale  
Per impostazione predefinita sull'asse verticale vengono visualizzati solo alcuni valori. È possibile modificare il grafico per visualizzare tutte le categorie.  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Fare clic con il pulsante destro del mouse sull'asse verticale, quindi scegliere **Proprietà asse verticale**.  
  
3.  Nella casella **Intervallo**di **Intervallo asse** digitare **1**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
> [!NOTE]  
> Se i nomi dei venditori sull'asse verticale non sono leggibili, è possibile aumentare l'altezza del grafico o modificare le opzioni di formattazione per le etichette dell'asse.  
  
### <a name="CategoryExpression"></a>Visualizzare cognome e nome sull'asse verticale  
È possibile modificare l'espressione delle categorie per includere il cognome seguito dal nome di ogni venditore.  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Fare doppio clic sul grafico per visualizzare il riquadro **Dati grafico** .  
  
3.  Nell'area **Gruppi di categorie** fare clic con il pulsante destro del mouse sul campo [LastName] e scegliere **Proprietà gruppo categorie**.  
  
4.  In Etichetta fare clic sul pulsante espressione (Fx).  
  
5.  Digitare l'espressione seguente: `=Fields!LastName.Value & ", " & Fields!FirstName.Value`  
  
    Questa espressione determina la concatenazione di cognome, virgola e nome.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
Se i nomi non vengono visualizzati quando si esegue il report, è possibile aggiornare i dati manualmente. Mentre si è ancora in modalità anteprima, fare clic su **Aggiorna** nel gruppo **Navigazione** della scheda **Esegui**.  
  
> [!NOTE]  
> Se i nomi dei venditori sull'asse verticale non sono leggibili, è possibile aumentare l'altezza del grafico o modificare le opzioni di formattazione per le etichette dell'asse.  
  
## <a name="Sort"></a>4. Modificare l'ordinamento sull'asse verticale  
Quando si ordinano i dati in un grafico si modifica l'ordine dei valori sull'asse delle categorie.  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Fare doppio clic sul grafico per visualizzare il riquadro **Dati grafico** .  
  
3.  Nell'area **Gruppi di categorie** fare clic con il pulsante destro del mouse sul campo [LastName] e scegliere **Proprietà gruppo categorie**.  
  
4.  Fare clic su **Ordinamento**. Nella pagina **Modificare le opzioni di ordinamento** viene visualizzato un elenco di espressioni di ordinamento. Per impostazione predefinita, l'elenco dispone di un'unica espressione di ordinamento che equivale all'espressione originale di raggruppamento delle categorie.  
  
5.  In **Ordinamento**, fare clic su **[SalesYear2015]**.  
  
6.  Nell'elenco **Ordine** , selezionare **Dalla A alla Z** in modo che i nomi siano visualizzati in ordine a partire dalle vendite più alte alle più basse del 2015.
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
I nomi sull'asse orizzontale vengono ordinati a partire dalle vendite più alte alle più basse del 2015, con **Zeng** nella parte superiore.  
  
## <a name="Legend"></a>5. Spostare la legenda  
Per migliorare la leggibilità dei valori del grafico, è possibile spostare la legenda del grafico. In un grafico a barre in cui le barre sono visualizzate orizzontalmente, è ad esempio possibile modificare la posizione della legenda in modo che si trovi al di sopra o al di sotto dell'area del grafico. In questo modo lo spazio orizzontale disponibile per le barre risulterà maggiore.  
  
#### <a name="to-display-the-legend-below-the-chart-area-of-a-bar-chart"></a>Per visualizzare la legenda al di sotto dell'area del grafico di un grafico a barre  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Fare clic con il pulsante destro del mouse sulla legenda nel grafico.  
  
3.  Selezionare **Proprietà legenda**.  
  
4.  In **Posizione legenda**selezionare un'altra posizione, ad esempio la posizione centrale inferiore.  
  
    Quando la legenda viene posizionata alla fine o all'inizio di un grafico, il relativo layout viene modificato da verticale in orizzontale. È possibile selezionare un altro layout nell'elenco a discesa **Layout** .  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
## <a name="ChartTitle"></a>6. Spostare il titolo del grafico  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Selezionare le parole **Titolo grafico** nella parte superiore del grafico, quindi digitare il testo seguente: **Vendite del 2014 e 2015**.  
  
3.  Quando il titolo è selezionato, modificare **Colore** in **Nero** e **Carattere** in **12pt**nel riquadro Proprietà. 
  
4.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
## <a name="Horizontal"></a>7. Formattare l'asse orizzontale e assegnare un'etichetta  
Per impostazione predefinita, sull'asse orizzontale vengono visualizzati valori in un formato generale che viene ridimensionato automaticamente in base alle dimensioni del grafico. È possibile modificarlo nel formato di valuta.  
   
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Fare clic sull'asse orizzontale lungo il bordo inferiore del grafico per selezionarlo.  
  
3.  Nella scheda **Home** > gruppo **Numero** > **Valuta**. Le etichette dell'asse orizzontale vengono convertite nel formato valuta.  
  
3.  (Facoltativo) Rimuovere le cifre decimali. Fare clic due volte sul pulsante **Diminuisci decimali** accanto al pulsante **Valuta** .  
  
4.  Fare clic con il pulsante destro del mouse sull'asse orizzontale e scegliere **Proprietà asse orizzontale**.  
  
5.  Nella scheda **Numero** selezionare **Mostra valori in Migliaia**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  

8.  Fare clic con il pulsante destro del mouse sull'asse orizzontale e scegliere **Mostra titolo asse**.
  
7.  Nella casella **Titolo asse** digitare **Vendite in migliaia** e premere INVIO.  

    >**Nota:** mentre si digita, la casella Titolo dell'asse viene visualizzata sull'asse verticale. Ma quando si preme INVIO, passa all'asse orizzontale.
  
9. Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
Il report visualizza l'importo delle vendite sull'asse orizzontale come valuta in migliaia senza cifre decimali.  
  
## <a name="Filter"></a>8. Aggiungere un filtro per visualizzare i primi cinque valori  
È possibile aggiungere un filtro al grafico per specificare quali dati del set di dati includere o escludere.   
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Fare doppio clic sul grafico per visualizzare il riquadro **Dati grafico** .  
  
3.  Nell'area **Gruppi di categorie** fare clic con il pulsante destro del mouse sul campo [LastName] e scegliere **Proprietà gruppo categorie**.  
  
4.  Fare clic su **Filtri**. Nella pagina **Modificare i filtri** può essere visualizzato un elenco di espressioni di filtro. Per impostazione predefinita, tale elenco è vuoto.  
  
5.  Scegliere **Aggiungi**. Verrà visualizzato un nuovo filtro vuoto.  
  
6.  In **Espressione**digitare **[Sum(SalesYear2015)]**. Viene creata l'espressione sottostante `=Sum(Fields!SalesYear2015.Value)`, che può essere visualizzata facendo clic sul pulsante **fx** .  
  
7.  Verificare che il tipo di dati sia **Text**.  
  
8.  In **Operatore**selezionare **Top N** nell'elenco a discesa.  
  
9. In **Valore**digitare l'espressione seguente: **=5**  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
Se i risultati non vengono filtrati quando si esegue il report, sarà possibile aggiornare i dati manualmente. Nella scheda **Esegui** del gruppo **Navigazione** fare clic su **Aggiorna**.  
  
Nel grafico verranno visualizzati i nomi dei primi cinque venditori dai dati relativi alle vendite del 2015.  
  
## <a name="Title"></a>9. Aggiungere un titolo al report  
  
1.  Nell'area di progettazione fare clic su **Fare clic per aggiungere il titolo**.  
  
2.  Digitare **Grafico a barre - Vendite**, premere INVIO, quindi digitare **Primi cinque venditori del 2015**in modo da ottenere un risultato analogo al seguente:  
  
    **Grafico a barre - Vendite**  
  
    **Primi cinque venditori del 2015**  
  
3.  Selezionare **Grafico a barre - Vendite**e fare clic sul pulsante **Grassetto** .  
  
4.  Selezionare **Primi cinque venditori del 2015**e nella sezione **Carattere** della scheda **Home** impostare le dimensioni del carattere su **10**.  
  
5.  (Facoltativo) Potrebbe essere necessario aumentare l'altezza della casella di testo Titolo e spostare verso il basso la parte superiore del grafico a barre per fare spazio alle due linee di testo.  
  
    Il titolo verrà visualizzato nella parte superiore del report. Quando non è definita un'intestazione di pagina, gli elementi nella parte superiore del corpo del report equivalgono a un'intestazione di report.  
  
6.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
## <a name="Save"></a>10. Salvare il report  
  
1.  Passare alla visualizzazione di progettazione report.  
  
2.  Fare clic su **File** > **Salva con nome**.  
  
3.  In **Nome**digitare **Grafico a barre - Vendite**.  

    È possibile salvarlo nel computer o nel server di report.
  
4.  Fare clic su **Salva**.   
  
## <a name="next-steps"></a>Next Steps  
Questo passaggio conclude l'esercitazione relativa all'aggiunta di un grafico a barre al report. Per altre informazioni sui grafici, vedere [Grafici](../reporting-services/report-design/charts-report-builder-and-ssrs.md) e [Grafici a barre](../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedere anche  
[Esercitazioni di Generatore report](../reporting-services/report-builder-tutorials.md)  
[Generatore report in SQL Server](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  

