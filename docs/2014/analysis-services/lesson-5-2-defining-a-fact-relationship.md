---
title: Definizione di una relazione di tipo fact | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 4b49a078-6848-4286-bc71-cf4862d29064
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4408e9b884e2cb5a0b47d9e6f95a16dec2bd20f6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "69493858"
---
# <a name="defining-a-fact-relationship"></a>Definizione di una relazione di tipo Fatti
  Talvolta può essere necessario dimensionare le misure in base ai dati contenuti nella tabella dei fatti o eseguire query per trovare informazioni correlate specifiche aggiuntive, come ad esempio i numeri delle fatture o degli ordini di acquisto collegati a operazioni di vendita specifiche. Quando viene definita una dimensione basata su un elemento della tabella dei fatti di questo tipo, la dimensione viene denominata *dimensione dei fatti*. Le dimensioni dei fatti sono inoltre note come dimensioni degeneri. Le dimensioni dei fatti sono utili per raggruppare righe di tabelle dei fatti collegate, come ad esempio tutte le righe collegate a un particolare numero di fattura. Sebbene sia possibile inserire queste informazioni in una tabella della dimensione separata del database relazionale, la creazione di una tale tabella non si rivela vantaggiosa in quanto la tabella della dimensione aumenterebbe allo stesso modo della tabella dei fatti determinando un'inutile duplicazione dei dati nonché un'inutile complessità.  
  
 In [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]è possibile determinare se duplicare i dati delle dimensioni dei fatti in una struttura della dimensione MOLAP per aumentare le prestazioni delle query o se definire la dimensione dei fatti come una dimensione ROLAP per risparmiare spazio di archiviazione a discapito delle prestazioni delle query. Quando si archivia una dimensione con modalità MOLAP, tutti i membri della dimensione vengono archiviati nell'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] in una struttura MOLAP a compressione elevata, oltre a essere archiviati nelle partizioni del gruppo di misure. Quando si archivia una dimensione con la modalità di archiviazione ROLAP, solo la definizione della dimensione viene archiviata nella struttura MOLAP. i membri della dimensione stessi vengono sottoposti a query dalla tabella dei fatti relazionale sottostante in fase di query. È possibile decidere la modalità di archiviazione appropriata in base alla frequenza con la quale vengono eseguite query sulla dimensione dei fatti, al numero delle righe restituite da una query tipica, alle prestazioni delle query e ai costi di elaborazione. Se una dimensione viene definita come ROLAP non è necessario che anche tutti i cubi in cui viene utilizzata la dimensione siano archiviati tramite la modalità di archiviazione ROLAP. La modalità di archiviazione di ogni dimensione può essere configurata in modo indipendente.  
  
 Quando si definisce una dimensione dei fatti, è possibile definire la relazione tra la dimensione dei fatti e il gruppo di misure come una relazione di tipo Fatti. Alle relazioni di tipo Fatti si applicano i vincoli seguenti:  
  
-   L'attributo di granularità deve essere la colonna chiave della dimensione che crea una relazione uno-a-uno tra la dimensione e i fatti nella tabella dei fatti.  
  
-   Una dimensione può avere una relazione di tipo Fatti con un solo gruppo di misure.  
  
> [!NOTE]  
>  È inoltre necessario eseguire aggiornamenti incrementali delle dimensioni dei fatti dopo ogni aggiornamento del gruppo di misure a cui fa riferimento la relazione di tipo Fatti.  
  
 Per altre informazioni, vedere [Relazioni tra dimensioni](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)e [Definire una relazione di tipo Fatti e le relative proprietà](multidimensional-models/define-a-fact-relationship-and-fact-relationship-properties.md).  
  
 Nelle attività di questo argomento verrà aggiunta una nuova dimensione del cubo basata sulla colonna **CustomerPONumber** della tabella dei fatti **FactInternetSales** . Verrà quindi definita come relazione di tipo Fatti la relazione tra questa nuova dimensione del cubo e il gruppo di misure **Internet Sales** .  
  
## <a name="defining-the-internet-sales-orders-fact-dimension"></a>Definizione della dimensione dei fatti Internet Sales Orders  
  
1.  In Esplora soluzioni fare clic con il pulsante destro del mouse su **dimensioni**, quindi scegliere **nuova dimensione**.  
  
2.  Nella pagina iniziale di **Creazione guidata dimensione** fare clic su **Avanti**.  
  
3.  Nella pagina **Selezione metodo di creazione** verificare che la pagina **Usa una tabella esistente** sia selezionata e fare clic su **Avanti**.  
  
4.  Nella pagina **Impostazione informazioni origine** verificare che sia selezionata la vista origine dati **Adventure Works DW 2012** .  
  
5.  Nell'elenco **Tabella principale** selezionare **InternetSales**.  
  
6.  Nell'elenco **Colonne chiave** verificare che siano presenti **SalesOrderNumber** e **SalesOrderLineNumber** .  
  
7.  Nell'elenco **Colonna nome** selezionare **SalesOrderLineNumber**.  
  
8.  Fare clic su **Avanti**.  
  
9. Nella pagina **Selezione tabelle correlate** deselezionare le caselle di controllo accanto a tutte le tabelle e quindi fare clic su **Avanti**.  
  
10. Nella pagina **Selezione attributi dimensione** fare clic due volte sulla casella di controllo nell'intestazione per deselezionare tutte le caselle di controllo. L'attributo **Sales Order Number** rimarrà selezionato perché è l'attributo chiave.  
  
11. Selezionare l'attributo **Customer PO Number** e quindi fare clic su **Avanti**.  
  
12. Nella pagina **Completamento procedura guidata** modificare il nome in **Internet Sales Order Details** e quindi fare clic su **Fine** per completare la procedura guidata.  
  
13. Scegliere **Salva tutti** dal menu **File**.  
  
14. Nel riquadro **attributi** di Progettazione dimensioni per la dimensione **Internet Sales Order Details** , selezionare **Sales Order Number**, quindi modificare la proprietà **Name** nel finestra Proprietà`Item Description.`  
  
15. Nella cella della proprietà **NameColumn** fare clic sul pulsante Sfoglia **(...)**. Nella finestra di dialogo **colonna nome** selezionare **Product** dall'elenco **tabella di origine** , selezionare **EnglishProductName** per colonna di **origine**e quindi fare clic su **OK**.  
  
16. Aggiungere l'attributo **Sales Order Number** alla dimensione trascinando la colonna **SalesOrderNumber** dalla tabella **InternetSales** del riquadro **Vista origine dati** al riquadro **Attributi** .  
  
17. Modificare la proprietà **Name** del nuovo attributo **Sales Order Number** in `Order Number`e modificare la proprietà **OrderBy** in **Key**.  
  
18. Nel riquadro **gerarchie** creare una gerarchia utente **Internet Sales Orders** contenente i livelli di `Order Number` **Descrizione dell'elemento** e, in questo ordine.  
  
19. Nel riquadro **Attributi** selezionare **Internet Sales Order Details**e quindi controllare il valore della proprietà **StorageMode** nella finestra Proprietà.  
  
     Si noti che per impostazione predefinita la dimensione viene archiviata come una dimensione MOLAP. Sebbene la modifica della modalità di archiviazione in ROLAP consenta di risparmiare tempo di elaborazione e spazio di archiviazione, ciò avviene a discapito delle prestazioni delle query. Ai fini di questa esercitazione, verrà utilizzata la modalità di archiviazione MOLAP.  
  
20. Per aggiungere la dimensione appena creata al cubo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial, come una dimensione del cubo, passare a **Progettazione cubi**. Fare clic con il pulsante destro del mouse nel riquadro **Dimensioni** della scheda **Struttura cubo** e selezionare **Aggiungi dimensione al cubo**.  
  
21. Nella finestra di dialogo **Aggiungi dimensione al cubo**selezionare **Internet Sales Order Details** e fare clic su **OK**.  
  
## <a name="defining-a-fact-relationship-for-the-fact-dimension"></a>Definizione di una relazione di tipo Fatti per la dimensione dei fatti  
  
1.  In Progettazione cubi per il cubo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial fare clic sulla scheda **Utilizzo dimensioni** .  
  
     Si noti che la dimensione del cubo **Internet Sales Order Details** viene configurata automaticamente come provvista di una relazione di tipo Fatti, indicata dall'icona univoca.  
  
2.  Fare clic sul pulsante Sfoglia (**...**) nella cella **Descrizione elemento** , all'intersezione tra il gruppo di misure **Internet Sales** e la dimensione **Internet Sales Order Details** , per esaminare le proprietà della relazione di tipo fact.  
  
     Verrà visualizzata la finestra di dialogo **Definisci relazione** . Si noti che non è possibile configurare le proprietà.  
  
     L'immagine seguente illustra le proprietà della relazione di tipo Fatti nella finestra di dialogo **Definisci relazione** .  
  
     ![Finestra di dialogo Definisci relazione](../../2014/tutorials/media/l5-factrelationship-2.gif "Finestra di dialogo Definisci relazione")  
  
3.  Fare clic su **Annulla**.  
  
## <a name="browsing-the-cube-by-using-the-fact-dimension"></a>Esplorazione del cubo tramite la dimensione dei fatti  
  
1.  Nel menu **Compila** scegliere **Distribuisci Analysis Services Tutorial** per distribuire le modifiche all'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ed elaborare il database.  
  
2.  Dopo aver completato la distribuzione, selezionare la scheda **Esplorazione** in Progettazione cubi per il cubo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial e fare clic sul pulsante **Riconnetti** .  
  
3.  Deselezionare tutte le misure e le gerarchie del riquadro Dati, quindi aggiungere la misura **Internet Sales-Sales Amount** all'area dati del riquadro Dati.  
  
4.  Nel riquadro Metadati espandere **Customer**, **Location**, **Customer Geography**, **Members**, **All Customers**, **Australia**, **Queensland**, **Brisbane**, **4000**, fare clic con il pulsante destro del mouse su **Adam Powell**e quindi scegliere **Aggiungi a filtro**.  
  
     Il filtraggio degli ordini di vendita relativi ad un singolo cliente consente di eseguire il drill-down del dettaglio sottostante in una tabella dei fatti estesa senza determinare un significativo peggioramento delle prestazioni delle query.  
  
5.  Aggiungere la gerarchia definita dall'utente **Internet Sales Orders** dalla dimensione **Internet Sales Order Details** all'area riga del riquadro Dati.  
  
     Si noti che i numeri relativi agli ordini di vendita e i ricavi tramite Internet di Adam Powell vengono visualizzati nel riquadro Dati.  
  
     Nell'immagine seguente viene illustrato il risultato dei passaggi precedenti.  
  
     ![Dimensionamento di Internet Sales-Sales Amount](../../2014/tutorials/media/l5-factrelationship-3.gif "Dimensionamento di Internet Sales-Sales Amount")  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Definizione di una relazione molti-a-molti](lesson-5-3-defining-a-many-to-many-relationship.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Relazioni tra dimensioni](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [Definire una relazione di tipo Fatti e le relative proprietà](multidimensional-models/define-a-fact-relationship-and-fact-relationship-properties.md)  
  
  
