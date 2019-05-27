---
title: 'Lezione 8: Creare un filtro dei dati | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 19ccbdba-e3da-40a4-b652-32c628cf32e5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5204cab43e3c801acf80113ec92c51e00c0f9d13
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66108385"
---
# <a name="lesson-8-create-a-data-filter"></a>Lezione 8: Creare un filtro di dati
  Dopo aver aggiunto un'azione drill-through nel report padre, il passaggio successivo consiste nel creare un filtro di dati per la tabella di dati definita per il report figlio.  
  
 È possibile creare un filtro basato su tabella **o** un filtro query per il report drill-through. In questa lezione vengono fornite le istruzioni per entrambe le opzioni.  
  
## <a name="table-based-filter"></a>Filtro basato su tabella  
 È necessario completare le attività seguenti per implementare un filtro basato su tabella.  
  
-   Aggiungere un'espressione di filtro alla Tablix nel report figlio.  
  
-   Creare una funzione mediante la quale vengono selezionati i dati non filtrati dalla tabella `PurchaseOrderDetail`.  
  
-   Aggiungere un gestore eventi mediante il quale viene associato l'oggetto DataTable di `PurchaseOrderDetail` al report figlio.  
  
#### <a name="to-add-a-filter-expression-to-the-tablix-in-the-child-report"></a>Per aggiungere un'espressione di filtro alla Tablix nel report figlio  
  
1.  Aprire il report figlio.  
  
2.  Selezionare un'intestazione di colonna nella tablix, fare clic sulla cella grigia visualizzata sopra l'intestazione di colonna e quindi fare clic su **proprietà Tablix**.  
  
3.  Fare clic sui **filtri** pagina e quindi fare clic su **Add**.  
  
4.  Nel **espressione** segnalati, fare clic su `ProductID` nell'elenco a discesa. Si tratta della colonna a cui applicare il filtro.  
  
5.  Fare clic su di uguale (**=**) operatore nel **operatore** elenco a discesa.  
  
6.  Fare clic sul pulsante espressione accanto al **valore** campo, fare clic su **parametri** nel **categoria** area e quindi fare doppio clic `productid` nel  **I valori** area. Il **imposta espressione per: Valore** campo deve contenere un'espressione simile a **= parametri! productid. Valore**.  
  
7.  Fare clic su **OK,** e **OK** nuovamente il **proprietà Tablix** nella finestra di dialogo.  
  
8.  Salvare il file con estensione rdlc.  
  
#### <a name="to-create-a-function-that-selects-unfiltered-data-from-the-purchaseordedetail-table"></a>Per creare una funzione mediante la quale vengono selezionati i dati non filtrati dalla tabella PurchaseOrderDetail  
  
1.  In Esplora soluzioni espandere Default.aspx, quindi fare doppio clic su Default.aspx.cs.  
  
2.  Creare una nuova funzione che accetta un parametro, `productid`, di tipo Integer, restituisce un oggetto `datatable` e consente di eseguire le operazioni riportate di seguito.  
  
    1.  Crea un'istanza del set di dati, `DataSet2`, che è stato creato nel passaggio 2 della [lezione 4: Definire una connessione dati e un tabella di dati per il Report figlio](lesson-4-define-a-data-connection-and-data-table-for-child-report.md).  
  
    2.  Creare una connessione al database di SQL Server per eseguire la query definita **lezione 4: Definire i dati di un connessione e una tabella dati per il Report figlio**.  
  
    3.  Tramite la query verranno restituiti i dati non filtrati.  
  
    4.  Inserire i dati non filtrati nell'istanza di DataSet eseguendo la query.  
  
    5.  Restituire l'oggetto DataTable di `PurchaseOrderDetail`.  
  
         La funzione sarà simile alla seguente e dovrà essere utilizzata solo come riferimento. È infatti possibile utilizzare qualsiasi modello desiderato per recuperare i dati necessari per il report figlio.  
  
        ```  
        /// <summary>  
            /// Function to query PurchaseOrderDetail table, fetch the  
            /// unfiltered data and bind it with the Child report  
            /// </summary>  
            /// <returns>A dataTable of type PurchaseOrderDetail</returns>  
            private DataTable GetPurchaseOrderDetail()  
            {  
                try  
                {  
                    //Create the instance for the typed dataset, DataSet2 which will   
                    //hold the [PurchaseOrderDetail] table details.  
                    //The dataset was created as part of the tutorial in Step 4.  
                    DataSet2 ds = new DataSet2();  
  
                    //Create a SQL Connection to the AdventureWorks2008 database using Windows Authentication.  
                    using (SqlConnection sqlconn = new SqlConnection("Data Source=.;Initial Catalog=Adventureworks;Integrated Security=SSPI"))  
                    {  
                        //Building the dynamic query with the parameter ProductID.  
                        SqlDataAdapter adap = new SqlDataAdapter("SELECT PurchaseOrderID, PurchaseOrderDetailID, OrderQty, ProductID, ReceivedQty, RejectedQty, StockedQty FROM Purchasing.PurchaseOrderDetail ", sqlconn);  
                        //Executing the QUERY and fill the dataset with the PurchaseOrderDetail table data.  
                        adap.Fill(ds, "PurchaseOrderDetail");  
                    }  
  
                    //Return the PurchaseOrderDetail table for the Report Data Source.  
                    return ds.PurchaseOrderDetail;  
                }  
                catch  
                {  
                    throw;  
                }  
            }  
        ```  
  
#### <a name="to-add-an-event-handler-that-binds-the-purchaseorderdetail-datatable-to-the-child-report"></a>Per aggiungere un gestore eventi mediante il quale viene associato l'oggetto DataTable di PurchaseOrderDetail al report figlio  
  
1.  Aprire Default.aspx.  
  
2.  Fare clic con il pulsante destro del controllo ReportViewer e quindi fare clic su **proprietà.**  
  
3.  Nel **delle proprietà** pagina, fare clic sul **eventi** icona.  
  
4.  Fare doppio clic il **drill-through** evento.  
  
     Verrà aggiunta una sezione del gestore eventi nel codice, che sarà simile al blocco riportato di seguito.  
  
    ```  
    protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
    {  
    }  
    ```  
  
5.  Completare il gestore eventi nel quale dovrebbe essere inclusa la funzionalità riportata di seguito.  
  
    1.  Recuperare il riferimento all'oggetto del report figlio dal parametro *DrillthroughEventArgs* .  
  
    2.  Chiamare la funzione, `GetPurchaseOrderDetail`  
  
    3.  Associare l'oggetto DataTable di `PurchaseOrderDetail` all'origine dati corrispondente del report.  
  
         Il codice del gestore eventi completato sarà simile al seguente.  
  
        ```  
        protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
            {  
                try  
                {  
                     //Get the instance of the Target report, in our case the JumpReport.rdlc.  
                    LocalReport report = (LocalReport)e.Report;  
  
                     //Binding the DataTable to the Child report dataset.  
                    //The name DataSet1 which can be located from,   
                    //Go to Design view of Child.rdlc, Click View menu -> Report Data  
                    //You'll see this name under DataSet2.  
                    report.DataSources.Add(new ReportDataSource("DataSet1", GetPurchaseOrderDetail()));  
                }  
                catch (Exception ex)  
                {  
                    Response.Write(ex.Message);  
                }  
            }  
        ```  
  
6.  Salvare il file.  
  
## <a name="query-filter"></a>Filtro query  
 È necessario completare le attività seguenti per implementare un filtro query.  
  
-   Creare una funzione mediante la quale sono stati selezionati i dati filtrati dalla tabella `PurchaseOrderDetail`.  
  
-   Aggiungere un gestore eventi mediante il quale vengono recuperati i valori dei parametri e viene associato l'oggetto DataTable di `PurchaseOrdeDetail` al report figlio.  
  
#### <a name="to-create-a-function-that-selects-filtered-data-from-the-purchaseorderdetail-table"></a>Per creare una funzione mediante la quale vengono selezionati i dati filtrati dalla tabella PurchaseOrderDetail  
  
1.  In Esplora soluzioni espandere Default.aspx, quindi fare doppio clic su Default.aspx.cs.  
  
2.  Creare una nuova funzione che accetta un parametro, `productid`, di tipo Integer, restituisce un oggetto `datatable` e consente di eseguire le operazioni riportate di seguito.  
  
    1.  Crea un'istanza del set di dati, `DataSet2`, che è stato creato nel passaggio 2 della [lezione 4: Definire una connessione dati e un tabella di dati per il Report figlio](lesson-4-define-a-data-connection-and-data-table-for-child-report.md).  
  
    2.  Creare una connessione al database di SQL Server per eseguire la query definita **lezione 4: Definire i dati di un connessione e una tabella dati per il Report figlio**.  
  
    3.  Nella query sarà incluso un parametro, `productid`, per garantire che i dati restituiti vengano filtrati in base a `ProductID` selezionato nel report padre.  
  
    4.  Inserire i dati filtrati nell'istanza di DataSet eseguendo la query.  
  
    5.  Restituire l'oggetto DataTable di `PurchaseOrderDetail`.  
  
         La funzione sarà simile alla seguente e dovrà essere utilizzata solo come riferimento. È infatti possibile utilizzare qualsiasi modello desiderato per recuperare i dati necessari per il report figlio.  
  
        ```  
        /// <summary>  
            /// Function to query PurchaseOrderDetail table and filter the  
            /// data for a specific ProductID selected in the Parent report.  
            /// </summary>  
            /// <param name="productid">Parameter passed from the Parent report to filter data.</param>  
            /// <returns>A dataTable of type PurchaseOrderDetail</returns>  
            private DataTable GetPurchaseOrderDetail(int productid)  
            {  
                try  
                {  
                    //Create the instance for the typed dataset, DataSet2 which will   
                    //hold the [PurchaseOrderDetail] table details.  
                    //The dataset was created as part of the tutorial in Step 4.  
                    DataSet2 ds = new DataSet2();  
  
                    //Create a SQL Connection to the AdventureWorks2008 database using Windows Authentication.  
                    using (SqlConnection sqlconn = new SqlConnection("Data Source=.;Initial Catalog=Adventureworks;Integrated Security=SSPI"))  
                    {  
                        //Building the dynamic query with the parameter ProductID.  
                        SqlDataAdapter adap = new SqlDataAdapter("SELECT PurchaseOrderID, PurchaseOrderDetailID, OrderQty, ProductID, ReceivedQty, RejectedQty, StockedQty FROM Purchasing.PurchaseOrderDetail where ProductID = " + productid, sqlconn);  
                        //Executing the QUERY and fill the dataset with the PurchaseOrderDetail table data.  
                        adap.Fill(ds, "PurchaseOrderDetail");  
                    }  
  
                    //Return the PurchaseOrderDetail table for the Report Data Source.  
                    return ds.PurchaseOrderDetail;  
                }  
                catch  
                {  
                    throw;  
                }  
            }  
        ```  
  
#### <a name="to-add-an-event-handler-that-retrieves-parameter-values-and-binds-the-purchaseordedetail-datatable-to-the-child-report"></a>Per aggiungere un gestore eventi mediante il quale vengono recuperati i valori dei parametri e viene associato l'oggetto DataTable di PurchaseOrderDetail al report figlio  
  
1.  Aprire Default.aspx.  
  
2.  Il pulsante destro del controllo ReportViewer e quindi fare clic su **proprietà**.  
  
3.  Nel **le proprietà** riquadro, fare clic sul **eventi** icona.  
  
4.  Fare doppio clic il **drill-through** evento.  
  
     Verrà aggiunta una sezione del gestore eventi nel codice, che sarà simile a quanto riportato di seguito.  
  
    ```  
    protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
    {  
    }  
    ```  
  
5.  Completare il gestore eventi nel quale dovrebbe essere inclusa la funzionalità riportata di seguito.  
  
    1.  Recuperare il riferimento all'oggetto del report figlio dal parametro *DrillthroughEventArgs* .  
  
    2.  Ottenere l'elenco dei parametri del report figlio dall'oggetto del report figlio recuperato.  
  
    3.  Scorrere la raccolta dei parametri e recuperare il valore per il parametro, `ProductID`, passato dal report padre.  
  
    4.  Chiamare la funzione, `GetPurchaseOrderDetail`, e passare il valore per il parametro `ProductID`.  
  
    5.  Associare l'oggetto DataTable di `PurchaseOrderDetail` all'origine dati corrispondente del report.  
  
         Il codice del gestore eventi completato sarà simile al seguente.  
  
        ```  
        protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
            {  
                try  
                {  
                    //Variable to store the parameter value passed from the MainReport.  
                    int productid = 0;  
  
                    //Get the instance of the Target report, in our case the JumpReport.rdlc.  
                    LocalReport report = (LocalReport)e.Report;  
  
                    //Get all the parameters passed from the main report to the target report.  
                    //OriginalParametersToDrillthrough actually returns a Generic list of   
                    //type ReportParameter.  
                    IList<ReportParameter> list = report.OriginalParametersToDrillthrough;  
  
                    //Parse through each parameters to fetch the values passed along with them.  
                    foreach (ReportParameter param in list)  
                    {  
                        //Since we know the report has only one parameter and it is not a multivalued,   
                        //we can directly fetch the first value from the Values array.  
                        productid = Convert.ToInt32(param.Values[0].ToString());  
                    }  
  
                    //Binding the DataTable to the Child report dataset.  
                    //The name DataSet1 which can be located from,   
                    //Go to Design view of Child.rdlc, Click View menu -> Report Data  
                    //You'll see this name under DataSet2.  
                    report.DataSources.Add(new ReportDataSource("DataSet1", GetPurchaseOrderDetail(productid)));  
                }  
                catch (Exception ex)  
                {  
                    Response.Write(ex.Message);  
                }  
            }  
        ```  
  
6.  Salvare il file.  
  
## <a name="next-task"></a>Attività successiva  
 È stato creato correttamente un filtro di dati per la tabella di dati definita per il report figlio. Successivamente, verrà compilata ed eseguita l'applicazione del sito Web.  
  
  
