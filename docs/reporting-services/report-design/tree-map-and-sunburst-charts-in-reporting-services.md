---
title: Grafici mappa ad albero e radiali in SQL Server Reporting Services | Microsoft Docs
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.custom: ''
ms.date: 04/26/2019
ms.openlocfilehash: fd9ac9ccd0906ee34a66b7144fdd964d05e5f050
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "68259359"
---
# <a name="treemap-and-sunburst-charts-in-reporting-services"></a>Grafici mappa ad albero e radiali in Reporting Services 

Le visualizzazioni mappa ad albero e radiali di SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sono ideali per la rappresentazione visiva dei dati gerarchici. Questo argomento offre una panoramica su come aggiungere un grafico mappa ad albero o radiale a un report di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. L'articolo include anche una query di esempio AdventureWorks per iniziare.  
  
##  <a name="treemap-chart"></a><a name="bkmk_treemap_chart"></a> Grafico mappa ad albero  

Un grafico mappa ad albero divide l'area del grafico in rettangoli che rappresentano i diversi livelli e le relative dimensioni della gerarchia dei dati. La mappa è simile ai rami degli alberi che iniziano dal tronco e si suddividono via via in rami sempre più piccoli. Ogni rettangolo viene suddiviso in rettangoli più piccoli che rappresentano il livello successivo nella gerarchia. I rettangoli al livello superiore della mappa ad albero sono disposti con il rettangolo più grande nell'angolo superiore sinistro e il rettangolo più piccolo nell'angolo inferiore destro del grafico.  All'interno di ogni rettangolo, il livello successivo del rettangolo superiore presenta rettangoli dalla parte superiore sinistra fino in basso a destra.  

Ad esempio, nell'immagine di esempio seguente del grafico mappa ad albero il territorio Southwest (Sud-Ovest) è il più grande e il territorio Germany (Germania) è il più piccolo. All'interno di del quadrato Sud-Ovest, il rettangolo Road Bikes è più grande del rettangolo Mountain Bikes.  

![ssrs_treemap_example](../../reporting-services/report-design/media/ssrs-treemap-example.png "ssrs_treemap_example")  
  
### <a name="to-insert-a-treemap-chart-and-set-up-the-sample-adventureworks-data"></a>Per inserire un grafico mappa ad albero e configurare i dati AdventureWorks di esempio  

> [!NOTE]
> Prima di aggiungere un grafico al report, creare un'origine dati e un set di dati.  Per i dati di esempio e una query di esempio, vedere [Dati AdventureWorks di esempio](#bkmk_sample_data).  
  
1. Fare clic con il pulsante destro del mouse nell'area di progettazione e selezionare **Inserisci** > **Grafico**. Selezionare l'icona **Mappa ad albero**.

    ![ssrs_treemap_icon](../../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon")  

2. Riposizionare e ridimensionare il grafico. Per l'uso con i dati di esempio, è consigliabile iniziare con un grafico di 5 pollici.  
  
3. Aggiungere i seguenti campi dai dati di esempio:  
  
    * **Valori**: LineTotal
    * **Gruppi di categorie** (nel seguente ordine):
        1. CategoryName
        2. SubcategoryName
    * **Gruppi di serie**: TerritoryName  

    ![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")
  
4. Per ottimizzare le dimensioni della pagina per la forma generale di un grafico mappa ad albero, impostare la posizione della legenda nella parte inferiore.  
  
5. Per aggiungere descrizioni comando che consentono di visualizzare la sottocategoria e il totale della riga, fare clic con il pulsante destro del mouse su **LineTotal** e selezionare **Proprietà serie**.  
  
     ![ssrs_visualization_seriesproperties](../../reporting-services/report-design/media/ssrs-visualization-seriesproperties.png "ssrs_visualization_seriesproperties")  
  
     Impostare la proprietà **Descrizione comando** con il valore seguente:  
  
    ```
    =Fields!SubcategoryName.Value &": " &Format(Sum(Fields!LineTotal.Value),"C")  
    ```  
  
    Per altre informazioni, vedere [Visualizzare descrizioni comando in una serie &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md).  
  
6. Modificare il titolo predefinito del grafico in **Categorized Sales by Territory**.  
  
7. Il numero di valori di etichetta visualizzati dipende dalle dimensioni del carattere, dalle dimensioni dell'area totale del grafico e dalle dimensioni dei rettangoli specifici. Per visualizzare più etichette, impostare la proprietà **Carattere etichetta** di **LineTotal** su **10 pt** modificando il valore predefinito **8 pt**.  

##  <a name="sunburst-chart"></a><a name="bkmk_sunburst_chart"></a> Grafico radiale  

In un grafico radiale la gerarchia è rappresentata da una serie di cerchi. Il livello più alto della gerarchia si trova al centro e i livelli inferiori della gerarchia sono anelli concentrici.  Il livello più basso della gerarchia è rappresentato dall'anello esterno.  
  
![ssrs_sunburst_example](../../reporting-services/report-design/media/ssrs-sunburst-example.png "ssrs_sunburst_example")  
  
### <a name="to-insert-a-sunburst-chart-and-set-up-the-sample-adventureworks-data"></a>Per inserire un grafico radiale e configurare i dati AdventureWorks di esempio

> [!NOTE]
> Prima di aggiungere un grafico al report, creare un'origine dati e un set di dati. Per i dati di esempio e una query di esempio, vedere [Dati AdventureWorks di esempio](#bkmk_sample_data).  
  
1. Fare clic con il pulsante destro del mouse nell'area di progettazione e selezionare **Inserisci** > **Grafico**. Selezionare l'icona **Radiale**.

     ![ssrs_sunburst_icon](../../reporting-services/media/ssrs-sunburst-icon.png "ssrs_sunburst_icon")  
  
2. Riposizionare e ridimensionare il grafico. Per l'uso con i dati di esempio, è consigliabile iniziare con un grafico di 5 pollici.  
  
3. Aggiungere i seguenti campi dai dati di esempio:  

    * **Valori**: LineTotal
    * **Gruppi di categorie** (nel seguente ordine):
        1. CategoryName
        2. SubcategoryName
        3. SalesReasonName
    * **Gruppi di serie**: TerritoryName  

    ![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")
  
4. Per ottimizzare le dimensioni della pagina per la forma generale di un grafico radiale, impostare la posizione della legenda nella parte inferiore.  
  
5. Modificare il titolo predefinito del grafico in **Categorized Sales by Territory, with sales reason**.  
  
6. Per aggiungere i valori dei gruppi di categoria al grafico radiale come etichette, impostare le proprietà delle etichette come segue: **Visible=true** e **UseValueAsLabel=False**.<br /><br /> I valori di etichetta visualizzati dipendono dalle dimensioni del carattere, dalle dimensioni dell'area totale del grafico e dalle dimensioni dei rettangoli specifici.  Per visualizzare più etichette, impostare la proprietà **Carattere etichetta** di **LineTotal** su **10 pt** modificando il valore predefinito **8 pt**.

    ![ssrs_sunburst_linetotalproperties](../../reporting-services/report-design/media/ssrs-sunburst-linetotalproperties.png "ssrs_sunburst_linetotalproperties")
  
7. Se si desidera una combinazione di colori diversa, modificare la proprietà **Tavolozza** del grafico.  

     ![ssrs_visualization_palette](../../reporting-services/report-design/media/ssrs-visualization-palette.png "ssrs_visualization_palette")  

##  <a name="sample-adventureworks-data"></a><a name="bkmk_sample_data"></a> Dati AdventureWorks di esempio

Questa sezione include una query di esempio e la procedura di base per la creazione di un'origine e di un set di dati in [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)]. Se il report contiene già un'origine e un set di dati, ignorare questa sezione.  
  
La query restituisce dati dettagliati sugli ordini di vendita AdventureWorks con il territorio di vendita, la categoria e la sottocategoria del prodotto e dati sul motivo della vendita.  
  
1. **Ottenere i dati**.  
  
     La query in questa sezione è basata sul database AdventureWorks, disponibile per il download in GitHub: [Adventure Works 2016 full database backup](https://github.com/Microsoft/sql-server-samples/releases) (Backup completo del database Adventure Works 2016).  

2. **Creare un'origine dati**.  
  
    1. In **Dati report** fare clic con il pulsante destro del mouse su **Origini dati** e selezionare **Aggiungi origine dati**.  
  
    2. Selezionare **Usa una connessione incorporata nel report**.  
  
    3. Per il tipo di connessione selezionare **Microsoft SQL Server**.  
  
    4. Immettere la stringa di connessione per il server e il database. Ad esempio:  
  
        ```
        Data Source=[server name];Initial Catalog=AdventureWorks2016  
        ```  
  
    5. Per verificare la connessione fare clic sul pulsante **Verifica connessione** e quindi selezionare **OK**.  
  
     Per altre informazioni sulla creazione di un'origine dati, vedere [Aggiungere e verificare una connessione dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
3. **Creare un set di dati**.  
  
    1. In **Dati report** fare clic con il pulsante destro del mouse su **Set di dati** e selezionare **Aggiungi set di dati**.  
  
    2. Scegliere **Utilizzare un set di dati incorporato nel report**.  
  
    3. Selezionare l'origine dati che è stata creata.  
  
    4. Selezionare il tipo di query **Testo**, quindi copiare e incollare la query seguente nella casella di testo **Query**:  
  
        ```sql
        SELECT    Sales.SalesOrderHeader.SalesOrderID, Sales.SalesOrderHeader.OrderDate, Sales.SalesOrderDetail.SalesOrderDetailID, Sales.SalesOrderDetail.ProductID, Sales.SalesOrderDetail.LineTotal,   
                                 Sales.SalesOrderDetail.UnitPrice, Sales.SalesOrderDetail.OrderQty, Production.Product.Name, Production.Product.ProductNumber, Sales.SalesTerritory.TerritoryID, lower(Sales.SalesTerritory.Name) AS TerritoryName,   
                                 Production.ProductSubcategory.Name AS SubcategoryName, Production.ProductCategory.Name AS CategoryName, Sales.SalesReason.SalesReasonID, Sales.SalesReason.Name AS SalesReasonName  
        FROM            Sales.SalesOrderDetail INNER JOIN  
                                 Sales.SalesOrderHeader ON Sales.SalesOrderDetail.SalesOrderID = Sales.SalesOrderHeader.SalesOrderID INNER JOIN  
                                 Production.Product ON Sales.SalesOrderDetail.ProductID = Production.Product.ProductID INNER JOIN  
                                 Sales.SalesTerritory ON Sales.SalesOrderHeader.TerritoryID = Sales.SalesTerritory.TerritoryID AND Sales.SalesOrderHeader.TerritoryID = Sales.SalesTerritory.TerritoryID AND   
                                 Sales.SalesOrderHeader.TerritoryID = Sales.SalesTerritory.TerritoryID INNER JOIN  
                                 Production.ProductSubcategory ON Production.Product.ProductSubcategoryID = Production.ProductSubcategory.ProductSubcategoryID AND   
                                 Production.Product.ProductSubcategoryID = Production.ProductSubcategory.ProductSubcategoryID AND   
                                 Production.Product.ProductSubcategoryID = Production.ProductSubcategory.ProductSubcategoryID INNER JOIN  
                                 Production.ProductCategory ON Production.ProductSubcategory.ProductCategoryID = Production.ProductCategory.ProductCategoryID AND   
                                 Production.ProductSubcategory.ProductCategoryID = Production.ProductCategory.ProductCategoryID AND   
                                 Production.ProductSubcategory.ProductCategoryID = Production.ProductCategory.ProductCategoryID INNER JOIN  
                                 Sales.SalesOrderHeaderSalesReason ON Sales.SalesOrderHeader.SalesOrderID = Sales.SalesOrderHeaderSalesReason.SalesOrderID AND   
                                 Sales.SalesOrderHeader.SalesOrderID = Sales.SalesOrderHeaderSalesReason.SalesOrderID AND Sales.SalesOrderHeader.SalesOrderID = Sales.SalesOrderHeaderSalesReason.SalesOrderID AND   
                                 Sales.SalesOrderHeader.SalesOrderID = Sales.SalesOrderHeaderSalesReason.SalesOrderID INNER JOIN  
                                 Sales.SalesReason ON Sales.SalesOrderHeaderSalesReason.SalesReasonID = Sales.SalesReason.SalesReasonID AND   
                                 Sales.SalesOrderHeaderSalesReason.SalesReasonID = Sales.SalesReason.SalesReasonID AND Sales.SalesOrderHeaderSalesReason.SalesReasonID = Sales.SalesReason.SalesReasonID AND   
                                 Sales.SalesOrderHeaderSalesReason.SalesReasonID = Sales.SalesReason.SalesReasonID  
        ```  
  
    5. Selezionare **OK**.  
  
     Per altre informazioni sulla creazione di un set di dati, vedere [Creare un set di dati condiviso o un set di dati incorporato &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedere anche

* [Visualizzazione di progettazione set di dati condiviso &#40;Generatore report&#41;](../../reporting-services/report-builder/shared-dataset-design-view-report-builder.md)

* [Visualizzazione di descrizioni comandi in una serie &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)

* [Esercitazione: Mappe ad albero in Power BI](https://support.powerbi.com/knowledgebase/articles/556200-tutorial-treemaps-in-power-bi)

* [Treemap: Microsoft Research Data Visualization Apps for Office (Mappa ad albero: App di visualizzazione dati di Microsoft Research per Office)](https://research.microsoft.com/projects/msrdatavis/treemap.aspx)