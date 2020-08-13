---
title: 'Esercitazione: Aggiungere un parametro al report (Generatore report) | Microsoft Docs'
description: Informazioni su come aggiungere un parametro in un report impaginato di Reporting Services per consentire ai lettori del report di filtrare i dati in base a uno o più valori.
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: eab34ec4-b3ad-4a76-95cc-07b2f75ee6d7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: cd5fab649fc481bdb91b42c34be33f5976b5af93
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87245678"
---
# <a name="tutorial-add-a-parameter-to-your-report-report-builder"></a>Esercitazione: Aggiungere un parametro al report (Generatore report)
In questa esercitazione viene aggiunto un parametro in un report impaginato di [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] per consentire ai lettori del report di filtrare i dati in base a uno o più valori. 
  
![report-builder-parameter-tutorial](../reporting-services/media/report-builder-parameter-tutorial.png)

I parametri di report vengono creati automaticamente per ogni parametro di query incluso in una query del set di dati. Il tipo di dati determina il modo in cui il parametro viene presentato sulla barra degli strumenti della visualizzazione report. 
   
> [!NOTE]  
> In questa esercitazione, i passaggi per la procedura guidata sono consolidati in un'unica procedura. Per istruzioni dettagliate su come selezionare un server di report, come scegliere un'origine dati e come creare un set di dati, vedere la prima esercitazione di questa serie: [Esercitazione: Creazione di un report tabella semplice &#40;Generatore report&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
Tempo stimato per il completamento dell'esercitazione: 25 minuti  
  
## <a name="requirements"></a>Requisiti  
Per informazioni sui requisiti, vedere [Prerequisiti per le esercitazioni &#40;Generatore report&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="1-create-a-matrix-report-and-dataset-in-the-table-or-matrix-wizard"></a><a name="Setup"></a>1. Creare un report matrice e un set di dati nella Creazione guidata tabella o matrice  
Creare un report matrice, un'origine dati e un set di dati.  
  
> [!NOTE]  
> Nella query di questa esercitazione sono contenuti i valori dei dati in modo che non sia necessaria un'origine dati esterna. Tale condizione rende tuttavia la query piuttosto lunga. In una query di un ambiente aziendale non sarebbe incluso alcun dato. Questo esempio è solo a scopo illustrativo.  
  
### <a name="to-create-a-new-matrix-report"></a>Per creare un nuovo report matrice  
  
1.  [Avviare Generatore report](../reporting-services/report-builder/start-report-builder.md) dal computer, dal portale Web di [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] o in modalità integrata SharePoint.  
  
    Si apre la finestra di dialogo **Nuovo report o set di dati** .  
  
    Se la finestra di dialogo **Nuovo report o set di dati** non viene visualizzata, scegliere **Nuovo** dal menu **File**.  
  
2.  Nel riquadro sinistro assicurarsi che sia selezionata l'opzione **Nuovo report** .  
  
3.  Nel riquadro destro fare clic su **Creazione guidata tabella o matrice**.  
  
4.  Nella pagina **Scegliere un set di dati** fare clic su **Crea un set di dati** > **Avanti**.  
  
7.  Nella pagina **Scegliere una connessione a un'origine dei dati** selezionare un'origine dati dall'elenco o passare al server di report per selezionarne una. Selezionare un'origine dati di tipo **SQL Server**.  
      
8.  Fare clic su **Avanti**.  

    Potrebbe essere necessario immettere le credenziali.    
     
9. Nella pagina **Progetta query** fare clic su **Modifica come testo**.  
  
10. Incollare la query seguente nel riquadro vuoto superiore:  
  
    ```  
    ;WITH CTE (StoreID, Subcategory, Quantity)   
    AS (  
    SELECT 200 AS StoreID, 'Digital SLR Cameras' AS Subcategory, 2002 AS Quantity  
    UNION SELECT  200 AS StoreID, 'Camcorders' AS Subcategory, 1954 AS Quantity  
    UNION SELECT  200 AS StoreID, 'Accessories' AS Subcategory, 1895 AS Quantity  
    UNION SELECT  199 AS StoreID, 'Digital Cameras' AS Subcategory, 1849 AS Quantity  
    UNION SELECT  306 AS StoreID, 'Digital SLR Cameras' AS Subcategory, 1579 AS Quantity  
    UNION SELECT  306 AS StoreID, 'Camcorders' AS Subcategory, 1561 AS Quantity  
    UNION SELECT  306 AS StoreID, 'Digital Cameras' AS Subcategory, 1553 AS Quantity  
    UNION SELECT  306 AS StoreID, 'Accessories' AS Subcategory, 1534 AS Quantity  
    UNION SELECT 307 AS StoreID, 'Accessories' AS Subcategory, 1755 AS Quantity  
    UNION SELECT 307 AS StoreID, 'Camcorders' AS Subcategory, 1631 AS Quantity  
    UNION SELECT 307 AS StoreID, 'Digital SLR Cameras' AS Subcategory, 1772 AS Quantity)  
    SELECT StoreID, Subcategory, Quantity  
    FROM CTE  
    ```  
  
    Questa query combina i risultati di diverse istruzioni SELECT di [!INCLUDE[tsql_md](../includes/tsql-md.md)] in un'espressione di tabella comune per specificare valori basati sui dati di vendita semplificati per le fotocamere del database di esempio Contoso. Le sottocategorie sono costituite da fotocamere digitali, fotocamere single lens reflex (SLR), cineprese e accessori.  
  
11. Sulla barra degli strumenti di Progettazione query fare clic su **Esegui** ( **!** ) per visualizzare i dati.   
  
    Il set di risultati include 11 righe di dati che mostrano la quantità di articoli venduti per ogni sottocategoria in quattro punti vendita nelle colonne seguenti: StoreID, Subcategory, Quantity. Il nome del punto vendita non è incluso nel set di risultati. Più avanti in questa esercitazione, si cercherà il nome del punto vendita che corrisponde all'identificatore del punto vendita in un set di dati separato.  
  
    Questa query non contiene parametri di query. Verranno aggiunti più avanti in questa esercitazione.   
  
12. Fare clic su **Avanti**.  
  
## <a name="2-organize-data-and-choose-layout-in-the-wizard"></a><a name="CompleteWizard"></a>2. Organizzare i dati e scegliere il layout nella procedura guidata  
La procedura guidata offre una progettazione iniziale per la visualizzazione dei dati. Il riquadro di anteprima nella procedura guidata consente di visualizzare il risultato del raggruppamento di dati prima di completare la progettazione della tabella o della matrice.  
  
### <a name="to-organize-data-into-groups"></a>Per organizzare i dati in gruppi  
  
1.  Nella pagina **Disponi campi** trascinare Subcategory in **Gruppi di righe**.  
  
2.  Trascinare StoreID in **Gruppi di colonne**.  
  
3.  Trascinare Quantity in **Valori**.  
  
    I valori delle quantità vendute sono stati organizzati in righe raggruppate per sottocategoria, con una colonna per ogni punto vendita.  
  
4.  Fare clic su **Avanti**.  
  
5.  Nella pagina **Scegliere il layout** in **Opzioni**verificare che la casella **Mostra subtotali e totali complessivi** sia selezionata.  
  
    Quando si esegue il report, nell'ultima colonna verrà mostrata la quantità totale di ogni sottocategoria per tutti i punti vendita mentre nell'ultima riga verrà mostrata la quantità totale per tutte le sottocategorie per ogni punto vendita.  
  
6.  Fare clic su **Avanti**.  
  
8.  Fare clic su **Fine**.  
  
    La matrice viene aggiunta all'area di progettazione. Nella matrice sono visualizzate tre colonne e tre righe. Il contenuto delle celle nella prima riga è Sottocategoria, [StoreID] e Totale. Nelle celle della seconda riga sono visualizzate le espressioni che rappresentano la sottocategoria, la quantità di articoli venduti per ogni punto vendita e la quantità totale per ogni sottocategoria per tutti i punti vendita. Nelle celle della riga finale è visualizzato il totale complessivo per ogni punto vendita.  
      
    ![ssRB_ParamTut_Design](../reporting-services/media/ssrb-paramtut-design.png)  
  
9. Fare clic nella matrice, posizionare il puntatore sul bordo della prima colonna, fare clic sul quadratino di ridimensionamento ed espandere la larghezza della colonna.  
  
   ![ssRB_ParamTut_Drag](../reporting-services/media/ssrb-paramtut-drag.png)  
  
10. Fare clic su **Esegui** per visualizzare l'anteprima del report.  
  
Il report verrà eseguito nel server di report, con il titolo e l'ora di elaborazione del report visualizzati.  

![ssRB_ParamTut__Preview1](../reporting-services/media/ssrb-paramtut-preview1.png)
  
Le intestazioni di colonna visualizzano l'identificatore ma non il nome del punto vendita. Più avanti in questa esercitazione, verrà aggiunta un'espressione per cercare il nome del punto vendita in un set di dati che contiene la coppia identificatore/nome del punto vendita.  
  
## <a name="3-add-a-query-parameter-to-create-a-report-parameter"></a><a name="Query"></a>3. Aggiungere un parametro di query per creare un parametro di report  
Quando si aggiunge un parametro di query a una query, in Generatore report viene creato automaticamente un parametro di report a valore singolo con proprietà predefinite per nome, messaggio di richiesta e tipo di dati.  
  
### <a name="to-add-a-query-parameter"></a>Per aggiungere un parametro di query  
  
1.  Fare clic su **Progettazione** per tornare alla visualizzazione della struttura.  
  
2.  Nel riquadro Dati report espandere la cartella **Set di dati** , fare clic con il pulsante destro del mouse su **DataSet1**e quindi fare clic su **Query**.  
  
3.  Aggiungere la seguente clausola [!INCLUDE[tsql](../includes/tsql-md.md)] **WHERE** come ultima riga della query:  
  
    ```  
    WHERE StoreID = (@StoreID)  
    ```  
  
    La clausola **WHERE** limita i dati recuperati all'identificatore del punto vendita specificato dal parametro di query *\@StoreID*.  
  
4.  Nella barra degli strumenti Progettazione query fare clic su **Esegui** ( **!** ). Si aprirà la finestra di dialogo **Definisci parametri query** nella quale viene richiesto un valore per il parametro di query *\@StoreID*.  
  
5.  In **Valore parametro**digitare **200**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    Nel set di risultati vengono visualizzate le quantità vendute di accessori, cineprese e fotocamere SLR digitali per l'identificatore del punto vendita **200**.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Nel riquadro Dati report espandere la cartella **Parametri** .  
  
Si noti che è ora presente un parametro del report denominato *\@StoreID* e un riquadro Parametri in cui è possibile visualizzare i parametri del report.   
  
![ssRB_ParamPane](../reporting-services/media/ssrb-parampane.png)  
  
Non è visualizzato un riquadro Parametri? Nel menu **Visualizza** selezionare **Parametri**.  
  
## <a name="4-change-default-data-type-and-other-properties-for-a-report-parameter"></a><a name="ChangeDefaultProperties"></a>4. Modificare il tipo di dati e altre proprietà predefiniti per un parametro di report  
Dopo aver creato un parametro di report, è possibile impostare i valori predefiniti per le proprietà.  
  
### <a name="to-change-the-default-data-type-for-a-report-parameter"></a>Per modificare il tipo di dati predefinito per un parametro di report  
  
Per impostazione predefinita, il parametro creato ha il tipo di dati **Text**. Poiché l'identificatore del punto vendita è un intero, è possibile modificare il tipo di dati in Integer.  
  
1.  Nel riquadro Dati report nel nodo **Parametri** fare clic con il pulsante destro del mouse su *\@StoreID*, quindi fare clic su **Proprietà parametri**.  
  
2.  In **Messaggio di richiesta**digitare **Identificatore punto vendita?** Questo testo viene visualizzato nella barra degli strumenti del visualizzatore di report quando si esegue il report.  
  
3.  In **Tipo di dati**selezionare **Integer**nell'elenco a discesa.  
  
4.  Accettare i valori predefiniti rimanenti nella finestra di dialogo.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  Fare clic su **Esegui** per visualizzare l'anteprima del report. Il visualizzatore di report visualizza il messaggio di richiesta **Identificatore punto vendita?** per *\@StoreID*.  
  
7.  Nella barra degli strumenti del visualizzatore di report, accanto a Store ID, digitare **200**e quindi fare clic su **Visualizza report**.  
  
![SSRB_ParamTutStoreID](../reporting-services/media/ssrb-paramtutstoreid.png)  
  
## <a name="4a-add-a-dataset-to-provide-available-values-and-display-names"></a><a name="AddDataset"></a>4a. Aggiungere un set di dati per fornire i valori disponibili e i nomi visualizzati  
Per assicurarsi che i lettori del report digitino solo valori validi per un parametro, è possibile creare un elenco a discesa di valori tra cui scegliere. I valori possono provenire da un set di dati o da un elenco che si specifica. I valori disponibili devono provenire da un set di dati con una query che non contiene un riferimento al parametro.  
  
### <a name="to-create-a-dataset-for-valid-values-for-a-parameter"></a>Per creare un set di dati per i valori validi per un parametro  
  
1.  Fare clic su **Progettazione** per passare alla visualizzazione della struttura.  
  
2.  Nel riquadro Dati report fare clic con il pulsante destro del mouse sula cartella **Datasets** e quindi fare clic su **Aggiungi set di dati**.  
  
3.  In **Nome**digitare **Punti vendita**.  
  
4.  Scegliere **Utilizzare un set di dati incorporato nel report**.  
  
5.  In **Origine dati**scegliere l'origine dati usata nella prima procedura dall'elenco a discesa.  
  
6.  In **Tipo di query**verificare che sia selezionata l'opzione **Testo** .  
  
7.  In **Query**incollare il testo seguente:  
  
    ```  
    SELECT 200 AS StoreID, 'Contoso Catalog Store' as StoreName  
    UNION SELECT 199 AS StoreID, 'Contoso North America Online Store' as StoreName  
    UNION SELECT 307 AS StoreID, 'Contoso Asia Online Store' as StoreName  
    UNION SELECT 306 AS StoreID, 'Contoso Europe Online Store' as StoreName  
    ```  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    Nel riquadro Dati report sono visualizzati i campi StoreID e StoreName nel nodo del set di dati **Punti vendita** .  
  
## <a name="4b-specify-available-values-to-show-in-a-list"></a><a name="AvailableValues"></a>4b. Specificare i valori disponibili da visualizzare in un elenco 
Dopo aver creato un set di dati per offrire i valori disponibili, modificare le proprietà del report per specificare il set di dati e il campo da usare per popolare l'elenco a discesa di valori validi nella barra degli strumenti del visualizzatore di report.  
  
### <a name="to-provide-available-values-for-a-parameter-from-a-dataset"></a>Per fornire i valori disponibili per un parametro da un set di dati  
  
1.  Nel riquadro Dati report fare clic con il pulsante destro del mouse sul parametro *\@StoreID*, quindi scegliere **Proprietà parametri**.  
  
2.  Fare clic su **Valori disponibili**e quindi su **Ottieni valori da una query**.  
  
3.  In **Set di dati**fare clic su **Punti vendita**nell'elenco a discesa.  
  
4.  In **Campo valori**fare clic su StoreID nell'elenco a discesa.  
  
5.  In **Campo etichette**fare clic su StoreName nell'elenco a discesa. Il campo etichette consente di specificare il nome visualizzato per il valore.  
  
6.  Fare clic su **Generale**.  
  
7.  In **Prompt**modificare **Identificatore punto vendita?** in **Nome punto vendita?**  
  
    I lettori del report effettueranno ora la selezione da un elenco di nomi di punti vendita anziché un elenco di identificatori. Si noti che il tipo di dati del parametro rimane **Integer** perché il parametro si basa sull'identificatore del punto vendita, non sul nome.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. Visualizzare l'anteprima del report.  
  
    Nella barra degli strumenti del visualizzatore di report, la casella di testo del parametro è ora un elenco a discesa denominato **Selezionare un valore**.  
  
10. Nell'elenco a discesa selezionare Contoso Catalog Store e quindi fare clic su **Visualizza report**.  
  
Nel report viene visualizzata la quantità venduta di accessori, cineprese e fotocamere SLR digitali per l'identificatore del punto vendita **200**.  
  
## <a name="4c-specify-a-default-value"></a><a name="DefaultValues"></a>4c. Specificare un valore predefinito 
È possibile specificare un valore predefinito per ciascun parametro in modo che il report venga eseguito automaticamente.  
  
### <a name="to-specify-a-default-value-from-a-dataset"></a>Per specificare un valore predefinito da un set di dati  
  
1.  Passare alla Visualizzazione della struttura.  
  
2.  Nel riquadro Dati report fare clic con il pulsante destro del mouse su *\@StoreID*, quindi scegliere **Proprietà parametri**.  
  
3.  Fare clic su **Valori predefiniti**e quindi su **Ottieni valori da una query**.  
  
4.  In **Set di dati**fare clic su **Punti vendita**nell'elenco a discesa.  
  
5.  In **Campo valori**fare clic su StoreID nell'elenco a discesa.  
  
6.  [!INCLUDE[clickOK_md](../includes/clickok-md.md)]  
  
7.  Visualizzare l'anteprima del report.  
  
Per *\@StoreID*, nel Visualizzatore di report viene visualizzato il valore "Contoso America del Nord Online Store" perché è il primo valore del set di risultati per il set di dati **Punti vendita**. Nel report viene visualizzata la quantità venduta di fotocamere digitali per l'identificatore del punto vendita **199**.  
  
### <a name="to-specify-a-custom-default-value"></a>Per specificare un valore predefinito personalizzato  
  
1.  Passare alla Visualizzazione della struttura.  
  
2.  Nel riquadro Dati report fare clic con il pulsante destro del mouse su *\@StoreID*, quindi scegliere **Proprietà parametri**.  
  
3.  Fare clic su **Valori predefiniti** > **Specifica valori** > **Aggiungi**. Verrà aggiunta una nuova riga di valori.  
  
4.  In **Valore**digitare **200**.  
  
5.  [!INCLUDE[clickOK_md](../includes/clickok-md.md)] 
  
6.  Visualizzare l'anteprima del report.  
  
Nel visualizzatore di report per *\@StoreID* viene visualizzato "Contoso Catalog Store" poiché si tratta del nome visualizzato per l'identificatore di punto vendita **200**. Nel report viene visualizzata la quantità venduta di accessori, cineprese e fotocamere SLR digitali per l'identificatore del punto vendita **200**.  
  
## <a name="4d-look-up-a-namevalue-pair"></a><a name="NameValue"></a>4d. Cercare una coppia nome/valore  
Un set di dati potrebbe contenere sia l'identificatore e che il campo del nome corrispondente. Quando si dispone solo di un identificatore, è possibile cercare il nome corrispondente in un set di dati creato che include coppie nome/valore.  
  
### <a name="to-look-up-a-value-from-a-dataset"></a>Per cercare un valore in un set di dati  
  
1.  Passare alla Visualizzazione della struttura.  
  
2.  Nell'area di progettazione nella matrice nell'intestazione di colonna della prima riga fare clic con il pulsante destro del mouse su `[StoreID]` e fare clic su **Espressione**.  
  
3.  Nel riquadro dell'espressione eliminare qualsiasi testo eccetto il **segno di uguale** (=) iniziale.  
  
4.  In **Categoria**espandere **Funzioni comuni**e fare clic su **Varie**. Nel riquadro Elemento è visualizzato un set di funzioni.  
  
5.  In Elemento fare doppio clic su **Ricerca**. Nel riquadro dell'espressione viene visualizzato `=Lookup(`. Nel riquadro Esempio viene visualizzato un esempio di sintassi di Lookup.  
  
6.  Digitare l'espressione seguente: 

    ```  
    =Lookup(Fields!StoreID.Value,Fields!StoreID.Value,Fields!StoreName.Value,"Stores")      
    ```  
  
    La funzione di ricerca accetta il valore per StoreID, lo cerca nel set di dati "Punti vendita" e restituisce il valore StoreName.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    Nell'intestazione di colonna del punto vendita è contenuto il testo visualizzato per un'espressione complessa: **Expr**.  
  
8.  Visualizzare l'anteprima del report.  
  
L'intestazione di colonna nella parte superiore di ogni colonna visualizza il nome del punto vendita anziché l'identificatore.  
  
## <a name="5-display-the-selected-parameter-value-in-the-report"></a><a name="Expression"></a>5. Visualizzare il valore del parametro selezionato nel report  
Quando un lettore ha delle domande su un report, è utile sapere quali valori di parametri sono stati scelti. È possibile mantenere i valori selezionati dall'utente per ogni parametro nel report. Un modo consiste nel visualizzare i parametri in una casella di testo nel piè di pagina della pagina.  
  
### <a name="to-display-the-selected-parameter-value-and-label-on-a-page-footer"></a>Per visualizzare il valore del parametro selezionato e l'etichetta nel piè di pagina di una pagina  
  
1.  Passare alla Visualizzazione della struttura.  
  
2.  Fare clic con il pulsante destro del mouse sul piè di pagina della pagina > **Inserisci** > **Casella di testo**. Trascinare la casella di testo accanto alla casella di testo con il timestamp. Fare clic sul quadratino di ridimensionamento laterale della casella di testo ed espanderla in larghezza.  
  
3.  Trascinare il parametro *\@StoreID* dal riquadro Dati report nella casella di testo. Nella casella di testo viene visualizzato `[@StoreID]`.  
  
4.  Per visualizzare l'etichetta del parametro, fare clic nella casella di testo finché il cursore di inserimento non viene visualizzato dopo l'espressione esistente, immettere uno spazio, quindi trascinare un'altra copia del parametro dal riquadro dei dati del report nella casella di testo. Nella casella di testo viene visualizzato `[@StoreID] [@StoreID]`.  
  
5.  Fare clic con il pulsante destro del mouse sulla prima occorrenza di `[@StoreID]` e quindi fare clic su **Espressione**. Verrà visualizzata la finestra di dialogo **Espressione** . Sostituire il testo `Value` con `Label`.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    Verrà visualizzato il testo: `[@StoreID.Label] [@StoreID]`.  
  
7.  Visualizzare l'anteprima del report.  
  
## <a name="6-use-the-report-parameter-in-a-filter"></a><a name="Filter"></a>6. Utilizzare il parametro del report in un filtro  
I filtri consentono di controllare quali dati utilizzare in un report dopo averli recuperati da un'origine dati esterna. Per consentire ai lettori del report di controllare i dati visualizzati, è possibile includere il parametro del report in un filtro per la matrice.  
  
### <a name="to-specify-a-parameter-in-a-matrix-filter"></a>Per specificare un parametro in un filtro della matrice  
  
1.  Passare alla Visualizzazione della struttura.  
  
2.  Fare clic con il pulsante destro del mouse sul quadratino di ridimensionamento dell'intestazione di una riga o colonna della matrice e quindi fare clic su **Proprietà Tablix**.  
  
3.  Fare clic su **Filtri**e quindi su **Aggiungi**. Verrà visualizzata una nuova riga del filtro.  
  
4.  In **Espressione**selezionare il campo del set di dati StoreID nell'elenco a discesa. I dati visualizzati sono di tipo **Integer**. Se il valore dell'espressione è un campo del set di dati, il tipo di dati viene impostato automaticamente.  
  
5.  In **Operatore**verificare che sia selezionato il **segno di uguale** (=).  
  
6.  In **Valore**digitare `[@StoreID]`. 

    `[@StoreID]` è la sintassi dell'espressione semplice che rappresenta `=Parameters!StoreID.Value`.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Visualizzare l'anteprima del report.  
  
    La matrice visualizza dati solo per "Contoso Catalog Store".  
  
9. Nella barra degli strumenti del visualizzatore di report, per **Nome punto vendita?** selezionare **Contoso Asia Online Store**e quindi fare clic su **Visualizza report**.  
  
La matrice visualizza dati che corrispondono al punto vendita che è stato selezionato.  
  
## <a name="7-change-the-report-parameter-to-accept-multiple-values"></a><a name="Multivalued"></a>7. Modificare il parametro di report in modo che vengano accettati più valori  
Per modificare un parametro da singolo a multivalore, è necessario modificare la query e tutte le espressioni che contengono un riferimento a quel parametro, inclusi i filtri. Un parametro multivalore è una matrice di valori. In una query del set di dati, la sintassi della query deve verificare l'inclusione di un valore in un set di valori. In un'espressione di report, la sintassi dell'espressione deve accedere a una matrice di valori anziché a un valore singolo.  
  
### <a name="to-change-a-parameter-from-single-to-multivalued"></a>Per modificare un parametro da singolo a multivalore  
  
1.  Passare alla Visualizzazione della struttura.  
  
2.  Nel riquadro Dati report fare clic con il pulsante destro del mouse su *\@StoreID*, quindi scegliere **Proprietà parametri**.  
  
3.  Selezionare **Consenti più valori**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  Nel riquadro Dati report espandere la cartella **Set di dati** , fare clic con il pulsante destro del mouse su **DataSet1**e quindi fare clic su **Query**.  
  
6.  Modificare il **segno di uguale** (=) in **IN** nella clausola [!INCLUDE[tsql](../includes/tsql-md.md)] **WHERE** nell'ultima riga della query:  
  
    ```  
    WHERE StoreID IN (@StoreID)  
    ```  
  
    L'operatore **IN** verifica un valore per l'inclusione in un set di valori.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Fare clic con il pulsante destro del mouse sul quadratino di ridimensionamento dell'intestazione di una riga o colonna della matrice e quindi fare clic su **Proprietà Tablix**.  
  
9. Fare clic su **Filtri**.  
  
10. In **Operatore**selezionare **In**.  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. Nella casella di testo in cui è visualizzato il parametro nel piè di pagina, eliminare qualsiasi testo.  
  
13. Fare clic con il pulsante destro del mouse sulla casella di testo e quindi fare clic su **Espressione**. Digitare l'espressione seguente: `=Join(Parameters!StoreID.Label, ", ")`  
  
    Questa espressione concatena tutti i nomi dei punti vendita che l'utente ha selezionato, separati da una virgola e uno spazio.  
  
14. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
15. Fare clic nella casella di testo che precede l'espressione appena creata e quindi digitare quanto segue: 

    **Valori del parametro selezionati:** 
  
16. Visualizzare l'anteprima del report.  
  
17. Fare clic sull'elenco a discesa accanto a Nome punto vendita?  
  
    Ogni valore valido appare accanto a una casella di controllo.  
  
18. Fare clic su **Seleziona tutto**quindi fare clic su **Visualizza report**.  
  
    Il report visualizza la quantità venduta per tutte le sottocategorie per tutti i punti vendita.  
  
19. Dall'elenco a discesa fare clic su **Seleziona tutto** per cancellare l'elenco, fare clic su "Contoso Catalog Store" e "Contoso Asia Online Store" e quindi scegliere **Visualizza report**.  

    ![report-builder-parameter-multiselect](../reporting-services/media/report-builder-parameter-multiselect.png)
  
 
## <a name="8-add-a-boolean-parameter-for-conditional-visibility"></a><a name="Boolean"></a>8. Aggiungere un parametro booleano per la visibilità condizionale  
  
### <a name="to-add-a-boolean-parameter"></a>Per aggiungere un parametro booleano  
  
1.  Nell'area di progettazione nel riquadro Dati report fare clic con il pulsante destro del mouse su **Parametri**e fare clic su **Aggiungi parametro**.  
  
2.  Nella casella **Nome**digitare ShowSelections.  
  
3.  In **Messaggio di richiesta**digitare Mostra selezioni?  
  
4.  In **Tipo di dati**, fare clic su **booleano**.  
  
5.  Fare clic su **Valori predefiniti**.  
  
6.  Fare clic su **Imposta valori**e quindi su **Aggiungi**.  
  
7.  In **Valore**digitare **False**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-set-visibility-based-on-a-boolean-parameter"></a>Per impostare la visibilità in base a un parametro booleano  
  
1.  Nell'area di progettazione fare clic con il pulsante destro del mouse nella casella di testo nel piè di pagina che visualizza i valori del parametro e quindi fare clic su **Proprietà casella di testo**.  
  
2.  Fare clic su **Visibilità**.  
  
3.  Selezionare l'opzione **Mostra o nascondi in base a un'espressione**e quindi fare clic sul pulsante di espressione **Fx**.  
  
4.  Digitare l'espressione seguente: `=Not Parameters!ShowSelections.Value`  
  
    L'opzione di visibilità della casella di testo viene controllata dalla proprietà Hidden. Applicare l'operatore **Not** in modo che quando viene selezionato il parametro, la proprietà Hidden sia impostata su false e venga visualizzata la casella di testo.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Visualizzare l'anteprima del report.  
  
    La casella di testo che visualizza le opzioni per il parametro nel piè di pagina non è visualizzata.  
  
8.  Nella barra degli strumenti del visualizzatore di report accanto a **Mostra selezioni**fare clic su **True** > **Visualizza report**.  
  
    Viene visualizzata la casella di testo nel piè di pagina contenente tutti i nomi di punto vendita selezionati.  
  
## <a name="9-add-a-report-title"></a><a name="Title"></a>9. Aggiungere un titolo al report  
  
### <a name="to-add-a-report-title"></a>Per aggiungere il titolo di un report  

1.  Passare alla Visualizzazione della struttura.  
   
1.  Nell'area di progettazione fare clic su **Fare clic per aggiungere il titolo**.  
  
2.  Digitare Vendite prodotto con parametri, quindi fare clic all'esterno della casella di testo.  
  
## <a name="10-save-the-report"></a><a name="Save"></a>10. Salvare il report  
  
### <a name="to-save-the-report-on-a-report-server"></a>Per salvare il report in un server di report  
  
1.  Fare clic sul pulsante **Generatore report** , quindi su **Salva con nome**.  
  
2.  Fare clic su **Siti e server recenti**.  
  
3.  Selezionare o digitare il nome del server di report per il quale si dispone delle autorizzazioni di salvataggio dei report.  
  
    Viene visualizzato il messaggio **Connessione al server di report**. Al termine della connessione, verrà visualizzato il contenuto della cartella di report specificata dall'amministratore del server di report come posizione predefinita per i report.  
  
4.  In **Nome**sostituire il nome predefinito con Report delle vendite con parametri.  
  
5.  Fare clic su **Salva**.  
  
Il report verrà salvato sul server di report. Il server di report al quale si è connessi verrà visualizzato sulla barra di stato nella parte inferiore della finestra.  
  
## <a name="next-steps"></a>Passaggi successivi  
Questa operazione conclude la procedura dettagliata per l'aggiunta di un parametro al report. Per altre informazioni sui parametri, vedere [Parametri report &#40;Generatore report e Progettazione report&#41;](../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
## <a name="see-also"></a>Vedere anche  
* [Esercitazioni di Generatore report](../reporting-services/report-builder-tutorials.md)
* [Generatore report in SQL Server](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
*  [Funzione Lookup](../reporting-services/report-design/report-builder-functions-lookup-function.md)   
