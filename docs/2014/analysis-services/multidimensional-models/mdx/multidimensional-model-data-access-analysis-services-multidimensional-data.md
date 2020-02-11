---
title: Accesso ai dati di modelli multidimensionali (Analysis Services-Dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SSAS, data access interfaces
- objects [Analysis Services], data access interfaces
- Analysis Services data access interfaces
- data retrieval [Analysis Services]
- retrieving data
- metadata [Analysis Services]
- data access interfaces [Analysis Services]
- manipulating objects [Analysis Services]
- Analysis Services data access interfaces, about data access interfaces
ms.assetid: 46388efb-3c78-47a2-b5c9-5a69ff394d03
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9e3db19179e74b20837f58602a236721debc18b2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66073841"
---
# <a name="multidimensional-model-data-access-analysis-services---multidimensional-data"></a>Accesso ai dati di modelli multidimensionali (Analysis Services - Dati multidimensionali)
  Utilizzare le informazioni in questo argomento per accedere ai dati multidimensionali di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] utilizzando metodi a livello di codice, script o applicazioni client che includono il supporto integrato per la connessione a un server [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] sulla rete locale.  
  
 In questo argomento sono incluse le sezioni seguenti:  
  
 [Applicazioni client](#bkmk_clientapps)  
  
 [Linguaggi di query](#bkmk_querylang)  
  
 [Interfacce programmatiche](#bkmk_api)  
  
##  <a name="bkmk_clientapps"></a>Applicazioni client  
 Anche se in Analysis Services sono disponibili interfacce che consentono di compilare o integrare database multidimensionali a livello di codice, un approccio più comune consiste nell'utilizzare applicazioni client esistenti di Microsoft e gli altri fornitori di software che dispongono di funzionalità integrate di accesso ai dati di Analysis Services.  
  
 Nelle applicazioni Microsoft seguenti sono supportate connessioni native ai dati multidimensionali.  
  
### <a name="excel"></a>Excel  
 I dati multidimensionali di Analysis Services vengono spesso presentati tramite tabelle pivot e controlli di grafico pivot in una cartella di lavoro di Excel. Le tabelle pivot sono indicate per i dati multidimensionali poiché gerarchie, aggregazioni e costrutti di navigazione del modello sono facilmente associabili alle funzionalità di riepilogo dei dati di una tabella pivot. In un'installazione di Excel è incluso un provider di dati OLE DB di Analysis Services per facilitare l'impostazione delle connessioni dati. Per ulteriori informazioni, vedere [Creare una connessione o importare dati da SQL Server Analysis Services](https://go.microsoft.com/fwlink/?linkID=215150).  
  
### <a name="reporting-services-reports"></a>Report di Reporting Services  
 È possibile utilizzare Generatore report o Progettazione report per creare report che utilizzano database di Analysis Services contenenti dati analitici. Sia in Generatore report che in Progettazione report è incluso Progettazione query MDX che può essere utilizzato per digitare o progettare istruzioni MDX che recuperano dati da un'origine dati disponibile. Per altre informazioni, vedere [Origini dati supportate da Reporting Services &#40;SSRS&#41;](../../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md) e [Tipo di connessione Analysis Services per MDX &#40;SSRS&#41;](../../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md).  
  
### <a name="performancepoint-dashboards"></a>Dashboard di PerformancePoint  
 I dashboard di PerformancePoint vengono utilizzati per creare scorecard in SharePoint che comunicano prestazioni aziendali in base a misure predefinite. In PerformancePoint è incluso il supporto per le connessioni dati ai dati multidimensionali di Analysis Services. Per altre informazioni, vedere ulteriori informazioni, vedere [Creare una connessione da Dashboard Designer a un cubo di dati di Analysis Services con PerformancePoint Services](https://go.microsoft.com/fwlink/?linkid=232471).  
  
### <a name="sql-server-data-tools"></a>SQL Server Data Tools  
 I progettisti di modelli e report utilizzano SQL Server Data Tools per compilare soluzioni che includono modelli multidimensionali. La distribuzione della soluzione a un'istanza di Analysis Services crea il database al quale viene successivamente stabilita la connessione da Excel, Reporting Services e le altre applicazioni client di Business Intelligence.  
  
 SQL Server Data Tools è basato su una shell di Visual Studio e utilizza progetti per organizzare e contenere il modello. Per altre informazioni, vedere [Creazione di modelli multidimensionali tramite SQL Server Data Tools &#40;SSDT&#41;](../creating-multidimensional-models-using-sql-server-data-tools-ssdt.md).  
  
### <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 Per gli amministratori del database SQL Server Management Studio è un ambiente integrato per la gestione delle istanze di SQL Server, incluse le istanze di Analysis Services e i database multidimensionali. Per altre informazioni, vedere [SQL Server Management Studio](../../../ssms/sql-server-management-studio-ssms.md) e [Connetti ad Analysis Services](../../instances/connect-to-analysis-services.md).  
  
##  <a name="bkmk_querylang"></a>Linguaggi di query  
 MDX è un linguaggio di calcolo e query standard di settore utilizzato per recuperare dati da database OLAP. In Analysis Services MDX è il linguaggio di query utilizzato per recuperare dati, ma supporta anche la definizione e la manipolazione dei dati. Editor MDX sono integrati in SQL Server Management Studio, Reporting Services e SQL Server Data Tools. È possibile utilizzare gli editor MDX per creare query ad hoc o script riutilizzabili se l'operazione sui dati è ripetibile.  
  
 In alcuni strumenti e applicazioni, ad esempio Excel, vengono utilizzati internamente costrutti MDX per eseguire query su un'origine dati Analysis Services. È inoltre possibile utilizzare MDX a livello di codice, includendo un'istruzione MDX in una richiesta Execute XMLA.  
  
 Tramite i collegamenti seguenti è possibile ottenere ulteriori informazioni su MDX:  
  
 [Query su dati multidimensionali con MDX](querying-multidimensional-data-with-mdx.md)  
  
 [Concetti chiave di MDX &#40;Analysis Services&#41;](../key-concepts-in-mdx-analysis-services.md)  
  
 [Nozioni fondamentali sulle query MDX &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
 [Nozioni fondamentali sullo scripting MDX &#40;Analysis Services&#41;](mdx-scripting-fundamentals-analysis-services.md)  
  
##  <a name="bkmk_api"></a>Interfacce programmatiche  
 Se si compila un'applicazione personalizzata che utilizza dati multidimensionali, l'approccio per l'accesso ai dati rientrerà molto probabilmente in una delle categorie seguenti:  
  
-   **XMLA**. Utilizzare XMLA quando è richiesta la compatibilità con un'ampia gamma di sistemi operativi e protocolli. XMLA offre la massima flessibilità, ma spesso a scapito del miglioramento delle prestazioni e della facilità di programmazione.  
  
-   **Librerie client**. Utilizzare librerie client di Analysis Services, ad esempio ADOMD.NET, AMO e OLE DB quando si desidera accedere ai dati a livello di codice da applicazioni client eseguite in un sistema operativo Microsoft Windows. Le librerie client eseguono il wrapping di XMLA con un modello a oggetti e ottimizzazioni che consentono di ottenere prestazioni migliori.  
  
     Le librerie client ADOMD.NET e AMO sono destinate ad applicazioni scritte in codice gestito. Utilizzare OLE DB per Analysis Services se l'applicazione è scritta in codice nativo.  
  
 Nella tabella seguente vengono forniti ulteriori dettagli e collegamenti relativi alle librerie client utilizzate per la connessione di Analysis Services a un'applicazione personalizzata.  
  
|Interfaccia|Descrizione|  
|---------------|-----------------|  
|Analysis Services Management Objects (AMO)|AMO è il modello a oggetti principale per l'amministrazione di istanze di Analysis Services e database multidimensionali nel codice. Ad esempio, in SQL Server Management Studio viene utilizzato AMO per supportare l'amministrazione di server e database. Per altre informazioni, vedere [Sviluppo con AMO &#40;Analysis Management Objects&#41;](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo).|  
|ADOMD.NET|ADOMD.NET è il modello a oggetti principale per la creazione e l'accesso ai dati multidimensionali in applicazioni personalizzate. È possibile usare ADOMD.NET in un'applicazione client gestita per recuperare informazioni su [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] usando interfacce comuni di accesso ai dati di Microsoft .NET Framework. Per altre informazioni, vedere [Sviluppo con ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/developing-with-adomd-net) e [Programmazione di client ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-client/adomd-net-client-programming).|  
|Provider OLE DB per Analysis Services (MSOLAP.dll)|È possibile utilizzare il provider OLE DB nativo per accedere a [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] a livello di codice da un'API non gestita. Per altre informazioni, vedere [Provider OLE DB per Analysis Services &#40;Analysis Services - Dati multidimensionali&#41;](../../dev-guide/analysis-services-ole-db-provider-analysis-services-multidimensional-data.md).|  
|Set di righe dello schema|Le tabelle del set di righe dello schema sono strutture di dati contenenti informazioni descrittive su un modello multidimensionale distribuito nel server, oltre a informazioni sull'attività corrente nel server. I programmatori possono eseguire query su tabelle di set di righe dello schema in applicazioni client per esaminare i metadati archiviati in un'istanza di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] , nonché recuperare da tale istanza informazioni relative al supporto e al monitoraggio. È possibile utilizzare set di righe dello schema con le seguenti interfacce programmatiche: OLE DB, OLE DB per Analysis Services, OLE DB per data mining o XMLA. Per altre informazioni, vedere [Set di righe dello schema di Analysis Services](https://docs.microsoft.com/bi-reference/schema-rowsets/analysis-services-schema-rowsets).<br /><br /> Nell'elenco seguente vengono illustrati diversi approcci per l'utilizzo di set di righe dello schema:<br /><br /> Eseguire query DMV in SQL Server Management Studio o nei report personalizzati per accedere a set di righe dello schema tramite la sintassi SQL. Per altre informazioni, vedere [Usare DMV per monitorare Analysis Services](../../instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md).<br /><br /> Scrivere codice ADOMD.NET che chiama un set di righe dello schema.<br /><br /> Eseguire direttamente il metodo XMLA `Discover` in un'istanza di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] per recuperare informazioni sul set di righe dello schema. Per altre informazioni, vedere [Metodo Discover &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover).|  
|XMLA|XMLA è l'API di livello più basso disponibile per un programmatore di Analysis Services ed è il denominatore comune su cui si basano tutte le metodologie di accesso ai dati di Analysis Services. XMLA è un protocollo XML basato su SOAP standard di settore che supporta l'accesso ai dati universale a qualsiasi origine dati multidimensionale standard disponibile su una connessione HTTP. Utilizza SOAP per formulare richieste e risposte per i dati multidimensionali. Se l'applicazione viene eseguita su una piattaforma non-Windows, è possibile utilizzare XMLA per accedere a un database multidimensionale in esecuzione in un server Windows sulla rete locale. Per altre informazioni, vedere [Sviluppo con XMLA in Analysis Services](../../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md).|  
|ASSL (Analysis Services Scripting Language)|ASSL è un termine descrittivo che si applica alle estensioni di Analysis Services del protocollo XMLA. Le estensioni ASSL consentono di utilizzare costrutti XMLA in Analysis Services oltre le funzionalità di base del protocollo, aggiungendo il supporto per definizione dei dati, manipolazione dei dati e controllo dei dati.  Mentre i metodi Execute e Discover vengono descritti dal protocollo XMLA, ASSL aggiunge la funzionalità seguente:<br /><br /> Script XMLA<br /><br /> Definizioni di oggetti XMLA<br /><br /> Comandi XMLA<br /><br /> <br /><br /> Per ulteriori informazioni, vedere [Sviluppo con Analysis Services Scripting Language &#40;ASSL&#41;](../scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).|  
  
## <a name="see-also"></a>Vedere anche  
 [Connetti a Analysis Services](../../instances/connect-to-analysis-services.md)   
 [Sviluppo con Analysis Services linguaggio di scripting &#40;ASSL&#41;](../scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [Sviluppo con XMLA in Analysis Services](../../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)   
 [Accesso ai dati di modello tabulare](../../tabular-models/tabular-model-data-access.md)  
  
  
