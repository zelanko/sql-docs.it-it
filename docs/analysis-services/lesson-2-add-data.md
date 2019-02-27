---
title: 'Lezione 2: Aggiungere dati | Microsoft Docs'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b135362a9f64ac8e1bd0f696f88b8aa92d8af283
ms.sourcegitcommit: c3b190f8f87a4c80bc9126bb244896197a6dc453
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852936"
---
# <a name="lesson-2-add-data"></a>Lezione 2: Aggiungere dati
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

In questa lezione si userà l'importazione guidata tabella in SSDT per connettersi al database SQL AdventureWorksDW di esempio, selezionare i dati, visualizzare in anteprima e filtrare i dati e quindi importare i dati nell'area di lavoro modello.  
  
Mediante l'Importazione guidata tabella è possibile importare dati da un'ampia gamma di origini relazionali: Access, SQL, Oracle, Sybase, Informix, DB2, Teradata e altre ancora. I passaggi per l'importazione dei dati da ognuna di queste origini relazionali sono molto simili a quanto descritto di seguito. I dati possono essere selezionati anche utilizzando una stored procedure. Per altre informazioni sull'importazione di dati e i diversi tipi di origini dati che è possibile importare, vedere [Zdroje dat](../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md).  
  
Tempo stimato per il completamento della lezione: **20 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
Questo argomento fa parte di un'esercitazione relativa alla modellazione tabulare che deve essere completata nell'ordine specificato. Prima di eseguire le attività in questa lezione, è necessario avere completato la lezione precedente: [Lezione 1: Creare un nuovo progetto di modello tabulare](../analysis-services/lesson-1-create-a-new-tabular-model-project.md).  
  
## <a name="create-a-connection"></a>Creare una connessione  
  
#### <a name="to-create-a-connection-to-a-the-adventureworksdw2014-database"></a>Per creare una connessione a un database AdventureWorksDW2014  
  
1.  In Esplora modelli tabulari, fare doppio clic su **Zdroje dat** > **Importa da origine dati**.  
  
    Verrà avviata l'importazione guidata tabella, che ti assisterà l'impostazione di una connessione a un'origine dati. Se non viene visualizzato Esplora modelli tabulari, fare doppio clic su **Model. bim** nelle **Esplora soluzioni** per aprire il modello nella finestra di progettazione. 
    
    ![as-tabular-lesson2-tme](../analysis-services/media/as-tabular-lesson2-tme.png) 

    Nota: Se si crea il modello a livello di compatibilità 1400, scoprirai la nuova esperienza recupera dati anziché l'importazione guidata tabella. Le finestre di dialogo verrà visualizzato un po' diverse dalla procedura, ma sarà comunque in grado di seguire la procedura. 
  
2.  Nell'Importazione guidata tabella, sotto **database relazionali**, fare clic su **Microsoft SQL Server** > **Avanti**.  
  
3.  Nella pagina **Connessione a un database di Microsoft SQL Server** , in **Nome descrittivo connessione**digitare **Adventure Works DB da SQL**.  
  
4.  Nelle **nome Server**, digitare il nome del server in cui è installato il database AdventureWorksDW.  
  
5.  Nel **nome del Database** campi, selezionare **AdventureWorksDW**, quindi fare clic su **Avanti**.  
  
    ![as-tabular-lesson2-tiw-name](../analysis-services/media/as-tabular-lesson2-tiw-name.png)
  
6.  Nella pagina **Impostazioni di rappresentazione** specificare le credenziali usate da Analysis Services per la connessione all'origine dati quando vengono importati ed elaborati i dati. Verificare che l'opzione **Nome utente e password specifici di Windows** sia selezionata, immettere le credenziali di accesso a Windows in **Nome utente** e **Password**e fare clic su **Avanti**.  
  
    > [!NOTE]  
    > L'utilizzo di un account utente e una password di Windows rappresenta il metodo più sicuro per la connessione a un'origine dati. Per altre informazioni, vedere [rappresentazione](../analysis-services/tabular-models/impersonation-ssas-tabular.md).  
  
7.  Nella pagina **Scelta della modalità di importazione dei dati** verificare che l'opzione **Seleziona da un elenco di tabelle e viste per scegliere i dati da importare** sia selezionata. Poiché si vuole selezionare da un elenco di tabelle e viste, fare clic su **Avanti** per visualizzare un elenco di tutte le tabelle di origine nel database di origine.  
  
8.  Nel **selezione tabelle e viste** pagina, selezionare la casella di controllo per le tabelle seguenti: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**,  **DimProductSubcategory**, e **FactInternetSales**.  
  
    **NON** fare clic su **Fine**.  
  
## <a name="FilterData"></a>Filter the table data  
La tabella dimcustomer importata dal database di esempio si sta importando contiene un subset dei dati dal database di SQL Server Adventure Works originale. Verranno escluse tramite filtro ancora delle colonne della tabella DimCustomer che non sono necessarie quando importato nel modello. Quando possibile, è opportuno filtrare i dati che non verrà usati per risparmiare spazio nella memoria utilizzato dal modello.  
  
#### <a name="to-filter-the-table-data-prior-to-importing"></a>Per filtrare i dati della tabella prima dell'importazione  
  
1.  Selezionare la riga per il **DimCustomer** tabella e quindi fare clic su **anteprima e Applica filtro**. Verrà visualizzata la finestra **Anteprima tabella selezionata** in cui sono visualizzate tutte le colonne della tabella di origine DimCustomer visualizzata.  
  
2.  Deselezionare la casella di controllo nella parte superiore delle colonne seguenti. **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**. 

    ![as-tabular-lesson2-tiw-clear](../analysis-services/media/as-tabular-lesson2-tiw-clear.png)
  
    Poiché i valori per queste colonne non sono attinenti all'analisi delle vendite Internet, non è necessario importare queste colonne. Eliminazione delle colonne superflue renderà il modello più piccoli e più efficiente.  
  
3.  Verificare che tutte le altre colonne siano selezionate e fare clic su **OK**.  
  
    Si noti che le parole **filtri applicati** sono ora visualizzate nel **dettagli filtro** colonna il **DimCustomer** riga; se si fa clic su tale collegamento, viene visualizzata una descrizione di testo il filtri che appena applicati.  
    
    ![as-tabular-lesson2-applied-filters](../analysis-services/media/as-tabular-lesson2-applied-filters.png)
    
  
4.  Filtrare le tabelle restanti deselezionando le caselle di controllo per le colonne seguenti in ogni tabella:  
    
    **DimDate**
    
      |colonna|  
      |--------|  
      |**DateKey**|  
      |**SpanishDayNameOfWeek**|  
      |**FrenchDayNameOfWeek**|  
      |**SpanishMonthName**|  
      |**FrenchMonthName**|  
  
    **DimGeography**
  
      |colonna|  
      |-------------|  
      |**SpanishCountryRegionName**|  
      |**FrenchCountryRegionName**|  
      |**IpAddressLocator**|  
  
    **DimProduct**
  
      |colonna|  
      |-----------|  
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
  
    **DimProductCategory**
  
      |colonna|  
      |--------------------|  
      |**SpanishProductCategoryName**|  
      |**FrenchProductCategoryName**|  
  
    **DimProductSubcategory**
  
      |colonna|  
      |-----------------------|  
      |**SpanishProductSubcategoryName**|  
      |**FrenchProductSubcategoryName**|  
  
    **FactInternetSales**
  
      |colonna|  
      |------------------|  
      |**OrderDateKey**|  
      |**DueDateKey**|  
      |**ShipDateKey**|   
  
## <a name="Import"></a>Import the selected tables and column data  
Dopo aver visualizzato in anteprima e filtrati i dati non necessari, è possibile importare il resto dei dati che si desidera. La procedura guidata consente di importare i dati delle tabelle e qualsiasi relazione presente tra le tabelle. Vengono create nuove tabelle e colonne nel modello e non verranno importati i dati esclusi tramite filtro.  
  
#### <a name="to-import-the-selected-tables-and-column-data"></a>Per importare i dati delle tabelle e delle colonne selezionati  
  
1.  Verificare le selezioni. Se tutto sembra corretto, fare clic su **fine**.  
  
    Durante l'importazione dei dati la procedura guidata visualizza il numero di righe recuperate. Una volta importati tutti i dati, verrà visualizzato un messaggio in cui viene indicato il completamento dell'operazione.  
    
    ![as-tabular-lesson2-success](../analysis-services/media/as-tabular-lesson2-success.png) 
  
    > [!TIP]  
    > Per vedere le relazioni create automaticamente tra le tabelle importate, fare clic su **Dettagli** nella riga **Preparazione dati**. 
  
2.  Scegliere **Chiudi**.  
  
    Chiusura della procedura guidata e Progettazione modelli viene ora illustrato le tabelle importate. 
  
## <a name="save-your-model-project"></a>Salvare il progetto di modello  
È importante salvare frequentemente il progetto di modello.  
  
#### <a name="to-save-the-model-project"></a>Per salvare il progetto di modello  
  
-   Click **Salva tutto** > **File**.  
  
## <a name="whats-next"></a>Quali sono le operazioni successive?
Passare alla lezione successiva: [Lezione 3: Contrassegna come tabella data](../analysis-services/lesson-3-mark-as-date-table.md).

  
  
