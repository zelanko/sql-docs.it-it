---
title: Connessioni in Integration Services (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.asvs.connectionmanager.f1
- sql13.dts.designer.adddtsconnection.f1
helpviewer_keywords:
- Integration Services packages, connections
- SSIS packages, connections
- sources [Integration Services], connections
- packages [Integration Services], connections
- destinations [Integration Services], connections
- tasks [Integration Services], connections
- connections [Integration Services], about connections
- connections [Integration Services]
- SQL Server Integration Services packages, connections
ms.assetid: 72f5afa3-d636-410b-9e81-2ffa27772a8c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7a09cef6ce1e90fe9fce7b7bd4b025598a387c1f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "79112276"
---
# <a name="integration-services-ssis-connections"></a>Connessioni in Integration Services (SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  I pacchetti di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usano le connessioni per eseguire varie attività e implementare le funzionalità di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] seguenti:  
  
-   Connessione ad archivi dati di origine e destinazione, ad esempio file di testo, file XML, cartelle di lavoro di Excel e database relazionali, per l'estrazione e il caricamento dei dati.  
  
-   Connessione a database relazionali contenenti dati di riferimento per l'esecuzione di ricerche esatte o fuzzy.  
  
-   Connessione a database relazionali per l'esecuzione di stored procedure e istruzioni SQL quali i comandi SELECT, DELETE e INSERT.  
  
-   Connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'esecuzione di attività di manutenzione e trasferimento quali il backup di database e il trasferimento di account di accesso.  
  
-   Scrittura di voci di log in file di testo e XML e scrittura di configurazioni di pacchetto e tabelle di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in tabelle di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la creazione di tabelle di lavoro temporanee, necessarie per l'esecuzione delle operazioni previste da alcune trasformazioni.  
  
-   Connessione a database e progetti di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per l'accesso a modelli di data mining, l'elaborazione di cubi e dimensioni, nonché l'esecuzione di codice DDL.  
  
-   Creazione o indicazione di file e cartelle da utilizzare con attività ed enumeratori del ciclo Foreach.  
  
-   Connessione a code di messaggi e a server di posta elettronica, Web, Strumentazione gestione Windows (WMI) e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects (SMO).  
  
 Per stabilire queste connessioni, in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] vengono utilizzate le gestioni connessioni, come descritto nella sezione successiva.  
  
## <a name="connection-managers"></a>Gestioni connessioni  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] viene utilizzata la gestione connessione come rappresentazione logica di una connessione. In fase di progettazione si impostano le proprietà della gestione connessione per descrivere la connessione fisica che verrà creata da [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] durante l'esecuzione del pacchetto. Le gestioni connessioni includono ad esempio la proprietà **ConnectionString** , che viene impostata in modalità progettazione. In fase di esecuzione verrà quindi creata una connessione fisica utilizzando il valore archiviato nella proprietà relativa alla stringa di connessione.  
  
 In un pacchetto è possibile utilizzare più istanze di un determinato tipo di gestione connessione ed è possibile impostare proprietà specifiche per ogni istanza. In fase di esecuzione ogni istanza di un determinato tipo di gestione connessione crea una connessione con attributi diversi.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] offre diversi tipi di gestioni connessioni che consentono di stabilire connessioni tra i pacchetti e un'ampia gamma di server e origini dati:  
  
-   Durante l'installazione di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]vengono installate le gestioni connessioni predefinite.  
  
-   Dal sito Web [!INCLUDE[msCoName](../../includes/msconame-md.md)] è possibile scaricare alcune gestioni connessioni.  
  
-   Se le gestioni connessioni esistenti non soddisfano le proprie esigenze, è possibile creare una gestione connessione personalizzata.  

### <a name="package-level-and-project-level-connection-managers"></a>Gestioni connessioni al livello del pacchetto e del progetto
Una gestione connessione può essere creata al livello del pacchetto o al livello del progetto. La gestione connessione creata al livello del progetto è disponibile per tutti i pacchetti nel progetto. La gestione connessione creata al livello del pacchetto è invece disponibile per quel pacchetto specifico.  
  
 È possibile utilizzare le gestioni connessioni create a livello di progetto al posto delle origini dati per condividere le connessioni alle origini. Per aggiungere una gestione connessione a livello del progetto, nel progetto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] deve essere utilizzato il modello di distribuzione del progetto. Quando un progetto viene configurato per usare questo modello, in **Esplora soluzioni** viene aggiunta la cartella **Gestioni connessioni** e rimossa la cartella **Origini dati** dal **Esplora soluzioni**.  
  
> [!NOTE]  
>  Se si desidera utilizzare le origini dati del pacchetto, è necessario convertire il progetto nel modello di distribuzione del pacchetto.  
>   
>  Per altre informazioni sui due modelli e sulla conversione di un progetto nel modello di distribuzione del progetto, vedere [Distribuire progetti e pacchetti di Integration Services (SSIS)](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md).

### <a name="built-in-connection-managers"></a>Gestioni connessioni predefinite  
 Nella tabella seguente sono elencati i tipi di gestione connessione disponibili in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Type|Descrizione|Argomento|  
|----------|-----------------|-----------|  
|ADO|Consente di connettersi a oggetti ADO (ActiveX Data Objects).|[Gestione connessione ADO](../../integration-services/connection-manager/ado-connection-manager.md)|  
|ADO.NET|Consente di connettersi a un'origine dei dati tramite un provider .NET.|[Gestione connessione ADO.NET](../../integration-services/connection-manager/ado-net-connection-manager.md)|  
|CACHE|Consente di leggere i dati dal flusso di dati o da un file di cache (caw) e di salvare i dati nel file di cache.|[Gestione connessione della cache](../../integration-services/connection-manager/cache-connection-manager.md)|  
|DQS|Consente di connettersi a un server Data Quality Services e a un database Data Quality Services nel server.|[Gestione connessione DQS Cleansing](../../integration-services/connection-manager/dqs-cleansing-connection-manager.md)|  
|EXCEL|Consente di connettersi a un file della cartella di lavoro di Excel.|[Gestione connessione Excel](../../integration-services/connection-manager/excel-connection-manager.md)|  
|FILE|Consente di connettersi a un file o a una cartella.|[Gestione connessione file](../../integration-services/connection-manager/file-connection-manager.md)|  
|FLATFILE|Consente di connettersi ai dati contenuti in un singolo file flat.|[Gestione connessione file flat](../../integration-services/connection-manager/flat-file-connection-manager.md)|  
|FTP|Consente di connettersi a un server FTP.|[Gestione connessione FTP](../../integration-services/connection-manager/ftp-connection-manager.md)|  
|HTTP|Consente di connettersi a un server Web.|[Gestione connessione HTTP](../../integration-services/connection-manager/http-connection-manager.md)|  
|MSMQ|Consente di connettersi a una coda di messaggi.|[Gestione connessione MSMQ](../../integration-services/connection-manager/msmq-connection-manager.md)|  
|MSOLAP100|Consente di connettersi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o a un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|[Gestione connessione Analysis Services](../../integration-services/connection-manager/analysis-services-connection-manager.md)|  
|MULTIFILE|Consente di connettersi a più file e cartelle.|[Gestione connessione per più file](../../integration-services/connection-manager/multiple-files-connection-manager.md)|  
|MULTIFLATFILE|Consente di connettersi a più file e cartelle di dati.|[Gestione connessione per più file flat](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)|  
|OLEDB|Consente di connettersi a un'origine dei dati tramite un provider OLE DB.|[Gestione connessione OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md)|  
|ODBC|Consente di connettersi a un'origine dei dati tramite ODBC.|[Gestione connessione ODBC](../../integration-services/connection-manager/odbc-connection-manager.md)|  
|SMOServer|Consente di connettersi a un server SMO ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects).|[Gestione connessione SMO](../../integration-services/connection-manager/smo-connection-manager.md)|  
|SMTP|Consente di connettersi a un server di posta SMTP.|[Gestione connessione SMTP](../../integration-services/connection-manager/smtp-connection-manager.md)|  
|SQLMOBILE|Consente di connettersi a un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.|[Gestione connessione SQL Server Compact Edition](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|  
|WMI|Consente di connettersi a un server e specifica l'ambito della gestione WMI (Windows Management Instrumentation, Strumentazione gestione Windows) sul server.|[Gestione connessione WMI](../../integration-services/connection-manager/wmi-connection-manager.md)|  
  
### <a name="connection-managers-available-for-download"></a>Gestioni connessioni disponibili per download  
 Nella tabella seguente sono elencati i tipi aggiuntivi di gestione connessione che è possibile scaricare dal sito Web [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
> [!IMPORTANT]  
>  Le gestioni connessioni elencate nella tabella seguente funzionano unicamente con [!INCLUDE[ssEnterpriseEd11](../../includes/ssenterpriseed11-md.md)] e [!INCLUDE[ssDeveloperEd11](../../includes/ssdevelopered11-md.md)].  
  
|Type|Descrizione|Argomento|  
|----------|-----------------|-----------|  
|ORACLE|Consente di connettersi a un server Oracle \<informazioni versione\>.|La gestione connessione Oracle è il componente per la gestione delle connessioni del connettore [!INCLUDE[msCoName](../../includes/msconame-md.md)] per Oracle di Attunity. Il connettore [!INCLUDE[msCoName](../../includes/msconame-md.md)] per Oracle di Attunity include anche un'origine e una destinazione. Per ulteriori informazioni, vedere la pagina di download relativa ai [connettori Microsoft per Oracle e Teradata di Attunity](https://go.microsoft.com/fwlink/?LinkId=251526).|  
|SAPBI|Consente di connettersi a un sistema SAP NetWeaver BI versione 7.|La gestione connessione SAP BI è il componente per la gestione delle connessioni del connettore [!INCLUDE[msCoName](../../includes/msconame-md.md)] per SAP BI. Il connettore [!INCLUDE[msCoName](../../includes/msconame-md.md)] per SAP BI include anche un'origine e una destinazione. Per ulteriori informazioni, vedere la pagina di download relativa al [Feature Pack di Microsoft SQL Server 2008](https://www.microsoft.com/download/details.aspx?id=30440).|  
|TERADATA|Consente di connettersi a un server Teradata \<informazioni versione\>.|La gestione connessione Teradata è il componente per la gestione delle connessioni del connettore [!INCLUDE[msCoName](../../includes/msconame-md.md)] per Teradata di Attunity. Il connettore [!INCLUDE[msCoName](../../includes/msconame-md.md)] per Teradata di Attunity include anche un'origine e una destinazione. Per ulteriori informazioni, vedere la pagina di download relativa ai [connettori Microsoft per Oracle e Teradata di Attunity](https://go.microsoft.com/fwlink/?LinkId=251526).|  
  
### <a name="custom-connection-managers"></a>Gestioni connessioni personalizzate  
 È inoltre possibile scrivere gestioni connessioni personalizzate. Per ulteriori informazioni, vedere [Developing a Custom Connection Manager](../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md).  
  
## <a name="create-connection-managers"></a>Creare gestioni connessioni
  In [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] è disponibile un'ampia gamma di gestioni connessioni che consentono di soddisfare le esigenze di attività che si connettono a diversi tipi di server e origini dati. Le gestioni connessioni vengono utilizzate dai componenti del flusso di dati che estraggono e caricano dati in diversi tipi di archivi dati e dai provider di log che scrivono log in un server, in una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o in un file. Un pacchetto che include un'attività Invia messaggi, ad esempio, utilizza un tipo di gestione connessione SMTP (Simple Mail Transfer Protocol) per connettersi a un server SMTP. Un pacchetto che include un'attività Esegui SQL può usare una gestione connessione OLE DB per connettersi a un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Connessioni in Integration Services &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md).  
  
 Per creare e configurare automaticamente gestioni connessioni durante la creazione di un nuovo pacchetto, è possibile usare Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La procedura guidata consente anche di creare e configurare le origini e le destinazioni che usano le gestioni connessioni. Per altre informazioni, vedere [Creare pacchetti in SQL Server Data Tools](../../integration-services/create-packages-in-sql-server-data-tools.md).  
  
 Per creare manualmente una nuova gestione connessione e aggiungerla a un pacchetto esistente, è possibile usare l'area **Gestioni connessioni** disponibile nelle schede **Flusso di controllo**, **Flusso di dati** e **Gestori eventi** di Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)]. Dall'area **Gestione connessione** è possibile scegliere il tipo di gestione connessione da creare e quindi impostare le proprietà della gestione connessione utilizzando la finestra di dialogo disponibile in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)]. Per ulteriori informazioni, vedere la sezione "Utilizzo dell'area Gestioni connessioni" più avanti in questo argomento.  
  
 Dopo avere aggiunto la gestione connessione a un pacchetto è possibile utilizzarla in attività, contenitori Ciclo Foreach, origini, trasformazioni e destinazioni. Per altre informazioni, vedere [Attività di Integration Services](../../integration-services/control-flow/integration-services-tasks.md), [Contenitore Ciclo Foreach](../../integration-services/control-flow/foreach-loop-container.md) e [Flusso di dati](../../integration-services/data-flow/data-flow.md).  
  
### <a name="using-the-connection-managers-area"></a>Utilizzo dell'area Gestioni connessioni  
 È possibile creare gestioni connessioni quando è attiva la scheda **Flusso di controllo**, **Flusso di dati** o **Gestori eventi** di Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)].  
  
 Nella figura seguente viene illustrata l'area **Gestioni connessioni** della scheda **Flusso di controllo** di Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)].  
  
 ![Screenshot della finestra di progettazione del flusso di controllo con pacchetto](../../integration-services/connection-manager/media/samplecontrolflow.gif "Screenshot della finestra di progettazione del flusso di controllo con pacchetto")    
  
### <a name="32-bit-and-64-bit-providers-for-connection-managers"></a>Provider a 32 e 64 bit per le gestioni connessioni  
 Molti dei provider utilizzati dalle gestioni connessioni sono disponibili sia in versione a 32 bit che in versione a 64 bit. Poiché l'ambiente di progettazione [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] è a 32 bit, durante la progettazione dei pacchetti in tale ambiente sono disponibili solo provider a 32 bit. Pertanto è possibile solo configurare una gestione connessione in modo da utilizzare uno specifico provider a 64 bit, se nel computer è installata anche la versione a 32 bit dello stesso provider.  
  
 In fase di esecuzione viene utilizzata la versione corretta, anche se in fase di progettazione era stata specificata la versione a 32 bit del provider. È possibile eseguire la versione a 64 bit del provider anche se il pacchetto viene eseguito in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
  Entrambe le versioni del provider hanno lo stesso ID. Per specificare se il runtime [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] deve usare la versione a 64 bit del provider, è necessario impostare la proprietà Run64BitRuntime del progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Se la proprietà Run64BitRuntime è impostata su **true**, il runtime trova e usa il provider a 64 bit, se invece Run64BitRuntime è impostata su **false**, il runtime trova e usa il provider a 32 bit. Per altre informazioni sulle proprietà che è possibile impostare in progetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vedere [Integration Services (SSIS) e ambienti Studio](https://msdn.microsoft.com/library/ms140028.aspx).   

## <a name="add-a-connection-manager"></a>Aggiungere una gestione connessione
###  <a name="add-a-connection-manager-when-you-create-a-package"></a><a name="wizard"></a> Aggiungere una gestione connessione durante la creazione di un pacchetto  
  
-   Utilizzare l'Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     Oltre a creare e configurare una gestione connessione, tramite la procedura guidata è anche possibile creare e configurare le origini e le destinazioni in cui è utilizzata la gestione connessione. Per altre informazioni, vedere [Creare pacchetti in SQL Server Data Tools](../../integration-services/create-packages-in-sql-server-data-tools.md).  
  
###  <a name="add-a-connection-manager-to-an-existing-package"></a><a name="package"></a> Aggiungere una gestione connessione a un pacchetto esistente  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo  
  
3.  In Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] fare clic sulla scheda **Flusso di controllo** , **Flusso di dati** o **Gestore evento** in modo da rendere disponibile l'area **Gestioni connessioni** .  
  
4.  Fare clic in un punto qualsiasi dell'area **Gestioni connessioni** , quindi eseguire una delle operazioni seguenti:  
  
    -   Fare clic sul tipo di gestione connessione da aggiungere al pacchetto.  
  
         -oppure-  
  
    -   Se il tipo desiderato non è incluso nell'elenco, fare clic su **Nuova connessione** . Verrà visualizzata la finestra di dialogo **Aggiungi gestione connessione SSIS** . Selezionare un tipo di gestione connessione, quindi fare clic su **OK**.  
  
     Verrà visualizzata la finestra di dialogo specifica per il tipo di gestione connessione selezionato. Per ulteriori informazioni sui tipi di gestione connessione e sulle opzioni disponibili, vedere la tabella seguente.  
  
    |Gestione connessione|Opzioni|  
    |------------------------|-------------|  
    |[Gestione connessione ADO](../../integration-services/connection-manager/ado-connection-manager.md)|[Configura gestione connessione OLE DB](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[Gestione connessione ADO.NET](../../integration-services/connection-manager/ado-net-connection-manager.md)|[Configura gestione connessione ADO.NET](../../integration-services/connection-manager/configure-ado-net-connection-manager.md)|  
    |[Gestione connessione Analysis Services](../../integration-services/connection-manager/analysis-services-connection-manager.md)|[Riferimento all'interfaccia utente della finestra di dialogo Aggiungi gestione connessione Analysis Services](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Gestione connessione Excel](../../integration-services/connection-manager/excel-connection-manager.md)|[Editor gestione connessione Excel](../../integration-services/connection-manager/excel-connection-manager-editor.md)|  
    |[Gestione connessione file](../../integration-services/connection-manager/file-connection-manager.md)|[Editor gestione connessione file](../../integration-services/connection-manager/file-connection-manager-editor.md)|  
    |[Gestione connessione per più file](../../integration-services/connection-manager/multiple-files-connection-manager.md)|[Riferimento all'interfaccia utente della finestra di dialogo Aggiungi gestione connessione file](../../integration-services/connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[Gestione connessione file flat](../../integration-services/connection-manager/flat-file-connection-manager.md)|[Editor gestione connessione file flat &#40;pagina Generale&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md)<br /><br /> [Editor gestione connessione file flat &#40;pagina Colonne&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [Editor gestione connessione file flat &#40;pagina Avanzate&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [Editor gestione connessione file flat &#40;pagina Anteprima&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md)|  
    |[Gestione connessione per più file flat](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)|[Editor gestione connessione per più file flat &#40;pagina Generale&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [Editor gestione connessione per più file flat &#40;pagina Colonne&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [Editor gestione connessione per più file flat &#40;pagina Avanzate&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [Editor gestione connessione per più file flat &#40;pagina Anteprima&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[Gestione connessione FTP](../../integration-services/connection-manager/ftp-connection-manager.md)|[Editor gestione connessione FTP](../../integration-services/connection-manager/ftp-connection-manager-editor.md)|  
    |[Gestione connessione HTTP](../../integration-services/connection-manager/http-connection-manager.md)|[Editor gestione connessione HTTP &#40;pagina Server&#41;](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)<br /><br /> [Editor gestione connessione HTTP &#40;pagina Proxy&#41;](../../integration-services/connection-manager/http-connection-manager-editor-proxy-page.md)|  
    |[Gestione connessione MSMQ](../../integration-services/connection-manager/msmq-connection-manager.md)|[Editor gestione connessione MSMQ](../../integration-services/connection-manager/msmq-connection-manager-editor.md)|  
    |[Gestione connessione ODBC](../../integration-services/connection-manager/odbc-connection-manager.md)|[Riferimento all'interfaccia utente di Gestione connessione ODBC](../../integration-services/connection-manager/odbc-connection-manager-ui-reference.md)|  
    |[Gestione connessione OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md)|[Configura gestione connessione OLE DB](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[Gestione connessione SMO](../../integration-services/connection-manager/smo-connection-manager.md)|[Editor gestione connessione SMO](../../integration-services/connection-manager/smo-connection-manager-editor.md)|  
    |[Gestione connessione SMTP](../../integration-services/connection-manager/smtp-connection-manager.md)|[Editor gestione connessione SMTP](../../integration-services/connection-manager/smtp-connection-manager-editor.md)|  
    |[Gestione connessione SQL Server Compact Edition](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|[Editor gestione connessione SQL Server Compact Edition &#40;pagina Connessione&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [Editor gestione connessione SQL Server Compact Edition &#40;pagina Tutte&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[Gestione connessione WMI](../../integration-services/connection-manager/wmi-connection-manager.md)|[Editor gestione connessione WMI](../../integration-services/connection-manager/wmi-connection-manager-editor.md)|  
  
     Nell'area **Gestioni connessioni** è indicata la gestione connessione aggiunta.  
  
5.  Facoltativamente, fare clic con il pulsante destro del mouse sulla gestione connessione, scegliere **Rinomina**, quindi modificare il nome predefinito della gestione connessione.  
  
6.  Per salvare il pacchetto aggiornato scegliere **Salva elementi selezionati** dal menu **File** .  
  
###  <a name="add-a-connection-manager-at-the-project-level"></a><a name="project"></a> Aggiungere una gestione connessione al livello del progetto  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
2.  In **Esplora soluzioni**fare clic con il pulsante destro del mouse su **Gestioni connessioni**, quindi fare clic su **Nuova gestione connessione**.  
  
3.  Nella finestra di dialogo **Aggiungi gestione connessione SSIS** selezionare il tipo di gestione connessione, quindi scegliere **Aggiungi**.  
  
     Verrà visualizzata la finestra di dialogo specifica per il tipo di gestione connessione selezionato. Per ulteriori informazioni sui tipi di gestione connessione e sulle opzioni disponibili, vedere la tabella seguente.  
  
    |Gestione connessione|Opzioni|  
    |------------------------|-------------|  
    |[Gestione connessione ADO](../../integration-services/connection-manager/ado-connection-manager.md)|[Configura gestione connessione OLE DB](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[Gestione connessione ADO.NET](../../integration-services/connection-manager/ado-net-connection-manager.md)|[Configura gestione connessione ADO.NET](../../integration-services/connection-manager/configure-ado-net-connection-manager.md)|  
    |[Gestione connessione Analysis Services](../../integration-services/connection-manager/analysis-services-connection-manager.md)|[Riferimento all'interfaccia utente della finestra di dialogo Aggiungi gestione connessione Analysis Services](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Gestione connessione Excel](../../integration-services/connection-manager/excel-connection-manager.md)|[Editor gestione connessione Excel](../../integration-services/connection-manager/excel-connection-manager-editor.md)|  
    |[Gestione connessione file](../../integration-services/connection-manager/file-connection-manager.md)|[Editor gestione connessione file](../../integration-services/connection-manager/file-connection-manager-editor.md)|  
    |[Gestione connessione per più file](../../integration-services/connection-manager/multiple-files-connection-manager.md)|[Riferimento all'interfaccia utente della finestra di dialogo Aggiungi gestione connessione file](../../integration-services/connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[Gestione connessione file flat](../../integration-services/connection-manager/flat-file-connection-manager.md)|[Editor gestione connessione file flat &#40;pagina Generale&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md)<br /><br /> [Editor gestione connessione file flat &#40;pagina Colonne&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [Editor gestione connessione file flat &#40;pagina Avanzate&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [Editor gestione connessione file flat &#40;pagina Anteprima&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md)|  
    |[Gestione connessione per più file flat](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)|[Editor gestione connessione per più file flat &#40;pagina Generale&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [Editor gestione connessione per più file flat &#40;pagina Colonne&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [Editor gestione connessione per più file flat &#40;pagina Avanzate&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [Editor gestione connessione per più file flat &#40;pagina Anteprima&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[Gestione connessione FTP](../../integration-services/connection-manager/ftp-connection-manager.md)|[Editor gestione connessione FTP](../../integration-services/connection-manager/ftp-connection-manager-editor.md)|  
    |[Gestione connessione HTTP](../../integration-services/connection-manager/http-connection-manager.md)|[Editor gestione connessione HTTP &#40;pagina Server&#41;](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)<br /><br /> [Editor gestione connessione HTTP &#40;pagina Proxy&#41;](../../integration-services/connection-manager/http-connection-manager-editor-proxy-page.md)|  
    |[Gestione connessione MSMQ](../../integration-services/connection-manager/msmq-connection-manager.md)|[Editor gestione connessione MSMQ](../../integration-services/connection-manager/msmq-connection-manager-editor.md)|  
    |[Gestione connessione ODBC](../../integration-services/connection-manager/odbc-connection-manager.md)|[Riferimento all'interfaccia utente di Gestione connessione ODBC](../../integration-services/connection-manager/odbc-connection-manager-ui-reference.md)|  
    |[Gestione connessione OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md)|[Configura gestione connessione OLE DB](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[Gestione connessione SMO](../../integration-services/connection-manager/smo-connection-manager.md)|[Editor gestione connessione SMO](../../integration-services/connection-manager/smo-connection-manager-editor.md)|  
    |[Gestione connessione SMTP](../../integration-services/connection-manager/smtp-connection-manager.md)|[Editor gestione connessione SMTP](../../integration-services/connection-manager/smtp-connection-manager-editor.md)|  
    |[Gestione connessione SQL Server Compact Edition](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|[Editor gestione connessione SQL Server Compact Edition &#40;pagina Connessione&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [Editor gestione connessione SQL Server Compact Edition &#40;pagina Tutte&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[Gestione connessione WMI](../../integration-services/connection-manager/wmi-connection-manager.md)|[Editor gestione connessione WMI](../../integration-services/connection-manager/wmi-connection-manager-editor.md)|  
  
     La gestione connessione aggiunta verrà visualizzata sotto il nodo **Gestioni connessioni** in **Esplora soluzioni**. Verrà inoltre visualizzata nella scheda **Gestioni connessioni** nella finestra **Progettazione SSIS** per tutti i pacchetti nel progetto. Il nome della gestione connessione in questa scheda conterrà un prefisso **(progetto)** per differenziarla dalle gestioni connessioni al livello del pacchetto.  
  
4.  Facoltativamente, fare clic con il pulsante destro del mouse sulla gestione connessione nella finestra **Esplora soluzioni** sotto il nodo **Gestioni connessioni** (oppure) nella scheda **Gestioni connessioni** della finestra **Progettazione SSIS** , fare clic su **Rinomina**, quindi modificare il nome predefinito della gestione connessione.  
  
    > [!NOTE]  
    >  Nella scheda **Gestioni connessioni** della finestra **Progettazione SSIS** non sarà possibile sovrascrivere il prefisso **(progetto)** dal nome della gestione connessione. Questo si verifica per motivi strutturali.  

### <a name="add-ssis-connection-manager-dialog-box"></a>Finestra di dialogo Aggiungi gestione connessione SSIS
Utilizzare la finestra di dialogo **Aggiungi gestione connessione SSIS** per selezionare il tipo di connessione da aggiungere a un pacchetto.  
  
 Per altre informazioni sulle gestioni connessioni, vedere [Connessioni di Integration Services &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md).  
  
#### <a name="options"></a>Opzioni  
 **Tipo gestione connessione**  
 Selezionare un tipo di connessione e quindi fare clic su **Aggiungi**oppure fare doppio clic su un tipo di connessione per specificare le proprietà della connessione usando l'editor specifico per ogni tipo di connessione.  
  
 **Aggiungere**  
 Consente di specificare le proprietà della connessione utilizzando l'editor per ogni tipo di connessione.  
   
##  <a name="create-a-parameter-for-a-connection-manager-property"></a><a name="parameter"></a> Creare un parametro per una proprietà della gestione connessione  
  
1.  Nell'area **Gestioni connessioni** fare clic con il pulsante destro del mouse sulla gestione connessione per cui creare un parametro e scegliere **Imposta parametri**.  
  
2.  Configurare le impostazioni dei parametri nella finestra di dialogo **Imposta parametri** . Per altre informazioni, vedere [Finestra di dialogo Imposta parametri](https://msdn.microsoft.com/library/fac02b6d-d247-447a-8940-e8700c7ac350).  

## <a name="delete-a-connection-manager"></a>Eliminare una gestione connessione 
###  <a name="delete-a-connection-manager-from-a-package"></a><a name="DeletePackageLevel"></a> Eliminare una gestione connessione da un pacchetto  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  In Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] fare clic sulla scheda **Flusso di controllo** , **Flusso di dati** o **Gestore evento** in modo da rendere disponibile l'area **Gestioni connessioni** .  
  
4.  Fare clic con il pulsante destro del mouse sulla gestione connessione da eliminare, quindi scegliere **Elimina**.  
  
     Se si elimina una gestione connessione utilizzata da un elemento del pacchetto, come un'attività Esegui SQL o un'origine OLE DB, si verificheranno i problemi seguenti:  
  
    -   Viene visualizzata un'icona di errore sull'elemento del pacchetto che utilizzava la gestione connessione eliminata.  
  
    -   La convalida del pacchetto non riesce.  
  
    -   Non è possibile eseguire il pacchetto.  
  
5.  Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
###  <a name="delete-a-shared-connection-manager-project-level-connection-manager"></a><a name="DeleteProjectLevel"></a> Eliminare una gestione connessione condivisa (gestione connessione al livello del progetto)  
  
1.  Per eliminare una gestione connessione al livello del progetto, fare clic con il pulsante destro del mouse sotto il nodo **Gestioni connessioni** nella finestra **Esplora soluzioni** , quindi scegliere **Elimina**. [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] visualizza il messaggio di avviso seguente:  
  
    > [!WARNING]  
    >  Quando si elimina una gestione connessione del progetto, è possibile che i pacchetti che utilizzano la gestione connessione non vengano eseguiti. Non è possibile annullare questa azione. Eliminare la gestione connessione?  
  
2.  Fare clic su OK per eliminare la gestione connessione o Annulla per mantenerla.  
  
    > [!NOTE]  
    >  È anche possibile eliminare una gestione connessione al livello del progetto dalla scheda **Gestione connessione** della finestra **Progettazione SSIS** aperta per i pacchetti del progetto. A tale scopo, fare clic con il pulsante destro del mouse sulla gestione connessione nella scheda, quindi scegliere **Elimina**. 
    
## <a name="set-the-properties-of-a-connection-manager"></a>Impostazione delle proprietà di una gestione connessione
Tutti i tipi di gestione connessione possono essere configurati nella finestra **Proprietà** .  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] include anche finestre di dialogo personalizzate per la modifica dei vari tipi di gestione connessione in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Queste finestre di dialogo includono opzioni diverse a seconda del tipo di gestione connessione.  
  
### <a name="modify-a-connection-manager-using-the-properties-window"></a>Modificare una gestione connessione usando la finestra Proprietà  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  In Progettazione SSIS fare clic sulla scheda **Flusso di controllo** , **Flusso di dati** o **Gestore evento** in modo da rendere disponibile l'area **Gestioni connessioni** .  
  
4.  Fare clic con il pulsante destro del mouse sulla gestione connessione e quindi scegliere **Proprietà**.  
  
5.  Nella finestra **Proprietà** modificare i valori delle proprietà. La finestra **Proprietà** consente di accedere ad alcune proprietà che non è possibile configurare nell'editor standard di una gestione connessione.  
  
6.  Fare clic su **OK**.  
  
7.  Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
### <a name="modify-a-connection-manager-using-a-connection-manager-dialog-box"></a>Modificare una gestione connessione tramite la relativa finestra di dialogo  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  In Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] fare clic sulla scheda **Flusso di controllo** , **Flusso di dati** o **Gestore evento** in modo da rendere disponibile l'area **Gestioni connessioni** .  
  
4.  Nell'area **Gestioni connessioni** fare doppio clic sulla gestione connessione desiderata. Verrà visualizzata la finestra di dialogo **Gestione connessione** . Per informazioni su tipi di gestione connessione specifici e sulle opzioni disponibili per ogni tipo di gestione connessione, vedere la tabella seguente.  
  
    |Gestione connessione|Opzioni|  
    |------------------------|-------------|  
    |[Gestione connessione ADO](../../integration-services/connection-manager/ado-connection-manager.md)|[Configura gestione connessione OLE DB](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[Gestione connessione ADO.NET](../../integration-services/connection-manager/ado-net-connection-manager.md)|[Configura gestione connessione ADO.NET](../../integration-services/connection-manager/configure-ado-net-connection-manager.md)|  
    |[Gestione connessione Analysis Services](../../integration-services/connection-manager/analysis-services-connection-manager.md)|[Riferimento all'interfaccia utente della finestra di dialogo Aggiungi gestione connessione Analysis Services](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Gestione connessione Excel](../../integration-services/connection-manager/excel-connection-manager.md)|[Editor gestione connessione Excel](../../integration-services/connection-manager/excel-connection-manager-editor.md)|  
    |[Gestione connessione file](../../integration-services/connection-manager/file-connection-manager.md)|[Editor gestione connessione file](../../integration-services/connection-manager/file-connection-manager-editor.md)|  
    |[Gestione connessione per più file](../../integration-services/connection-manager/multiple-files-connection-manager.md)|[Riferimento all'interfaccia utente della finestra di dialogo Aggiungi gestione connessione file](../../integration-services/connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[Gestione connessione file flat](../../integration-services/connection-manager/flat-file-connection-manager.md)|[Editor gestione connessione file flat &#40;pagina Generale&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md)<br /><br /> [Editor gestione connessione file flat &#40;pagina Colonne&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [Editor gestione connessione file flat &#40;pagina Avanzate&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [Editor gestione connessione file flat &#40;pagina Anteprima&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md)|  
    |[Gestione connessione per più file flat](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)|[Editor gestione connessione per più file flat &#40;pagina Generale&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [Editor gestione connessione per più file flat &#40;pagina Colonne&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [Editor gestione connessione per più file flat &#40;pagina Avanzate&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [Editor gestione connessione per più file flat &#40;pagina Anteprima&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[Gestione connessione FTP](../../integration-services/connection-manager/ftp-connection-manager.md)|[Editor gestione connessione FTP](../../integration-services/connection-manager/ftp-connection-manager-editor.md)|  
    |[Gestione connessione HTTP](../../integration-services/connection-manager/http-connection-manager.md)|[Editor gestione connessione HTTP &#40;pagina Server&#41;](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)<br /><br /> [Editor gestione connessione HTTP &#40;pagina Proxy&#41;](../../integration-services/connection-manager/http-connection-manager-editor-proxy-page.md)|  
    |[Gestione connessione MSMQ](../../integration-services/connection-manager/msmq-connection-manager.md)|[Editor gestione connessione MSMQ](../../integration-services/connection-manager/msmq-connection-manager-editor.md)|  
    |[Gestione connessione ODBC](../../integration-services/connection-manager/odbc-connection-manager.md)|[Riferimento all'interfaccia utente di Gestione connessione ODBC](../../integration-services/connection-manager/odbc-connection-manager-ui-reference.md)|  
    |[Gestione connessione OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md)|[Configura gestione connessione OLE DB](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[Gestione connessione SMO](../../integration-services/connection-manager/smo-connection-manager.md)|[Editor gestione connessione SMO](../../integration-services/connection-manager/smo-connection-manager-editor.md)|  
    |[Gestione connessione SMTP](../../integration-services/connection-manager/smtp-connection-manager.md)|[Editor gestione connessione SMTP](../../integration-services/connection-manager/smtp-connection-manager-editor.md)|  
    |[Gestione connessione SQL Server Compact Edition](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|[Editor gestione connessione SQL Server Compact Edition &#40;pagina Connessione&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [Editor gestione connessione SQL Server Compact Edition &#40;pagina Tutte&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[Gestione connessione WMI](../../integration-services/connection-manager/wmi-connection-manager.md)|[Editor gestione connessione WMI](../../integration-services/connection-manager/wmi-connection-manager-editor.md)|  
  
5.  Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  

## <a name="related-content"></a>Contenuto correlato  
  
-   Video sull' [utilizzo del Connettore Microsoft per Oracle di Attunity per migliorare le prestazioni del pacchetto](https://technet.microsoft.com/sqlserver/gg598963.aspx)sul sito Web technet.microsoft.com  
  
-   Articoli di Wiki sulla [connettività di SSIS](https://social.technet.microsoft.com/wiki/contents/articles/sql-server-integration-services-ssis.aspx#Connectivity), sul sito Web social.technet.microsoft.com  
  
-   Intervento nel blog relativo alla [connessione a MySQL da SSIS](https://go.microsoft.com/fwlink/?LinkId=217669)sul sito blogs.msdn.com.  
  
-   Articolo tecnico relativo all' [estrazione e al caricamento dei dati SharePoint in SQL Server Integration Services](https://go.microsoft.com/fwlink/?LinkId=247826)sul sito Web msdn.microsoft.com.  
  
-   Articolo tecnico [You get "DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER" error message when using Oracle connection manager in SSIS](https://go.microsoft.com/fwlink/?LinkId=233696)(Visualizzazione del messaggio di errore "DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER" quando si utilizza la gestione connessione Oracle in SSIS) sul sito support.microsoft.com.  
  
  
