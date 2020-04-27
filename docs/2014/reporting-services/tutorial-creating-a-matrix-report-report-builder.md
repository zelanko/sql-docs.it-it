---
title: 'Esercitazione: Creazione di un report tabella semplice (Generatore report) | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 9ee19c2e-2a8c-4bb0-9274-04a5812c2e96
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f87c1188b0abd1b576da63412829464368275b0f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66098914"
---
# <a name="tutorial-creating-a-matrix-report-report-builder"></a>Esercitazione: Creazione di un report matrice (Generatore report)
  In questa esercitazione viene illustrato come creare un report matrice semplice basato su dati di vendita di esempio. La matrice presenta gruppi di righe e di colonne annidati, nonché un gruppo di colonne adiacente. Verrà inoltre illustrato come formattare le colonne e ruotare il testo. Nell'immagine seguente viene illustrato un report simile a quello che verrà creato.  
  
 ![rs_CreateMatixReportTutorial](../../2014/tutorials/media/rs-creatematixreporttutorial.gif "rs_CreateMatixReportTutorial")  
  
 Una versione avanzata del report che verrà creato in questa esercitazione è disponibile come report di esempio di Generatore report di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Per ulteriori informazioni sul download di questo report di esempio e di altri, vedere [Generatore report report di esempio](https://go.microsoft.com/fwlink/?LinkId=184851).  
  
##  <a name="what-you-will-learn"></a><a name="BackToTop"></a>Cosa si apprenderà  
 In questa esercitazione verranno illustrate le procedure per:  
  
1.  [Creare un report matrice e un set di dati tramite la Creazione guidata tabella o matrice](#CreateMatrix)  
  
2.  [Organizzare i dati e scegliere il layout e lo stile tramite la Creazione guidata tabella o matrice](#Groups)  
  
3.  [Formattare i dati](#FormatData)  
  
4.  [Aggiungere un gruppo di colonne adiacente](#AdjacentGroup)  
  
5.  [Modificare la larghezza delle colonne](#Width)  
  
6.  [Unire le celle della matrice](#MergeCells)  
  
7.  [Aggiungere un'intestazione e un titolo al report](#HeaderTitle)  
  
8.  [Salva il report](#Save)  
  
### <a name="other-optional-step"></a>Altro passaggio facoltativo  
  
1.  [Ruotare la casella di testo di 270 gradi](#RotateTextBox)  
  
 Il tempo stimato per il completare l'esercitazione è di 20 minuti.  
  
## <a name="requirements"></a>Requisiti  
 Per altre informazioni sui requisiti, vedere [Prerequisiti per le esercitazioni &#40;Generatore report&#41;](../reporting-services/report-builder-tutorials.md).  
  
##  <a name="1-create-a-matrix-report-and-dataset-from-the-new-table-or-matrix-wizard"></a><a name="CreateMatrix"></a>1. creare un report matrice e un set di dati dalla creazione guidata tabella o matrice  
 Nella finestra di dialogo **Introduzione** in Generatore report scegliere un'origine dati condivisa, creare un set di dati incorporato e visualizzare i dati in una matrice.  
  
> [!NOTE]  
>  Per evitare di dover disporre di un'origine dati esterna, nella query di questa esercitazione sono già inclusi i valori dei dati. Tale condizione rende tuttavia la query piuttosto lunga. In una query di un ambiente aziendale non sarebbe incluso alcun dato. Questo esempio è solo a scopo illustrativo.  
  
#### <a name="to-create-a-new-matrix"></a>Per creare una nuova matrice  
  
1.  Fare clic sul menu **Start**, scegliere **Programmi**, **Generatore report per Microsoft SQL Server 2012**e quindi fare clic su **Generatore report**.  
  
    > [!NOTE]  
    >  Verrà visualizzata la finestra di dialogo **Riquadro attività iniziale** . In caso contrario, fare clic sul pulsante Generatore report, quindi su **nuovo**.  
  
2.  Nel riquadro sinistro verificare che sia selezionata l'opzione **Nuovo report** .  
  
3.  Nel riquadro destro fare clic su **Creazione guidata tabella o matrice**.  
  
4.  Nella pagina **Scegliere un set di dati** fare clic su **Crea un set di dati**.  
  
5.  Fare clic su **Avanti**.  
  
6.  Nella pagina **scegliere una connessione a un'origine dei dati** selezionare un'origine dati esistente o individuare il server di report, quindi selezionare un'origine dati. Se non è disponibile un'origine dati o non si dispone dell'accesso a un server di report, sarà possibile utilizzare un'origine dati incorporata. Per ulteriori informazioni sulla creazione di un'origine dati incorporata, vedere [esercitazione: creazione di un report tabella semplice &#40;Generatore report&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
7.  Fare clic su **Avanti**.  
  
8.  Nella pagina **Progetta query** fare clic su **Modifica come testo**.  
  
9. Copiare e incollare la query seguente nel relativo riquadro:  
  
    ```  
    SELECT CAST('2009-01-05' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13747.25 AS money) AS Sales, 55 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(9248.15 AS money) As Sales, 37 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1800.00 AS money) AS Sales, 24 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1125.00 AS money) AS Sales, 15 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory,  'Lens Adapter' as Product, CAST(742.50 AS money) AS Sales, 11 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1417.50 AS money) AS Sales, 21 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13497.30 AS money) AS Sales, 54 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(11997.60 AS money) AS Sales, 48 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(10247.95 AS money) As Sales, 41 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory, 'Tripod' as Product, CAST(1200.00 AS money) AS Sales, 16 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(2025.00 AS money) AS Sales, 27 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1425.00 AS money) AS Sales, 19 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(887.50 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'North' as Territory, 'Accessories' as Subcategory, 'Lens Adapter' as Product, CAST(607.50 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1215.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(10191.00 AS money) AS Sales, 79 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'North' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8772.00 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(10578.00 AS money) AS Sales, 82 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Central' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(7218.10 AS money) AS Sales, 38 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'North' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'South' as Territory,'Digital' as Subcategory,'Slim Digital' as Product, CAST(9307.55 AS money) AS Sales, 49 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(3870.00 AS money) AS Sales, 30 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'North' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(5805.00 AS money) AS Sales, 45 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8643.00 AS money) AS Sales, 67 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Central' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(9877.40 AS money) AS Sales, 52 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'North' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(12536.70 AS money) AS Sales, 66 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'South' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(6648.25 AS money) AS Sales, 35 as Quantity  
    ```  
  
10. Fare clic su **Avanti**.  
  
##  <a name="2-organize-data-and-choose-layout-and-style-from-the-new-table-or-matrix-wizard"></a><a name="Groups"></a>2. organizzare i dati e scegliere il layout e lo stile dalla procedura guidata nuova tabella o matrice  
 Utilizzare la procedura guidata per fornire una progettazione iniziale in cui visualizzare i dati. Il riquadro di anteprima nella procedura guidata consente di visualizzare il risultato del raggruppamento di dati prima di completare la progettazione della matrice.  
  
#### <a name="to-organize-data-into-groups-and-choose-a-layout-and-style"></a>Per organizzare i dati in gruppi e scegliere un layout e uno stile  
  
1.  Nella pagina **Disponi campi** trascinare Territory da **Campi disponibili** in **Gruppi di righe**.  
  
2.  Trascinare SalesDate in **Gruppi di righe** e posizionarlo sotto Territory.  
  
     L'ordine in cui i campi vengono elencati in **Gruppi di righe** consente di definire la gerarchia di gruppi. I passaggi 1 e 2 consentono di organizzare i valori dei campi prima in base al territorio, quindi in base alle date di vendita.  
  
3.  Trascinare Subcategory in **Gruppi di colonne**.  
  
4.  Trascinare Product in **gruppi di colonne,** quindi posizionarlo sotto Subcategory.  
  
     L'ordine in cui i campi vengono elencati in **gruppi di colonne** definisce la gerarchia di gruppi.  
  
     I passaggi 3 e 4 consentono di organizzare i valori per i campi prima in base alla sottocategoria, quindi in base al prodotto.  
  
5.  Trascinare Sales in **Valori**.  
  
     Le vendite vengono riepilogate con la funzione Sum, ovvero la funzione predefinita per il riepilogo di campi numerici.  
  
6.  Trascinare Quantity in **Valori**.  
  
     La quantità viene riepilogata con la funzione Sum.  
  
     I passaggi 5 e 6 consentono di specificare i dati da visualizzare nella celle di dati della matrice.  
  
7.  Fare clic su **Avanti**.  
  
8.  Nella pagina Scegliere il layout, in **Opzioni**, verificare che la casella **Mostra subtotali e totali complessivi** sia selezionata.  
  
9. Verificare che l'opzione **Bloccato, subtotale sotto** sia selezionata.  
  
10. Verificare che l'opzione **Espandi/comprimi gruppi** sia selezionata.  
  
11. Fare clic su **Avanti**.  
  
12. Nel riquadro Stili della pagina Scegliere uno stile selezionare **Ardesia**.  
  
13. Fare clic su **Fine**.  
  
     La matrice viene aggiunta all'area di progettazione. Nel riquadro Gruppi di righe vengono visualizzati due gruppi di righe, ovvero Territory e SalesDate. Nel riquadro Gruppi di colonne vengono visualizzati due gruppi di colonne, ovvero Subcategory e Product. I dati dettaglio costituiscono tutti i dati recuperati dalla query del set di dati.  
  
14. Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
 Per ogni prodotto venduto in una data specifica, nella matrice viene visualizzata la sottocategoria alla quale appartiene il prodotto, nonché il territorio delle vendite.  
  
##  <a name="3-format-data"></a><a name="FormatData"></a>3. formattare i dati  
 Per impostazione predefinita, i dati riepilogativi per il campo Sales vengono visualizzati come numero generico e nel campo SalesDate vengono visualizzate le informazioni di data e ora. Formattare il campo Sales in modo che il numero venga visualizzato come valuta e formattare il campo SalesDate in modo che venga visualizzata solo la data. Attivare o disattivare **Stili segnaposto** per visualizzare caselle di testo formattate e testo segnaposto come valori di esempio.  
  
#### <a name="to-format-fields"></a>Per formattare i campi  
  
1.  Fare clic su **progettazione** per passare alla visualizzazione progettazione.  
  
2.  Premere CTRL e selezionare le nove celle contenenti `[Sum(Sales)]`.  
  
3.  Nel gruppo **Numero** della scheda **Home** fare clic su **Valuta**. I numeri nelle celle verranno visualizzati nel formato di valuta.  
  
     Se la lingua delle impostazioni locali è Inglese (Stati Uniti), il testo di esempio predefinito sarà [**$12,345.00**]. Se non viene visualizzato un valore di valuta di esempio, fare clic su **Stili segnaposto** nel gruppo **numeri** , quindi fare clic su **valori di esempio**.  
  
4.  Fare clic sulla cella contenente `[SalesDate]`.  
  
5.  Nel gruppo **numero** selezionare **Data**nell'elenco a discesa.  
  
     Nella cella viene visualizzata la data di esempio **[1/31/2000]**. Se non viene visualizzata una data di esempio, fare clic su **Stili segnaposto** nel gruppo **Numeri** , quindi fare clic su **Valori di esempio**.  
  
6.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
 I valori di data verranno visualizzati solo come date mentre i valori delle vendite verranno visualizzati come valuta.  
  
##  <a name="4-add-adjacent-column-group"></a><a name="AdjacentGroup"></a>4. aggiungere un gruppo di colonne adiacente  
 È possibile annidare gruppi di righe e colonne nelle relazioni padre-figlio oppure gruppi di righe e colonne adiacenti nelle relazioni di pari livello.  
  
 Aggiungere un gruppo di colonne adiacente al gruppo di colonne Subcategory, copiare le celle per popolare il nuovo gruppo di colonne, quindi utilizzare un'espressione per creare il valore dell'intestazione del gruppo di colonne.  
  
#### <a name="to-add-an-adjacent-column-group"></a>Per aggiungere un gruppo di colonne adiacente  
  
1.  Fare clic su **Progettazione** per tornare alla visualizzazione Struttura.  
  
2.  Fare clic con il pulsante destro del mouse sulla cella contenente `[Subcategory]`, scegliere **Aggiungi gruppo**, quindi fare clic su **Adiacente a destra**.  
  
     Verrà visualizzata la finestra di dialogo **Gruppo Tablix** .  
  
3.  Nell'elenco **Raggruppa per** selezionare SalesDate, quindi fare clic su **OK**.  
  
     Un nuovo gruppo di colonne verrà aggiunto a sinistra del gruppo di colonne Subcategory.  
  
4.  Fare clic con il pulsante destro del mouse sulla cella del nuovo gruppo di colonne contenente `[SalesDate],` quindi scegliere **Espressione**.  
  
5.  Copiare l'espressione seguente nella casella dell'espressione.  
  
    ```  
    =WeekdayName(DatePart("w",Fields!SalesDate.Value))  
    ```  
  
     Questa espressione consente di estrarre il nome del giorno della settimana dalla data in cui è stata realizzata la vendita. Per altre informazioni, vedere [Espressioni &#40;Generatore report e SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md).  
  
6.  Fare clic con il pulsante destro del mouse sul gruppo di colonne Subcategory contenente Total, quindi scegliere **Copia**.  
  
7.  Fare clic con il pulsante destro del mouse sulla cella posta immediatamente sotto a quella contenente l'espressione creata nel passaggio 5 e scegliere **Incolla**.  
  
8.  Premere CTRL.  
  
9. Nel gruppo Subcategory fare clic sull'intestazione di colonna Sales e sulle tre celle sottostanti, fare clic con il pulsante destro del mouse, quindi scegliere **Copia**.  
  
10. Incollare le quattro celle nelle quattro celle vuote del nuovo gruppo di colonne.  
  
11. Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
 Nel report sono incluse due colonne denominate Monday e Tuesday. Il set di dati contiene i dati solo per questi due giorni.  
  
> [!NOTE]  
>  Diversamente, nel report sarebbero state incluse le colonne per gli altri giorni della settimana. Ogni colonna presenta l'intestazione di colonna `Sales`, e i totali delle vendite per territorio.  
  
##  <a name="5-change-column-widths"></a><a name="Width"></a>5. modificare la larghezza delle colonne  
 Al momento dell'esecuzione, un report contenente una matrice si espande in genere orizzontalmente e verticalmente. Il controllo di espansione orizzontale è particolarmente importante quando si intende esportare il report in un formato quale Microsoft Word o Adobe PDF utilizzato per i report stampati. Se il report si espande orizzontalmente su più pagine, sarà difficile interpretare il report stampato. Per contenere l'espansione orizzontale, è possibile ridimensionare le colonne alla larghezza minima necessaria per visualizzare i dati su una sola riga. È inoltre possibile rinominare le colonne in modo che i relativi titoli si adattino alla larghezza necessaria per visualizzare i dati.  
  
#### <a name="to-rename-and-resize-the-columns"></a>Per rinominare e ridimensionare le colonne  
  
1.  Fare clic su **Progettazione** per tornare alla visualizzazione Struttura.  
  
2.  Selezionare il testo nella colonna Quantity all'estrema sinistra, quindi digitare **QTA**.  
  
     Il titolo della colonna corrisponderà a QTA.  
  
3.  Ripetere il passaggio 2 per le altre colonne denominate Quantity, ovvero due delle colonne presenti.  
  
4.  Fare clic nella matrice in modo che vengano visualizzati gli handle di riga e di colonna sopra e accanto alla matrice.  
  
     Le barre grigie lungo la parte superiore e laterale della tabella sono gli handle di riga e di colonna.  
  
5.  Per ridimensionare la colonna della quantità all'estrema destra, posizionare il puntatore del mouse sulla riga posta tra gli handle di colonna in modo che il cursore assuma la forma di una doppia freccia. Trascinare la colonna verso sinistra fino a quando non raggiunge una larghezza di 1 centimetro circa.  
  
     Una larghezza di colonna di circa 1 centimetro è ideale per visualizzare la quantità.  
  
6.  Ripetere il passaggio 5 per le altre colonne denominate QTA.  
  
7.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
 Le colonne del report contenenti le quantità risulteranno ora denominate QTA e saranno più strette.  
  
##  <a name="6-merge-matrix-cells"></a><a name="MergeCells"></a>6. unire le celle della matrice  
 L'area dell'angolo si trova in corrispondenza dell'angolo superiore sinistro della matrice. Il numero di celle nell'area dell'angolo varia a seconda del numero di righe e di gruppi di colonne presenti nella matrice. La matrice creata in questa esercitazione dispone di quattro celle nell'area dell'angolo corrispondente. Le celle vengono disposte in due righe e due colonne, in modo da riflettere il livello delle gerarchie di gruppo di righe e colonne. Le quattro celle non vengono utilizzate in questo report e verranno unite in un'unica cella.  
  
#### <a name="to-merge-matrix-cells"></a>Per unire le celle della matrice  
  
1.  Fare clic su **Progettazione** per tornare alla visualizzazione Struttura.  
  
2.  Fare clic nella matrice in modo che vengano visualizzati gli handle di riga e di colonna sopra e accanto alla matrice.  
  
3.  Premere CTRL e selezionare quindi le quattro celle d'angolo.  
  
4.  Fare clic con il pulsante destro del mouse sulle celle, quindi scegliere **Unisci celle**.  
  
5.  Fare clic con il pulsante destro del mouse sulla cella d'angolo, quindi scegliere **Proprietà casella di testo**.  
  
6.  Fare clic sulla scheda **Riempimento** .  
  
7.  Fare clic sul pulsante (***FX***) per **colore riempimento**.  
  
8.  Copiare e incollare l'espressione seguente nella casella dell'espressione:  
  
    ```  
    #96a4b2  
    ```  
  
     Si tratta del valore esadecimale RGB per un colore blu grigio utilizzato nello stile Ardesia.  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
 La matrice nell'angolo superiore è costituita da un'unica cella e ha lo stesso colore delle celle del gruppo di righe e del gruppo di colonne.  
  
##  <a name="7-add-a-report-header-and-report-title"></a><a name="HeaderTitle"></a>7. aggiungere un'intestazione e un titolo al report  
 Nella parte superiore del report viene visualizzato il titolo del report. È possibile posizionare il titolo del report in un'apposita intestazione oppure, se ne è privo, in una casella di testo nella parte superiore del corpo del report. In questa esercitazione verrà rimossa la casella di testo nella parte superiore del report e verrà aggiunto un titolo all'intestazione.  
  
#### <a name="to-add-a-report-header-and-report-title"></a>Per aggiungere un'intestazione e un titolo al report  
  
1.  Fare clic su **Progettazione** per tornare alla visualizzazione Struttura.  
  
2.  Fare clic sulla casella di testo nella parte superiore del corpo del report che contiene **clic per aggiungere il titolo**, quindi premere il tasto CANC.  
  
3.  Nella scheda **Inserisci** della barra multifunzione fare clic su **intestazione** e quindi su **Aggiungi intestazione**.  
  
     Nella parte superiore del corpo del report verrà aggiunta un'intestazione.  
  
4.  Nella scheda **Inserisci** fare clic su **Casella di testo**, quindi trascinare una casella di testo nell'intestazione del report. Assegnare alla casella di testo una lunghezza di circa 15 centimetri e un'altezza di circa 2 centimetri e posizionarla nella parte sinistra dell'intestazione del report.  
  
5.  Nella casella di testo digitare **Vendite per territorio, sottocategoria e giorno**.  
  
6.  Selezionare il testo digitato, fare clic con il pulsante destro del mouse e quindi scegliere **Proprietà testo**.  
  
    > [!NOTE]  
    >  Per applicare contemporaneamente la formattazione, è necessario che i caratteri siano contigui.  
  
7.  Nella finestra di dialogo **Proprietà testo** fare clic su **tipo di carattere**.  
  
8.  Nell'elenco **tipo di carattere** selezionare **Times New Roman**; in **dimensioni** selezionare **24 PT**, in **colore** selezionare **marrone**e in **stile** selezionare **corsivo**.  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
 Nel report visualizzato è incluso il titolo di un report nella relativa intestazione.  
  
##  <a name="8-save-the-report"></a><a name="Save"></a>8. salvare il report  
 È possibile salvare i report in un server di report, in una raccolta di SharePoint o nel computer locale.  
  
 In questa esercitazione il report verrà salvato in un server di report. Se non si dispone dell'accesso a un server di report, sarà possibile salvare il report nel computer locale.  
  
#### <a name="to-save-the-report-on-a-report-server"></a>Per salvare il report in un server di report  
  
1.  Fare clic sul pulsante **Generatore report** , quindi su **Salva con nome**.  
  
2.  Fare clic su **Siti e server recenti**.  
  
3.  Selezionare o digitare il nome del server di report per il quale si dispone delle autorizzazioni di salvataggio dei report.  
  
     Verrà visualizzato il messaggio "Connessione al server di report". Al termine della connessione, verrà visualizzato il contenuto della cartella di report specificata dall'amministratore del server di report come posizione predefinita per i report.  
  
4.  In **Nome**sostituire il nome predefinito con **VenditePerTerritorioSottocategoria**.  
  
5.  Fare clic su **Save**.  
  
 Il report verrà salvato sul server di report. Il nome del server di report al quale si è connessi verrà visualizzato sulla barra di stato nella parte inferiore della finestra.  
  
#### <a name="to-save-the-report-on-your-computer"></a>Per salvare il report nel computer  
  
1.  Fare clic sul pulsante **Generatore report** , quindi su **Salva con nome**.  
  
2.  Fare clic su **Desktop**, **Documenti**o **Risorse del computer**, quindi selezionare la cartella in cui si desidera salvare il report.  
  
3.  In **Nome**sostituire il nome predefinito con **VenditePerTerritorioSottocategoria**.  
  
4.  Fare clic su **Save**.  
  
##  <a name="9-optional-rotate-text-box-270-degrees"></a><a name="RotateTextBox"></a>9. (facoltativo) ruotare la casella di testo 270 gradi  
 Al momento dell'esecuzione, un report con matrici può espandersi orizzontalmente e verticalmente. La rotazione verticale, o di 270 gradi, delle caselle di testo consente di risparmiare spazio orizzontale. Il report visualizzabile risulterà quindi più stretto e nel caso venga esportato in un formato quale Microsoft Word si adatterà con maggiore facilità alle dimensioni della pagina stampata.  
  
 Il testo in una casella di testo può inoltre essere visualizzato in senso orizzontale e verticale (dall'alto in basso). Per altre informazioni, vedere [Caselle di testo &#40;Generatore report e SSRS&#41;](report-design/text-boxes-report-builder-and-ssrs.md).  
  
#### <a name="to-rotate-text-box-270-degrees"></a>Per ruotare una casella di testo di 270 gradi  
  
1.  Fare clic su **Progettazione** per tornare alla visualizzazione Struttura.  
  
2.  Fare clic sulla cella contenente `[Territory].`  
  
3.  Nel riquadro Proprietà individuare la proprietà WritingMode e nell'elenco a discesa selezionare **Rotate270**.  
  
     Se il riquadro Proprietà non viene visualizzato, fare clic sulla scheda **Visualizza** e selezionare **Proprietà**.  
  
4.  Verificare che la proprietà CanGrow sia impostata su `True`.  
  
5.  Ridimensionare la colonna Territory assegnandole una larghezza di circa 1 centimetro ed eliminare il titolo della colonna.  
  
6.  Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
 Il nome dell'area risulterà scritto in senso verticale, dal basso verso l'alto. L'altezza del gruppo di righe Territory dipenderà dalla lunghezza del nome del territorio.  
  
## <a name="next-steps"></a>Passaggi successivi  
 L'esercitazione sulla creazione di un report matrice è terminata. Per ulteriori informazioni sulle matrici, vedere [tabelle, matrici ed elenchi &#40;Generatore report e ssrs&#41;](report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md), [matrici &#40;Generatore report e SSRS&#41;](report-design/create-a-matrix-report-builder-and-ssrs.md), [aree dell'area dati tablix &#40;Generatore report e SSRS&#41;](report-design/tablix-data-region-areas-report-builder-and-ssrs.md)e [celle, righe e colonne dell'area dati Tablix &#40;Generatore report&#41; e SSRS](report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Esercitazioni &#40;Generatore report&#41;](report-builder-tutorials.md)   
 [Generatore report in SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)  
  
  
