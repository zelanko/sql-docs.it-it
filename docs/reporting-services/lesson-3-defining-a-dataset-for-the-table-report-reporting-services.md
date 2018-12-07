---
title: 'Lesson 3: Defining a Dataset for the Table Report (Reporting Services) (Lezione 3: Definizione di un set di dati per il report tabella (Reporting Services)) | Microsoft Docs'
ms.date: 05/23/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: ee93dfcb-8f52-4d63-b4f6-0d38e00fd350
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 60f613e075c032faa9e81b30a48b9d6f630c0b5c
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52516978"
---
# <a name="lesson-3-defining-a-dataset-for-the-table-report-reporting-services"></a>Lezione 3: Definizione di un set di dati per il report tabella (Reporting Services)
Dopo aver definito l'origine dati, è necessario definire un set di dati. In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]i dati utilizzati nei report sono contenuti in un *set di dati*. Un set di dati contiene un puntatore a un'origine dati e la query utilizzata dal report, nonché le variabili e i campi calcolati.  
  
Per progettare il set di dati usare la finestra Progettazione query in Progettazione report. In questa esercitazione verrà creata una query per il recupero delle informazioni sugli ordini di vendita dal database [!INCLUDE [ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] .  
  
### <a name="to-define-a-transact-sql-query-for-report-data"></a>Per definire una query Transact-SQL per i dati del report  
  
1.  Nel riquadro **Dati report** fare clic su **Nuovo**, quindi su **Set di dati...** Verrà visualizzata la finestra di dialogo **Proprietà set di dati** .  
  
2.  Nella casella **Nome** digitare **AdventureWorksDataset**.  
  
3.  Fare clic su **Usare un set di dati incorporato nel report**.  
  
4.  Selezionare l'origine dati creata nella lezione precedente, [!INCLUDE [ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)].   
5. Selezionare **Testo** per **Tipo di query**.  
  
6.  Digitare oppure copiare e incollare la query Transact-SQL seguente nella casella **Query** .  
  
    ```  
    SELECT   
       soh.OrderDate AS [Date],   
       soh.SalesOrderNumber AS [Order],   
       pps.Name AS Subcat, pp.Name as Product,    
       SUM(sd.OrderQty) AS Qty,  
       SUM(sd.LineTotal) AS LineTotal  
    FROM Sales.SalesPerson sp   
       INNER JOIN Sales.SalesOrderHeader AS soh   
          ON sp.BusinessEntityID = soh.SalesPersonID  
       INNER JOIN Sales.SalesOrderDetail AS sd   
          ON sd.SalesOrderID = soh.SalesOrderID  
       INNER JOIN Production.Product AS pp   
          ON sd.ProductID = pp.ProductID  
       INNER JOIN Production.ProductSubcategory AS pps   
          ON pp.ProductSubcategoryID = pps.ProductSubcategoryID  
       INNER JOIN Production.ProductCategory AS ppc   
          ON ppc.ProductCategoryID = pps.ProductCategoryID  
    GROUP BY ppc.Name, soh.OrderDate, soh.SalesOrderNumber, pps.Name, pp.Name,   
       soh.SalesPersonID  
    HAVING ppc.Name = 'Clothing'  
    ```  
  
7.  (Facoltativo) Fare clic sul pulsante **Progettazione query** . La query verrà visualizzata nella finestra Progettazione query basata su testo. È possibile passare alla finestra Progettazione query con interfaccia grafica facendo clic su **Modifica come testo**. Per visualizzare i risultati della query, fare clic sul pulsante di esecuzione ![ssrs_querydesigner_run](../reporting-services/media/ssrs-querydesigner-run.png)  sulla barra degli strumenti Progettazione query.  
  
    Verranno visualizzati i dati contenuti in sei campi di quattro tabelle differenti del database [!INCLUDE [ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] . Nella query vengono utilizzate funzionalità di Transact-SQL come gli alias. Ad esempio, la tabella SalesOrderHeader è denominata *soh*.  
  
8.  Fare clic su **OK** per chiudere la finestra Progettazione query.  
  
9.  Fare clic su **OK** per chiudere la finestra di dialogo **Proprietà set di dati** .  
  
    I campi e il set di dati di **AdventureWorksDataset** vengono visualizzati nel riquadro Dati report.  
    ![ssrs_adventureworksdataset](../reporting-services/media/ssrs-adventureworksdataset.png)  
  
## <a name="next-task"></a>Attività successiva  
In questo modo si è specificata una query che recupera i dati per il report. Il passaggio successivo consiste nella creazione del layout del report. Vedere [Lezione 4: Aggiunta di una tabella al report &#40;Reporting Services&#41;](../reporting-services/lesson-4-adding-a-table-to-the-report-reporting-services.md).  
  
## <a name="see-also"></a>Vedere anche  
[Strumenti di progettazione query &#40;SSRS&#41;](../reporting-services/report-data/query-design-tools-ssrs.md)  
[Tipo di connessione SQL Server &#40;SSRS&#41;](../reporting-services/report-data/sql-server-connection-type-ssrs.md)  
[Esercitazione: Scrittura di istruzioni Transact-SQL](../t-sql/tutorial-writing-transact-sql-statements.md)  
  
  
  

