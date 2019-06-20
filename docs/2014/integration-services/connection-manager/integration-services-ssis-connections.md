---
title: Connessioni in Integration Services (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 78c3ba452d3ba681823e5c9f473d7a86f55809a1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62833785"
---
# <a name="integration-services-ssis-connections"></a>Connessioni in Integration Services (SSIS)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] vengono utilizzate le connessioni per eseguire varie attività e implementare le funzionalità di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] seguenti:  
  
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
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] viene utilizzata la gestione connessione come rappresentazione logica di una connessione. In fase di progettazione si impostano le proprietà della gestione connessione per descrivere la connessione fisica che verrà creata da [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] durante l'esecuzione del pacchetto. Le gestioni connessioni includono ad esempio la proprietà `ConnectionString`, che viene impostata in modalità progettazione. In fase di esecuzione verrà quindi creata una connessione fisica utilizzando il valore archiviato nella proprietà relativa alla stringa di connessione.  
  
 In un pacchetto è possibile utilizzare più istanze di un determinato tipo di gestione connessione ed è possibile impostare proprietà specifiche per ogni istanza. In fase di esecuzione ogni istanza di un determinato tipo di gestione connessione crea una connessione con attributi diversi.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] consentono di stabilire connessioni tra i pacchetti e un'ampia gamma di server e origini dati:  
  
-   Durante l'installazione di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]vengono installate le gestioni connessioni predefinite.  
  
-   Dal sito Web [!INCLUDE[msCoName](../../includes/msconame-md.md)] è possibile scaricare alcune gestioni connessioni.  
  
-   Se le gestioni connessioni esistenti non soddisfano le proprie esigenze, è possibile creare una gestione connessione personalizzata.  
  
### <a name="built-in-connection-managers"></a>Gestioni connessioni predefinite  
 Nella tabella seguente sono elencati i tipi di gestione connessione disponibili in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
|Type|Descrizione|Argomento|  
|----------|-----------------|-----------|  
|ADO|Consente di connettersi a oggetti ADO (ActiveX Data Objects).|[Gestione connessione ADO](ado-connection-manager.md)|  
|ADO.NET|Consente di connettersi a un'origine dei dati tramite un provider .NET.|[Gestione connessione ADO.NET](ado-net-connection-manager.md)|  
|CACHE|Consente di leggere i dati dal flusso di dati o da un file di cache (caw) e di salvare i dati nel file di cache.|[Gestione connessione della cache](cache-connection-manager.md)|  
|DQS|Consente di connettersi a un server Data Quality Services e a un database Data Quality Services nel server.|[Gestione connessione DQS Cleansing](dqs-cleansing-connection-manager.md)|  
|EXCEL|Consente di connettersi a un file della cartella di lavoro di Excel.|[Gestione connessione Excel](excel-connection-manager.md)|  
|FILE|Consente di connettersi a un file o a una cartella.|[Gestione connessione file](file-connection-manager.md)|  
|FLATFILE|Consente di connettersi ai dati contenuti in un singolo file flat.|[Gestione connessione file flat](flat-file-connection-manager.md)|  
|FTP|Consente di connettersi a un server FTP.|[Gestione connessione FTP](ftp-connection-manager.md)|  
|HTTP|Consente di connettersi a un server Web.|[Gestione connessione HTTP](http-connection-manager.md)|  
|MSMQ|Consente di connettersi a una coda di messaggi.|[Gestione connessione MSMQ](msmq-connection-manager.md)|  
|MSOLAP100|Consente di connettersi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o a un progetto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|[Gestione connessione Analysis Services](analysis-services-connection-manager.md)|  
|MULTIFILE|Consente di connettersi a più file e cartelle.|[Gestione connessione per più file](multiple-files-connection-manager.md)|  
|MULTIFLATFILE|Consente di connettersi a più file e cartelle di dati.|[Gestione connessione per più file flat](multiple-flat-files-connection-manager.md)|  
|OLEDB|Consente di connettersi a un'origine dei dati tramite un provider OLE DB.|[Gestione connessione OLE DB](ole-db-connection-manager.md)|  
|ODBC|Consente di connettersi a un'origine dei dati tramite ODBC.|[Gestione connessione ODBC](odbc-connection-manager.md)|  
|SMOServer|Consente di connettersi a un server SMO ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects).|[Gestione connessione SMO](smo-connection-manager.md)|  
|SMTP|Consente di connettersi a un server di posta SMTP.|[Gestione connessione SMTP](smtp-connection-manager.md)|  
|SQLMOBILE|Consente di connettersi a un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.|[Gestione connessione SQL Server Compact Edition](sql-server-compact-edition-connection-manager.md)|  
|WMI|Consente di connettersi a un server e specifica l'ambito della gestione WMI (Windows Management Instrumentation, Strumentazione gestione Windows) sul server.|[Gestione connessione WMI](wmi-connection-manager.md)|  
  
### <a name="connection-managers-available-for-download"></a>Gestioni connessioni disponibili per download  
 Nella tabella seguente sono elencati i tipi aggiuntivi di gestione connessione che è possibile scaricare dal sito Web [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
> [!IMPORTANT]  
>  Le gestioni connessioni elencate nella tabella seguente funzionano unicamente con [!INCLUDE[ssEnterpriseEd11](../../includes/ssenterpriseed11-md.md)] e [!INCLUDE[ssDeveloperEd11](../../includes/ssdevelopered11-md.md)].  
  
|Type|Descrizione|Argomento|  
|----------|-----------------|-----------|  
|ORACLE|Si connette a un Oracle \<informazioni versione > server.|La gestione connessione Oracle è il componente per la gestione delle connessioni del connettore [!INCLUDE[msCoName](../../includes/msconame-md.md)] per Oracle di Attunity. Il connettore [!INCLUDE[msCoName](../../includes/msconame-md.md)] per Oracle di Attunity include anche un'origine e una destinazione. Per ulteriori informazioni, vedere la pagina di download relativa ai [connettori Microsoft per Oracle e Teradata di Attunity](https://go.microsoft.com/fwlink/?LinkId=251526).|  
|SAPBI|Consente di connettersi a un sistema SAP NetWeaver BI versione 7.|La gestione connessione SAP BI è il componente per la gestione delle connessioni del connettore [!INCLUDE[msCoName](../../includes/msconame-md.md)] per SAP BI. Il connettore [!INCLUDE[msCoName](../../includes/msconame-md.md)] per SAP BI include anche un'origine e una destinazione. Per ulteriori informazioni, vedere la pagina di download relativa al [Feature Pack di Microsoft SQL Server 2008](https://go.microsoft.com/fwlink/?LinkId=262016).|  
|TERADATA|Si connette a un Teradata \<informazioni versione > server.|La gestione connessione Teradata è il componente per la gestione delle connessioni del connettore [!INCLUDE[msCoName](../../includes/msconame-md.md)] per Teradata di Attunity. Il connettore [!INCLUDE[msCoName](../../includes/msconame-md.md)] per Teradata di Attunity include anche un'origine e una destinazione. Per ulteriori informazioni, vedere la pagina di download relativa ai [connettori Microsoft per Oracle e Teradata di Attunity](https://go.microsoft.com/fwlink/?LinkId=251526).|  
  
### <a name="custom-connection-managers"></a>Gestioni connessioni personalizzate  
 È inoltre possibile scrivere gestioni connessioni personalizzate. Per ulteriori informazioni, vedere [Developing a Custom Connection Manager](../extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md).  
  
## <a name="related-tasks"></a>Attività correlate  
 Per informazioni dettagliate su come aggiungere o eliminare una gestione connessione in un pacchetto, vedere [Aggiunta, eliminazione o condivisione di una gestione connessione in un pacchetto](../add-delete-or-share-a-connection-manager-in-a-package.md).  
  
 Per informazioni dettagliate su come impostare le proprietà di una gestione connessione in un pacchetto, vedere [Impostazione delle proprietà di una gestione connessione](../set-the-properties-of-a-connection-manager.md).  
  
## <a name="related-content"></a>Contenuto correlato  
  
-   Video sull' [utilizzo del Connettore Microsoft per Oracle di Attunity per migliorare le prestazioni del pacchetto](https://technet.microsoft.com/sqlserver/gg598963.aspx)sul sito Web technet.microsoft.com  
  
-   Articoli di Wiki sulla [connettività di SSIS](https://social.technet.microsoft.com/wiki/contents/articles/sql-server-integration-services-ssis.aspx#Connectivity), sul sito Web social.technet.microsoft.com  
  
-   Intervento nel blog relativo alla [connessione a MySQL da SSIS](https://go.microsoft.com/fwlink/?LinkId=217669)sul sito blogs.msdn.com.  
  
-   Articolo tecnico relativo all' [estrazione e al caricamento dei dati SharePoint in SQL Server Integration Services](https://go.microsoft.com/fwlink/?LinkId=247826)sul sito Web msdn.microsoft.com.  
  
-   Articolo tecnico [You get "DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER" error message when using Oracle connection manager in SSIS](https://go.microsoft.com/fwlink/?LinkId=233696) (Visualizzazione del messaggio di errore "DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER" quando si utilizza la gestione connessione Oracle in SSIS) sul sito support.microsoft.com.  
  
  
