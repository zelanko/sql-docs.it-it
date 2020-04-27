---
title: 'Lezione 2: aggiungere dati | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 13c3a8cc-b1db-4aba-ad9b-038b7971be8d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 370e368843fa1e9584cc341397853fcdad26922a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66078969"
---
# <a name="lesson-2-add-data"></a>Lezione 2: Aggiungere dati
  In questa lezione verrà utilizzata l'Importazione guidata tabella in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] per connettersi al database SQL AdventureWorksDW, selezionare i dati, visualizzare un'anteprima, filtrare i dati e quindi importarli nell'area di lavoro del modello.  
  
 Utilizzando l'Importazione guidata tabella è possibile importare dati da diverse origini relazionali, quali Access, SQL, Oracle, Sybase, Informix, DB2, Teradata e così via. I passaggi per l'importazione dei dati da ognuna di queste origini relazionali sono molto simili a quanto descritto di seguito. I dati possono inoltre essere selezionati utilizzando una stored procedure.  
  
 Per altre informazioni sull'importazione di dati e sui diversi tipi di origine dati da cui è possibile importare, vedere [Origini dati &#40;SSAS tabulare&#41;](data-sources-ssas-tabular.md).  
  
 Tempo previsto per il completamento della lezione: **20 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
 Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato. Prima di eseguire le attività in questa lezione, è necessario aver completato la lezione precedente: [Lezione 1: Creare un nuovo modello di progetto tabulare](lesson-1-create-a-new-tabular-model-project.md).  
  
## <a name="create-a-connection"></a>Creare una connessione  
  
#### <a name="to-create-a-connection-to-a-the-adventureworksdw2012-database"></a>Per creare una connessione al database AdventureWorksDW2012  
  
1.  In [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]fare clic sul menu **Modello** e scegliere **Importa da origine dati**.  
  
     Verrà avviata l'Importazione guidata tabella, che consente di eseguire i passaggi per l'impostazione di una connessione a un'origine dati. Se la voce **Importa da origine dati** è disattivata, fare doppio clic su **Model.bim** in **Esplora soluzioni** per aprire il modello nella finestra di progettazione.  
  
2.  Nell' **Importazione guidata tabella**, in **Database relazionali**fare clic su **Microsoft SQL Server**e su **Avanti**.  
  
3.  Nella pagina **connessione a un database di Microsoft SQL Server** , in **nome descrittivo connessione**, digitare `Adventure Works DB from SQL`.  
  
4.  In **Nome server**digitare il nome del server in cui è installato il database AdventureWorksDW.  
  
5.  Nel campo **Nome database** fare clic sulla freccia giù, selezionare **AdventureWorksDW**e scegliere **Avanti**.  
  
6.  Nella pagina **Impostazioni di rappresentazione** specificare le credenziali usate da Analysis Services per la connessione all'origine dati quando vengono importati ed elaborati i dati. Verificare che l'opzione **Nome utente e password specifici di Windows** sia selezionata, immettere le credenziali di accesso a Windows in **Nome utente** e **Password**e fare clic su **Avanti**.  
  
    > [!NOTE]  
    >  L'utilizzo di un account utente e una password di Windows rappresenta il metodo più sicuro per la connessione a un'origine dati. Per altre informazioni, vedere [Rappresentazione &#40;SSAS tabulare&#41;](tabular-models/impersonation-ssas-tabular.md).  
  
7.  Nella pagina **Scelta della modalità di importazione dei dati** verificare che l'opzione **Seleziona da un elenco di tabelle e viste per scegliere i dati da importare** sia selezionata. Poiché si vuole selezionare da un elenco di tabelle e viste, fare clic su **Avanti** per visualizzare un elenco di tutte le tabelle di origine nel database di origine.  
  
8.  Nella pagina **Selezione tabelle e viste** selezionare le caselle di controllo corrispondenti alle tabelle seguenti: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**e **FactInternetSales**.  
  
9. Si desidera fornire nomi più comprensibili per le tabelle nel modello. Fare clic sulla cella nella colonna **Nome descrittivo** per **DimCustomer**. Rinominare la tabella rimuovendo "Dim" da DimCustomer.  
  
10. Rinominare le altre tabelle:  
  
    |Nome origine|Nome descrittivo|  
    |-----------------|-------------------|  
    |DimDate|Date|  
    |DimGeography|Area geografica|  
    |DimProduct|Prodotto|  
    |DimProductCategory|Categoria di prodotto|  
    |DimProductSubcategory|Product Subcategory|  
    |FactInternetSales|Internet Sales|  
  
     **NON** fare clic su **Fine**.  
  
 Dopo avere stabilito la connessione al database, avere selezionato le tabelle da importare e avere assegnato nomi descrittivi alle tabelle, passare alla sezione successiva per [filtrare i dati della tabella prima dell'importazione](#FilterData).  
  
##  <a name="filter-the-table-data"></a><a name="FilterData"></a>Filtrare i dati della tabella  
 La tabella DimCustomer importata dal database contiene un subset dei dati del database SQL Server Adventure Works originale. Verranno filtrate alcune colonne della tabella DimCustomer che non sono necessarie. Quando possibile, utilizzare filtri per escludere dati che non verranno utilizzati, per risparmiare spazio in memoria utilizzato dal modello.  
  
#### <a name="to-filter-the-table-data-prior-to-importing"></a>Per filtrare i dati della tabella prima dell'importazione  
  
1.  Selezionare la riga per la tabella **Customer** e fare clic su **Visualizza anteprima e applica filtro**. Verrà visualizzata la finestra **Anteprima tabella selezionata** in cui sono visualizzate tutte le colonne della tabella di origine DimCustomer visualizzata.  
  
2.  Deselezionare la casella di controllo nella parte superiore delle colonne seguenti.  
  
    |Customer|  
    |--------------|  
    |**SpanishEducation**|  
    |**FrenchEducation**|  
    |**SpanishOccupation**|  
    |**FrenchOccupation**|  
  
     Poiché i valori per queste colonne non sono attinenti all'analisi delle vendite Internet, non è necessario importare queste colonne. Eliminando le colonne non necessarie, è possibile ridurre le dimensioni del modello.  
  
3.  Verificare che tutte le altre colonne siano selezionate e fare clic su **OK**.  
  
     Si noti che le parole **filtri applicati** sono ora visualizzate nella colonna **Dettagli filtro** nella riga **Customer** ; Se si fa clic su tale collegamento, viene visualizzata una descrizione testuale dei filtri appena applicati.  
  
4.  Filtrare le tabelle restanti deselezionando le caselle di controllo per le colonne seguenti in ogni tabella:  
  
    |Date|  
    |----------|  
    |**DateKey**|  
    |**SpanishDayNameOfWeek**|  
    |**FrenchDayNameOfWeek**|  
    |**SpanishMonthName**|  
    |**FrenchMonthName**|  
  
    |Area geografica|  
    |---------------|  
    |**SpanishCountryRegionName**|  
    |**FrenchCountryRegionName**|  
    |**IpAddressLocator**|  
  
    |Prodotto|  
    |-------------|  
    |**SpanishProductName**|  
    |**FrenchProductName**|  
    |**FrenchDescription**|  
    |**ChineseDescription**|  
    |**ArabicDescription**|  
    |**HebrewDescription**|  
    |**ThaiDescription**|  
    |**GermanDescription**|  
    |**JapaneseDescription**|  
    |**TurkishDescription**|  
  
    |Categoria di prodotto|  
    |----------------------|  
    |**SpanishProductCategoryName**|  
    |**FrenchProductCategoryName**|  
  
    |Product Subcategory|  
    |-------------------------|  
    |**SpanishProductSubcategoryName**|  
    |**FrenchProductSubcategoryName**|  
  
    |Internet Sales|  
    |--------------------|  
    |**OrderDateKey**|  
    |**DueDateKey**|  
    |**ShipDateKey**|  
  
 Dopo avere visualizzato l'anteprima ed escluso tramite filtro i dati non necessari, è possibile importare i dati. Passare alla sezione successiva **Importare i dati di tabelle e colonna selezionati**.  
  
##  <a name="import-the-selected-tables-and-column-data"></a><a name="Import"></a>Importa i dati delle tabelle e delle colonne selezionate  
 È ora possibile importare i dati selezionati. La procedura guidata consente di importare i dati delle tabelle e qualsiasi relazione presente tra le tabelle. Nel modello verranno create nuove tabelle e colonne utilizzando i nomi descrittivi specificati e i dati esclusi tramite filtro non verranno importati.  
  
#### <a name="to-import-the-selected-tables-and-column-data"></a>Per importare i dati delle tabelle e delle colonne selezionate  
  
1.  Controllare le selezioni. Se sono corrette, fare clic su **Fine**.  
  
     Durante l'importazione dei dati la procedura guidata visualizza il numero di righe recuperate. Una volta importati tutti i dati, verrà visualizzato un messaggio in cui viene indicato il completamento dell'operazione.  
  
    > [!TIP]  
    >  Per vedere le relazioni create automaticamente tra le tabelle importate, fare clic su **Dettagli** nella riga **Preparazione dati**.  
  
2.  Fare clic su **Chiudi**.  
  
     La procedura guidata verrà chiusa e verrà visualizzata la finestra Progettazione modelli. Ogni tabella è stata aggiunta come nuova scheda in Progettazione modelli.  
  
## <a name="save-the-model-project"></a>Salvare il progetto di modello.  
 È importante salvare frequentemente il progetto di modello.  
  
#### <a name="to-save-the-model-project"></a>Per salvare il progetto del modello  
  
-   In [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]scegliere **Salva tutto** dal menu **File**.  
  
## <a name="next-step"></a>passaggio successivo  
 Per continuare questa esercitazione, passare alla lezione successiva: [Lezione 3: Rinominare colonne](rename-columns.md).  
  
  
