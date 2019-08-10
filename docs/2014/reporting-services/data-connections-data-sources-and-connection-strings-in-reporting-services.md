---
title: Connessioni dati, origini dati e stringhe di connessione in Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- connections [Reporting Services], data sources
- reports [Reporting Services], data
- expressions [Reporting Services], data sources
- data sources [Reporting Services], connections
- connection strings [Reporting Services]
- shared data sources [Reporting Services]
- Reporting Services, data sources
- logins [Reporting Services]
ms.assetid: 4d8f0ae1-102b-4b3d-9155-fa584c962c9e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8147471dc662b651ac9c99cc9290a383cc235ee8
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2019
ms.locfileid: "68891566"
---
# <a name="data-connections-data-sources-and-connection-strings-in-reporting-services"></a>Connessioni dati, origini dati e stringhe di connessione in Reporting Services
  Per includere i dati in un report di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , è necessario creare innanzitutto le *origini dati* e i *set di dati*. Questo argomento illustra il tipo di origini dati, come creare le origini dati e informazioni importanti relative alle credenziali delle origini dati. Un'origine dati include il tipo di origine dati, le informazioni di connessione e il tipo di credenziali da usare. Esistono due tipi di origini dati, ovvero incorporate e condivise. Un'origine dati incorporata viene definita nel report e viene utilizzata solo dal report specifico, mentre un'origine dati condivisa viene definita indipendentemente da un report e può essere utilizzata da più report. Per altre informazioni, vedere [Connessioni dati o origini dati incorporate e condivise &#40;Generatore report e SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md) e [Set di dati condivisi e incorporati &#40;Generatore report e SSRS&#41;](report-data/embedded-and-shared-datasets-report-builder-and-ssrs.md).  
  
||  
|-|  
|**[!INCLUDE[applies](../includes/applies-md.md)]** Modalità nativa di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] &#124; Modalità SharePoint di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  

  
##  <a name="bkmk_data_sources"></a> Origini dati incorporate e condivise  
 La differenza tra le origini dati incorporate e quelle condivise dipende dalle diverse modalità di creazione, archiviazione e gestione.  
  
-   In Progettazione report creare origini dati incorporate o condivise come parte di un progetto di [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] . È possibile controllare se utilizzarle in locale per l'anteprima o distribuirle come parte del progetto in un server di report o in un sito di SharePoint. È possibile utilizzare estensioni per i dati personalizzate installate nel computer e nel server di report o nel sito di SharePoint dove vengono distribuiti i report.  
  
     Gli amministratori di sistema possono installare e configurare estensioni per l'elaborazione dati e provider di dati .NET Framework aggiuntivi. Per altre informazioni, vedere [Estensioni per l'elaborazione dati e provider di dati .NET Framework &#40;SSRS&#41;](report-data/data-processing-extensions-and-net-framework-data-providers-ssrs.md).  
  
     Gli sviluppatori possono usare l'API <xref:Microsoft.ReportingServices.DataProcessing> per creare estensioni per l'elaborazione dati che supportino ulteriori tipi di origine dati.  
  
-   In Generatore report accedere a un server di report o a un sito di SharePoint e selezionare le origini dati condivise oppure creare origini dati incorporate nel report. Non è possibile creare un'origine dati condivisa in Generatore report. Né è possibile usare estensioni per i dati personalizzate in Generatore report.  
  
##  <a name="bkmk_DataConnections"></a> Estensioni per i dati predefinite  
 Le estensioni per i dati predefinite in [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] includono i tipi di connessioni dati seguenti:  
  
-   Microsoft SQL Server  
  
-   Microsoft SQL Server Analysis Services  
  
-   Elenco Microsoft SharePoint  
  
-   [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)]  
  
-   Microsoft SQL Server Parallel Data Warehouse  
  
-   OLE DB  
  
-   Oracle  
  
-   SAP NetWeaver BI  
  
-   Hyperion Essbase  
  
-   Teradata  
  
-   XML  
  
-   ODBC  
  
-   Microsoft BI Semantic Model per Power View: In un sito di SharePoint configurato per una raccolta PowerPivot e [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]questo tipo di origine dati è disponibile. Questo tipo di origine dati viene usato solo per le presentazioni [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] . Per altre informazioni, vedere il video relativo alla [creazione di modelli tabulari BI Semantic perfetti per Power View](https://technet.microsoft.com/video/building-the-perfect-bi-semantic-tabular-models-for-power-view.aspx).  
  
 Per un elenco completo di origini dati e versioni supportate da [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], vedere [Origini dati supportate da Reporting Services &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md).  
  
##  <a name="bkmk_create_data_source"></a>Creare un'origine dati  
 Per creare un'origine dati, è necessario disporre delle informazioni seguenti:  
  
-   **Tipo di origine dati** Tipo di connessione, ad esempio [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Selezionare questo valore nell'elenco a discesa dei tipi di connessione.  
  
-   **Informazioni di connessione** Nelle informazioni di connessione sono inclusi il nome e il percorso dell'origine dati, nonché le proprietà di connessione specifiche di ogni provider di dati. La *stringa di connessione* è la rappresentazione di testo di informazioni di connessione. Ad esempio, se l'origine dati è un database di SQL Server, è possibile specificare il nome del database. Per le origini dati incorporate, è inoltre possibile scrivere stringhe di connessione basate su espressioni che vengono valutate in fase di esecuzione. Per altre informazioni, vedere [Stringhe di connessione basate su espressioni](#bkmk_Expressions_in_connection_strings) più avanti in questo argomento.  
  
-   **Credenziali** Consente di specificare le credenziali necessarie per l'accesso ai dati. Il proprietario dell'origine dati deve concedere all'utente le autorizzazioni appropriate per l'accesso all'origine dati e ai dati specifici di tale origine. Per eseguire, ad esempio, la connessione al database di esempio [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] installato in un server di rete, è necessario disporre dell'autorizzazione per la connessione al server, nonché di quella per l'accesso in sola lettura al database.  
  
    > [!NOTE]  
    >  In base alle caratteristiche di progettazione, le credenziali vengono gestite indipendentemente dalle origini dati. Le credenziali usate per visualizzare in anteprima il report in un sistema locale potrebbero non corrispondere a quelle necessarie per visualizzare il report pubblicato. Dopo aver salvato un'origine dati nel server di report o nel sito di SharePoint, potrebbe essere necessario modificare le credenziali per tale percorso. Per ulteriori informazioni, vedere [Credenziali per le origini dati](#bkmk_credentials).  
  
> [!NOTE]  
>  Quando si crea un'origine dati incorporata per un report in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], è necessario creare l'origine dati di Progettazione report in Esplora soluzioni o nel riquadro dei dati del report, ma non in Esplora server. Progettazione report [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] non supporta origini dati di [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] create in Esplora server.  
  
 Nel riquadro dei dati del report vengono visualizzati origini dati incorporate e riferimenti a origini dati condivise aggiunte al report. In Generatore report un riferimento all'origine dati condivisa punta a un'origine dati condivisa in un server di report o in un sito di SharePoint. In Progettazione report un riferimento all'origine dati condivisa punta a un'origine dati condivisa in Esplora soluzioni nella cartella Origine dati condivisa.  
  
##  <a name="bkmk_credentials"></a>Credenziali per le origini dati  
 In base alle caratteristiche di progettazione, le credenziali possono essere salvate e gestite indipendentemente dalle informazioni di connessione. Vengono usate per creare un'origine dati, per eseguire una query del set di dati e per visualizzare un report in anteprima.  
  
> [!NOTE]  
>  Si consiglia di non includere informazioni di accesso, ad esempio nomi di accesso e password, alle proprietà di connessione dell'origine dati. Usare origini dati condivise con le credenziali archiviate, quando è possibile. In un ambiente di creazione, usare la pagina Credenziali della finestra di dialogo **Origine dati** per immettere credenziali quando si crea una connessione dati o si esegue una query del set di dati.  
  
 Le credenziali immesse per l'accesso ai dati dal computer vengono archiviate in modo protetto nel file di configurazione del progetto locale e sono specifiche del computer. Se si copiano i file di progetto in un altro computer, è necessario ridefinire le credenziali per l'origine dati.  
  
 Quando si distribuisce un report nel server di report o nel sito di SharePoint, le relative origini dati incorporate e condivise vengono gestite in modo indipendente. Le credenziali dell'origine dati necessarie per accedere ai dati dal computer potrebbero non corrispondere da quelle necessarie per l'accesso del server di report ai dati.  
  
 ![Nota](media/rs-fyinote.png "Nota") È consigliabile verificare che le connessioni alle origini dati continuino a connettersi correttamente dopo la pubblicazione di un report. Se è necessario modificare le credenziali, è possibile farlo direttamente nel server di report.  
  
 Per modificare le origini dati utilizzate da un report, è possibile modificare le proprietà del report in modalità nativa Gestione report o dalle raccolte documenti in modalità SharePoint. Per ulteriori informazioni, vedere quanto segue:  
  
-   [Archiviare le credenziali in un'origine dati Reporting Services](report-data/store-credentials-in-a-reporting-services-data-source.md) [Archiviare le credenziali in un'origine dati Reporting Services](report-data/store-credentials-in-a-reporting-services-data-source.md)  
  
-   [Specificare le credenziali e le informazioni sulla connessione per le origini dati del report](report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
-   [Specificare le connessioni per le estensioni per l'elaborazione dati personalizzate](report-data/specify-connections-for-custom-data-processing-extensions.md)  
  
-   [Specifica di credenziali in Generatore report](../../2014/reporting-services/specify-credentials-in-report-builder.md)  
  
-   [Aggiungere e verificare una connessione dati o un'origine &#40;dati Generatore report e SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
##  <a name="bkmk_connection_examples"></a> Esempi comuni di stringhe di connessione  
 Le stringhe di connessione sono la rappresentazione di testo delle proprietà di connessione per un provider di dati. Nella tabella seguente sono elencati esempi di stringhe di connessione per diversi tipi di connessione dati.  
  
|**Origine dati**|**Esempio**|**Descrizione**|  
|---------------------|-----------------|---------------------|  
|Database SQL Server sul server locale|`data source="(local)";initial catalog=AdventureWorks`|Impostare il tipo di origine dati su `Microsoft SQL Server`. Per altre informazioni, vedere [Tipo di connessione SQL Server &#40;SSRS&#41;](report-data/sql-server-connection-type-ssrs.md).|  
|Database SQL Server sul server locale|`data source="(local)";initial catalog=AdventureWorks`|Impostare il tipo di origine dati su `Microsoft SQL Server`.|  
|Istanza di SQL Server<br /><br /> database|`Data Source=localhost\MSSQL10_50.InstanceName; Initial Catalog=AdventureWorks`|Impostare il tipo di origine dati su `Microsoft SQL Server`.|  
|Database SQL Server Express|`Data Source=localhost\MSSQL10_50.SQLEXPRESS; Initial Catalog=AdventureWorks`|Impostare il tipo di origine dati su `Microsoft SQL Server`.|  
|[!INCLUDE[ssSDS](../includes/sssds-md.md)]nel cloud|`Data Source=<host>;Initial Catalog=AdventureWorks; Encrypt=True`|Impostare il tipo di origine dati su `Windows Azure SQL Database`. Per altre informazioni, vedere [Tipo di connessione SQL Azure &#40;SSRS&#41;](report-data/sql-azure-connection-type-ssrs.md).|  
|SQL Server Parallel Data Warehouse|`HOST=<IP address>;database= AdventureWorks; port=<port>`|Impostare il tipo di origine dati su `Microsoft SQL Server Parallel Data Warehouse`. Per altre informazioni, vedere [Tipo di connessione SQL Server Parallel Data Warehouse &#40;SSRS&#41;](report-data/sql-server-parallel-data-warehouse-connection-type-ssrs.md).|  
|Database Analysis Services sul server locale|`data source=localhost;initial catalog=Adventure Works DW`|Impostare il tipo di origine dati su `Microsoft SQL Server Analysis Services`. Per altre informazioni, vedere [Tipo di connessione Analysis Services per MDX &#40;SSRS&#41;](report-data/analysis-services-connection-type-for-mdx-ssrs.md) e [Tipo di connessione di Analysis Services per DMX &#40;SSRS&#41;](report-data/analysis-services-connection-type-for-dmx-ssrs.md).|  
|Database modello tabulare di Analysis Services con la prospettiva Sales|`Data source=<servername>;initial catalog= Adventure Works DW;cube='Sales'`|Impostare il tipo di origine dati su `Microsoft SQL Server Analysis Services`. Specificare il nome della prospettiva nell'impostazione cube=. Per altre informazioni, vedere [Prospettive &#40;SSAS tabulare&#41;](https://docs.microsoft.com/analysis-services/tabular-models/perspectives-ssas-tabular).|  
|Origine dati del modello di report su un server di report configurato in modalità nativa|`Server=http://myreportservername/reportserver; datasource=/models/Adventure Works`|Specificare l'URL del server di report o della raccolta documenti e il percorso di un modello pubblicato nello spazio dei nomi della cartella del server di report o della raccolta documenti.
|Origine dati del modello di report su un server di report configurato in modalità integrata SharePoint|`Server=http://server; datasource=http://server/site/documents/models/Adventure Works.smdl`|Specificare l'URL del server di report o della raccolta documenti e il percorso di un modello pubblicato nello spazio dei nomi della cartella del server di report o della raccolta documenti.|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Server [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 2000|`provider=MSOLAP.2;data source=<remote server name>;initial catalog=FoodMart 2000`|Impostare il tipo di origine dati su `OLE DB Provider for OLAP Services 8.0`.<br /><br /> È possibile ottenere una connessione più veloce alle origini dati [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2000 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] impostando la proprietà `ConnectTo` su `8.0`. Per impostare questa proprietà, usare la finestra di dialogo **Proprietà connessione** nella scheda **Proprietà avanzate** .|  
|Server Oracle|`data source=myserver`|Impostare il tipo di origine dati su `Oracle`. È necessario installare gli strumenti client Oracle nel computer di Progettazione report e nel server di report. Per altre informazioni, vedere [Tipo di connessione Oracle &#40;SSRS&#41;](report-data/oracle-connection-type-ssrs.md).|  
|Origine dati SAP NetWeaver BI|`DataSource=http://mySAPNetWeaverBIServer:8000/sap/bw/xml/soap/xmla`|Impostare il tipo di origine dati su `SAP NetWeaver BI`. Per altre informazioni, vedere [Tipo di connessione SAP NetWeaver BI &#40;SSRS&#41;](report-data/sap-netweaver-bi-connection-type-ssrs.md).|  
|Origine dati Hyperion Essbase|`Data Source=http://localhost:13080/aps/XMLA; Initial Catalog=Sample`|Impostare il tipo di origine dati su `Hyperion Essbase`. Per altre informazioni, vedere [Tipo di connessione Hyperion Essbase &#40;SSRS&#41;](report-data/hyperion-essbase-connection-type-ssrs.md).|  
|Origine dati Teradata|`data source=`\<NNN>.\<NNN>.\<NNN>.\<NNN>`;`|Impostare il tipo di origine dati su `Teradata`. La stringa di connessione è un indirizzo IP (Internet Protocol) nel formato in quattro campi, ognuno dei quali può contenere da una a tre cifre. Per altre informazioni, vedere [Tipo di connessione Teradata &#40;SSRS&#41;](report-data/teradata-connection-type-ssrs.md).|  
|Origine dati XML, servizio Web|`data source=http://adventure-works.com/results.aspx`|Impostare il tipo di origine dati su `XML`. La stringa di connessione è un URL per un servizio Web che supporta Web Services Definition Language (WSDL). Per altre informazioni, vedere [Tipo di connessione XML &#40;SSRS&#41;](report-data/xml-connection-type-ssrs.md).|  
|Origine dati XML, documento XML|`http://localhost/XML/Customers.xml`|Impostare il tipo di origine dati su `XML`. La stringa di connessione è un URL per il documento XML.|  
|Origine dati XML, documento XML incorporato|*Vuoto*|Impostare il tipo di origine dati su `XML`. I dati XML vengono incorporati nella definizione del report.|  
  
Se non è possibile connettersi a un server di report utilizzando `localhost`, verificare che il protocollo di rete per TCP/IP sia abilitato. Per altre informazioni, vedere [Configure Client Protocols](../database-engine/configure-windows/configure-client-protocols.md).  
  
##  <a name="bkmk_special_password_characters"></a> Caratteri speciali in una password  
 Se si configura l'origine dei dati ODBC o SQL per la richiesta di una password o l'inclusione della password nella stringa di connessione e un utente immette la password con caratteri speciali quali segni di punteggiatura, è possibile che alcuni driver dell'origine dei dati sottostante non convalidino i caratteri speciali. In tal caso, quando si elabora il report verrà visualizzato un messaggio che indica che la password non è valida. Se la modifica della password è complessa, è possibile rivolgersi all'amministratore del database per fare in modo che vengano archiviate sul server le credenziali appropriate come parte del nome di un'origine dei dati (DSN) ODBC del sistema. Per altre informazioni, vedere "OdbcConnection.ConnectionString" nella documentazione di [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] SDK.  
  
##  <a name="bkmk_Expressions_in_connection_strings"></a> Stringhe di connessione basate su espressioni  
 Le stringhe di connessione basate su espressioni vengono valutate in fase di esecuzione. È ad esempio possibile specificare l'origine dati come parametro, includere il riferimento del parametro nella stringa di connessione e consentire all'utente di scegliere un'origine dati per il report. Si supponga ad esempio che una società multinazionale abbia server dei dati in diversi paesi. Con una stringa di connessione basata su un'espressione, un utente che esegue un report relativo alle vendite può selezionare un'origine dei dati per un determinato paese prima dell'esecuzione del report.  
  
 Nell'esempio seguente viene illustrato l'utilizzo di un'espressione di origine dati in una stringa di connessione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Nell'esempio si presuppone che sia stato creato un parametro di report denominato `ServerName`:  
  
```  
="data source=" & Parameters!ServerName.Value & ";initial catalog=AdventureWorks"  
```  
  
 Le espressioni delle origini dati vengono elaborate in fase di esecuzione oppure quando si visualizza l'anteprima di un report. L'espressione deve essere scritta in [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]. Utilizzare le linee guida seguenti per definire un'espressione di origine dati:  
  
-   Progettare il report utilizzando una stringa di connessione statica. Un stringa di connessione statica fa riferimento a una stringa di connessione che non viene impostata tramite un'espressione. Una stringa di connessione statica viene definita, ad esempio, quando si esegue la procedura per la creazione di un'origine dei dati in base al report o condivisa. L'utilizzo di una stringa di connessione statica consente all'utente di connettersi all'origine dei dati in Progettazione report per ottenere i risultati della query necessari per la creazione del report.  
  
-   Quando si definisce la connessione all'origine dei dati, non utilizzare un'origine dei dati condivisa. Non è possibile utilizzare un'espressione di origine dati in un'origine dati condivisa. È necessario definire un'origine dati incorporata per il report.  
  
-   Specificare le credenziali separatamente rispetto alla stringa di connessione. È possibile utilizzare credenziali archiviate, credenziali fornite dall'utente o sicurezza integrata.  
  
-   Aggiungere un parametro del report per specificare un'origine dei dati. Per i valori dei parametri è possibile specificare un elenco statico dei valori disponibili, in questo caso le origini dei dati che possono essere utilizzate per il report, oppure definire una query che recupera un elenco di origini dei dati in fase di esecuzione.  
  
-   Assicurarsi che l'elenco delle origini dei dati condivida lo stesso schema di database. Ogni progettazione di report inizia dalle informazioni relative allo schema. Se non c'è corrispondenza tra lo schema utilizzato per definire il report e lo schema effettivamente utilizzato dal report in fase di esecuzione, il report potrebbe non essere eseguito.  
  
-   Prima della pubblicazione del report, sostituire la stringa di connessione statica con un'espressione. Attendere di aver completato la progettazione del report prima di eseguire questa operazione. Dopo aver utilizzato un'espressione, non è possibile eseguire la query in Progettazione report. L'elenco dei campi del riquadro dei dati del report e l'elenco Parametri, inoltre, non verranno aggiornati automaticamente.  
  
## <a name="see-also"></a>Vedere anche  
 [Connessioni dati o origini dati incorporate e condivise &#40;Generatore report e SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)   
 [Gestire origini dati dei report](report-data/manage-report-data-sources.md)   
 [Finestra di dialogo Proprietà origine dati, credenziali](../../2014/reporting-services/data-source-properties-dialog-box-credentials.md)   
 [Finestra di dialogo Proprietà origine dati condivisa, credenziali](../../2014/reporting-services/shared-data-source-properties-dialog-box-credentials.md)   
 [Creare, modificare ed eliminare origini dati condivise &#40;SSRS&#41;](report-data/create-modify-and-delete-shared-data-sources-ssrs.md)   
 [Impostare le proprietà di distribuzione &#40;Reporting Services&#41;](tools/set-deployment-properties-reporting-services.md)   
 [Specificare le credenziali e le informazioni sulla connessione per le origini dati del report](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Aggiungere e verificare una connessione dati o un'origine &#40;dati Generatore report e SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
