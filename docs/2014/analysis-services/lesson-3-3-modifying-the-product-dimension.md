---
title: Modifica della dimensione Product | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 8e3ffecd-7f40-41a8-8735-bc9858a310cb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 430ac56191fcfc2c601c50f9f31de128d5d58368
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62729307"
---
# <a name="modifying-the-product-dimension"></a>Modifica della dimensione Product
  Nelle attività di questo argomento si utilizzerà un calcolo denominato per fornire nomi più descrittivi per le linee di prodotti, si definirà una gerarchia nella dimensione Product e si specificherà il nome membro (Totale) per la gerarchia. Si raggrupperanno inoltre gli attributi in cartelle di visualizzazione.  
  
## <a name="adding-a-named-calculation"></a>Aggiunta di un calcolo denominato  
 È possibile aggiungere un calcolo denominato a una tabella in una vista origine dati. Nell'attività seguente verrà creato un calcolo denominato che consente di visualizzare il nome completo della linea di prodotti.  
  
#### <a name="to-add-a-named-calculation"></a>Per aggiungere un calcolo denominato  
  
1.  Per aprire la vista origine dati **Adventure Works DW 2012** , fare doppio clic su **Adventure Works DW 2012** nella cartella **Viste origine dati** in Esplora soluzioni.  
  
2.  Nella parte inferiore del riquadro diagramma fare clic con il pulsante destro del mouse sull'intestazione di tabella **Product** , quindi scegliere **Nuovo calcolo denominato**.  
  
3.  Nel **Crea calcolo denominato** finestra di dialogo, digitare `ProductLineName` nel **nome colonna** casella.  
  
4.  Nella casella **Espressione** digitare o copiare e incollare l'istruzione **CASE** seguente:  
  
    ```  
    CASE ProductLine  
       WHEN 'M' THEN 'Mountain'  
       WHEN 'R' THEN 'Road'  
       WHEN 'S' THEN 'Accessory'  
       WHEN 'T' THEN 'Touring'  
       ELSE 'Components'  
    END  
    ```  
  
     Con questa istruzione **CASE** vengono creati nomi descrittivi per ogni linea di prodotti nel cubo.  
  
5.  Fare clic su **OK** per creare il `ProductLineName` calcolo denominato. Potrebbe essere necessario attendere alcuni istanti.  
  
6.  Scegliere **Salva tutti** dal menu **File**.  
  
## <a name="modifying-the-namecolumn-property-of-an-attribute"></a>Modifica della proprietà NameColumn di un attributo  
  
#### <a name="to-modify-the-namecolumn-property-value-of-an-attribute"></a>Per modificare il valore della proprietà NameColumn di un attributo  
  
1.  Passare a Progettazione dimensioni per la dimensione Product. A tale scopo, fare doppio clic sulla dimensione **Product** nel nodo **Dimensioni** di Esplora soluzioni.  
  
2.  Nel riquadro **Attributi** della scheda **Struttura dimensione** selezionare **Product Line**.  
  
3.  Nella finestra proprietà sul lato destro dello schermo, scegliere il **NameColumn** campo nella parte inferiore della finestra proprietà e quindi fare clic su Sfoglia (**...** ) per aprire la **colonna nome** nella finestra di dialogo. Per aprire la finestra Proprietà, potrebbe essere necessario fare clic sulla scheda **Proprietà** sul lato destro dello schermo.  
  
4.  Selezionare `ProductLineName` nella parte inferiore della **Source column** elenco e quindi fare clic su **OK**.  
  
     Il campo NameColumn ora contiene il testo **Product.ProductLineName (WChar)**. I membri della gerarchia dell'attributo **Product Line** ora vengono visualizzati con il nome completo della linea di prodotti anziché con un nome abbreviato.  
  
5.  Nel riquadro **Attributi** della scheda **Struttura dimensione** selezionare **Product Key**.  
  
6.  Nella finestra Proprietà scegliere il **NameColumn** proprietà campo e quindi fare clic sui puntini (**...** ) per aprire la **colonna nome** nella finestra di dialogo.  
  
7.  Selezionare **EnglishProductName** nell'elenco **Colonna di origine** , quindi fare clic su **OK**.  
  
     Il campo NameColumn ora contiene il testo **Product.EnglishProductName (WChar)**.  
  
8.  Nella finestra Proprietà scorrere verso l'alto, fare clic sui **Name** campo della proprietà e quindi digitare `Product Name`.  
  
## <a name="creating-a-hierarchy"></a>Creazione di una gerarchia  
  
#### <a name="to-create-a-hierarchy"></a>Per creare una gerarchia  
  
1.  Trascinare l'attributo **Product Line** dal riquadro **Attributi** al riquadro **Gerarchie** .  
  
2.  Trascinare il **Model Name** dell'attributo dal **attributi** riquadro il  **\<nuovo livello >** cella il **gerarchie** riquadro, sotto il **linea di prodotti** livello.  
  
3.  Trascinare il `Product Name` dell'attributo dal **attributi** riquadro il  **\<nuovo livello >** cella il **gerarchie** riquadro, sotto il  **Nome modello** livello. L'attributo Product Key è stato rinominato in Product Name nella sezione precedente.  
  
4.  Nel **gerarchie** riquadro della finestra il **struttura dimensione** scheda, fare clic sulla barra del titolo del **gerarchia** gerarchia, fare clic su **rinominare** , quindi digitare `Product Model Lines`.  
  
     Il nome della gerarchia è ora `Product Model Lines`.  
  
5.  Scegliere **Salva tutti** dal menu **File**.  
  
## <a name="specifying-folder-names-and-all-member-names"></a>Impostazione dei nomi delle cartelle e dei nomi di membro Totale  
  
#### <a name="to-specify-the-folder-and-member-names"></a>Per impostare i nomi delle cartelle e dei membri  
  
1.  Nel riquadro **Attributi** tenere premuto CTRL e fare clic su ognuno dei seguenti attributi per selezionarli:  
  
    -   **Classe**  
  
    -   **Colore**  
  
    -   **Days To Manufacture**  
  
    -   **Reorder Point**  
  
    -   **Safety Stock Level**  
  
    -   **Dimensione**  
  
    -   **Size Range**  
  
    -   **Stile di visualizzazione**  
  
    -   **Weight**  
  
2.  Nel **AttributeHierarchyDisplayFolder** campo della proprietà nella finestra Proprietà, tipo `Stocking`.  
  
     Questi attributi sono stati ora raggruppati in un'unica cartella di visualizzazione.  
  
3.  Nel riquadro **Attributi** selezionare i seguenti attributi:  
  
    -   **Dealer Price**  
  
    -   **List Price**  
  
    -   **Standard Cost**  
  
4.  Nel **AttributeHierarchyDisplayFolder** cella di proprietà nella finestra Proprietà, tipo `Financial`.  
  
     Questi attributi sono stati ora raggruppati in una seconda cartella di visualizzazione.  
  
5.  Nel riquadro **Attributi** selezionare i seguenti attributi:  
  
    -   **End Date**  
  
    -   **Data inizio**  
  
    -   **Stato**  
  
6.  Nel **AttributeHierarchyDisplayFolder** cella di proprietà nella finestra Proprietà, tipo `History`.  
  
     Questi attributi sono stati ora raggruppati in una terza cartella di visualizzazione.  
  
7.  Selezionare il `Product Model Lines` gerarchia nel **gerarchie** riquadro e modificare le **AllMemberName** proprietà nella finestra proprietà per `All Products`.  
  
8.  Fare clic su un'area aperta del **gerarchie** riquadro e modificare il **AttributeAllMemberName** nella parte superiore della finestra proprietà per proprietà `All Products`.  
  
     Facendo clic su un'area libera è possibile modificare le proprietà della dimensione Product stessa. È inoltre possibile fare clic su **Product** nella parte superiore dell'elenco di attributi nel riquadro **Attributi** .  
  
9. Scegliere **Salva tutti** dal menu **File**.  
  
## <a name="defining-attribute-relationships"></a>Definizione di relazioni tra attributi  
 Se i dati sottostanti le supportano, è consigliabile definire relazioni tra gli attributi. La definizione di relazioni tra attributi consente di velocizzare l'elaborazione di dimensioni, partizioni e query. Per altre informazioni, vedere [Definire relazioni tra attributi](multidimensional-models/attribute-relationships-define.md) e [Relazioni tra attributi](multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md).  
  
#### <a name="to-define-attribute-relationships"></a>Per definire relazioni tra attributi  
  
1.  In **Progettazione dimensioni** per la dimensione Product fare clic sulla scheda **Relazioni tra attributi** .  
  
2.  Nel diagramma fare clic con il pulsante destro del mouse sull'attributo **Model Name** , quindi scegliere **Nuova relazione tra attributi**.  
  
3.  Nella finestra di dialogo **Crea relazione tra attributi** l'opzione **Attributo di origine** è impostata su **Model Name**. Impostare **Attributo correlato** su **Product Line**.  
  
     Nell'elenco **Tipo di relazione** lasciare il tipo di relazione impostato su **Flessibile** perché le relazioni tra i membri potrebbero cambiare nel corso del tempo. Ad esempio, un modello di prodotto può essere spostato in una linea di prodotti diversa.  
  
4.  Fare clic su **OK**.  
  
5.  Scegliere **Salva tutti** dal menu **File**.  
  
## <a name="reviewing-product-dimension-changes"></a>Esame delle modifiche alla dimensione Product  
  
#### <a name="to-review-the-product-dimension-changes"></a>Per esaminare le modifiche alla dimensione Product  
  
1.  Scegliere **Distribuisci Analysis Services Tutorial** dal menu [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]Compila **di**.  
  
2.  Dopo la visualizzazione del messaggio **Distribuzione completata** , fare clic sulla scheda **Esplorazione** di **Progettazione dimensioni** per la dimensione **Product** , quindi fare clic sul pulsante Riconnetti sulla barra degli strumenti della finestra di progettazione.  
  
3.  Verificare che `Product Model Lines` sia selezionato nel **gerarchia** elenco e quindi espandere `All Products`.  
  
     Si noti che il nome del **tutte** membro viene visualizzato come `All Products`. Infatti, è stato modificato il **AllMemberName** proprietà per la gerarchia allo `All Products` nella lezione precedente. Inoltre, i membri del livello **Product Line** hanno ora nomi descrittivi anziché abbreviazioni costituite da una sola lettera.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Modifica della dimensione Date](lesson-3-4-modifying-the-date-dimension.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Definire calcoli denominati in una vista origine dati &#40;Analysis Services&#41;](multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)   
 [Creare gerarchie definite dall'utente](multidimensional-models/user-defined-hierarchies-create.md)   
 [Configurare il livello &#40;Totale&#41; per le gerarchie di attributi](multidimensional-models/database-dimensions-configure-the-all-level-for-attribute-hierarchies.md)  
  
  
