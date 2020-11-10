---
title: 'Esercitazione: Creazione di un report in formato libero (Generatore report) | Microsoft Docs'
description: Informazioni su come creare un report impaginato che abbia l'aspetto di un notiziario e in cui ogni pagina visualizzi testo statico, oggetti visivi di riepilogo e dati di vendita di esempio dettagliati.
ms.date: 09/02/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 87288b59-faf2-4b1d-a8e4-a7582baedf2f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a3a4bada590dc9bea822aadffd102b49e75d10cf
ms.sourcegitcommit: 9e2c682929ee64c051dc62f8917d147861f7c635
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/30/2020
ms.locfileid: "93043832"
---
# <a name="tutorial-creating-a-free-form-report-report-builder"></a>Esercitazione: Creazione di un report in formato libero (Generatore report)
In questa esercitazione viene creato un rapporto impaginato che ha l'aspetto di un notiziario. Ogni pagina visualizza testo statico, elementi visivi di riepilogo e dati di vendita di esempio dettagliati.

![Screenshot di un report in formato libero di Generatore report.](../reporting-services/media/report-builder-free-form-report-complete.png)

Nel report le informazioni vengono raggruppate per territorio e vengono visualizzati il nome del responsabile vendite del territorio e informazioni dettagliate e riepilogative relative alle vendite. Si inizia con un'area dati elenco come base per il report in formato libero, quindi si aggiunge un pannello decorativo con un'immagine, testo statico contenente dati, una tabella per la visualizzazione di informazioni dettagliate e facoltativamente grafici a torta e istogrammi per la visualizzazione di informazioni di riepilogo.  
  
Tempo stimato per il completamento dell'esercitazione: 20 minuti.  
  
## <a name="requirements"></a>Requisiti  
Per altre informazioni sui requisiti, vedere [Prerequisiti per le esercitazioni &#40;Generatore report&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="1-create-a-blank-report-data-source-and-dataset"></a><a name="BlankReport"></a>1. Creare un report vuoto, un'origine dati e un set di dati  
  
> [!NOTE]  
> Nella query di questa esercitazione sono contenuti i valori dei dati in modo che non sia necessaria un'origine dati esterna. Tale condizione rende tuttavia la query piuttosto lunga. In una query di un ambiente aziendale non sarebbe incluso alcun dato. Questo esempio è solo a scopo illustrativo.  
  
### <a name="to-create-a-blank-report"></a>Per creare un report vuoto  
  
1.  [Avviare Generatore report](../reporting-services/report-builder/start-report-builder.md) dal computer, dal portale Web di [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] o in modalità integrata SharePoint.  
  
    Si apre la finestra di dialogo **Nuovo report o set di dati** .  
  
    Se la finestra di dialogo **Nuovo report o set di dati** non viene visualizzata, scegliere **Nuovo** dal menu **File**.  
  
2.  Nel riquadro sinistro assicurarsi che sia selezionata l'opzione **Nuovo report** . 
 
3.  Nel riquadro destro fare clic su **Report vuoto**.  
  
### <a name="to-create-a-new-data-source"></a>Per creare una nuova origine dati  
  
1.  Nel riquadro Dati report fare clic su **Nuovo** > **Origine dati**.  
  
2.  Nella casella **Nome** digitare: **ListDataSource**  
  
3.  Fare clic su **Usa una connessione incorporata nel report**.  
  
4.  Verificare che il tipo di connessione sia Microsoft SQL Server, quindi nella casella **Stringa di connessione** digitare: **Origine dati = \<servername>**  
  
    **\<servername>** , ad esempio Report001 specifica un computer in cui viene installata un'istanza del motore di database di SQL Server. Poiché i dati di questo report non vengono estratti da un database di SQL Server, non è necessario includere il nome di un database. Per analizzare la query viene usato il database predefinito nel server specificato.  
  
5.  Fare clic su **Credenziali** , quindi immettere le credenziali necessarie per la connessione all'istanza del motore di database di SQL Server.  
  
6.  Fare clic su **OK**.  
  
### <a name="to-create-a-new-dataset"></a>Per creare un nuovo set di dati  
  
1.  Nel riquadro Dati report fare clic su **Nuovo** > **Set di dati**.  
  
2.  Nella casella **Nome** digitare: **ListDataset**.  
  
3.  Fare clic su **Utilizzare un set di dati incorporato nel report** , quindi verificare che l'origine dati sia **ListDataSource**.  
  
4.  Verificare che il tipo di query **Testo** sia selezionato, quindi fare clic su **Progettazione query**.  
  
5.  Fare clic su **Modifica come testo**.  
  
6.  Copiare e incollare la query seguente nel relativo riquadro:  
  
    ```  
    SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13747.25 AS money) AS Sales, 55 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(9248.15 AS money) As Sales, 37 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1800.00 AS money) AS Sales, 24 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1125.00 AS money) AS Sales, 15 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,  'Lens Adapter' as Product, CAST(742.50 AS money) AS Sales, 11 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1417.50 AS money) AS Sales, 21 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13497.30 AS money) AS Sales, 54 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(11997.60 AS money) AS Sales, 48 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(10247.95 AS money) As Sales, 41 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Tripod' as Product, CAST(1200.00 AS money) AS Sales, 16 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(2025.00 AS money) AS Sales, 27 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1425.00 AS money) AS Sales, 19 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(887.50 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Lens Adapter' as Product, CAST(607.50 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1215.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(10191.00 AS money) AS Sales, 79 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8772.00 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(10578.00 AS money) AS Sales, 82 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(7218.10 AS money) AS Sales, 38 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory,'Digital' as Subcategory,'Slim Digital' as Product, CAST(9307.55 AS money) AS Sales, 49 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(3870.00 AS money) AS Sales, 30 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(5805.00 AS money) AS Sales, 45 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8643.00 AS money) AS Sales, 67 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(9877.40 AS money) AS Sales, 52 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(12536.70 AS money) AS Sales, 66 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(6648.25 AS money) AS Sales, 35 as Quantity  
    ```  
  
7.  Fare clic sull'icona **Esegui** (!) per eseguire la query.  
  
    I risultati della query corrispondono ai dati disponibili per la visualizzazione nel report.  
  
    ![Screenshot della finestra Progettazione query che mostra i dati disponibili per la visualizzazione nel report in formato libero di Generatore report.](../reporting-services/media/report-builder-free-form-tutorial-data.png) 
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="2-add-and-configure-a-list"></a><a name="List"></a>2. Aggiungere e configurare un elenco  
In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] l'area dati elenco è ideale per la creazione di report in formato libero. È basata sull'area dati *tablix* come le tabelle e le matrici. Per altre informazioni, vedere [Creare fatture e moduli con elenchi](../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md).  
  
Verrà usato un elenco per visualizzare le informazioni sulle vendite relative ai territori di vendita in un report simile a un notiziario. Le informazioni vengono raggruppate per territorio. Si aggiungerà un nuovo gruppo di righe per il raggruppamento dei dati per territorio e si eliminerà quindi il gruppo di righe Dettagli incorporato.  
  
### <a name="to-add-a-list"></a>Per aggiungere un elenco  
  
1.  Nella scheda **Inserisci** fare clic su **Aree dati** > **Elenco**. 

2. Fare clic nel corpo del report, tra le aree del titolo e del piè di pagina, e trascinare per creare la casella di riepilogo. Assegnare alla casella di riepilogo un'altezza di 18 cm e una larghezza di 16 cm. Per ottenere la dimensione esatta, nel riquadro **Proprietà** digitare in **Posizione** i valori per **larghezza** e **altezza** .
  
    > [!NOTE]  
    > Questo report utilizza il formato carta Letter (21,7 X 27,9 cm) e margini di 2,54 cm. Una casella di riepilogo più alta di 23 cm o più larga di 16,5 cm potrebbe causare la generazione di pagine vuote.  
  
2.  Fare clic nella casella di riepilogo, fare clic con il pulsante destro del mouse sulla parte superiore dell'elenco, quindi scegliere **Proprietà Tablix**.  
  
    ![Screenshot che mostra l'opzione Proprietà Tablix per il report in formato libero di Generatore report.](../reporting-services/media/report-builder-free-form-tablix-properties.png) 
  
3.  Nell'elenco a discesa **Nome set di dati** selezionare **ListDataset**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  Fare clic con il pulsante destro del mouse nell'elenco, quindi scegliere **Proprietà rettangolo**.  
  
6.  Nella scheda **Generale** selezionare la casella di controllo **Aggiungi un'interruzione di pagina dopo** .  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-add-a-new-row-group-and-to-delete-the-details-group"></a>Per aggiungere un nuovo gruppo di righe ed eliminare il gruppo Dettagli  
  
1.  Nel riquadro Gruppi di righe fare clic con il pulsante destro del mouse sul gruppo Dettagli, scegliere **Aggiungi gruppo** , quindi fare clic su **Gruppo padre**.  
  
    ![Screenshot che mostra come aggiungere un gruppo padre a un report in formato libero di Generatore report.](../reporting-services/media/report-builder-free-form-add-parent-group.png)  
  
2.  Nell'elenco **Raggruppa per** selezionare `[Territory].`  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    Una colonna contenente la cella `[Territory]` viene aggiunta all'elenco.
  
4.  Fare clic con il pulsante destro del mouse sulla colonna Territory, quindi scegliere **Elimina colonne**.  
  
    ![Screenshot che mostra come eliminare una colonna da un report in formato libero di Generatore report.](../reporting-services/media/report-builder-free-form-delete-columns.png)
  
5.  Selezionare **Elimina solo colonne**.  
  
6.  Nel riquadro Gruppi di righe fare clic con il pulsante destro del mouse sul gruppo **Dettagli** > **Elimina gruppo**.  
   
7.  Selezionare **Elimina solo gruppo**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="3-add-graphic-elements"></a><a name="Graphics"></a>3. Aggiungere elementi grafici  
Uno dei vantaggi offerti da un'area dati elenco consiste nella possibilità di aggiungere elementi del report, quali rettangoli e caselle di testo, in qualsiasi posizione, anziché essere limitati a un layout tabulare. L'aggiunta di un elemento grafico, ad esempio un rettangolo colorato, conferirà al report un aspetto più gradevole.  
  
### <a name="to-add-graphic-elements-to-the-report"></a>Per aggiungere elementi grafici al report  
  
1.  Selezionare **Rettangolo** nella scheda **Inserisci**. 

2. Fare clic nell'angolo superiore sinistro dell'elenco e trascinare per rendere il rettangolo alto 18 cm e largo 9 cm. Anche in questo caso, per ottenere la dimensione esatta, nel riquadro **Proprietà** digitare in **Posizione** i valori per **larghezza** e **altezza**.
  
2.  Fare clic con il pulsante destro del mouse sul rettangolo, quindi scegliere **Proprietà rettangolo**.  
  
3.  Fare clic sulla scheda **Riempimento** .  
  
4.  In **Colore riempimento** selezionare **Grigio chiaro**.  
   
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
Nella parte sinistra del report è ora presente un elemento grafico verticale costituito da un rettangolo di colore grigio chiaro, come illustrato nell'immagine che segue.  
  
![Screenshot di Generatore report che mostra un grafico verticale costituito da un rettangolo grigio chiaro.](../reporting-services/media/report-builder-free-form-gray-rectangle.png)
 
## <a name="4-add-free-form-text"></a><a name="Text"></a>4. Aggiungere testo in formato libero  
È possibile aggiungere caselle di testo per visualizzare il testo statico ripetuto in ogni pagina del report, nonché campi dati.  
  
### <a name="to-add-text-to-the-report"></a>Per aggiungere testo al report  
  
1.  Fare clic su **Progettazione** per tornare alla visualizzazione Struttura.  
  
2.  Fare clic su **Casella testo** nella scheda **Inserisci**. Fare clic nell'angolo superiore sinistro dell'elenco, all'interno del rettangolo aggiunto in precedenza, e trascinare per fare in modo che la casella di testo sia larga 8,7 cm e alta 12,7 cm circa.  
  
3.  Con il cursore nella casella di testo, digitare: **Notiziario per** . Includere uno spazio dopo la parola "per", per separare il testo del campo che verrà aggiunto nel passaggio successivo.   
  
    ![Aggiungi testo di intestazione newsletter](../reporting-services/media/tutorial-newsletterfor.png "Aggiungi testo di intestazione newsletter")  
  
4.  Trascinare il campo `[Territory]` da ListDataSet nel riquadro dei dati del report nella casella di testo e posizionarlo dopo "Notiziario per".  
  
    ![Screenshot che mostra come trascinare il campo Territory nel report in formato libero di Generatore report.](../reporting-services/media/report-builder-free-form-territory-field.png)
  
5.  Selezionare il testo e il campo `[Territory]` .  
  
6.  Nella scheda **Home** in **Carattere** selezionare: 
  
    *  **Segoe Semibold**.
    *  **20 pt**.
    *  **Cremisi**.  
  
9. Posizionare il cursore sotto il testo digitato nel passaggio 3 e digitare: **Salve** con uno spazio dopo la parola, per separare il testo e il campo che si aggiungerà nel passaggio successivo.  
 
10. Trascinare il campo `[FullName]` da ListDataSet nel riquadro dei dati del report nella casella di testo e posizionarlo dopo "Salve", quindi digitare una virgola (,).  
   
11. Selezionare il testo aggiunto nei passaggi precedenti.
  
12. Nella scheda **Home** in **Carattere** selezionare: 
  
    *  **Segoe Semibold**.
    *  **16 pt**.
    *  **Nero**.  
   
15. Posizionare il cursore sotto il testo aggiunto nei passaggi da 9 a 13, quindi copiare e incollare il testo fittizio seguente:  
  
    ```  
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin sed dolor in ipsum pulvinar egestas. Sed sed lacus at leo ornare ultricies. Vivamus velit risus, euismod nec sodales gravida, gravida in dui. Etiam ullamcorper elit vitae justo fermentum ut ullamcorper augue sodales. 
    Ut placerat, nisl quis feugiat adipiscing, nibh est aliquet est, mollis faucibus mauris lectus quis arcu. In mollis tincidunt lacinia. In vitae erat ut lorem tincidunt luctus. Curabitur et magna nunc, sit amet adipiscing nisi. Nulla rhoncus elementum orci nec tincidunt. 
    Aliquam imperdiet cursus erat vel tincidunt. Donec et neque ac urna rutrum sodales. In id purus et nisl dignissim dapibus. Sed rhoncus metus at felis feugiat eu tempor dolor vehicula. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam faucibus consectetur diam eu pellentesque.   
 
    ```  
  
16. Selezionare il testo appena aggiunto.  
  
17.  Nella scheda **Home** in **Carattere** selezionare: 
  
      *  **Segoe UI**.
      *  **10 pt**.
      *  **Nero**.  
 
20. Posizionare il cursore all'interno della casella di testo, sotto il testo fittizio, e digitare: **Congratulazioni per le vendite totali di** , con uno spazio dopo la parola per separare il testo e il campo che verrà aggiunto nel passaggio successivo. 
  
21. Trascinare il campo Sales nella casella di testo, posizionarlo dopo il testo digitato nel passaggio precedente, quindi digitare un punto esclamativo (!).  

25. Selezionare il testo e il campo appena aggiunto.  
  
17.  Nella scheda **Home** in **Carattere** selezionare: 
  
      *  **Segoe Semibold**.
      *  **16 pt**.
      *  **Nero**.  
  
22. Selezionare solo il campo `[Sales]`, fare clic con il pulsante destro del mouse sul campo > **Espressione**.  
  
23. Nella casella **Espressione** modificare l'espressione per includere la funzione Sum nel modo seguente:  
  
    ```  
    =Sum(Fields!Sales.value)  
    ```  
  
24. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    ![Screenshot che mostra una casella di testo in un report in formato libero di Generatore report.](../reporting-services/media/report-builder-free-form-text-box.png)
 
29. Con `[Sum(Sales)]` sempre selezionato, nella scheda **Home** > gruppo **Numero** > **Valuta**.  
  
30. Fare clic con il pulsante destro del mouse sulla casella di testo contenente il testo "Fare clic per aggiungere il titolo", quindi scegliere **Elimina**.  
  
31. Selezionare la casella di riepilogo. Selezionare le due frecce a due punte e spostarle nella parte superiore della pagina.  

    ![Screenshot che mostra come trascinare un elenco in un report in formato libero di Generatore report.](../reporting-services/media/report-builder-drag-list.png)
  
32. Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
Nel report viene visualizzato il testo statico e in ogni pagina del report sono inclusi i dati relativi a un territorio. Le vendite vengono formattate come valuta.  
  
![Screenshot che mostra l'anteprima della pagina della newsletter nel report in formato libero di Generatore report.](../reporting-services/media/report-builder-newsletter-page-preview.png)
  
## <a name="5-add-a-table-to-show-sales-details"></a><a name="Table"></a>5. Aggiungere una tabella per la visualizzazione dei dettagli delle vendite  
Utilizzare la procedura guidata Nuova tabella o matrice per aggiungere una tabella al report in formato libero. Dopo avere completato la procedura guidata, si aggiungerà manualmente una riga per i totali.  
  
### <a name="to-add-a-table"></a>Per aggiungere una tabella  
  
1.  Nella scheda **Inserisci** > area **Aree dati** > **Tabella** > **Creazione guidata Tabella**.  
  
2.  Nella pagina **Scegliere un set di dati** fare clic su **ListDataset** > **Avanti**.  
  
4.  Nella pagina **Disponi campi** trascinare il campo Product da **Campi disponibili** a **Valori**.  
  
5.  Ripetere il passaggio 3 per SalesDate, Quantity e Sales. Posizionare SalesDate sotto Product, Quantity sotto SalesDate e Sales sotto SalesDate.  
  
6.  Fare clic su **Avanti**.  
  
7.  Nella pagina **Scegliere il layout** visualizzare il layout della tabella.  
  
    La tabella è semplice: cinque colonne senza gruppi di righe o colonne. Poiché non dispone di gruppi, le opzioni di layout correlate ai gruppi non sono disponibili. Più avanti nell'esercitazione si aggiornerà manualmente la tabella per includere un totale.  
  
8.  Fare clic su **Avanti**.  
  
9. Fare clic su **Fine**.  
  
11. Trascinare la tabella sotto la casella di testo aggiunta nella lezione 4.  
  
    > [!NOTE]  
    > Verificare che la tabella sia all'interno della casella di riepilogo e all'interno del rettangolo grigio.  
  
12. Con la tabella selezionata, nel riquadro **Gruppo righe** fare clic con il pulsante destro del mouse su **Dettagli** > **Aggiungi totale** > **Dopo**.  
  
    ![Screenshot che mostra come aggiungere totali al report in formato libero di Generatore report.](../reporting-services/media/report-builder-free-form-table-totals.png)
  
13. Selezionare la cella nella colonna Product e digitare **Totale**.

    ![Screenshot di una cella nella colonna Product con Totale digitato.](../reporting-services/media/report-builder-free-form-type-total.png)

12. Selezionare il campo [SalesDate]. Nella scheda **Home** > **Numero** modificare **Predefinito** in **Data**.

13. Selezionare i campi [Sum(Sales)]. Nella scheda **Home** > **Numero** modificare **Predefinito** in **Valuta**.

Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
Nel report verrà visualizzata una tabella con i dettagli e i totali delle vendite.  
  
![Screenshot che mostra l'anteprima della tabella nel report in formato libero di Generatore report.](../reporting-services/media/report-builder-free-form-with-table.png)
   
## <a name="6-save-the-report"></a><a name="Save"></a>6. Salvare il report  
È possibile salvare i report in un server di report, in una raccolta di SharePoint o nel computer locale.  
  
In questa esercitazione il report verrà salvato in un server di report. Se non si dispone dell'accesso a un server di report, sarà possibile salvare il report nel computer locale.  
  
### <a name="to-save-the-report-on-a-report-server"></a>Per salvare il report in un server di report  
  
1.  Fare clic sul pulsante **Generatore report** , quindi su **Salva con nome**.  
  
2.  Fare clic su **Siti e server recenti**.  
  
3.  Selezionare o digitare il nome del server di report per il quale si dispone delle autorizzazioni di salvataggio dei report.  
  
    Verrà visualizzato il messaggio "Connessione al server di report". Al termine della connessione, verrà visualizzato il contenuto della cartella di report specificata dall'amministratore del server di report come posizione predefinita per i report.  
  
4.  In **Nome** sostituire il nome predefinito con **InformazioniVenditePerTerritorio**.  
  
5.  Fare clic su **Salva**.  
  
Il report verrà salvato sul server di report. Il nome del server di report al quale si è connessi verrà visualizzato sulla barra di stato nella parte inferiore della finestra.  
  
### <a name="to-save-the-report-on-your-computer"></a>Per salvare il report nel computer  
  
1.  Fare clic sul pulsante **Generatore report** , quindi su **Salva con nome**.  
  
2.  Fare clic su **Desktop** , **Documenti** o **Risorse del computer** , quindi selezionare la cartella in cui si desidera salvare il report.  
  
3.  In **Nome** sostituire il nome predefinito con **InformazioniVenditePerTerritorio**.  
  
4.  Fare clic su **Salva**.  
  
## <a name="7-optional-add-a-line-to-separate-areas-of-the-report"></a><a name="Line"></a>7. (Facoltativo) Aggiungere una linea per separare le aree del report  
Aggiungere una linea per separare l'area editoriale da quella dei dettagli del report.  
  
### <a name="to-add-a-line"></a>Per aggiungere una linea  
  
1.  Fare clic su **Progettazione** per tornare alla visualizzazione Struttura.  
  
2.  Nella scheda **Inserisci** > **Elementi del report** > **Linea.**  
  
3.  Disegnare una linea sotto la casella di testo aggiunta nella lezione 4.  
  
4.  Fare clic sulla linea e nella scheda **Home** > **Bordo** selezionare:
     * **Larghezza** : selezionare **3** pt.
     * **Colore** : selezionare **Cremisi**.  
  
## <a name="8-optional-add-summary-data-visualizations"></a><a name="Visualization"></a>8. (Facoltativo) Aggiungere visualizzazioni dei dati di riepilogo  
I rettangoli consentono di controllare la modalità di rendering del report. Posizionare un grafico a torta e un istogramma all'interno di un rettangolo per essere certi che il rendering del report venga eseguito nel modo desiderato.  
  
### <a name="to-add-a-rectangle"></a>Per aggiungere un rettangolo  
  
1.  Fare clic su **Progettazione** per tornare alla visualizzazione Struttura.  
  
2.  Nella scheda **Inserisci** > **Elementi del report** >  **Rettangolo**. Trascinare il rettangolo all'interno della casella di riepilogo a destra della tabella per creare un rettangolo largo 5,7 cm e alto 20 cm circa.  
  
3.  Con il nuovo rettangolo selezionato, nel riquadro Proprietà impostare **colore del bordo su grigio chiaro** , **stile del bordo su linea continua** e **larghezza del bordo su 2 pt**. 

4. Allineare le parti superiori del rettangolo e della tabella.  
  
## <a name="to-add-a-pie-chart"></a>Per aggiungere un grafico a torta  
  
1.  Nella scheda **Inserisci** scegliere **Visualizzazioni dati** > **Grafico** > **Creazione guidata grafico**.  
  
2.  Nella pagina **Scegliere un set di dati** fare clic su **ListDataset** > **Avanti**.  
  
3.  Fare clic su **Torta** > **Avanti**.  
  
4.  Nella pagina Disponi campi del grafico trascinare Product in **Categorie**.  
  
5.  Trascinare Quantity in **Valori** , quindi fare clic su **Avanti**.  
  
6.  Fare clic su **Fine**.  
  
8.  Ridimensionare il grafico visualizzato nell'angolo superiore sinistro del report in modo che abbia un'altezza di 5,7 cm e una larghezza di 9 cm circa.  
  
9. Trascinare il grafico all'interno del rettangolo.  
   
10. Selezionare il titolo del grafico e digitare: **Quantità di prodotto vendute**.  
  
12. Nella scheda **Home** > **Carattere** impostare per il titolo:
    * **Tipo di carattere** **Segoe UI Semibold**.
    * **Dimensioni** **12 pt**.
    * **Colore** **Nero**.  

13. Fare clic con il pulsante destro del mouse sulla legenda > **Proprietà legenda**.

14. In **Posizione legenda** nella scheda **Generale** selezionare il punto centrale in basso. 
  
15. [!INCLUDE[clickOK](../includes/clickok-md.md)]  

16. Trascinare per aumentare l'altezza dell'area del grafico, se necessario.

     ![Screenshot che mostra il grafico a torta da aggiungere al report in formato libero di Generatore report.](../reporting-services/media/report-builder-free-form-pie.png)
  
## <a name="to-add-a-column-chart"></a>Per aggiungere un istogramma  
  
1.  Nella scheda **Inserisci** scegliere **Visualizzazioni dati** > **Grafico** > **Creazione guidata grafico**.  
  
2.  Nella pagina **Scegliere un set di dati** fare clic su **ListDataset** , quindi su **Avanti**.  
  
3.  Fare clic su **Colonna** , quindi su **Avanti**.  
  
4.  Nella pagina **Disponi campi del grafico** trascinare il campo Product in **Categorie**.  
  
5.  Trascinare Sales in **Valori** , quindi fare clic su **Avanti**.  
  
    I valori vengono visualizzati sull'asse verticale.  
  
6.  Fare clic su **Fine**.  
  
    Un istogramma verrà aggiunto all'angolo superiore sinistro del report.  
  
8.  Ridimensionare il grafico in modo che sia largo circa 5,7 cm e alto quasi 10 cm.  
  
9. Trascinare il grafico all'interno del rettangolo sotto il grafico a torta.  
   
10. Selezionare il titolo del grafico e digitare: **Vendite prodotto**.  
  
12. Nella scheda **Home** > **Carattere** impostare per il titolo:
    * **Tipo di carattere** **Segoe UI Semibold**.
    * **Dimensioni** **12 pt**.
    * **Colore** **Nero**.  
  
15. Fare clic con il pulsante destro del mouse sulla legenda, quindi scegliere **Elimina legenda**.  
  
    > [!NOTE]  
    > La rimozione della legenda rende il grafico più leggibile quando il grafico è piccolo.  
  
    ![Screenshot che mostra l'istogramma da aggiungere al report in formato libero di Generatore report.](../reporting-services/media/report-builder-free-form-column.png)

12. Selezionare l'asse del grafico e quindi nella scheda **Home** > **Numero** > **Valuta**.

13. Selezionare **Diminuisci decimali** due volte, in modo che il numero indichi solo i dollari e non i centesimi.      
### <a name="to-verify-the-charts-are-inside-the-rectangle"></a>Per verificare che i grafici siano all'interno del rettangolo  

È possibile usare i rettangoli come contenitori per altri elementi di una pagina del report. Sono disponibili altre informazioni sull'uso dei [rettangoli come contenitori](../reporting-services/report-design/rectangles-and-lines-report-builder-and-ssrs.md).
  
1.  Selezionare il rettangolo creato e aggiunto ai grafici in precedenza in questa lezione.  
  
    La proprietà **Name** nel riquadro Proprietà indica il nome del rettangolo.  
  
    ![Screenshot che mostra come visualizzare la proprietà Name nel report in formato libero di Generatore report.](../reporting-services/media/report-builder-free-form-rectangle-name.png) 
  
2.  Fare clic sul grafico a torta.  
  
3.  Nel riquadro **Proprietà** verificare che la proprietà **Parent** contenga il nome del rettangolo.  
  
     ![Screenshot che mostra come visualizzare la proprietà Parent nel report in formato libero di Generatore report.](../reporting-services/media/report-builder-free-form-pie-parent.png) 
  
4.  Fare clic sull'istogramma e ripetere il passaggio 3.  
  
    > [!NOTE]  
    > Se non si trovano all'interno del rettangolo, i grafici non verranno visualizzati insieme nel report visualizzabile.  
  
### <a name="to-make-the-charts-the-same-size"></a>Per assegnare ai grafici le stesse dimensioni  
  
1.  Selezionare il grafico a torta, premere CTRL, quindi selezionare l'istogramma.  
  
2.  Con entrambi i grafici selezionati, fare clic con il pulsante destro del mouse su > **Layout** > **Assegna stessa larghezza**.  
  
    > [!NOTE]  
    > Il primo elemento selezionato determina la larghezza di tutti gli elementi selezionati.  
  
3.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
Nel report verranno visualizzati i dati di vendita riepilogativi in diagrammi a torta e istogrammi.  
  

  
## <a name="next-steps"></a>Passaggi successivi  
L'esercitazione sulla creazione di un report in formato libero è terminata.  
  
Per altre informazioni sugli elenchi, vedere: 
* [Tabelle, matrici ed elenchi &#40;Generatore report e SSRS&#41;](../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md) 
* [Creare fatture e moduli con elenchi](../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)
* [Celle, righe e colonne dell'area dati Tablix &#40;Generatore report e SSRS&#41;](../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
Per altre informazioni sulla progettazione delle query, vedere [Finestre di progettazione query (SSRS)](report-data/query-design-tools-ssrs.md) e [Interfaccia utente di Progettazione query basata su testo &#40;Generatore report&#41;](../reporting-services/report-data/text-based-query-designer-user-interface-report-builder.md).  
  
## <a name="see-also"></a>Vedere anche  
[Esercitazioni di Generatore report](../reporting-services/report-builder-tutorials.md) 
  

