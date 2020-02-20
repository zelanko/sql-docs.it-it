---
title: "Lezione 2: Modifica delle proprietà dell'origine dati del report | Microsoft Docs"
ms.date: 05/23/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: c962b0ff-ce8a-4742-8262-dc730901afcf
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 466415ebd4075afd5dda83e95a498a32b50af453
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "62651726"
---
# <a name="lesson-2-modifying-the-report-data-source-properties"></a>Lezione 2: Modifica delle proprietà dell'origine dati del report
In questa lezione dell'esercitazione [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] verrà usato il portale Web per selezionare un report da recapitare ai destinatari. Con la sottoscrizione guidata dai dati che verrà definita verrà distribuito il report **Ordine vendita** creato nell'esercitazione [Creare un report tabella semplice &#40;esercitazione su SSRS&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md).  Nei passaggi seguenti verranno modificate le informazioni di connessione all'origine dei dati utilizzate dal report per acquisire i dati. Solo i report in cui vengono usate **credenziali archiviate** per accedere a un'origine dati del report possono essere distribuiti attraverso una sottoscrizione guidata dai dati. Le credenziali archiviate sono necessarie per l'esecuzione automatica dei report.  
  
Inoltre, verrà modificato il set di dati e il report per utilizzare un parametro al fine di filtrare il report in `[Order]` in modo che tramite la sottoscrizione sia possibile restituire istanze differenti del report per formati di rendering e ordini specifici.  
  
## <a name="bkmk_modify_datasource"></a>Per modificare l'origine dati per l'uso delle credenziali archiviate  
  
1.  Accedere al portale Web di [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] con privilegi di amministratore, ad esempio, fare clic con il pulsante destro del mouse sull'icona di Internet Explorer e scegliere **Esegui come amministratore**.  
 
2.    Individuare l'URL del portale Web.  Ad esempio:   
    `https://<server name>/reports`.  
    `https://localhost/reports`
 **Nota:** l'URL del *portale* Web è "Reports", non l'URL del *server* di report di "Reportserver".  
3.  Selezionare la cartella contenente il report **Ordini vendita** e nel menu di scelta rapida del report fare clic su **Gestisci**.  
 
 ![ssrs_tutorial_datadriven_manage_report](../reporting-services/media/ssrs-tutorial-datadriven-manage-report.png)
  
3.  Fare clic su **origini dati** nel riquadro a sinistra.  
  
4.  Verificare che il **tipo di connessione** sia **Microsoft SQL Server**.  
  
5.  Verificare che la stringa di connessione sia quella riportata di seguito. Si presuppone che il database di esempio si trovi in un server di database locale:  
  
    ```  
    Data source=localhost; initial catalog=AdventureWorks2014  
    ```  
  
6.  Fare clic su **Usa le credenziali seguenti**.  
  
7. In **Tipo di credenziali**selezionare **Nome utente di Windows e password**
8. Digitare il nome utente nel formato *dominio\utente*e la password. Se non si è autorizzati ad accedere al database AdventureWorks2014, specificare un account di accesso autorizzato.  
    
9. Fare clic su **Test connessione** per verificare che sia possibile connettersi all'origine dati.  
  
10. Fare clic su **Salva**.
11. Fare clic su **Annulla**  
  
11. Visualizzare il report per verificare che venga eseguito con le credenziali specificate. .  
  
## <a name="bkmk_modify_dataset"></a>Per modificare AdventureWorksDataset  
 Nei passaggi successivi si modificherà il set di dati in modo da usare un parametro per filtrare il set di dati in base a un numero di ordine.
1.  Aprire il report **Ordini vendita** in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]  
  
2.  Fare clic con il pulsante destro del mouse sul set di dati `AdventureWorksDataset` e scegliere **Proprietà set di dati**.  
    ![ssrs_tutorial_datadriven_datasetproperties](../reporting-services/media/ssrs-tutorial-datadriven-datasetproperties.png)  
3.  Aggiungere l'istruzione `WHERE (UPPER(SalesOrderNumber) =UPPER(@OrderNumber) or  @OrderNumber IS NULL)` prima dell'istruzione `Group By` . La sintassi della query completa è la seguente:  
  
    ```  
    SELECT soh.OrderDate AS Date, soh.SalesOrderNumber AS [Order], pps.Name AS Subcat, pp.Name AS Product, SUM(sd.OrderQty) AS Qty, SUM(sd.LineTotal)  AS LineTotal  
    FROM Sales.SalesPerson AS sp INNER JOIN  
      Sales.SalesOrderHeader AS soh ON sp.BusinessEntityID = soh.SalesPersonID INNER JOIN  
       Sales.SalesOrderDetail AS sd ON sd.SalesOrderID = soh.SalesOrderID INNER JOIN  
       Production.Product AS pp ON sd.ProductID = pp.ProductID  
    INNER JOIN  
       Production.ProductSubcategory AS pps ON pp.ProductSubcategoryID = pps.ProductSubcategoryID   
    INNER JOIN  
        Production.ProductCategory AS ppc ON ppc.ProductCategoryID = pps.ProductCategoryID  
  
    WHERE (UPPER(SalesOrderNumber) =UPPER(@OrderNumber) or  @OrderNumber IS NULL)  
  
    GROUP BY ppc.Name, soh.OrderDate, soh.SalesOrderNumber, pps.Name, pp.Name, soh.SalesPersonID  
    HAVING (ppc.Name = 'Clothing')  
    ```  
  
4.  Fare clic su **OK**.  
 Nei passaggi seguenti si aggiungerà un parametro al report.  Il parametro del report determina il parametro del set di dati. 
## <a name="bkmk_add_reportparameter"></a>Per aggiungere un parametro del report e ripubblicare il report  
  
1.  Nel riquadro **Dati report** espandere la cartella dei parametri e fare doppio clic sul parametro **Ordernumber** .  Il parametro è stato creato automaticamente nei passaggi precedenti quando è stato aggiunto al set di dati. Fare clic su **Nuovo** e quindi su **Parametro**  
 ![ssrs_tutorial_datadriven_parameter](../reporting-services/media/ssrs-tutorial-datadriven-parameter.png) 
2.  Verificare che **Nome** sia `OrderNumber`.  
  
3.  Verificare che **Prompt** sia `OrderNumber`.  
  
4.  Selezionare **Consenti nessun valore ("")** .  
  
5.  Selezionare **Consenti valore Null**.  
  
6.  Fare clic su **OK**.  
  
7.  Fare clic sulla scheda **Anteprima** per eseguire il report. Notare la casella di input dei parametri nella parte superiore del report. È possibile:  
  
    -   Fare clic su Visualizza report per visualizzare il report completo senza l'utilizzo di parametri.  
  
    -   Deselezionare l'opzione **Null** e digitare un numero di ordine, ad esempio *so71949*, quindi fare clic su **Visualizza report** per visualizzare solo quell'ordine nel report.  
    ![ssrs_tutorial_datadriven_reportviewer_parameter](../reporting-services/media/ssrs-tutorial-datadriven-reportviewer-parameter.png) 
 
  
## <a name="bkmk_redeploy"></a>Ridistribuire il report  
  
1.  Distribuire di nuovo il report in modo che con la configurazione della sottoscrizione nella prossima lezione sia possibile utilizzare le modifiche apportate in questa lezione. Per altre informazioni sulle proprietà del progetto usate nell'esercitazione relativa alla tabella, vedere la sezione "Per pubblicare il report nel server di report (facoltativo)" di [Lezione 6: Aggiunta di gruppi e totali &#40;Reporting Services&#41;](../reporting-services/lesson-6-adding-grouping-and-totals-reporting-services.md).  
  
2.  Sulla barra degli strumenti fare clic su **Compila** , quindi scegliere **Distribuisci Tutorial**.  
  
## <a name="next-steps"></a>Passaggi successivi  
+ In questo modo il report è stato configurato per l'acquisizione di dati usando credenziali archiviate e i dati possono essere filtrati con un parametro. 
+ Nella lezione successiva la sottoscrizione verrà configurata usando le pagine della sottoscrizione guidata dai dati del portale Web. Vedere [Lezione 3: Definizione di una sottoscrizione guidata dai dati](../reporting-services/lesson-3-defining-a-data-driven-subscription.md).  
  
## <a name="see-also"></a>Vedere anche  
[Gestire origini dati dei report](../reporting-services/report-data/manage-report-data-sources.md)  
[Specificare le credenziali e le informazioni sulla connessione per le origini dati del report](../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
[Creare una sottoscrizione guidata dai dati &#40;esercitazione su SSRS&#41;](../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)  
[Creare un report tabella semplice &#40;esercitazione su SSRS&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  
  
  
  

