---
title: Connessioni dati, origini dati e stringhe di connessione in Generatore Report | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10421"
ms.assetid: 7e103637-4371-43d7-821c-d269c2cc1b34
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: eb8d81c9c47f00ed84036accf86768d084072c4d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109486"
---
# <a name="data-connections-data-sources-and-connection-strings-in-report-builder"></a>Connessioni dati, origini dati e stringhe di connessione in Generatore report
  Per includere dati in un report, è possibile creare connessioni dati e set di dati. In una connessione dati sono incluse informazioni sulla modalità di accesso a un'origine dati esterna. In un set di dati è incluso un comando di query che consente di specificare i dati da includere tramite la connessione dati.  
  
1.  **Origini dati nel riquadro dei dati del report** Un'origine dati viene visualizzata nel riquadro dei dati del report in seguito alla creazione di un'origine dati incorporata o all'aggiunta di un'origine dati condivisa.  
  
2.  **Finestra di dialogo Connessione** Usare la finestra di dialogo Connessione per compilare o incollare una stringa di connessione.  
  
3.  **Informazioni sulla connessione dati** La stringa di connessione viene passata all'estensione per i dati.  
  
4.  **Credenziali** Le credenziali vengono gestite separatamente dalla stringa di connessione.  
  
5.  **Estensioni dati/provider di dati** La connessione ai dati può avvenire attraverso più livelli di accesso ai dati.  
  
6.  **Origini dati esterne** È possibile recuperare dati da database relazionali, database multidimensionali, elenchi SharePoint, servizi Web o modelli di report.  
  
 Per altre informazioni, vedere [incorporate e condivise le connessioni dati o origini dati &#40;Generatore Report e SSRS&#41; ](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md) e [connessioni dati, origini dati e stringhe di connessione in Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
 I dati possono anche essere inclusi in un report tramite origini dati condivise predefinite, set di dati condivisi e parti del report. Tali elementi dispongono già delle informazioni necessarie sulla connessione dati. Per altre informazioni, vedere [aggiungere dati a un Report &#40;Generatore Report e SSRS&#41;](report-data/report-datasets-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
 ![rs_DataSourcesStory](media/rs-datasourcesstory.gif "rs_DataSourcesStory")  
  
##  <a name="ConnectionString"></a> Esempi di stringhe di connessione  
 In una connessione dati è inclusa una stringa di connessione fornita in genere dal proprietario dell'origine dati esterna. Nella tabella seguente sono elencati esempi di stringhe di connessione per diversi tipi di origini dati esterne.  
  
|**Origine dati**|**Esempio**|**Descrizione**|  
|---------------------|-----------------|---------------------|  
|Database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nel server locale|`data source="(local)";initial catalog=AdventureWorks2012`|Impostare il tipo di origine dati su `SQL Server`.|  
|Database dell'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|`Data Source=localhost\MSSQL12.InstanceName; Initial Catalog= AdventureWorks2012`|Impostare il tipo di origine dati su `SQL Server`.|  
|Database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express|`Data Source=localhost\MSSQL12.SQLEXPRESS; Initial Catalog= AdventureWorks2012`|Impostare il tipo di origine dati su `SQL Server`.|  
|Database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] nel server locale|`data source=localhost;initial catalog=Adventure Works DW 2012`|Impostare il tipo di origine dati su `SQL Server Analysis Services`.|  
|Elenco SharePoint|`data source=http://MySharePointWeb/MySharePointSite/`|Impostare il tipo di origine dati su `SharePoint List`.|  
||||  
|Modelli di report|Non applicabile.|Non è necessaria una stringa di connessione per un modello di report. In Generatore report individuare il server di report e selezionare il file con estensione smdl che rappresenta il modello di report.|  
|Server Oracle|`data source=myserver`|Impostare il tipo di origine dati su `Oracle`. È necessario installare gli strumenti client Oracle nel computer di Generatore report e nel server di report.|  
|Origine dati SAP NetWeaver BI|`DataSource=http://mySAPNetWeaverBIServer:8000/sap/bw/xml/soap/xmla`|Impostare il tipo di origine dati su `SAP NetWeaver BI`.|  
|Origine dati Hyperion Essbase|`Data Source=http://localhost:13080/aps/XMLA; Initial Catalog=Sample`|Impostare il tipo di origine dati su `Hyperion Essbase`.|  
|Origine dati Teradata|`data source=` *\<NN>.\<NNN>.\<NNN>.\<N>* `;`|Impostare il tipo di origine dati su `Teradata`. La stringa di connessione è un indirizzo IP (Internet Protocol) nel formato in quattro campi, ognuno dei quali può contenere da una a tre cifre.|  
|Origine dati Teradata|`Database=` *\<nome database>* `; data source=` *\<NN*N *>.\<NNN>.\<NNN>.\<N*NN *>* `;Use X Views=False;Restrict to Default Database=True`|Impostare il tipo di origine dati su `Teradata`, analogamente all'esempio precedente. Utilizzare solo il database predefinito specificato nel tag Database e non individuare automaticamente le relazioni dei dati.|  
|Origine dati XML, servizio Web|`data source=http://adventure-works.com/results.aspx`|Impostare il tipo di origine dati su `XML`. La stringa di connessione è un URL per un servizio Web che supporta Web Services Definition Language (WSDL).|  
|Origine dati XML, documento XML|`http://localhost/XML/Customers.xml`|Impostare il tipo di origine dati su `XML`. La stringa di connessione è un URL per il documento XML.|  
|Origine dati XML, documento XML incorporato|*Vuoto*|Impostare il tipo di origine dati su `XML`. I dati XML vengono incorporati nella definizione del report.|  
  
 Per altre informazioni su ogni tipo di connessione, vedere [aggiungere dati da origini dati esterne &#40;SSRS&#41; ](report-data/add-data-from-external-data-sources-ssrs.md) e [origini dati supportate da Reporting Services &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md).  
  

  
##  <a name="Creating"></a> Creazione di origini dati  
 Per creare un'origine dati incorporata, l'utente deve disporre di una stringa di connessione e delle credenziali necessarie per l'accesso ai dati. Queste informazioni provengono solitamente dal proprietario dell'origine dati. La connessione dati viene salvata nella definizione del report come parte dell'origine dati. Le credenziali vengono gestite indipendentemente dalla connessione. Per istruzioni dettagliate, vedere [aggiungere e verificare una connessione dati o un'origine dati &#40;Generatore Report e SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  Alcuni tipi di credenziali potrebbero non supportare tutti gli scenari utilizzati da Generatore report: per eseguire una query in Progettazione query, visualizzare l'anteprima di un report dal computer in uso quando non si è connessi a un server di report ed eseguire il report dal server di report. Si consiglia di utilizzare le origini dati condivise tutte le volte che è consentito. È possibile archiviare le credenziali per un'origine dati condivisa sul server di report. Per altre informazioni, vedere [Specifica di credenziali in Generatore report](../../2014/reporting-services/specify-credentials-in-report-builder.md).  
  
 Per creare un'origine dati condivisa, è necessario utilizzare Gestione Report per creare l'origine dati direttamente nel server di report, oppure usare un ambiente di creazione quale progettazione Report in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Per altre informazioni, vedere [creare un'origine dati condivisa o un Embedded &#40;SSRS&#41;](../../2014/reporting-services/create-an-embedded-or-shared-data-source-ssrs.md).  
  

  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere dati a un Report &#40;Report e SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [Parti del report &#40;Generatore report e SSRS&#41;](report-parts-report-builder-and-ssrs.md)  
  
  
