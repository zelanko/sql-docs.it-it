---
title: 'Lesson 3: Defining a Dataset for the Table Report (Reporting Services) (Lezione 3: Definizione di un set di dati per il report tabella (Reporting Services)) | Microsoft Docs'
ms.date: 05/01/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: ee93dfcb-8f52-4d63-b4f6-0d38e00fd350
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: eaa2af570ae363e6a48c8d14e5b73c70e6790b5c
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2019
ms.locfileid: "65106018"
---
# <a name="lesson-3-defining-a-dataset-for-the-table-report-reporting-services"></a>Lezione 3: Definizione di un set di dati per il report tabella (Reporting Services)

Dopo aver definito l'origine dati, è necessario definire un set di dati. In [!INCLUDE[ssrsnoversion](../includes/ssrsnoversion-md.md)]i dati utilizzati nei report sono contenuti in un *set di dati*. Un set di dati include un puntatore a un'origine dati, la query usata dal report, campi calcolati e variabili.

Per definire il set di dati, usare Progettazione query in Progettazione report. In questa esercitazione si creerà una query che recupera le informazioni relative agli ordini di vendita dal database AdventureWorks2016.

## <a name="define-a-transact-sql-query-for-report-data"></a>Definire una query Transact-SQL per i dati del report  

1. Nel riquadro **Dati report** selezionare **Nuovo** > **Set di dati**. Verrà visualizzata la sezione **Query** della finestra di dialogo **Proprietà set di dati**.

    ![vs-data_set_properties_dialog](media/lesson-3-defining-a-dataset-for-the-table-report-reporting-services/vs-dataset-properties-dialog.png)

2. Nella casella di testo **Nome** digitare "AdventureWorksDataset".

3. Selezionare il pulsante di opzione **Utilizzare un set di dati incorporato nel report** sottostante.

4. Nella casella a discesa **Origine dati** selezionare AdventureWorks2016.

5. Per **Tipo di query** selezionare il pulsante di opzione **Testo**.

6. Digitare oppure copiare e incollare la query Transact-SQL seguente nella casella di testo **Query**.

    ```T-SQL
    SELECT
       soh.OrderDate AS [Date],
       soh.SalesOrderNumber AS [Order],
       pps.Name AS [Subcat],
       pp.Name as [Product],
       SUM(sd.OrderQty) AS [Qty],
       SUM(sd.LineTotal) AS [LineTotal]
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
    GROUP BY ppc.Name, soh.OrderDate, soh.SalesOrderNumber, pps.Name, pp.Name,soh.SalesPersonID  
    HAVING ppc.Name = 'Clothing'
    ```

7. (Facoltativo) Selezionare il pulsante **Progettazione query**. La query verrà visualizzata nella finestra *Progettazione query* basata su testo. Visualizzare i risultati della query selezionando il pulsante **Esegui** ![ssrs_querydesigner_run](media/ssrs-querydesigner-run.png) sulla barra degli strumenti di **Progettazione query**. Il set di dati visualizzato contiene sei campi di quattro tabelle del database AdventureWorks2016. Nella query vengono utilizzate funzionalità di Transact-SQL come gli alias. Ad esempio, la tabella SalesOrderHeader è denominata *soh*.

8. Selezionare **OK** per chiudere **Progettazione query**.

9. Selezionare **OK** per chiudere la finestra di dialogo **Proprietà set di dati**.

Nel riquadro **Dati report** verranno visualizzati il set di dati AdventureWorksDataset e i relativi campi.

   ![ssrs_adventureworksdataset](media/ssrs-adventureworksdataset.png)

## <a name="next-steps"></a>Passaggi successivi

È stata specificata una query che recupera i dati per il report. Verrà ora creato il layout del report. Passare a [Lezione 4: Aggiunta di una tabella al report &#40;Reporting Services&#41;](lesson-4-adding-a-table-to-the-report-reporting-services.md).

## <a name="see-also"></a>Vedere anche

[Strumenti di progettazione query &#40;SSRS&#41;](../reporting-services/report-data/query-design-tools-ssrs.md)
[Tipo di connessione SQL Server &#40;SSRS&#41;](../reporting-services/report-data/sql-server-connection-type-ssrs.md)
[Esercitazione: Scrittura di istruzioni Transact-SQL](../t-sql/tutorial-writing-transact-sql-statements.md)
