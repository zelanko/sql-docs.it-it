---
title: "Lezione 2: Modifica delle proprietà dell'origine dati del report | Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: c962b0ff-ce8a-4742-8262-dc730901afcf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 41679439c7c687cc4574a56369c535f019c77e13
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/28/2020
ms.locfileid: "78176931"
---
# <a name="lesson-2-modifying-the-report-data-source-properties"></a>Lezione 2: Modifica delle proprietà dell'origine dati del report
  In questa lezione verrà utilizzato Gestione report per seleziona un report da recapitare ai destinatari. Con la sottoscrizione guidata dai dati che verrà definita verrà distribuito il report **Ordine vendita** creato nell'esercitazione [Creare un report tabella semplice &#40;esercitazione su SSRS&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md). Nei passaggi seguenti verranno modificate le informazioni di connessione all'origine dei dati utilizzate dal report per acquisire i dati. Solo i report in cui vengono usate **credenziali archiviate** per accedere a un'origine dati del report possono essere distribuiti attraverso una sottoscrizione guidata dai dati. Le credenziali archiviate sono necessarie per l'esecuzione automatica dei report.

 Inoltre, verrà modificato il set di dati e il report per utilizzare un parametro al fine di filtrare il report in `[Order]` in modo che tramite la sottoscrizione sia possibile restituire istanze differenti del report per formati di rendering e ordini specifici.

 **Contenuto dell'argomento:**

-   [Per modificare le proprietà dell'origine dati](#bkmk_modify_datasource)

-   [Per modificare il AdventureWorksDataset](#bkmk_modify_dataset)

-   [Per aggiungere un parametro del report e ripubblicare il report](#bkmk_add_reportparameter)

-   [Per ridistribuire il report](#bkmk_redeploy)

##  <a name="bkmk_modify_datasource"></a>Per modificare le proprietà dell'origine dati

1.  Avviare [Gestione report &#40;modalità nativa SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md) con privilegi di amministratore, ad esempio, fare clic con il pulsante destro del mouse sull'icona di Internet Explorer e scegliere **Esegui come amministratore**.

2.  Selezionare la cartella contenente il report **Ordini vendita** e nel menu di scelta rapida del report fare clic su **Gestisci**.

     ![Aprire il menu di scelta rapida del report e selezionare Gestisci](../../2014/tutorials/media/ssrs-tutorial-datadriven-manage-report.gif "Aprire il menu di scelta rapida del report e selezionare Gestisci")

3.  Fare clic sulla scheda **Origini dati** .

4.  In **tipo di connessione**selezionare **Microsoft SQL Server**.

5.  La stringa di connessione dell'origine dati personalizzata sarà come riportata di seguito; inoltre, si presuppone che il database di esempio si trovi in un server di database locale:

    ```
    Data source=localhost; initial catalog=AdventureWorks2012
    ```

6.  Fare clic su **Credenziali archiviate in modo protetto nel server di report**.

7.  Digitare il nome utente nel formato *dominio\utente*e la password. Se non si dispone delle autorizzazioni per l'accesso al database [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] , specificare un account di accesso autorizzato.

8.  Fare clic su **Usa come credenziali di Windows per la connessione all'origine dei dati**e quindi su **OK**. Se non viene utilizzato un account di dominio, ad esempio se si utilizza un account di accesso di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], non selezionare questa casella di controllo.

9. Fare clic su **Test connessione** per verificare che sia possibile connettersi all'origine dati.

10. Fare clic su **Applica**.

11. Visualizzare il report per verificare che venga eseguito con le credenziali specificate. Per visualizzare il report, fare clic sulla scheda **Visualizza** . si noti che, una volta aperto il report, è necessario selezionare un nome di dipendente e quindi fare clic sul pulsante **Visualizza report** per visualizzare il report.

##  <a name="bkmk_modify_dataset"></a>Per modificare il AdventureWorksDataset

1.  Aprire il report Ordini vendita in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].

2.  Fare clic con il pulsante destro del mouse sul set di dati `AdventureWorksDataset` e scegliere **Proprietà set di dati**.

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

##  <a name="bkmk_add_reportparameter"></a>Per aggiungere un parametro del report e ripubblicare il report

1.  Nel riquadro dei dati del **** report fare clic su **Nuovo** , quindi scegliere **Parametro**.

2.  In **Nome**digitare `OrderNumber`.

3.  In **Messaggio di richiesta**digitare `OrderNumber`.

4.  Selezionare **Consenti nessun valore ("")**.

5.  Selezionare **Consenti valore Null**.

6.  Fare clic su **OK**. Il parametro verrà aggiunto al riquadro dei dati del **** report e l'immagine sarà simile alla seguente:

     ![Il nuovo parametro viene aggiunto al riquadro dei dati del report](../../2014/tutorials/media/ssrs-tutorial-datadriven-parameter.gif "Il nuovo parametro viene aggiunto al riquadro dei dati del report")

7.  Fare clic sulla scheda **Anteprima** per eseguire il report. Si noti la casella di input del parametro nella parte superiore del report. È possibile:

    -   Fare clic su Visualizza report per visualizzare il report completo senza l'utilizzo di parametri.

    -   Deselezionare l'opzione Null e digitare un numero di ordine, ad esempio so71949, per visualizzare solo quell'ordine nel report.

         ![Visualizzatore report con l'area dei parametri visibile](../../2014/tutorials/media/ssrs-tutorial-datadriven-reportviewer-parameter.gif "Visualizzatore report con l'area dei parametri visibile")

8.  Distribuire di nuovo il report in modo che con la configurazione della sottoscrizione nella prossima lezione sia possibile utilizzare le modifiche apportate in questa lezione. Per altre informazioni sulle proprietà del progetto usate nell'esercitazione relativa alla tabella, vedere la sezione "Per pubblicare il report nel server di report (facoltativo)" della [Lezione 6: Aggiunta di gruppi e totali &#40;Reporting Services&#41;](../reporting-services/lesson-6-adding-grouping-and-totals-reporting-services.md).

##  <a name="bkmk_redeploy"></a>Per ridistribuire il report

1.  Distribuire di nuovo il report in modo che con la configurazione della sottoscrizione nella prossima lezione sia possibile utilizzare le modifiche apportate in questa lezione. Per altre informazioni sulle proprietà del progetto usate nell'esercitazione relativa alla tabella, vedere la sezione "Per pubblicare il report nel server di report (facoltativo)" della [Lezione 6: Aggiunta di gruppi e totali &#40;Reporting Services&#41;](../reporting-services/lesson-6-adding-grouping-and-totals-reporting-services.md).

2.  Sulla barra degli strumenti fare clic su **Compila** , quindi scegliere **Distribuisci Tutorial**.

## <a name="next-steps"></a>Passaggi successivi
 In questo modo il report è stato configurato per l'acquisizione di dati utilizzando credenziali archiviate. Il passaggio successivo consiste nell'impostazione della sottoscrizione tramite le pagine relative disponibili in Gestione report. Vedere [Lezione 3: Definizione di una sottoscrizione guidata dai dati](../reporting-services/lesson-3-defining-a-data-driven-subscription.md).

## <a name="see-also"></a>Vedere anche
 [Gestione delle origini dati del report](report-data/manage-report-data-sources.md) [specificare le credenziali e le informazioni di connessione per le origini dati del report](report-data/specify-credential-and-connection-information-for-report-data-sources.md) [creare una sottoscrizione guidata dai dati &#40;esercitazione su SSRS&#41;](../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md) [creare un Report tabella semplice &#40;Esercitazione su SSRS&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)


