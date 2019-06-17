---
title: 'Lezione 3: Definizione di un set di dati per il report tabella (Reporting Services) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: ee93dfcb-8f52-4d63-b4f6-0d38e00fd350
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f4c78328e02215520b8d33213e01871f010f62d6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108456"
---
# <a name="lesson-3-defining-a-dataset-for-the-table-report-reporting-services"></a>Lezione 3: Definizione di un set di dati per il report tabella (Reporting Services)
  Dopo aver definito l'origine dati, è necessario definire un set di dati. In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]i dati utilizzati nei report sono contenuti in un *set di dati*. Un set di dati contiene un puntatore a un'origine dati e la query utilizzata dal report, nonché le variabili e i campi calcolati.  
  
 Per progettare la query è possibile utilizzare la finestra Progettazione query in Progettazione report. Per questa esercitazione si creerà una query che recupera informazioni sugli ordini di vendita dal [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] **2008** database.  
  
### <a name="to-define-a-transact-sql-query-for-report-data"></a>Per definire una query Transact-SQL per i dati del report  
  
1.  Nel riquadro **Dati report** fare clic su **Nuovo**, quindi su **Set di dati...** Verrà visualizzata la finestra di dialogo **Proprietà set di dati** .  
  
2.  Nella casella **Nome** digitare **AdventureWorksDataset**.  
  
3.  Fare clic su **Usare un set di dati incorporato nel report**.  
  
4.  Assicurarsi che il nome dell'origine dati, AdventureWorks2012, sia nel **zdroj dat** casella di testo e che le **tipo di Query** viene **testo**.  
  
5.  Digitare oppure copiare e incollare la query Transact-SQL seguente nella casella **Query** .  
  
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
  
6.  (Facoltativo) Fare clic sul pulsante **Progettazione query** . La query verrà visualizzata nella finestra Progettazione query basata su testo. È possibile passare alla finestra Progettazione query con interfaccia grafica facendo clic su **Modifica come testo**. Visualizzare i risultati della query facendo clic su esecuzione **(!)**  pulsante sulla barra degli strumenti Progettazione query.  
  
     Verranno visualizzati i dati contenuti in sei campi di quattro tabelle differenti del database [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] . Nella query vengono utilizzate funzionalità di Transact-SQL come gli alias. La tabella SalesOrderHeader viene ad esempio denominata soh.  
  
     Fare clic su **OK** per chiudere la finestra Progettazione query.  
  
7.  Fare clic su **OK** per chiudere la finestra di dialogo **Proprietà set di dati** .  
  
     I campi e il set di dati di **AdventureWorksDataset** vengono visualizzati nel riquadro Dati report.  
  
## <a name="next-task"></a>Attività successiva  
 In questo modo si è specificata una query che recupera i dati per il report. Il passaggio successivo consiste nella creazione del layout del report. Vedere [Lezione 4: Aggiunta di una tabella al report &#40;Reporting Services&#41;](lesson-4-adding-a-table-to-the-report-reporting-services.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire query di strumenti di progettazione di Report della finestra di progettazione di SQL Server Data Tools &#40;SSRS&#41;](report-data/query-design-tools-ssrs.md)   
 [Tipo di connessione SQL Server &#40;SSRS&#41;](report-data/sql-server-connection-type-ssrs.md)   
 [Esercitazione: Scrittura di istruzioni Transact-SQL](../t-sql/tutorial-writing-transact-sql-statements.md)  
  
  
