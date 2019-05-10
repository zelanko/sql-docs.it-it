---
title: Modifica della dimensione Customer | Microsoft Docs
ms.date: 05/06/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bbe4fbfc2cad2df41a1d9bd14fcb2620e2dec5c1
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2019
ms.locfileid: "65403643"
---
# <a name="lesson-3-2---modifying-the-customer-dimension"></a>Lezione 3-2: modifica della dimensione Customer
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

È possibile migliorare l'usabilità e le funzionalità delle dimensioni di un cubo in diversi modi. Nelle attività di questo argomento verrà modificata la dimensione Customer.  
  
## <a name="renaming-attributes"></a>Ridenominazione di attributi  
È possibile modificare i nomi degli attributi con la scheda **Struttura dimensione** di Progettazione dimensioni.  
  
#### <a name="to-rename-an-attribute"></a>Per rinominare un attributo  
  
1.  Passare a **Progettazione dimensioni** per la dimensione Customer in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. A tale scopo, fare doppio clic sulla dimensione **Customer** nel nodo **Dimensioni** di Esplora soluzioni.  
  
2.  Nel riquadro **Attributi** fare clic con il pulsante destro del mouse su **English Country Region Name**e scegliere **Rinomina**. Modificare il nome dell'attributo in **Country-Region**.  
  
3.  Modificare i nomi degli attributi seguenti allo stesso modo:  
  
    -   **English Education** degli attributi - modificare **Education**  
  
    -   **English Occupation** degli attributi - modificare **Occupation**  
  
    -   **State Province Name** degli attributi - modificare **State-Province**  
  
4.  Scegliere **Salva tutti** dal menu **File**.  
  
## <a name="creating-a-hierarchy"></a>Creazione di una gerarchia  
È possibile creare una nuova gerarchia trascinando un attributo dal riquadro **Attributi** al riquadro **Gerarchie** .  
  
#### <a name="to-create-a-hierarchy"></a>Per creare una gerarchia  
  
1.  Trascinare l'attributo **Country-Region** dal riquadro **Attributi** al riquadro **Gerarchie** .  
  
2.  Trascinare l'attributo **State-Province** dal riquadro **Attributi** alla cella **<new level>** nel riquadro **Gerarchie** , sotto il livello **Country-Region** .  
  
3.  Trascinare l'attributo **City** dal riquadro **Attributi** alla cella **<new level>** nel riquadro **Gerarchie** , sotto il livello **State-Province** .  
  
4.  Nel riquadro **Gerarchie** della scheda **Struttura dimensione** fare clic con il pulsante destro del mouse sulla barra del titolo della gerarchia **Gerarchia** , scegliere **Rinomina**e quindi digitare **Customer Geography**.  
  
    Il nome della gerarchia è ora **Customer Geography**.  
  
5.  Scegliere **Salva tutti** dal menu **File**.  
  
## <a name="adding-a-named-calculation"></a>Aggiunta di un calcolo denominato  
È possibile aggiungere un calcolo denominato, ovvero un'espressione SQL rappresentata da una colonna calcolata, a una tabella in una vista origine dati. L'espressione ha lo stesso aspetto e funziona allo stesso modo di una colonna di una tabella. I calcoli denominati consentono di estendere lo schema relazionale delle tabelle esistenti in una vista origine dati senza modificare la tabella dell'origine dei dati sottostante. Per altre informazioni, vedere [Definire calcoli denominati in una vista origine dati &#40;Analysis Services&#41;](../multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md).  
  
#### <a name="to-add-a-named-calculation"></a>Per aggiungere un calcolo denominato  
  
1.  Aprire la vista origine dati **[!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] DW 2012** facendo doppio clic su di essa nella cartella **Viste origine dati** di Esplora soluzioni.  
  
2.  Nel riquadro **Tabelle** a sinistra, fare clic con il pulsante destro del mouse su **Customer**e scegliere **Nuovo calcolo denominato**.  
  
3.  Nella finestra di dialogo **Crea calcolo denominato** digitare **FullName** nella casella **Nome colonna** e quindi digitare o copiare e incollare l'istruzione **CASE** seguente nella casella **Espressione** :  
  
    ```  
    CASE  
       WHEN MiddleName IS NULL THEN  
       FirstName + ' ' + LastName  
       ELSE  
       FirstName + ' ' + MiddleName + ' ' + LastName  
    END  
    ```  
  
    L'istruzione **CASE** consente di concatenare le colonne **FirstName**, **MiddleName**e **LastName** in un'unica colonna che verrà usata nella dimensione Customer come nome visualizzato dell'attributo **Customer** .  
  
4.  Fare clic su **OK**e quindi espandere **Customer** nel riquadro **Tabelle** .  
  
    Il calcolo denominato **FullName** verrà visualizzato nell'elenco di colonne della tabella Customer, con un'icona indicante che si tratta di un calcolo denominato.  
  
5.  Scegliere **Salva tutti** dal menu **File**.  
  
6.  Nel riquadro **Tabelle** fare clic con il pulsante destro del mouse su **Customer**e quindi scegliere **Esplora dati**.  
  
7.  Controllare l'ultima colonna della vista **Esplora tabella Customer** .  
  
    Si noti che la colonna **FullName** viene visualizzata nella vista origine dati, concatenando correttamente i dati di numerose colonne dell'origine dati sottostante e senza modificare l'origine dati originale.  
  
8.  Chiudere la scheda **Esplora tabella Customer**.  
  
## <a name="using-the-named-calculation-for-member-names"></a>Utilizzo del calcolo denominato per i nomi dei membri  
Dopo aver creato un calcolo denominato nella vista origine dati, è possibile utilizzarlo come proprietà di un attributo.  
  
#### <a name="to-use-the-named-calculation-for-member-names"></a>Per utilizzare il calcolo denominato per i nomi dei membri  
  
1.  Passare a Progettazione dimensioni per la dimensione Customer.  
  
2.  Nel riquadro **Attributi** della scheda **Struttura dimensione** fare clic sull'attributo **Customer Key** .  
  
3.  Aprire la finestra Proprietà e fare clic sul pulsante **Nascondi automaticamente** sulla barra del titolo in modo che rimanga aperta.  
  
4.  Nel campo proprietà **Name** digitare **Full Name**.  
  
5.  Fare clic nella **NameColumn** proprietà campo nella parte inferiore e quindi fare clic su Sfoglia (**...** ) per aprire la **colonna nome** nella finestra di dialogo.  
  
6.  Selezionare **FullName** nella parte inferiore dell'elenco **Colonna di origine** , quindi fare clic su **OK**.  
  
7.  Nella scheda Struttura dimensione trascinare l'attributo **Full Name** dal riquadro **Attributi** alla cella **<new level>** del riquadro **Gerarchie** , sotto il livello **City** .  
  
8.  Scegliere **Salva tutti** dal menu **File**.  
  
## <a name="defining-display-folders"></a>Definizione di cartelle di visualizzazione  
È possibile utilizzare cartelle di visualizzazione per raggruppare gerarchie utente e di attributi in strutture di cartelle per migliorare l'usabilità.  
  
#### <a name="to-define-display-folders"></a>Per definire cartelle di visualizzazione  
  
1.  Aprire la scheda **Struttura dimensione** per la dimensione Customer.  
  
2.  Nel riquadro **Attributi** tenere premuto CTRL e fare clic su ognuno dei seguenti attributi per selezionarli:  
  
    -   **City**  
  
    -   **Country-Region**  
  
    -   **Postal Code**  
  
    -   **State-Province**  
  
3.  Nella finestra Proprietà fare clic sul campo proprietà **AttributeHierarchyDisplayFolder** nella parte superiore (potrebbe essere necessario posizionare il puntatore per visualizzare il nome completo) e quindi digitare **Location**.  
  
4.  Nel riquadro **Gerarchie** fare clic su **Customer Geography**, quindi nella finestra Proprietà a destra selezionare **Location** come valore per la proprietà **DisplayFolder** .  
  
5.  Nel riquadro **Attributi** tenere premuto CTRL e fare clic su ognuno dei seguenti attributi per selezionarli:  
  
    -   **Commute Distance**  
  
    -   **Education**  
  
    -   **Gender**  
  
    -   **House Owner Flag**  
  
    -   **Marital Status**  
  
    -   **Number Cars Owned**  
  
    -   **Number Children At Home**  
  
    -   **Occupation**  
  
    -   **Total Children**  
  
    -   **Yearly Income**  
  
6.  Nella finestra Proprietà fare clic sul campo proprietà **AttributeHierarchyDisplayFolder** nella parte superiore e quindi digitare **Demographic**.  
  
7.  Nel riquadro **Attributi** tenere premuto CTRL e fare clic su ognuno dei seguenti attributi per selezionarli:  
  
    -   **Email Address**  
  
    -   **Phone**  
  
8.  Nella finestra Proprietà fare clic sul campo della proprietà **AttributeHierarchyDisplayFolder** e digitare **Contacts**.  
  
9. Scegliere **Salva tutti** dal menu **File**.  
  
## <a name="defining-composite-keycolumns"></a>Definizione della proprietà KeyColumns composta  
La proprietà **KeyColumns** contiene la colonna o le colonne che rappresentano la chiave per l'attributo. In questa lezione verrà creata una chiave composta per gli attributi **City** e **State-Province** . Le chiavi composte possono essere utili quando è necessario identificare in modo univoco un attributo. Ad esempio, quando si definiranno le relazioni tra attributi più avanti in questa esercitazione, un attributo **City** dovrà identificare in modo univoco un attributo **State-Province** . Tuttavia, è possibile che esistano varie città con lo stesso nome in stati diversi. Per questo motivo verrà creata una chiave composta, costituita dalle colonne **StateProvinceName** e **City** per l'attributo **City** . Per altre informazioni, vedere [Modificare la proprietà KeyColumn di un attributo](../multidimensional-models/attribute-properties-modify-the-keycolumn-property.md).  
  
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
  
2.  Nel riquadro **Attributi** fare clic sull'attributo **State-Province** .  
  
3.  Nella finestra **Proprietà** fare clic nel campo **KeyColumns** e quindi sul pulsante Sfoglia (**...**).  
  
4.  Nella finestra di dialogo **Colonne chiave** , nell'elenco **Colonne disponibili** selezionare la colonna **EnglishCountryRegionName**e fare clic sul pulsante **>** .  
  
    Le colonne **EnglishCountryRegionName** e **StateProvinceName** sono ora visualizzate nell'elenco **Colonne chiave** .  
  
5.  Fare clic su **OK**.  
  
6.  Per impostare la proprietà **NameColumn** dell'attributo **State-Province** fare clic nel campo **NameColumn** della finestra Proprietà e fare clic sul pulsante Sfoglia (**...**).  
  
7.  Nell'elenco **Colonna di origine** della finestra di dialogo **Colonna nome** selezionare **StateProvinceName**e fare clic su **OK**.  
  
8.  Scegliere **Salva tutti** dal menu **File**.  
  
## <a name="defining-attribute-relationships"></a>Definizione di relazioni tra attributi  
Se i dati sottostanti le supportano, è consigliabile definire relazioni tra gli attributi. La definizione di relazioni tra attributi consente di velocizzare l'elaborazione di dimensioni, partizioni e query. Per altre informazioni, vedere [Definire relazioni tra attributi](../multidimensional-models/attribute-relationships-define.md) e [Relazioni tra attributi](../multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md).  
  
#### <a name="to-define-attribute-relationships"></a>Per definire relazioni tra attributi  
  
1.  In **Progettazione dimensioni** per la dimensione Customer fare clic sulla scheda **Relazioni tra attributi** . Potrebbe essere necessario attendere alcuni istanti.  
  
2.  Nel diagramma fare clic con il pulsante destro del mouse sull'attributo **City** , quindi scegliere **Nuova relazione tra attributi**.  
  
3.  Nella finestra di dialogo **Crea relazione tra attributi** l'opzione **Attributo di origine** è impostata su **City**. Impostare **Attributo correlato** su **State-Province**.  
  
4.  Nell'elenco **Tipo di relazione** impostare il tipo di relazione su **Rigida**.  
  
    Il tipo di relazione è **Rigida** perché le relazioni tra i membri non cambieranno nel corso del tempo. Ad esempio, è raro che una città diventi parte di uno stato o di una provincia diversa.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  Nel diagramma fare clic con il pulsante destro del mouse sull'attributo **State-Province** e quindi scegliere **Nuova relazione tra attributi**.  
  
7.  Nella finestra di dialogo **Crea relazione tra attributi** l'opzione **Attributo di origine** è impostata su **State-Province**. Impostare **Attributo correlato** su **Country-Region**.  
  
8.  Nell'elenco **Tipo di relazione** impostare il tipo di relazione su **Rigida**.  
  
9. Fare clic su **OK**.  
  
10. Scegliere **Salva tutti** dal menu **File**.  
  
## <a name="deploying-changes-processing-the-objects-and-viewing-the-changes"></a>Distribuzione delle modifiche, elaborazione degli oggetti e visualizzazione delle modifiche  
Dopo aver modificato gli attributi e le gerarchie, prima di visualizzare le modifiche è necessario distribuirle e rielaborare gli oggetti correlati.  
  
#### <a name="to-deploy-the-changes-process-the-objects-and-view-the-changes"></a>Per distribuire le modifiche, elaborare gli oggetti e visualizzare le modifiche  
  
1.  Nel menu **Compila** di [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], scegliere **Distribuisci Analysis Services Tutorial**.  
  
2.  Dopo la visualizzazione del messaggio **Distribuzione completata** , fare clic sulla scheda **Esplorazione** di Progettazione dimensioni per la dimensione Customer e fare clic sul pulsante Riconnetti a sinistra della barra degli strumenti della finestra di progettazione.  
  
3.  Verificare che la gerarchia **Customer Geography** sia selezionata nell'elenco **Gerarchia** , quindi nel riquadro di esplorazione espandere **All**, **Australia**, **New South Wales**, e **Coffs Harbour**.  
  
    Verranno visualizzati i clienti della città.  
  
4.  Passare a **Progettazione cubi** per il cubo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Tutorial. A tale scopo, fare doppio clic sul cubo **Analysis Services Tutorial** nel nodo **Cubi** di **Esplora soluzioni**.  
  
5.  Fare clic sulla scheda **Esplorazione** e quindi scegliere il pulsante Riconnetti sulla barra degli strumenti della finestra di progettazione.  
  
6.  Nel riquadro **Gruppo di misure** espandere **Customer**.  
  
    Si noti che anziché un lungo elenco di attributi, sotto Customer vengono elencate solo le cartelle di visualizzazione e gli attributi che non presentano valori di cartelle di visualizzazione.  
  
7.  Scegliere **Salva tutti** dal menu **File**.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
[Modifica della dimensione Product](lesson-3-3-modifying-the-product-dimension.md)  
  
## <a name="see-also"></a>Vedere anche  
[Riferimento alle proprietà degli attributi delle dimensioni](../multidimensional-models/dimension-attribute-properties-reference.md)  
[Rimuovere un attributo da una dimensione](../multidimensional-models/attribute-properties-remove-an-attribute-from-a-dimension.md)  
[Rinominare un attributo](../multidimensional-models/attribute-properties-rename-an-attribute.md)  
[Definire calcoli denominati in una vista origine dati &#40;Analysis Services&#41;](../multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
