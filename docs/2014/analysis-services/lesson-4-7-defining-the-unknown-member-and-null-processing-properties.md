---
title: Definizione delle proprietà di elaborazione null e membro sconosciute | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d9abb09c-9bfa-4e32-b530-8590e4383566
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c8db9d2dd582651d852f34372d5d2ae74c958f72
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/28/2020
ms.locfileid: "78175310"
---
# <a name="defining-the-unknown-member-and-null-processing-properties"></a>Definizione delle proprietà UnknownMember e NullProcessing
  Quando [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] elabora una dimensione, tutti i valori distinti delle colonne sottostanti delle tabelle o viste incluse nella vista origine dati popolano gli attributi della dimensione. Se [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] rileva un valore Null durante l'elaborazione, per impostazione predefinita quest'ultimo viene convertito in un valore zero per le colonne di tipo numerico o in una stringa vuota per le colonne di tipo stringa. È possibile modificare le impostazioni predefinite oppure convertire i valori Null nell'eventuale processo di estrazione, trasformazione e caricamento del data warehouse relazionale sottostante. È anche possibile configurare [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] in modo che converta il valore Null in un valore designato impostando tre proprietà, ovvero **UnknownMember** e **UnknownMemberName** per la dimensione e **NullProcessing** per l'attributo chiave della dimensione.

 La Creazione guidata dimensione e la Creazione guidata cubo consentono di abilitare tali proprietà in modo appropriato a seconda che l'attributo chiave di una dimensione ammetta valori Null oppure che l'attributo radice di una dimensione con schema snowflake sia basato su una colonna che ammette valori Null. In questi casi la proprietà **NullProcessing** dell'attributo chiave viene impostata su **UnknownMember** e la proprietà **UnknownMember** su **Visible**.

 Quando si compilano dimensioni con schema snowflake in modo incrementale, come per la dimensione Product di questa esercitazione, oppure se si definiscono le dimensioni con Progettazione dimensioni e quindi si incorporano le dimensioni esistenti in un cubo, potrebbe tuttavia essere necessario impostare le proprietà **UnknownMember** e **NullProcessing** manualmente.

 Nelle attività di questo argomento si aggiungeranno gli attributi della categoria Product e della sottocategoria Product alla dimensione Product proveniente dalle tabelle con schema snowflake che si aggiungeranno alla vista origine dati di [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW. Sarà quindi abilitata la proprietà **UnknownMember** per la dimensione Product, si `Assembly Components` specificherà come valore per la proprietà **UnknownMemberName** , si `Subcategory` configureranno gli attributi e all'attributo Product Name e quindi si definirà la gestione degli errori personalizzata per l'attributo chiave del membro che collega le tabelle a `Category` fiocco di neve.

> [!NOTE]
>  Se gli attributi Subcategory e Category sono stati aggiunti durante la definizione iniziale del cubo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial mediante la Creazione guidata cubo, questi passaggi verranno eseguiti automaticamente.

## <a name="reviewing-error-handling-and-unknown-member-properties-in-the-product-dimension"></a>Esame delle proprietà ErrorHandling e UnknownMember nella dimensione Product

1.  Passare a Progettazione dimensioni per la dimensione **Product** , fare clic sulla scheda **Struttura dimensione** , quindi selezionare **Product** nel riquadro **Attributi** .

     In questo modo è possibile visualizzare e modificare le proprietà della dimensione stessa.

2.  Nella finestra Proprietà controllare le proprietà **UnknownMember** e **UnknownMemberName** .

     Si noti che la proprietà **UnknownMember** non è abilitata perché il relativo valore è impostato su **None** anziché **Visible** o **Hidden**e che non è specificato alcun nome per la proprietà **UnknownMemberName** .

3.  Nella finestra Proprietà selezionare **(personalizzata)** nella cella della proprietà **ErrorConfiguration** , quindi espandere la raccolta delle proprietà **ErrorConfiguration** .

     Se si imposta la proprietà **ErrorConfiguration** su **(personalizzata)** è possibile visualizzare le impostazioni di configurazione predefinite degli errori. Nessun'altra impostazione viene modificata.

4.  Esaminare le proprietà di configurazione Key e NullKeyError, ma non apportare modifiche.

     Si noti che per impostazione predefinita quando chiavi Null vengono convertite nel valore di UnknownMember, l'errore di elaborazione associato alla conversione stessa viene ignorato.

     Nella figura seguente vengono illustrate le impostazioni delle proprietà per la raccolta di proprietà **ErrorConfiguration** .

     ![Raccolta di proprietà ErrorConfiguration](../../2014/tutorials/media/l4-productdimensionerrorconfig-1.gif "Raccolta di proprietà ErrorConfiguration")

5.  Fare clic sulla scheda **esplorazione** , verificare che **Product Model Lines** sia selezionato nell'elenco **gerarchia** , quindi espandere `All Products`.

     Si notino i cinque membri del livello Product Line.

6.  Espandere **Components**e quindi espandere il membro senza etichetta del livello **Model Name** .

     Il livello contiene i componenti di assembly che vengono usati nella compilazione di altri componenti, a partire dal prodotto **Adjustable Race** , come illustrato nella figura seguente.

     ![Componenti di assembly usati per compilare altri componenti](../../2014/tutorials/media/l4-productdimensionerrorconfig-2.gif "Componenti di assembly usati per compilare altri componenti")

## <a name="defining-attributes-from-snowflaked-tables-and-a-product-category-user-defined-hierarchy"></a>Definizione di attributi provenienti da tabelle con schema snowflake e di una gerarchia definita dall'utente Product Category

1.  Aprire Progettazione vista origine dati per la vista origine dati [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW, selezionare **Reseller Sales** nel riquadro **Libreria diagrammi** , quindi scegliere **Aggiungi/Rimuovi oggetti** dal menu **Vista origine dati** di [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].

     Viene visualizzata la finestra di dialogo **Aggiungi/Rimuovi tabelle** .

2.  Nell'elenco **Oggetti inclusi** selezionare **DimProduct (dbo)**, quindi fare clic su **Aggiungi tabelle correlate**.

     Verranno aggiunti sia **DimProductSubcategory (dbo)** che **FactProductInventory (dbo)** . Rimuovere **FactProductInventory (dbo)** in modo che solo la tabella **DimProductSubcategory (dbo)** venga aggiunta all'elenco **Oggetti inclusi** .

3.  Con la tabella **DimProductSubcategory (dbo)** selezionata per impostazione predefinita come ultima tabella aggiunta, fare di nuovo clic su **Aggiungi tabelle correlate** .

     La tabella **DimProductCategory (dbo)** viene aggiunta all'elenco **Oggetti inclusi** .

4.  Fare clic su **OK**.

5.  Scegliere **Layout automatico** dal menu [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]Formato **di**e quindi fare clic su **Diagramma**.

     Si noti che la tabella **DimProductSubcategory (dbo)** e la tabella **DimProductCategory (dbo)** sono collegate tra loro e alla tabella **ResellerSales** attraverso la tabella **Product** .

6.  Passare a Progettazione dimensioni per la dimensione **Product** e fare clic sulla scheda **Struttura dimensione** .

7.  Fare clic in un punto qualsiasi del riquadro **Vista origine dati** e quindi fare clic su **Mostra tutte le tabelle**.

8.  Nel riquadro **Vista origine dati** individuare la tabella **DimProductCategory** , fare con il pulsante destro del mouse su **ProductCategoryKey** nella tabella stessa e quindi fare clic su **Nuovo attributo da colonna**.

9. Nel riquadro **attributi** modificare il nome di questo nuovo attributo in `Category`.

10. Nella Finestra Proprietà fare clic sul campo della proprietà **NameColumn** , quindi fare clic sul pulsante Sfoglia (**..**.) per aprire la finestra di dialogo **colonna nome** .

11. Selezionare **EnglishProductCategoryName** nell'elenco **Colonna di origine** , quindi fare clic su **OK**.

12. Nel riquadro **Vista origine dati** individuare la tabella **DimProductSubcategory** , fare clic con il pulsante destro del mouse su **ProductSubcategoryKey** nella tabella stessa e quindi fare clic su **Nuovo attributo da colonna**.

13. Nel riquadro **attributi** modificare il nome di questo nuovo attributo in `Subcategory`.

14. Nella finestra Proprietà fare clic sul campo della proprietà **NameColumn** , quindi fare clic sul pulsante Sfoglia **(...)** per aprire la finestra di dialogo **colonna nome** .

15. Selezionare **EnglishProductSubcategoryName** nell'elenco **Colonna di origine** , quindi fare clic su **OK**.

16. Creare una nuova gerarchia definita dall'utente denominata **Product Categories** con i seguenti livelli, nell'ordine dall'alto verso il `Category`basso `Subcategory`:, e il **nome del prodotto**.

17. Specificare `All Products` come valore per la proprietà **AllMemberName** della gerarchia definita dall'utente Product Categories.

## <a name="browsing-the-user-defined-hierarchies-in-the-product-dimension"></a>Esplorazione delle gerarchie definite dall'utente nella dimensione Product

1.  Nella barra degli strumenti della scheda **Struttura dimensione** di **Progettazione dimensioni** per la dimensione **Product** fare clic su **Elabora**.

2.  Fare clic su **Sì** per compilare il progetto e distribuirlo e quindi fare clic su **Esegui** per elaborare la dimensione **Product** .

3.  Al termine dell'elaborazione, espandere **Elaborazione di Dimensione 'Product' completata** nella finestra di dialogo **Stato elaborazione** , espandere **Elaborazione di Attributo dimensione 'Product Name' completata**, quindi espandere **Query SQL 1**.

4.  Fare clic sulla query SELECT DISTINCT, quindi su **Visualizza dettagli**.

     Si noti che alla clausola SELECT DISTINCT è stata aggiunta una clausola WHERE che rimuove i prodotti privi di valore nella colonna ProductSubcategoryKey, come illustrato nella figura seguente.

     ![Clausola SELECT DISTINCT con clausola WHERE](../../2014/tutorials/media/l4-productnametraceline-1.gif "Clausola SELECT DISTINCT con clausola WHERE")

5.  Fare clic su **Chiudi** tre volte per chiudere tutte le finestre di dialogo di elaborazione.

6.  Fare clic sulla scheda **Esplorazione** in Progettazione dimensioni per la dimensione **Product** e quindi fare clic su **Riconnetti**.

7.  Verificare che **Product Model Lines** sia visualizzato nell'elenco **gerarchia** , espandere `All Products`, quindi espandere **Components**.

8.  Selezionare **Product Categories** nell'elenco **gerarchia** , espandere `All Products`, quindi espandere **Components**.

     Si noti che non viene visualizzato nessun componente dell'assembly.

 Per modificare il comportamento indicato nell'attività precedente, è necessario abilitare la proprietà **UnknownMember** della dimensione Products, impostare un valore per la proprietà **UnknownMemberName** , impostare la proprietà **NullProcessing** `Subcategory` per gli attributi e **nome modello** su **UnknownMember**, definire l' `Category` attributo come attributo correlato dell' `Subcategory` attributo e quindi definire l'attributo **Product Line** come attributo correlato dell'attributo **Model Name** . Con questa procedura, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] userà il valore di UnknownMemberName per ogni prodotto che non presenta un valore nella colonna **SubcategoryKey** , come si vedrà nell'attività successiva.

## <a name="enabling-the-unknown-member-defining-attribute-relationships-and-specifying-custom-processing-properties-for-nulls"></a>Abilitazione della proprietà UnknownMember, definizione delle relazioni tra attributi e specifica di proprietà di elaborazione personalizzata per i valori Null

1.  Fare clic sulla scheda **Struttura dimensione** in Progettazione dimensioni per la dimensione **Product** , quindi selezionare **Product** nel riquadro **Attributi** .

2.  Nella finestra **Proprietà** modificare la proprietà **UnknownMember** in **Visible**, quindi modificare il valore della proprietà **UnknownMemberName** in `Assembly Components`.

     Modificando la proprietà **UnknownMember** in **Visible** o **Hidden** viene abilitata la proprietà **UnknownMember** per la dimensione.

3.  Fare clic sulla scheda **Relazioni tra attributi** .

4.  Nel diagramma fare clic con il pulsante destro `Subcategory` del mouse sull'attributo e quindi scegliere **nuova relazione tra attributi**.

5.  Nella finestra di dialogo **Crea relazione tra attributi** l' **attributo** di origine `Subcategory`è. Impostare **attributo correlato** su `Category`. Lasciare il tipo di relazione impostato su **Flessibile**.

6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]

7.  Nel riquadro **Attributi** selezionare **Subcategory**.

8.  Nella finestra Proprietà espandere la proprietà **KeyColumns** , quindi la proprietà **DimProductSubcategory.ProductSubcategoryKey (Integer)** .

9. Impostare la proprietà **NullProcessing** su **UnknownMember**.

10. Nel riquadro **Attributi** selezionare **Model Name**.

11. Nella finestra Proprietà espandere la proprietà **KeyColumns** , quindi la proprietà **Product.ModelName (WChar)** .

12. Impostare la proprietà **NullProcessing** su **UnknownMember**.

     A causa di queste modifiche, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] quando rileva un valore null per l' `Subcategory` attributo o l'attributo **Model Name** durante l'elaborazione, il valore del membro sconosciuto verrà sostituito come valore chiave e le gerarchie definite dall'utente verranno costruite correttamente.

## <a name="browsing-the-product-dimension-again"></a>Nuova esplorazione della dimensione Product

1.  Scegliere **Distribuisci Analysis Services Tutorial** dal menu **Compila**.

2.  Al termine della distribuzione fare clic sulla scheda **Esplorazione** in Progettazione dimensioni per la dimensione **Product** e quindi fare clic su **Riconnetti**.

3.  Verificare che **Product Categories** sia selezionato nell'elenco **gerarchia** , quindi espandere `All Products`.

     Si noti che Assembly Components appare come nuovo membro del livello Category.

4.  Espandere il `Assembly Components` membro del `Category` livello, quindi espandere il `Assembly Components` membro del `Subcategory` livello.

     Si noti che tutti i componenti di assembly vengono ora visualizzati nel livello **Product Name** , come illustrato nella figura seguente.

     ![Livello Product Name con visualizzazione dei componenti dell'assembly](../../2014/tutorials/media/l4-assemblycomponents-1.gif "Livello Product Name con visualizzazione dei componenti dell'assembly")

## <a name="next-lesson"></a>Lezione successiva
 [Lezione 5: Definizione delle relazioni tra dimensioni e gruppi di misure](lesson-5-defining-relationships-between-dimensions-and-measure-groups.md)


