---
title: Definizione di una relazione molti-a-molti | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 7bebb174-148c-4cbb-a285-2f6d536a16d5
author: minewiskan
ms.author: owend
ms.openlocfilehash: 8b0b1d50095584a86074ebe1fb7eac9b7de98256
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84542853"
---
# <a name="defining-a-many-to-many-relationship"></a>Definizione di una relazione molti-a-molti
  Quando si definisce una dimensione, generalmente ogni fatto viene unito in join a un solo membro della dimensione, mentre un singolo membro della dimensione può essere associato a molti fatti. A ogni cliente possono essere ad esempio associati più ordini, ma ogni ordine appartiene a un unico cliente. Nella terminologia dei database relazionali, questa viene definita una *relazione uno-a-molti*. A volte, tuttavia, è possibile che un singolo fatto venga unito in join a più membri della dimensione. Nella terminologia dei database relazionali, questa viene definita una *relazione molti-a-molti*. Ad esempio, i motivi che determinano un acquisto da parte di un cliente possono essere diversi e un motivo per l'acquisto può essere associato a più acquisti. Una tabella di join viene utilizzata per definire i motivi di vendita correlati a ogni acquisto. Una dimensione Sales Reason creata a partire da relazioni di questo tipo può disporre quindi di più membri che corrispondono a una singola transazione di vendita. Le dimensioni molti-a-molti consentono di espandere la modellazione dimensionale oltre lo schema star classico e supportano analisi complesse quando le dimensioni non sono direttamente associate a una tabella dei fatti.

 In [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]è possibile definire una relazione molti-a-molti tra una dimensione e un gruppo di misure specificando una tabella dei fatti intermedia unita in join alla tabella delle dimensioni. Una tabella dei fatti intermedia viene a sua volta unita in join a una tabella delle dimensioni intermedia alla quale è associata la tabella dei fatti. Le relazioni molti-a-molti che intercorrono tra la tabella dei fatti intermedia, le tabelle delle dimensioni nella relazione e la dimensione intermedia determinano la creazione delle relazioni molti-a-molti tra i membri della dimensione primaria e il gruppo di misure specificato dalla relazione. Per definire relazioni molti-a-molti tra una dimensione e un gruppo di misure tramite un gruppo di misure intermedio, quest'ultimo deve condividere una o più dimensioni con il gruppo di misure originale.

 Con una dimensione molti-a-molti, i valori sono di tipo distinct sommati, ovvero non verranno aggregati più di una volta nel membro Totale.

> [!NOTE]
>  Per supportare una relazione di tipo molti-a-molti, è necessario definire una relazione tra chiave primaria e chiave esterna nella vista origine dati tra tutte le tabelle necessarie. In caso contrario, non sarà possibile selezionare il gruppo di misure intermedio corretto quando la relazione viene stabilita nella scheda **Utilizzo dimensioni** di Progettazione cubi.

 Per altre informazioni, vedere [Relazioni tra dimensioni](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)e [Definire una relazione molti-a-molti e le relative proprietà](multidimensional-models/define-a-many-to-many-relationship-and-many-to-many-relationship-properties.md).

 Nelle attività di questo argomento vengono definiti la dimensione Sales Reasons e il gruppo di misure Sales Reasons nonché una relazione molti-a-molti tra la dimensione Sales Reasons e il gruppo di misure Internet Sales tramite il gruppo di misure Sales Reasons.

## <a name="adding-required-tables-to-the-data-source-view"></a>Aggiunta delle tabelle necessarie alla vista origine dati

1.  Aprire Progettazione vista origine dati per la vista origine dati **Adventure Works DW 2012** .

2.  Fare clic con il pulsante destro del mouse in un punto qualsiasi del riquadro **Libreria diagrammi** , scegliere **nuovo diagramma**e specificare `Internet Sales Order Reasons` come nome per il nuovo diagramma.

3.  Trascinare la tabella **InternetSales** dal riquadro **Tabelle** al riquadro **Diagramma** .

4.  Fare clic con il pulsante destro del mouse su un punto qualsiasi all'interno del riquadro **Diagramma** e quindi scegliere **Aggiungi/Rimuovi tabelle**.

5.  Nella finestra di dialogo **Aggiungi/Rimuovi tabelle** aggiungere le tabelle **DimSalesReason** e **FactInternetSalesReason** all'elenco **Oggetti inclusi** e quindi fare clic su **OK**.

     Si noti che le relazioni tra chiave primaria e chiave esterna tra le tabelle incluse vengono stabilite automaticamente poiché tali relazioni sono definite nel database relazionale sottostante. Se le relazioni non fossero definite nel database relazionale sottostante, sarebbe necessario definirle nella vista origine dati.

6.  Scegliere **Layout automatico** dal menu **Formato**e quindi fare clic su **Diagramma**.

7.  Nella Finestra Proprietà modificare la proprietà **FriendlyName** della tabella **DimSalesReason** in `SalesReason` , quindi modificare la proprietà **FriendlyName** della tabella **FactInternetSalesReason** in `InternetSalesReason` .

8.  Nel riquadro **Tabelle** espandere **InternetSalesReason (dbo.FactInternetSalesReason)**, fare clic su **SalesOrderNumber**e quindi controllare la proprietà **DataType** per questa colonna dati nella finestra Proprietà.

     Si noti che la colonna **SalesOrderNumber** è di tipo stringa.

9. Esaminare i tipi di dati per le altre colonne della `InternetSalesReason` tabella.

     Si noti che i tipi di dati delle altre due colonne della tabella sono tipi di dati numerici.

10. Nel riquadro **Tabelle** fare clic con il pulsante destro del mouse su **InternetSalesReason (dbo.FactInternetSalesReason)** e quindi scegliere **Esplora dati**.

     Si noti che per ogni numero di riga all'interno di ogni ordine un valore chiave identifica il motivo della vendita per l'acquisto di quell'elemento di riga, come illustrato nella figura seguente.

     ![Valore chiave per l'identificazione del motivo di vendita per gli acquisti](../../2014/tutorials/media/l5-many-to-many-1.gif "Valore chiave per l'identificazione del motivo di vendita per gli acquisti")

## <a name="defining-the-intermediate-measure-group"></a>Definizione del gruppo di misure intermedio

1.  Passare allo strumento Progettazione cubi per il cubo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial, quindi selezionare la scheda **Struttura del cubo** .

2.  Fare clic con il pulsante destro del mouse su un punto qualsiasi all'interno del riquadro **Misure** e quindi scegliere **Nuovo gruppo di misure**. Per altre informazioni, vedere [Creare misure e gruppi di misure nei modelli multidimensionali](multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md).

3.  Nella finestra di dialogo **nuovo gruppo di misure** , selezionare `InternetSalesReason` nell'elenco **selezionare una tabella dalla vista origine dati** , quindi fare clic su **OK**.

     Si noti che il gruppo di misure **Internet Sales Reason** viene visualizzato nel riquadro **Misure** .

4.  Espandere il gruppo di misure **Internet Sales Reason** .

     Si noti che per questo nuovo gruppo di misure è definita una sola misura, ovvero la misura **Internet Sales Reason Count** .

5.  Selezionare **Internet Sales Reason Count** e controllare le proprietà della misura della finestra Proprietà.

     Si noti che la proprietà **AggregateFunction** per questa misura è definita come **Conteggio** anziché come **Somma**. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]sceglie **count** perché il tipo di dati sottostante è un tipo di dati String. Le altre due colonne della tabella dei fatti sottostante non sono selezionate come misure poiché [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] le ha rilevate come chiavi numeriche anziché come misure effettive. Per altre informazioni, vedere [Definire una funzione semiadditiva](multidimensional-models/define-semiadditive-behavior.md).

6.  Nella finestra Proprietà, impostare la proprietà **Visible** della misura **Internet Sales Reason Count** su **False**.

     Questa misura viene utilizzata solo per unire in join la dimensione Sales Reason che verrà definita successivamente con il gruppo di misure Internet Sales. Non sarà possibile visualizzare direttamente questa misura.

     Nella figura successiva vengono illustrate le proprietà della misura **Internet Sales Reason Count** .

     ![Proprietà della misura Internet Sales Reason Count](../../2014/tutorials/media/l5-many-to-many-2.gif "Proprietà della misura Internet Sales Reason Count")

## <a name="defining-the-many-to-many-dimension"></a>Definizione della dimensione molti-a-molti

1.  In Esplora soluzioni fare clic con il pulsante destro del mouse su **Dimensioni**e quindi scegliere **Nuova dimensione**.

2.  Nella pagina iniziale di **Creazione guidata dimensione** fare clic su **Avanti**.

3.  Nella pagina **Selezione metodo di creazione** verificare che la pagina **Usa una tabella esistente** sia selezionata e fare clic su **Avanti**.

4.  Nella pagina **Impostazione informazioni origine** verificare che la vista origine dati [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW 2012 sia selezionata.

5.  Nell'elenco **tabella principale** selezionare `SalesReason` .

6.  Verificare che l'elenco **Colonne chiave** contenga **SalesReasonKey** .

7.  Nell'elenco **Colonna nome** selezionare **SalesReasonName**.

8.  Fare clic su **Avanti**.

9. Nella pagina **Selezione attributi dimensione** l'attributo **Sales Reason Key** è selezionato automaticamente perché è l'attributo chiave. Selezionare la casella di controllo accanto all'attributo **Sales Reason Reason Type** , modificare il nome in `Sales Reason Type` , quindi fare clic su **Avanti**.

10. Nella pagina **Completamento procedura guidata** fare clic su **Fine** per creare la dimensione Sales Reason.

11. Scegliere **Salva tutti** dal menu **File**.

12. Nel riquadro **attributi** di Progettazione dimensioni per la dimensione **Sales Reason** selezionare **Sales Reason Key**e quindi modificare la proprietà **Name** nel finestra Proprietà`Sales Reason.`

13. Nel riquadro **gerarchie** di Progettazione dimensioni creare una gerarchia utente **Sales Reasons** che contiene il `Sales Reason Type` livello e il livello **Sales Reason** , in questo ordine.

14. Nella Finestra Proprietà definire `All Sales Reasons` come valore per la proprietà **AllMemberName** della gerarchia Sales Reasons.

15. Definire `All Sales Reasons` come valore per la proprietà **AttributeAllMemberName** della dimensione Sales Reason.

16. Per aggiungere la dimensione appena creata al cubo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial, come una dimensione del cubo, passare a **Progettazione cubi**. Fare clic con il pulsante destro del mouse nel riquadro **Dimensioni** della scheda **Struttura cubo** e selezionare **Aggiungi dimensione al cubo**.

17. Nella finestra di dialogo **Aggiungi dimensione al cubo** selezionare **Sales Reason** e quindi fare clic su **OK**.

18. Scegliere **Salva tutti** dal menu **File**.

## <a name="defining-the-many-to-many-relationship"></a>Definizione della relazione molti-a-molti

1.  Passare allo strumento Progettazione cubi per il cubo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial, quindi scegliere la scheda **Utilizzo dimensioni** .

     Si noti che la dimensione **Sales Reason** ha una relazione di tipo Regolare definita con il gruppo di misure **Internet Sales Reason** ma nessuna relazione definita con i gruppi di misure **Internet Sales** o **Reseller Sales** . Si noti inoltre che la dimensione **Internet Sales Order Details** ha una relazione di tipo Regolare definita con la dimensione **Internet Sales Reason** , la quale a sua volta ha una **relazione di tipo Fatti** con il gruppo di misure **Internet Sales** . Se questa dimensione non è presente oppure manca un'altra dimensione con una relazione con entrambi i gruppi di misure **Internet Sales Reason** e **Internet Sales** , non sarà possibile definire la relazione molti-a-molti.

2.  Fare clic sulla cella nel punto di intersezione tra il gruppo di misure **Internet Sales** e la dimensione **Sales Reason** e quindi fare clic sul pulsante con i puntini di sospensione (**...**).

3.  Nella finestra di dialogo **Definisci relazione** selezionare **Molti-a-molti** nell'elenco **Selezionare il tipo di relazione** .

     È necessario definire il gruppo di misure intermedio di collegamento tra la dimensione Sales Reason e il gruppo di misure Internet Sales.

4.  Nell'elenco **Gruppo di misure intermedio** selezionare **Internet Sales Reason**.

     Nella figura seguente vengono illustrate le modifiche apportate alla finestra di dialogo **Definisci relazione** .

     ![Finestra di dialogo Definisci relazione](../../2014/tutorials/media/l5-many-to-many-3.gif "Finestra di dialogo Definisci relazione")

5.  Fare clic su **OK**.

     Si noti l'icona molti-a-molti che rappresenta la relazione tra la dimensione Sales Reason e il gruppo di misure Internet Sales.

## <a name="browsing-the-cube-and-the-many-to-many-dimension"></a>Visualizzazione del cubo e della dimensione molti-a-molti

1.  Scegliere **Distribuisci Analysis Services Tutorial** dal menu **Compila**.

2.  Al termine delle operazioni di distribuzione, passare alla scheda **Esplorazione** in Progettazione cubi per il cubo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial e quindi fare clic su **Riconnetti**.

3.  Aggiungere la misura **Internet Sales-Sales Amount** all'area dati del riquadro Dati.

4.  Aggiungere la gerarchia definita dall'utente **Sales Reasons** dalla dimensione **Sales Reason** all'area riga del riquadro Dati.

5.  Nel riquadro Metadati espandere **Customer**, **Location**, **Customer Geography**, **Members**, **All Customers**e **Australia**, fare clic con il pulsante destro del mouse su **Queensland**, quindi scegliere **Aggiungi a filtro**.

6.  Espandere ogni membro del `Sales Reason Type` livello per esaminare i valori in dollari associati a ogni motivo assegnato da un cliente in Queensland per l'acquisto di un [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] prodotto su Internet.

     Si noti che la somma dei totali associati a ciascun motivo di vendita risulta maggiore delle vendite totali. Ciò si spiega con il fatto che alcuni clienti danno più motivi per i loro acquisti.

     Nella figura seguente sono illustrati i riquadri **Filtro** e **Dati** di Progettazione cubi.

     ![Riquadri Filtro e Dati di Progettazione cubi](../../2014/tutorials/media/l5-many-to-many-5.gif "Riquadri Filtro e Dati di Progettazione cubi")

## <a name="next-task-in-lesson"></a>Attività successiva della lezione
 [Definizione della granularità della dimensione in un gruppo di misure](lesson-5-4-defining-dimension-granularity-within-a-measure-group.md)

## <a name="see-also"></a>Vedere anche
 [Utilizzare diagrammi in Progettazione vista origine dati &#40;Analysis Services relazioni&#41;](multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md) [dimensione](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md) [definiscono una relazione molti-a-molti e le proprietà delle relazioni molti-a-molti](multidimensional-models/define-a-many-to-many-relationship-and-many-to-many-relationship-properties.md)


