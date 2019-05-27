---
title: Modifica della dimensione Customer | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 5b5aed99-1760-4bc7-b248-52ecb0b97ebc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2530d42c70b506fe927d35fd4e6f862e22e1ea1a
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66078925"
---
# <a name="modifying-the-customer-dimension"></a>Modifica della dimensione Customer
  È possibile migliorare l'usabilità e le funzionalità delle dimensioni di un cubo in diversi modi. Nelle attività di questo argomento verrà modificata la dimensione Customer.  
  
## <a name="renaming-attributes"></a>Ridenominazione di attributi  
 È possibile modificare i nomi degli attributi con la scheda **Struttura dimensione** di Progettazione dimensioni.  
  
#### <a name="to-rename-an-attribute"></a>Per rinominare un attributo  
  
1.  Passare a **Progettazione dimensioni** per la dimensione Customer in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. A tale scopo, fare doppio clic sulla dimensione **Customer** nel nodo **Dimensioni** di Esplora soluzioni.  
  
2.  Nel riquadro **Attributi** fare clic con il pulsante destro del mouse su **English Country Region Name**e scegliere **Rinomina**. Modificare il nome dell'attributo da `Country-Region`.  
  
3.  Modificare i nomi degli attributi seguenti allo stesso modo:  
  
    -   **English Education** degli attributi - modificare in `Education`  
  
    -   **English Occupation** degli attributi - modificare in `Occupation`  
  
    -   **State Province Name** degli attributi - modificare in `State-Province`  
  
4.  Scegliere **Salva tutti** dal menu **File**.  
  
## <a name="creating-a-hierarchy"></a>Creazione di una gerarchia  
 È possibile creare una nuova gerarchia trascinando un attributo dal riquadro **Attributi** al riquadro **Gerarchie** .  
  
#### <a name="to-create-a-hierarchy"></a>Per creare una gerarchia  
  
1.  Trascinare il `Country-Region` dell'attributo dal **attributi** riquadro il **gerarchie** riquadro.  
  
2.  Trascinare il `State-Province` dell'attributo dal **attributi** riquadro il  **\<nuovo livello >** cella il **gerarchie** riquadro, sotto il `Country-Region` livello.  
  
3.  Trascinare il **Città** dell'attributo dal **attributi** riquadro il  **\<nuovo livello >** cella il **gerarchie** riquadro di sotto di `State-Province` livello.  
  
4.  Nel **gerarchie** riquadro della finestra il **struttura dimensione** scheda, fare clic sulla barra del titolo del **gerarchia** gerarchia, seleziona **rinominare**, quindi digitare `Customer Geography`.  
  
     Il nome della gerarchia è ora `Customer Geography`.  
  
5.  Scegliere **Salva tutti** dal menu **File**.  
  
## <a name="adding-a-named-calculation"></a>Aggiunta di un calcolo denominato  
 È possibile aggiungere un calcolo denominato, ovvero un'espressione SQL rappresentata da una colonna calcolata, a una tabella in una vista origine dati. L'espressione ha lo stesso aspetto e funziona allo stesso modo di una colonna di una tabella. I calcoli denominati consentono di estendere lo schema relazionale delle tabelle esistenti in una vista origine dati senza modificare la tabella dell'origine dei dati sottostante. Per altre informazioni, vedere [Definire calcoli denominati in una vista origine dati &#40;Analysis Services&#41;](multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md).  
  
#### <a name="to-add-a-named-calculation"></a>Per aggiungere un calcolo denominato  
  
1.  Aprire la vista origine dati **[!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW 2012** facendo doppio clic su di essa nella cartella **Viste origine dati** di Esplora soluzioni.  
  
2.  Nel riquadro **Tabelle** a sinistra, fare clic con il pulsante destro del mouse su **Customer**e scegliere **Nuovo calcolo denominato**.  
  
3.  Nel **Crea calcolo denominato** finestra di dialogo, digitare `FullName` nel **nome colonna** casella, digitare o copiare e incollare il codice seguente `CASE` istruzione nel **espressione**  casella:  
  
    ```  
    CASE  
       WHEN MiddleName IS NULL THEN  
       FirstName + ' ' + LastName  
       ELSE  
       FirstName + ' ' + MiddleName + ' ' + LastName  
    END  
    ```  
  
     Il `CASE` istruzione consente di concatenare il **FirstName**, **MiddleName**, e **LastName** colonne in una singola colonna che si userà il cliente della dimensione come il nome visualizzato per il **cliente** attributo.  
  
4.  Fare clic su **OK**e quindi espandere **Customer** nel riquadro **Tabelle** .  
  
     Il `FullName` calcolo denominato verrà visualizzato nell'elenco delle colonne della tabella Customer, con un'icona che indica che si tratta di un calcolo denominato.  
  
5.  Scegliere **Salva tutti** dal menu **File**.  
  
6.  Nel riquadro **Tabelle** fare clic con il pulsante destro del mouse su **Customer**e quindi scegliere **Esplora dati**.  
  
7.  Controllare l'ultima colonna della vista **Esplora tabella Customer** .  
  
     Si noti che il `FullName` colonna vengono visualizzate nella vista origine dati, concatenando correttamente i dati di numerose colonne dell'origine dati sottostante e senza modificare l'origine dati originale.  
  
8.  Chiudere la scheda **Esplora tabella Customer** .  
  
## <a name="using-the-named-calculation-for-member-names"></a>Utilizzo del calcolo denominato per i nomi dei membri  
 Dopo aver creato un calcolo denominato nella vista origine dati, è possibile utilizzarlo come proprietà di un attributo.  
  
#### <a name="to-use-the-named-calculation-for-member-names"></a>Per utilizzare il calcolo denominato per i nomi dei membri  
  
1.  Passare a Progettazione dimensioni per la dimensione Customer.  
  
2.  Nel riquadro **Attributi** della scheda **Struttura dimensione** fare clic sull'attributo **Customer Key** .  
  
3.  Aprire la finestra Proprietà e fare clic sul pulsante **Nascondi automaticamente** sulla barra del titolo in modo che rimanga aperta.  
  
4.  Nel **Name** campo della proprietà, tipo `Full Name`.  
  
5.  Fare clic nella **NameColumn** proprietà campo nella parte inferiore e quindi fare clic su Sfoglia (**...** ) per aprire la **colonna nome** nella finestra di dialogo.  
  
6.  Selezionare `FullName` nella parte inferiore della **Source column** elenco e quindi fare clic su **OK**.  
  
7.  Nella scheda struttura dimensione trascinare il `Full Name` dell'attributo dal **attributi** riquadro nel  **\<nuovo livello >** cella il **gerarchie** riquadro, sotto il **Città** livello.  
  
8.  Scegliere **Salva tutti** dal menu **File**.  
  
## <a name="defining-display-folders"></a>Definizione di cartelle di visualizzazione  
 È possibile utilizzare cartelle di visualizzazione per raggruppare gerarchie utente e di attributi in strutture di cartelle per migliorare l'usabilità.  
  
#### <a name="to-define-display-folders"></a>Per definire cartelle di visualizzazione  
  
1.  Aprire la scheda **Struttura dimensione** per la dimensione Customer.  
  
2.  Nel riquadro **Attributi** tenere premuto CTRL e fare clic su ognuno dei seguenti attributi per selezionarli:  
  
    -   **City**  
  
    -   `Country-Region`  
  
    -   **Postal Code**  
  
    -   `State-Province`  
  
3.  Nella finestra Proprietà scegliere il **AttributeHierarchyDisplayFolder** campo della proprietà nella parte superiore (potrebbe essere necessario in modo che punti a questo argomento per visualizzare il nome completo) e quindi digitare `Location`.  
  
4.  Nel **gerarchie** riquadro, fare clic su `Customer Geography`, quindi nella finestra proprietà a destra, selezionare `Location` come valore del **DisplayFolder** proprietà.  
  
5.  Nel riquadro **Attributi** tenere premuto CTRL e fare clic su ognuno dei seguenti attributi per selezionarli:  
  
    -   **Commute Distance**  
  
    -   `Education`  
  
    -   **Gender**  
  
    -   **House Owner Flag**  
  
    -   **Marital Status**  
  
    -   **Number Cars Owned**  
  
    -   **Number Children At Home**  
  
    -   `Occupation`  
  
    -   **Total Children**  
  
    -   **Yearly Income**  
  
6.  Nella finestra Proprietà scegliere il **AttributeHierarchyDisplayFolder** proprietà campo nella parte superiore e quindi digitare `Demographic`.  
  
7.  Nel riquadro **Attributi** tenere premuto CTRL e fare clic su ognuno dei seguenti attributi per selezionarli:  
  
    -   **Email Address**  
  
    -   **Phone**  
  
8.  Nella finestra Proprietà scegliere il **AttributeHierarchyDisplayFolder** campo della proprietà e il tipo `Contacts`.  
  
9. Scegliere **Salva tutti** dal menu **File**.  
  
## <a name="defining-composite-keycolumns"></a>Definizione della proprietà KeyColumns composta  
 La proprietà **KeyColumns** contiene la colonna o le colonne che rappresentano la chiave per l'attributo. In questa lezione, si crea una chiave composta per la **Città** e `State-Province` attributi. Le chiavi composte possono essere utili quando è necessario identificare in modo univoco un attributo. Ad esempio, quando si definiscono le relazioni tra attributi più avanti in questa esercitazione, un' **Città** attributo deve identificare in modo univoco un `State-Province` attributo. Tuttavia, è possibile che esistano varie città con lo stesso nome in stati diversi. Per questo motivo verrà creata una chiave composta, costituita dalle colonne **StateProvinceName** e **City** per l'attributo **City** . Per altre informazioni, vedere [Modificare la proprietà KeyColumn di un attributo](multidimensional-models/attribute-properties-modify-the-keycolumn-property.md).  
  
#### <a name="to-define-composite-keycolumns-for-the-city-attribute"></a>Per definire la proprietà KeyColumns composta per l'attributo City  
  
1.  Aprire la scheda **Struttura dimensione** per la dimensione Customer.  
  
2.  Nel riquadro **Attributi** fare clic sull'attributo **City** .  
  
3.  Nella finestra **Proprietà** fare clic nel campo **KeyColumns** nella parte inferiore e fare clic sul pulsante Sfoglia (**...**).  
  
4.  Nella finestra di dialogo **Colonne chiave** , nell'elenco **Colonne disponibili** selezionare la colonna **StateProvinceName**e fare clic sul pulsante **>** .  
  
     Le colonne **City** e **StateProvinceName** sono ora visualizzate nell'elenco **Colonne chiave** .  
  
5.  Fare clic su **OK**.  
  
6.  Per impostare la proprietà **NameColumn** dell'attributo **City** , fare clic nel campo **NameColumn** della finestra Proprietà e fare clic sul pulsante Sfoglia (**...**).  
  
7.  Nella finestra di dialogo **Colonna nome** , nell'elenco **Colonna di origine** selezionare **City**e fare clic su **OK**.  
  
8.  Scegliere **Salva tutti** dal menu **File**.  
  
#### <a name="to-define-composite-keycolumns-for-the-state-province-attribute"></a>Per definire la proprietà KeyColumns composta per l'attributo State-Province  
  
1.  Assicurarsi che la scheda **Struttura dimensione** per la dimensione Customer sia aperta.  
  
2.  Nel **attributi** riquadro, fare clic su di `State-Province` attributo.  
  
3.  Nella finestra **Proprietà** fare clic nel campo **KeyColumns** e quindi sul pulsante Sfoglia (**...**).  
  
4.  Nella finestra di dialogo **Colonne chiave** , nell'elenco **Colonne disponibili** selezionare la colonna **EnglishCountryRegionName**e fare clic sul pulsante **>** .  
  
     Le colonne **EnglishCountryRegionName** e **StateProvinceName** sono ora visualizzate nell'elenco **Colonne chiave** .  
  
5.  Fare clic su **OK**.  
  
6.  Per impostare il **NameColumn** proprietà delle `State-Province` dell'attributo, fare clic sul **NameColumn** campo nella finestra proprietà e quindi fare clic su Sfoglia (**...** ) pulsante.  
  
7.  Nell'elenco **Colonna di origine** della finestra di dialogo **Colonna nome** selezionare **StateProvinceName**e fare clic su **OK**.  
  
8.  Scegliere **Salva tutti** dal menu **File**.  
  
## <a name="defining-attribute-relationships"></a>Definizione di relazioni tra attributi  
 Se i dati sottostanti le supportano, è consigliabile definire relazioni tra gli attributi. La definizione di relazioni tra attributi consente di velocizzare l'elaborazione di dimensioni, partizioni e query. Per altre informazioni, vedere [Definire relazioni tra attributi](multidimensional-models/attribute-relationships-define.md) e [Relazioni tra attributi](multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md).  
  
#### <a name="to-define-attribute-relationships"></a>Per definire relazioni tra attributi  
  
1.  In **Progettazione dimensioni** per la dimensione Customer fare clic sulla scheda **Relazioni tra attributi** . Potrebbe essere necessario attendere alcuni istanti.  
  
2.  Nel diagramma fare clic con il pulsante destro del mouse sull'attributo **City** , quindi scegliere **Nuova relazione tra attributi**.  
  
3.  Nella finestra di dialogo **Crea relazione tra attributi** l'opzione **Attributo di origine** è impostata su **City**. Impostare il **attributo correlato** a `State-Province`.  
  
4.  Nell'elenco **Tipo di relazione** impostare il tipo di relazione su **Rigida**.  
  
     Il tipo di relazione è **Rigida** perché le relazioni tra i membri non cambieranno nel corso del tempo. Ad esempio, è raro che una città diventi parte di uno stato o di una provincia diversa.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  Nel diagramma, fare doppio clic il `State-Province` dell'attributo e quindi selezionare **nuova relazione tra attributi**.  
  
7.  Nel **Crea relazione tra attributi** finestra di dialogo, il **attributo di origine** è `State-Province`. Impostare il **attributo correlato** a `Country-Region`.  
  
8.  Nell'elenco **Tipo di relazione** impostare il tipo di relazione su **Rigida**.  
  
9. Fare clic su **OK**.  
  
10. Scegliere **Salva tutti** dal menu **File**.  
  
## <a name="deploying-changes-processing-the-objects-and-viewing-the-changes"></a>Distribuzione delle modifiche, elaborazione degli oggetti e visualizzazione delle modifiche  
 Dopo aver modificato gli attributi e le gerarchie, prima di visualizzare le modifiche è necessario distribuirle e rielaborare gli oggetti correlati.  
  
#### <a name="to-deploy-the-changes-process-the-objects-and-view-the-changes"></a>Per distribuire le modifiche, elaborare gli oggetti e visualizzare le modifiche  
  
1.  Nel menu **Compila** di [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], scegliere **Distribuisci Analysis Services Tutorial**.  
  
2.  Dopo la visualizzazione del messaggio **Distribuzione completata** , fare clic sulla scheda **Esplorazione** di Progettazione dimensioni per la dimensione Customer e fare clic sul pulsante Riconnetti a sinistra della barra degli strumenti della finestra di progettazione.  
  
3.  Verificare che `Customer Geography` sia selezionato nel **gerarchia** elenco e quindi nel riquadro di esplorazione, espandere **tutti**, espandere **Australia**, espandere **nuovo meridionale Ticino**, quindi espandere **Coffs Harbour**.  
  
     Verranno visualizzati i clienti della città.  
  
4.  Passare a **Progettazione cubi** per il cubo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial. A tale scopo, fare doppio clic sul cubo **Analysis Services Tutorial** nel nodo **Cubi** di **Esplora soluzioni**.  
  
5.  Fare clic sulla scheda **Esplorazione** e quindi scegliere il pulsante Riconnetti sulla barra degli strumenti della finestra di progettazione.  
  
6.  Nel riquadro **Gruppo di misure** espandere **Customer**.  
  
     Si noti che anziché un lungo elenco di attributi, sotto Customer vengono elencate solo le cartelle di visualizzazione e gli attributi che non presentano valori di cartelle di visualizzazione.  
  
7.  Scegliere **Salva tutti** dal menu **File**.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Modifica della dimensione Product](lesson-3-3-modifying-the-product-dimension.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento alle proprietà degli attributo delle dimensioni](multidimensional-models/dimension-attribute-properties-reference.md)   
 [Rimuovere un attributo da una dimensione](multidimensional-models/attribute-properties-remove-an-attribute-from-a-dimension.md)   
 [Rinominare un attributo](multidimensional-models/attribute-properties-rename-an-attribute.md)   
 [Definire calcoli denominati in una vista origine dati &#40;Analysis Services&#41;](multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
  
