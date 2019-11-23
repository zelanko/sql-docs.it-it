---
title: Origini dati supportate da Reporting Services (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SQL Server data processing extension [Reporting Services]
- XML data processing extension [Reporting Services]
- reports [Reporting Services], data
- data processing extensions [Reporting Services], data sources
- Oracle [Reporting Services]
- OLE DB data processing extension
- data sources [Reporting Services], about data sources
- ODBC data processing extension
- Reporting Services, data sources
ms.assetid: 9d11d055-a3be-45aa-99a7-46447a94ed42
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6e569240f708d209fc965fa3c6e393859044f528
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155116"
---
# <a name="data-sources-supported-by-reporting-services-ssrs"></a>Origini dei dati supportate da Reporting Services (SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] recupera i dati di report dalle origini dati tramite un livello di dati modulare ed estensibile che usa estensioni per l'elaborazione dati. Per recuperare dati di report da un'origine dati, è necessario selezionare un'estensione per l'elaborazione dati che supporti il tipo di origine dati, la versione del software in esecuzione su di essa e la relativa piattaforma (32 bit o 64 bit [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]).  
  
 Durante la distribuzione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], un set di estensioni per l'elaborazione dati viene installato e registrato automaticamente nel client di creazione report e nel server di report per fornire l'accesso a diversi tipi di origini dati. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] installa i tipi di origine dati seguenti:  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] per MDX, DMX, [!INCLUDE[msCoName](../../includes/msconame-md.md)] PowerPivot e i modelli tabulari  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Parallel data warehouse  
  
-   Oracle  
  
-   SAP NetWeaver BI  
  
-   [!INCLUDE[extEssbase](../../includes/extessbase-md.md)]  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Elenco SharePoint  
  
-   Teradata  
  
-   OLE DB  
  
-   ODBC  
  
-   XML  
  
 Gli amministratori di sistema possono anche installare e registrare estensioni per l'elaborazione dati personalizzata e provider di dati [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] standard. Per elaborare e visualizzare un report, è necessario che le estensioni per l'elaborazione dati e i provider di dati siano installati e registrati nel server di report. Per visualizzare l'anteprima di un report, essi devono essere installati e registrati nel client di creazione dei report. Le estensioni per l'elaborazione dati e i provider di dati devono essere compilati in modo nativo per la piattaforma in cui vengono installati. Se si distribuisce un'origine dati tramite il servizio Web SOAP a livello di programmazione, è necessario definire l'estensione dell'origine dati. Usare i valori dell'estensione per i dati contenuti nel file **RSReportDesigner.config** . Per impostazione predefinita, il file si trova nella seguente cartella:  
  
```  
<drive letter>\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssemblies  
```  
  
 Ad esempio, l'estensione per i dati [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è OLEDB-MD.  
  
 Molti provider di dati [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] standard di terze parti possono essere scaricati dall' [Area download Microsoft](https://go.microsoft.com/fwlink/?linkid=51456) e dai siti dei rispettivi produttori. È anche possibile eseguire ricerche nel forum pubblico relativo a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per ottenere informazioni sui provider di dati di terze parti.  
  
> [!NOTE]  
>  I provider di dati [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] standard non supportano necessariamente tutte le funzionalità offerte dalle estensioni per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Alcuni provider di dati OLE DB e driver ODBC possono inoltre essere utilizzati per creare e visualizzare in anteprima i report, tuttavia non sono progettati per supportare i report pubblicati in un server di report. Il provider [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB per Jet non è ad esempio supportato sul server di report. Per altre informazioni, vedere [Estensioni per l'elaborazione dati e provider di dati .NET Framework &#40;SSRS&#41;](data-processing-extensions-and-net-framework-data-providers-ssrs.md).  
  
 Per altre informazioni sulle estensioni per l'elaborazione dati personalizzate, vedere [Implementazione di un'estensione per l'elaborazione dati](../extensions/data-processing/implementing-a-data-processing-extension.md). Per altre informazioni sui provider di dati [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] standard, vedere lo spazio dei nomi <xref:System.Data> .  
  
 Per altre informazioni sulle estensioni per l'elaborazione dati supportate da Generatore report, vedere [Connessioni dati, origini dati e stringhe di connessione in Generatore report](../data-connections-data-sources-and-connection-strings-in-report-builder.md) nella [documentazione relativa a Generatore report](https://go.microsoft.com/fwlink/?LinkId=154494) nel sito msdn.microsoft.com.  
  
## <a name="platform-support-for-report-data-sources"></a>Supporto delle piattaforme per le origini dei dati del report  
 Le origini dati utilizzabili in una distribuzione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] variano in base all'edizione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], alla versione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e alla piattaforma. Per ulteriori informazioni sulle funzionalità di, vedere [funzionalità supportate dalle edizioni di SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md). Nella tabella disponibile più avanti in questo argomento sono disponibili informazioni sulle origini dei dati supportate per versione e piattaforma.  
  
 Le considerazioni sulle piattaforme per le origini dei dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sono diverse per il client di creazione dei report rispetto a quelle per il server di report.  
  
### <a name="on-the-report-authoring-client"></a>Nel client di creazione dei report  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] è un'applicazione a 32 bit. [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] non è supportato su una piattaforma basata su Itanium. Nelle piattaforme x64, per modificare e visualizzare l'anteprima dei report in Progettazione report, è necessario disporre di provider di dati a 32 bit installati nella directory della piattaforma (x86).  
  
### <a name="on-the-report-server"></a>Nel server di report  
 Quando si distribuisce un report a un server di report a 64 bit (x86), il server di report deve disporre di provider di dati a 64 bit compilati in modo nativo. Il wrapping di un provider di dati a 32 bit in interfacce a 64 bit non è supportato. Per ulteriori informazioni, consultare la documentazione relativa al provider di dati.  
  
## <a name="supported-data-sources"></a>Origini dati supportate  
 La tabella seguente elenca i provider di dati e le estensioni per l'elaborazione dati [!INCLUDE[msCoName](../../includes/msconame-md.md)] che è possibile usare per recuperare i dati per i set di dati e i modelli di report. Per ulteriori informazioni su un'estensione o un provider di dati, fare clic sul collegamento nella seconda colonna. Le colonne della tabella sono descritte come segue:  
  
-   Origine dei dati del report: il tipo di dati a cui si accede, ad esempio database relazionale, database multidimensionale, file flat o XML. In questa colonna è disponibile la risposta alla domanda "Quali tipi di dati [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è in grado di usato per un report?"  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Tipo di origine dati: uno dei tipi di origine dati disponibili nell'elenco a discesa quando si definisce un'origine dati in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Questo elenco viene compilato in base alle estensioni per l'elaborazione dati e ai provider di dati installati e registrati. In questa colonna è disponibile la risposta alla domanda "Quale tipo di origine dati deve essere selezionata nell'elenco a discesa quando si crea un'origine dati del report?"  
  
-   Nome dell'estensione per l'elaborazione dati/provider di dati: l'estensione per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o altro provider di dati corrispondente al tipo di origine dei dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] selezionato. In questa colonna è disponibile la risposta alla domanda" Quando si seleziona un tipo di origine dati, quale estensione per l'elaborazione dati o provider di dati corrispondente viene utilizzato?"  
  
-   Versione del provider di dati sottostante (facoltativo): alcuni tipi di origini dei dati supportano più di un provider di dati. Per un tipo di provider di dati, potrebbero essere disponibili versioni diverse dello stesso provider o implementazioni diverse di terze parti. Il provider viene spesso incluso nella stringa di connessione dopo aver configurato un'origine dati. In questa colonna è disponibile la risposta alla domanda "Dopo aver selezionato il tipo di origine dati, quale provider di dati occorre selezionare nella finestra di dialogo **Proprietà connessione**?"  
  
-   *\<Piattaforma>* dell'origine dati: la piattaforma dell'origine dati supportata dall'estensione per l'elaborazione dati o dal provider di dati per l'origine dati di destinazione. In questa colonna è disponibile la risposta alla domanda "'L'estensione per l'elaborazione dati o il provider di dati sono in grado di recuperare dati da un'origine in questo tipo di piattaforma?"  
  
-   Versione dell'origine dati: la versione dell'origine dati di destinazione supportata dall'estensione per l'elaborazione dati o dal provider di dati. In questa colonna è disponibile la risposta alla domanda "'L'estensione per l'elaborazione dati o il provider di dati sono in grado di recuperare dati da questa versione dell'origine dati?"  
  
-   *\<Piattaforma>* RS: le piattaforme per il server di report e il client di creazione dei report in cui è possibile installare un provider di dati o un'estensione per l'elaborazione dati personalizzata. Le estensioni per l'elaborazione dati incorporate in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sono incluse in tutte le installazioni di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Le estensioni per l'elaborazione dati e i provider di dati [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] devono essere compilati in modo nativo per una piattaforma specifica. In questa colonna è disponibile la risposta alla domanda "'L'estensione per l'elaborazione dati o il provider di dati può essere installato in questo tipo di piattaforma?"  
  
###  <a name="DataSourcesTable"></a> Tipi di origini dei dati  
  
|Origine di<br /><br /> Dati di report|Tipo di origine dati di Reporting Services|Nome dell'estensione per l'elaborazione dati/provider di dati|Versione del provider di dati sottostante<br /><br /> (Facoltativo)|Dati<br /><br /> Origine<br /><br /> Piattaforma x86|Dati<br /><br /> Origine<br /><br /> Piattaforma x64|Versione dell'origine dati|RS<br /><br /> Piattaforma x86|RS<br /><br /> Piattaforma x64|  
|-------------------------------|-----------------------------------------|------------------------------------------------------|-------------------------------------------------------|--------------------------------------|--------------------------------------|----------------------------|-------------------------|-------------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database relazionale|[Microsoft SQL Server](#MicrosoftSQLServer)|Estensione predefinita per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Estende System.Data.SqlClient|S|S|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive.|S|S|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database relazionale|[OLEDB](#OLEDBSQL)|Estensione predefinita per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Estende System.Data.OledbClient|S|S|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive.|S|S|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database relazionale|[ODBC](#ODBC)|Estensione predefinita per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Estende System.Data.OdbcClient|S|S|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive.|S|S|  
|[!INCLUDE[ssSDS](../../includes/sssds-md.md)]|[Database SQL di Azure](#Azure)|Estensione predefinita per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Estende System.Data.SqlClient|N/D|N/D|[!INCLUDE[ssSDS](../../includes/sssds-md.md)]|S|S|  
|[!INCLUDE[ssDW](../../includes/ssdw-md.md)] appliance|[Microsoft Parallel Data Warehouse](#PWD)|Estensione predefinita per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|N/D|N/D|N/D|[!INCLUDE[ssDWfull](../../includes/ssdwfull-md.md)]|S|S|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database multidimensionale|[Microsoft SQL Server Analysis Services](#AnalysisServices)|Estensione predefinita per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Utilizza ADOMD.NET|S|S|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e versioni successive<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive|S|S|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database multidimensionale|[OLEDB](#OLEDBAS9)|Estensione predefinita per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Estende System.Data.OledbClient<br /><br /> Versione 10.0|S|S|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|S|S|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database multidimensionale|[OLEDB](#OLEDBAS9)|Estensione predefinita per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Estende System.Data.OledbClient<br /><br /> Versione 9.0|S|S|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|S|S|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] database multidimensionale|OLEDB|Estensione predefinita per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Estende System.Data.OledbClient<br /><br /> Versione 8.0|S|N|N/D|S|N|  
|Elenchi SharePoint|[Elenco Microsoft SharePoint](#SharePointList)|Estensione predefinita per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Ottiene i dati da Lists.asmx o dalle interfacce API del modello a oggetti di SharePoint.<br /><br /> Vedere la [nota](#SharePointList).|N|S|Prodotti SharePoint 2013<br /><br /> Prodotti SharePoint 2010|S|S|  
|Elenchi SharePoint|[Elenco Microsoft SharePoint](#SharePointList)|Estensione predefinita per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Ottiene i dati da Lists.asmx o dalle interfacce API del modello a oggetti di SharePoint.<br /><br /> Vedere la [nota](#SharePointList).|S|S|[!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 3,0 e [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007|S|S|  
|XML|[XML](#XML)|Estensione predefinita per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Origini dati XML indipendenti dalla piattaforma.|N/D|N/D|[!INCLUDE[vstecwebservices](../../includes/vstecwebservices-md.md)] o documenti|S|S|  
|Modello Server report|Modello di report|Estensione predefinita per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per un file SMDL pubblicato|Le origini dati per un modello utilizzano le estensioni per l'elaborazione dati incorporate.<br /><br /> I modelli basati su Oracle richiedono componenti del client Oracle.<br /><br /> I modelli basati su Teradata richiedono provider di dati .NET per Teradata da Teradata.<br /><br /> Vedere la documentazione di Teradata per il supporto della piattaforma.|N/D|N/D|È possibile creare modelli da:[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive.<br /><br /> [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]<br /><br /> Oracle 9.2.0.3 o versione successiva<br /><br /> Teradata v14, v13, v12 e v6.2|S|S|  
|Database multidimensionale SAP|[SAP BI NetWeaver](#SapBINetWeaver)|Estensione predefinita per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Vedere la documentazione SAP per il supporto della piattaforma.|N/D|N/D|SAP BI NetWeaver 3.5|S|N/D|  
|[!INCLUDE[extEssbase](../../includes/extessbase-md.md)]|[Hyperion Essbase](#Hyperion)|Estensione predefinita per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Vedere la documentazione di Hyperion per il supporto della piattaforma|S|N/D|[!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 9.3.1|S|N/D|  
|Database relazionale Oracle|[Oracle](#OracleClient)|Estensione predefinita per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Estende System.Data.OracleClient<br /><br /> Richiede componenti client Oracle|S|N/D|Oracle 10g, 9, 8.1.7|S|S|  
|Database relazionale Teradata|[Teradata](#Teradata)|Estensione predefinita per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Estende il provider di dati .NET per Teradata da Teradata.<br /><br /> Richiede il provider di dati .NET per Teradata da Teradata.<br /><br /> Vedere la documentazione di Teradata per il supporto della piattaforma.|S|N/D|Teradata v14<br /><br /> Teradata v13<br /><br /> Teradata v12<br /><br /> Teradata v6.20|S|N|  
|Database relazionale DB2|Nome dell'estensione per i dati registrati e personalizzati||Host Integration (HI) Server 2004<br /><br /> Vedere la [documentazione di HI Server](https://msdn.microsoft.com/library/gg241192\(v=bts.10\).aspx).|S|N/D|N/D|S|N|  
|Origine dati OLE DB generica|[OLEDB](#OLEDBStandard)|Estensione predefinita per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Tutte le origini dei dati che supportano OLE DB.<br /><br /> Vedere la documentazione dell'origine dati per il supporto della piattaforma.|S|N/D|Tutte le origini dei dati che supportano OLE DB. Vedere la [nota](#OLEDBStandard).|S|N/D|  
|Origine dati ODBC generica|[ODBC](#ODBCGeneric)|Estensione predefinita per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Qualsiasi origine dati che supporti ODBC.<br /><br /> Vedere la documentazione dell'origine dati per il supporto della piattaforma.|S|N/D|Qualsiasi origine dati che supporti ODBC. Vedere la [nota](#ODBCGeneric).|S|S|  
  
 Per informazioni sull'utilizzo di un'origine dati tabulare, vedere [connessioni dati, origini dati e stringhe di connessione in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
 Per altre informazioni sull'uso di origini dati esterne, vedere [Aggiungere dati da origini dati esterne &#40;SSRS&#41;](add-data-from-external-data-sources-ssrs.md).  
  
 Molti provider di dati [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] standard vengono offerti da terze parti. Per ulteriori informazioni, cercare "terze parti" nei siti Web o nei forum.  
  
 Per installare e registrare un'estensione per l'elaborazione dati personalizzata o un provider di dati [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] standard, sarà necessario consultare la documentazione di riferimento del provider di dati. Per altre informazioni, vedere [Registrare un provider di dati .NET Framework standard &#40;SSRS&#41;](register-a-standard-net-framework-data-provider-ssrs.md).  
  
 [Torna alla tabella delle origini dati](#DataSourcesTable)  
  
## <a name="reporting-services-data-processing-extensions"></a>Estensioni per l'elaborazione dati in Reporting Services  
 Le estensioni per l'elaborazione dati seguenti vengono installate automaticamente con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]. Per ulteriori informazioni e per verificare l'installazione, vedere [file di configurazione di RSReportDesigner](../report-server/rsreportdesigner-configuration-file.md) e [file di configurazione RSReportServer](../report-server/rsreportserver-config-configuration-file.md).  
  
> [!NOTE]  
>  L'estensione per l'elaborazione dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] non è attualmente supportata.  
  
 Per altre informazioni sulle estensioni per l'elaborazione dati supportate da Generatore report, vedere [Connessioni dati, origini dati e stringhe di connessione in Generatore report](../data-connections-data-sources-and-connection-strings-in-report-builder.md) nella [documentazione relativa a Generatore report](https://go.microsoft.com/fwlink/?LinkId=154494) nel sito msdn.microsoft.com.  
  
###  <a name="MicrosoftSQLServer"></a> Estensione per l'elaborazione dati di Microsoft SQL Server  
 Il tipo di origine dati **Microsoft SQL Server** esegue il wrapping ed estende il provider di dati [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa estensione per l'elaborazione dati è compilata in modo nativo per piattaforme x86 e basate su [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)] e può essere eseguita su di esse.  
  
 In [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)], la finestra Progettazione query associata a questa estensione per i dati è la [finestra di progettazione di Visual Database Tools](../../ssms/visual-db-tools/visual-database-tool-designers.md). Se si utilizza l'interfaccia grafica di Progettazione query, la query verrà analizzata ed eventualmente riscritta. Utilizzare Progettazione query basata su testo se si desidera controllare la sintassi esatta di [!INCLUDE[tsql](../../includes/tsql-md.md)] utilizzata per una query. Per altre informazioni, vedere [Strumenti di progettazione di query e viste &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) e [Interfaccia utente della finestra Progettazione query con interfaccia grafica](graphical-query-designer-user-interface.md).  
  
 Per altre informazioni, vedere [Tipo di connessione SQL Server &#40;SSRS&#41;](sql-server-connection-type-ssrs.md).  
  
 In Generatore report, la finestra Progettazione query associata a questa estensione per i dati è Progettazione query relazionale. Per altre informazioni, vedere [Interfaccia utente di Progettazione query relazionale](../relational-query-designer-user-interface.md).  
  
 [Torna alla tabella delle origini dati](#DataSourcesTable)  
  
###  <a name="Azure"></a>Estensione per l'elaborazione del database SQL di Azure  
 Il tipo di origine dati **[!INCLUDE[ssSDS](../../includes/sssds-md.md)]** eseguito il wrapping ed estende il provider di dati [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 In [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] la finestra Progettazione query con interfaccia grafica associata a questa estensione per i dati è l'[interfaccia utente di Progettazione query relazionale](../relational-query-designer-user-interface.md), non la [finestra di progettazione di Visual Database Tools](../../ssms/visual-db-tools/visual-database-tool-designers.md) usata con il tipo di origine dati **Microsoft SQL Server**.  
  
 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] distingue automaticamente tra **[!INCLUDE[ssSDS](../../includes/sssds-md.md)]** e **Microsoft SQL Server** i tipi di origine dati e apre la finestra Progettazione query con interfaccia grafica associata al tipo di origine dati.  
  
 Se si utilizza l'interfaccia grafica di Progettazione query, la query verrà analizzata ed eventualmente riscritta. La finestra Progettazione query basata su testo è disponibile anche per la scrittura di query. Utilizzare Progettazione query basata su testo se si desidera controllare la sintassi esatta di [!INCLUDE[tsql](../../includes/tsql-md.md)] utilizzata per una query. Per altre informazioni, vedere [Interfaccia utente di Progettazione query basata su testo](../text-based-query-designer-user-interface.md).  
  
 Il recupero di dati da [!INCLUDE[ssSDS](../../includes/sssds-md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è simile, ma alcuni requisiti si applicano solo a [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Per altre informazioni, vedere [Tipo di connessione SQL Azure &#40;SSRS&#41;](sql-azure-connection-type-ssrs.md).  
  
 [Torna alla tabella delle origini dati](#DataSourcesTable)  
  
###  <a name="PWD"></a> Estensione per l'elaborazione di Microsoft SQL Server Parallel Data Warehouse  
 In [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] la finestra Progettazione query con interfaccia grafica associata a questa estensione per i dati è l'[interfaccia utente di Progettazione query relazionale](../relational-query-designer-user-interface.md), non la [finestra di progettazione di Visual Database Tools](../../ssms/visual-db-tools/visual-database-tool-designers.md) usata con il tipo di origine dati **Microsoft SQL Server**.  
  
 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] distingue automaticamente tra i tipi di origine dati **SQL Server Data Warehouse paralleli** e **Microsoft SQL Server** e apre la finestra Progettazione query con interfaccia grafica associata al tipo di origine dati.  
  
 Se si utilizza l'interfaccia grafica di Progettazione query, la query verrà analizzata ed eventualmente riscritta. La finestra Progettazione query basata su testo è disponibile anche per la scrittura di query. Utilizzare Progettazione query basata su testo se si desidera controllare la sintassi esatta di [!INCLUDE[tsql](../../includes/tsql-md.md)] utilizzata per una query. Per altre informazioni, vedere [Interfaccia utente di Progettazione query basata su testo](../text-based-query-designer-user-interface.md).  
  
 [!INCLUDE[ssDWCurrentFull](../../includes/ssdwcurrentfull-md.md)] non supporta l'utilizzo di stored procedure e funzioni con valori di tabella nelle query. Per altre informazioni, vedere [Tipo di connessione SQL Server Parallel Data Warehouse &#40;SSRS&#41;](sql-server-parallel-data-warehouse-connection-type-ssrs.md).  
  
 [Torna alla tabella delle origini dati](#DataSourcesTable)  
  
###  <a name="AnalysisServices"></a> Estensione per l'elaborazione dati di Microsoft SQL Server Analysis Services  
 Quando si seleziona il tipo di origine dati **Microsoft SQL Server Analysis Services**, viene seleziona un'estensione per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] che consente di estendere il provider di dati [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] per [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Questa estensione per l'elaborazione dati è compilata in modo nativo per piattaforme x86 e basate su x64 e può essere eseguita su di esse.  
  
 Il provider di dati utilizza il modello a oggetti ADOMD.NET per creare query mediante XML for Analysis (XMLA) versione 1.1. I risultati vengono restituiti in un set di righe bidimensionale. Per altre informazioni, vedere [Tipo di connessione Analysis Services per MDX &#40;SSRS&#41;](analysis-services-connection-type-for-mdx-ssrs.md), [Tipo di connessione Analysis Services per DMX &#40;SSRS&#41;](analysis-services-connection-type-for-dmx-ssrs.md), [Interfaccia utente di Progettazione query MDX di Analysis Services](analysis-services-mdx-query-designer-user-interface.md) e [Interfaccia utente di Progettazione query DMX di Analysis Services](analysis-services-dmx-query-designer-user-interface.md).  
  
 Quando ci si connette a un'origine dati [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , l'estensione per l'elaborazione dati di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] supporta parametri multivalore ed esegue il mapping di celle e proprietà dei membri alle proprietà estese supportate da [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Per altre informazioni, vedere [Proprietà di campo estese per un database di Analysis Services &#40;SSRS&#41;](extended-field-properties-for-an-analysis-services-database-ssrs.md).  
  
 È anche possibile creare modelli provenienti dalle origini dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
###  <a name="OLEDBAll"></a> OLE DB Data Processing Extension  
 L'estensione per l'elaborazione dati OLE DB richiede la scelta di un ulteriore livello di provider di dati in base alla versione dell'origine dati da utilizzare nel report. Se non si seleziona un provider di dati specifico, verrà utilizzato uno predefinito. Scegliere un provider di dati specifico tramite la finestra di dialogo **Proprietà connessione** a cui è possibile accedere tramite il pulsante **Modifica** nelle finestre di dialogo [Origine dati](../data-source-properties-dialog-box-general.md) o [Origine dati condivisa](../shared-data-source-properties-dialog-box-general.md).  
  
 Per altre informazioni sulla finestra Progettazione query associata OLE DB, vedere [Strumenti di progettazione di query e viste &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) e [Interfaccia utente della finestra Progettazione query con interfaccia grafica](graphical-query-designer-user-interface.md). Per altre informazioni sul supporto specifico per i provider OLE DB, vedere [Visual Studio .NET Designer Tool Supports Specific OLE DB Providers](https://support.microsoft.com/default.aspx/kb/811241) (Visual Studio .NET Designer Tool supporta specifici provider OLE DB) nella Knowledge Base [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
 [Torna alla tabella delle origini dati](#DataSourcesTable)  
  
####  <a name="OLEDBSQL"></a> OLE DB per SQL Server  
 Quando si seleziona il tipo di origine dei dati **OLE DB**, viene selezionata un'estensione per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] che consente di estendere il provider di dati [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] per OLE DB. Questa estensione per l'elaborazione dati è compilata in modo nativo per piattaforme x86 e x64 e può essere eseguita su di esse.  
  
 Per altre informazioni, vedere [Tipo di connessione OLE DB &#40;SSRS&#41;](ole-db-connection-type-ssrs.md).  
  
 [Torna alla tabella delle origini dati](#DataSourcesTable)  
  
####  <a name="OLEDBAS9"></a>OLE DB per Analysis Services 9,0  
 Per connettersi a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], selezionare il provider [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB per [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 9.0, scegliere il tipo di origine dati **OLE DB** e quindi il provider di dati sottostante in base al nome. La combinazione di estensione per l'elaborazione dati e provider di dati viene compilata in modo nativo ed eseguita su piattaforme x86 e x64.  
  
> [!NOTE]  
>  Questa estensione per l'elaborazione dati non supporta le aggregazioni di server, il mapping automatico delle proprietà di campo estese e i parametri nelle query. Il provider di dati consigliato per un'origine dati [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è **Microsoft SQL Server Analysis Services**.  
  
 Per altre informazioni, vedere [Tipo di connessione OLE DB &#40;SSRS&#41;](ole-db-connection-type-ssrs.md).  
  
 [Torna alla tabella delle origini dati](#DataSourcesTable)  
  
#### <a name="ole-db-for-olap-70"></a>OLE DB per OLAP 7.0  
 Il provider OLE DB per OLAP Services 7.0 non è supportato.  
  
 [Torna alla tabella delle origini dati](#DataSourcesTable)  
  
####  <a name="OracleOLEDB"></a> OLE DB per Oracle  
 L'estensione per l'elaborazione dati OLE DB per Oracle non supporta i tipi di dati Oracle BLOB, CLOB, NCLOB, BFILE, UROWID.  
  
 I parametri senza nome dipendenti dalla posizione sono supportati. I parametri denominati non sono supportati da questa estensione. Per usare i parametri denominati, usare l'estensione per l'elaborazione dati [Oracle](#OracleClient) .  
  
 Per altre informazioni sulla configurazione di Oracle come origine dati, vedere [Come usare Reporting Services per configurare e accedere a un'origine dati Oracle](https://support.microsoft.com/kb/834305). Per altre informazioni sulla configurazione di autorizzazioni aggiuntive, vedere [Come aggiungere autorizzazioni per l'entità di sicurezza SERVIZIO DI RETE](https://support.microsoft.com/kb/870668) nella [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base.  
  
 [Torna alla tabella delle origini dati](#DataSourcesTable)  
  
####  <a name="OLEDBStandard"></a> Provider di dati .NET Framework standard OLE DB  
 Per recuperare dati da un'origine dati che supporta i provider di dati [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] OLE DB, usare il tipo di origine dati **OLE DB** e selezionare il provider di dati predefinito oppure effettuare una selezione nell'elenco dei provider di dati installati nella finestra di dialogo **Stringa di connessione**.  
  
> [!NOTE]  
>  Sebbene un provider di dati possa supportare l'anteprima di un report sul relativo client di creazione, non tutti i provider di dati OLE DB sono progettati per supportare i report pubblicati su un server di report.  
  
 [Torna alla tabella delle origini dati](#DataSourcesTable)  
  
###  <a name="ODBC"></a> ODBC Data Processing Extension  
 Quando si seleziona il tipo di origine dati **ODBC**, viene scelta un'estensione per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] che consente di estendere il provider di dati [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] per ODBC. Questa estensione per l'elaborazione dati è compilata in modo nativo per piattaforme x86 e [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)] e può essere eseguita su di esse. Questa estensione può essere utilizzata per stabilire la connessione a qualsiasi origine dati provvista di un provider ODBC e recuperarne i dati.  
  
> [!NOTE]  
>  Sebbene un provider di dati possa supportare l'anteprima di un report sul client di creazione del report, non tutti i provider di dati ODBC sono progettati per supportare i report pubblicati su un server di report.  
  
 [Torna alla tabella delle origini dati](#DataSourcesTable)  
  
####  <a name="ODBCGeneric"></a> Provider di dati .NET Framework standard ODBC  
 Per recuperare dati da un'origine dati che supporta i provider di dati [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] ODBC, usare il tipo di origine dati **ODBC** e selezionare il provider di dati predefinito oppure effettuare una selezione nell'elenco dei provider di dati installati nella finestra di dialogo **Stringa di connessione**.  
  
> [!NOTE]  
>  Sebbene un provider di dati possa supportare l'anteprima di un report sul client di creazione del report, non tutti i provider di dati ODBC sono progettati per supportare i report pubblicati su un server di report.  
  
 [Torna alla tabella delle origini dati](#DataSourcesTable)  
  
###  <a name="OracleClient"></a> Estensione per l'elaborazione dati Oracle  
 Quando si seleziona il tipo di origine dati **Oracle**, viene scelta un'estensione per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] che consente di estendere il provider di dati [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] per Oracle. L'origine dati **Oracle** esegue il wrapping ed estende le classi <xref:System.Data.OracleClient> richieste da [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Per recuperare dati di report da un database Oracle, l'amministratore deve installare gli strumenti client di Oracle. Questo provider di dati utilizza l'interfaccia OCI (Oracle Call Interface) di Oracle 8i Release 3 come disponibile nel software client di Oracle. La versione dell'applicazione client deve essere 8.1.7 o successiva. Tali strumenti devono essere installati nel client di creazione del report per visualizzare l'anteprima dei report e nel server di report per visualizzare i report pubblicati.  
  
 I parametri denominati sono supportati da questa estensione. Per Oracle versione 9 o successive, i parametri multivalore sono supportati. Per i parametri senza nome dipendenti dalla posizione, usare l'estensione per l'elaborazione dati OLE DB con il provider di dati [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB per Oracle. Per altre informazioni sulla configurazione di Oracle come origine dati, vedere [Come usare Reporting Services per configurare e accedere a un'origine dati Oracle](https://support.microsoft.com/kb/834305). Per altre informazioni sulla configurazione di autorizzazioni aggiuntive, vedere [Come aggiungere autorizzazioni per l'entità di sicurezza SERVIZIO DI RETE](https://support.microsoft.com/kb/870668) nella [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base.  
  
 È possibile recuperare i dati da stored procedure con più parametri di input, tuttavia la stored procedure deve restituire un solo cursore di output. Per altre informazioni, vedere la sezione Oracle in [Recupero di dati mediante DataReader](https://go.microsoft.com/fwlink/?LinkId=81758).  
  
 Per altre informazioni, vedere [Tipo di connessione Oracle &#40;SSRS&#41;](oracle-connection-type-ssrs.md). Per altre informazioni sulla finestra Progettazione query associata, vedere [Strumenti di progettazione di query e viste &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) e [Interfaccia utente della finestra Progettazione query con interfaccia grafica](graphical-query-designer-user-interface.md).  
  
 È possibile creare anche modelli basati su un database Oracle.  
  
 [Torna alla tabella delle origini dati](#DataSourcesTable)  
  
###  <a name="Teradata"></a> Estensione per l'elaborazione dati Teradata  
 Quando si seleziona il tipo di origine dati **Teradata**, viene scelta un'estensione per l'elaborazione dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] che consente di estendere il provider di dati .NET Framework per Teradata. Per recuperare dati del report da un database Teradata, l'amministratore di sistema deve installare il provider di dati .NET Framework per Teradata nel client di creazione di report per modificare e visualizzare in anteprima report sul client e sul server di report per visualizzare i report pubblicati.  
  
 Per i progetti del server di report, non è disponibile una finestra Progettazione query con interfaccia grafica per questa estensione. Per creare query, è necessario utilizzare la finestra Progettazione query basata su testo.  
  
 La tabella seguente illustra le versioni del provider di dati .NET per Teradata supportate per la definizione di un'origine dati in una definizione di report in [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]:  
  
|[!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] version|Versione del database Teradata|Versione del provider di dati .NET Framework per Teradata|  
|-----------------------------------|-------------------------------|-------------------------------------------------------|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|12.00|12.00|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|6.20|12.00|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|12.00|12.00.01|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|6.20|12.00.01|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|13.00|13.0.0.1|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|12.00|12.00.01|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|6.20|12.00.01|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|13.00|13.0.0.1|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|6.20|12.00.01|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|12.00|12.00.01|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|13.00|13.0.0.1|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|14.00|14.00.01|  
  
 I parametri multivalore non sono supportati da questa estensione. Le macro possono essere specificate in una query tramite il comando EXECUTE in modalità query TEXT.  
  
 Per altre informazioni, vedere [Tipo di connessione Teradata &#40;SSRS&#41;](teradata-connection-type-ssrs.md).  
  
 È inoltre possibile creare modelli basati su un database Teradata. Per altre informazioni, vedere il white paper seguente nel sito Teradata [Microsoft SQL Server 2012 Reporting Services and Teradata Corporation](http://www.teradata.com/white-papers/Microsoft-SQL-Server-2012-Reporting-Services-and-Teradata-Corporation/?type=WP) (Microsoft SQL Server 2012 Reporting e Teradata Corporation).  
  
 [Torna alla tabella delle origini dati](#DataSourcesTable)  
  
###  <a name="SharePointList"></a> Estensione per i dati dell'elenco SharePoint  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] include l'estensione per i dati dell'elenco SharePoint di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] che consente di usare elenchi SharePoint come origine dati in un report. È possibile recuperare i dati elenco da:  
  
-   [!INCLUDE[SPS2013](../../includes/sps2013-md.md)]  
  
-   [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] e [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]  
  
-   [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 3,0 e [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007  
  
 Esistono tre implementazioni del provider di dati elenco di SharePoint.  
  
1.  In un ambiente di creazione di report quale Generatore report o Progettazione report in [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]o per un server di report configurato in modalità nativa, i dati elenco provengono dal servizio Web Lists.asmx per il sito di SharePoint.  
  
2.  In un server di report configurato in modalità integrata SharePoint, i dati elenco provengono dal servizio Web Lists.asmx corrispondente o dalle chiamate a livello di codice all'API SharePoint. In questa modalità, è possibile recuperare dati elenco da una farm di SharePoint.  
  
3.  Per [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] e [!INCLUDE[SPS2013](../../includes/sps2013-md.md)], il componente aggiuntivo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per le tecnologie [!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint consente di recuperare i dati elenco da un servizio Web Lists.asmx per un sito di SharePoint o da un sito di SharePoint che fa parte di una farm di SharePoint. Questo scenario è noto anche come *modalità locale* perché non è richiesto un server di report.  
  
 Le credenziali specificate dipendono dall'implementazione utilizzata dall'applicazione client. Per altre informazioni, vedere [Tipo di connessione Elenco Microsoft SharePoint &#40;SSRS&#41;](sharepoint-list-connection-type-ssrs.md).  
  
###  <a name="XML"></a> Estensione per l'elaborazione dati XML  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] include un'estensione per l'elaborazione dati XML che consente di usare dati XML in un report. I dati possono essere recuperati da un documento XML, da un servizio Web o da un'applicazione Web a cui è possibile accedere tramite un URL. Per altre informazioni, vedere [Tipo di connessione XML &#40;SSRS&#41;](xml-connection-type-ssrs.md). Per altre informazioni sulla finestra Progettazione query associata, vedere la sezione relativa alla progettazione di query basata su testo in [Interfaccia utente della finestra Progettazione query con interfaccia grafica](graphical-query-designer-user-interface.md). Per consultare degli esempi, vedere [Reporting Services: Using XML and Web Service Data Sources](https://go.microsoft.com/fwlink/?LinkId=81654) (Reporting Services: Uso di origini dati XML e servizio Web).  
  
 [Torna alla tabella delle origini dati](#DataSourcesTable)  
  
###  <a name="SapBINetWeaver"></a>Estensione per l'elaborazione dati SAP NetWeaver Business Intelligence  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] include un'estensione per l'elaborazione dati che consente di utilizzare dati in un report dati di un'origine dati [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)].  
  
 Per altre informazioni, vedere [Tipo di connessione SAP NetWeaver BI &#40;SSRS&#41;](sap-netweaver-bi-connection-type-ssrs.md). Per altre informazioni sulla finestra Progettazione query associata, vedere [Interfaccia utente di Progettazione query SAP NetWeaver BI](sap-netweaver-bi-query-designer-user-interface.md).  
  
 Per altre informazioni su [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)], vedere [Using SQL Server 2008 Reporting Services with SAP NetWeaver Business Intelligence](https://go.microsoft.com/fwlink/?LinkId=167352) (Uso di SQL Server 2008 Reporting Services con SAP NetWeaver BI).  
  
 [Torna alla tabella delle origini dati](#DataSourcesTable)  
  
###  <a name="Hyperion"></a> Estensione per l'elaborazione dati di Business Intelligence di Hyperion Essbase  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] include un'estensione per l'elaborazione dati che consente di usare dati di un'origine dati [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] in un report.  
  
 Per altre informazioni, vedere [Tipo di connessione Hyperion Essbase &#40;SSRS&#41;](hyperion-essbase-connection-type-ssrs.md). Per altre informazioni sulla finestra Progettazione query associata, vedere [Interfaccia utente di Progettazione query Hyperion Essbase](hyperion-essbase-query-designer-user-interface.md).  
  
 Per altre informazioni su [!INCLUDE[extEssbase](../../includes/extessbase-md.md)], vedere [Using SQL Server 2005 Reporting Services with Hyperion Essbase](https://go.microsoft.com/fwlink/?LinkId=81970) (Uso di SQL Server 2005 Reporting Services con Hyperion Essbase).  
  
 [Torna alla tabella delle origini dati](#DataSourcesTable)  
  
## <a name="see-also"></a>Vedere anche  
 [Connessioni dati, origini dati e stringhe di connessione in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Aggiunta di dati a un &#40;Generatore report di report e SSRS&#41;](report-datasets-ssrs.md)  
  
  
