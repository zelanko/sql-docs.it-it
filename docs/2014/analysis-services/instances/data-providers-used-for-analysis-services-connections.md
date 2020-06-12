---
title: Provider di dati utilizzati per le connessioni Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 128f6dde-409d-4c12-9820-3305bab57b75
author: minewiskan
ms.author: owend
ms.openlocfilehash: 0a48316bb89f92ba8b44e3160a6b38e77762f3be
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84543983"
---
# <a name="data-providers-used-for-analysis-services-connections"></a>Provider di dati usati per le connessioni ad Analysis Services
  Analysis Services fornisce tre provider di dati per l'accesso al server e ai dati. Tutte le applicazioni che si connettono ad Analysis Services effettuano l'accesso mediante una di tali provider. Due provider, ADOMD.NET e Analysis Services Management Objects (AMO), sono provider di dati gestiti, mentre il provider OLE DB di Analysis Services (MSOLAP DLL) è un provider di dati nativo.  
  
 Nelle organizzazioni in cui vengono eseguite più versioni di Analysis Services potrebbe essere necessario installare versioni più recenti dei provider di dati nelle workstation degli utenti che si connettono ai dati di Analysis Services. Le connessioni a versioni più recenti di Analysis Services richiedono provider di dati della stessa versione principale. Per accedere [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)], ad esempio, in ogni workstation deve essere presente un provider di dati della versione 2014. Sebbene con Excel vengano installati provider di dati a cui è necessario connettersi, il provider fornito spesso non è aggiornato rispetto alle istanze di Analysis Services in uso.  
  
 In questo argomento è contenuta la sezione seguente:  
  
 [Come determinare la versione del server](#bkmk_ServVers)  
  
 [Come determinare la versione dei provider di dati di Analysis Services](#bkmk_LibUpdate)  
  
 [Dove trovare li provider di dati con la versione più recente](#bkmk_downloadsite)  
  
 [Provider OLE DB per Analysis Services](#bkmk_OLE)  
  
 [ADOMD.NET](#bkmk_ADOMD)  
  
 [AMO](#blkmk_AMO)  
  
##  <a name="how-to-determine-server-version"></a><a name="bkmk_ServVers"></a>Come determinare la versione del server  
 Se si conosce la versione dell'istanza di Analysis Services, sarà possibile determinare se è necessario installare versioni più recenti dei provider di dati nelle workstation dell'organizzazione.  
  
-   In SQL Server Management Studio connettersi all'istanza di Analysis Services. Fare clic con il pulsante destro del mouse sull'istanza che si desidera controllare, scegliere **report**, quindi fare clic su **generale**. Nel report vengono visualizzate le informazioni su build di versione ed edizione.  
  
 Il numero della build principale della versione iniziale di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] is 12.0.2000.9.  
  
 Per ulteriori dettagli su come ottenere le informazioni sulla versione e sulla build, vedere [Identificazione della versione e dell'edizione di SQL Server e relativi componenti](https://support.microsoft.com/kb/321185).  
  
##  <a name="how-to-determine-the-version-of-the-analysis-services-data-providers"></a><a name="bkmk_LibUpdate"></a>Come determinare la versione dei provider di dati Analysis Services  
 I provider di dati vengono installati con Analysis Services e con le applicazioni client che si connettono normalmente ai database di Analysis Services, ad esempio Excel.  
  
 Office 2007 installa i provider di dati da SQL Server 2005. Office 2010 installa i provider di dati da SQL Server 2008. e in Office 2013 da SQL Server 2012. Se si utilizzano più versioni di Office o di SQL Server e le connessioni e funzionalità disponibili non sono quelle previste, potrebbe essere necessario installare una versione più recente dei provider di dati. È possibile eseguire più versioni principali di ogni provider di dati side-by-side sullo stesso computer.  
  
#### <a name="find-the-file-version-of-the-oledb-provider"></a>Individuazione della versione del file del provider OLEDB  
  
1.  Andare a \Programmi\Microsoft Analysis Services\AS OLEDB\120.  
  
2.  Fare clic con il pulsante destro del mouse su msolap120.dll e scegliere **Proprietà**.  
  
 Se il file non è presente in questo percorso o se il percorso della cartella include AS OLEDB\110 o AS OLEDB\90, la libreria in uso è obsoleta ed è necessario installare una versione più recente (AS OLEDB\11) per connettersi a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
#### <a name="find-the-file-version-of-adomdnet-and-amo"></a>Individuazione della versione di ADOMD.NET e AMO  
  
1.  Passare a C:\Windows\Assembly  
  
2.  Fare clic con il pulsante destro del mouse su Microsoft.AnalysisServices.AdomdClient e scegliere **Proprietà**. Fare clic su **Versione**.  
  
     Per AMO, fare clic con il pulsante destro del mouse su Microsoft.AnalysisServices.  
  
 Per ulteriori informazioni sui numeri di versione e di build, vedere [Build di SQL Server su Blogspot](http://sqlserverbuilds.blogspot.com).  
  
##  <a name="where-to-get-newer-version-data-providers"></a><a name="bkmk_downloadsite"></a>Dove ottenere i provider di dati della versione più recente  
 La versione installata nel computer client deve corrispondere alla versione principale del server che fornisce i dati. Se l'installazione del server è più recente dei provider di dati installati nelle workstation in rete, potrebbe essere necessario installare librerie più recenti.  
  
#### <a name="find-the-data-providers-on-the-download-site"></a>Individuare i provider di dati nel sito di download  
  
1.  Accedere all' [area download Microsoft](https://go.microsoft.com/fwlink/p/?LinkID=296473).  
  
2.  Espandere **Istruzioni di installazione**.  
  
3.  Scorrere verso il basso fino alla sezione contenente i componenti di Analysis Services. ADOMD.NET, il provider OLE DB e AMO sono la seconda, la terza e la quarta voce dell'elenco. Ogni libreria è disponibile nelle versioni a 32 o 64 bit. I server e le workstation più recenti che eseguono un sistema operativo a 64 bit richiedono la versione a 64 bit.  
  
##  <a name="analysis-services-ole-db-provider"></a><a name="bkmk_OLE"></a>Provider OLE DB Analysis Services  
 Il provider OLE DB per Analysis Services è il provider nativo per le connessioni di database Analysis Services. MSOLAP viene utilizzato indirettamente da ADOMD.NET e AMO, delegando le richieste di connessione al provider di dati. È inoltre possibile chiamare il provider OLE DB direttamente dal codice dell'applicazione, il che è possibile se i requisiti della soluzione precludono l'utilizzo di un'API gestita.  
  
 Il provider OLE DB per Analysis Services viene installato automaticamente dal programma di installazione di SQL Server, Excel e altre applicazioni utilizzate con frequenza per accedere ai database di Analysis Services. Può essere installato anche manualmente scaricandolo dall'Area download. Per impostazione predefinita, il provider è contenuto nella cartella \Programmi\Microsoft Analysis Services. Il provider deve essere installato su qualsiasi workstation utilizzata per accedere ai dati di Analysis Services.  
  
 MSOLAP130.dll è la versione del provider OLE DB per Analysis Services fornita con [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Altre versioni precedenti recenti includono MSOLAP10.dll (per SQL Server 2008 e 2008 R2) e MSOLAP90.dll (per SQL Server 2005).  
  
 I provider OLE DB vengono spesso specificati sulle stringhe di connessione. Una stringa di connessione Analysis Services utilizza una nomenclatura diversa per fare riferimento al provider OLE DB: MSOLAP. \<version> . dll  
  
 MSOLAP.5.dll è il provider OLE DB per Analysis Services corrente installato con Excel 2013. Le versioni precedenti, ad esempio MSOLAP.4.dll o MSOLAP.3.dll, sono spesso disponibili nelle workstation che eseguono versioni meno recenti di Excel. Alcune funzionalità di Analysis Services, ad esempio il componente aggiuntivo PowerPivot, richiedono versioni specifiche del provider OLE DB. Per altre informazioni, vedere [Proprietà delle stringhe di connessione &#40;Analysis Services&#41;](connection-string-properties-analysis-services.md).  
  
##  <a name="adomdnet"></a><a name="bkmk_ADOMD"></a>ADOMD.NET  
 ADOMD.NET è un provider di dati gestito utilizzata per eseguire query sui dati di Analysis Services. Excel utilizza ADOMD.NET per la connessione a un cubo di Analysis Services specifico. La stringa di connessione indicata in Excel è destinata a una connessione ADOMD.NET.  
  
 ADOMD.NET viene installato dal programma di installazione di SQL Server ed è utilizzato dalle applicazioni client SQL Server per la connessione ad Analysis Services. In Office questa libreria viene installata per supportare le connessioni dati da Excel. Come con altri provider di dati inclusi in SQL Server, è possibile ridistribuire ADOMD.NET se si utilizza la libreria nel codice personalizzato. È anche possibile scaricarlo e installarlo manualmente per ottenere la versione più recente. A questo proposito, vedere [Come determinare la versione dei provider di dati di Analysis Services](#bkmk_LibUpdate) in questo argomento.  
  
 Per controllare le informazioni sulla versione dei file, cercare ADOMD.NET nella Global Assembly Cache, dove è elencato come `Microsoft.AnalysisServices.AdomdClient`.  
  
 Quando ci si connette a un database, le proprietà della stringa di connessione per tutte e tre le librerie sono in gran parte corrispondenti. Quasi tutte le stringhe di connessione definite per ADOMD.NET (<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>) funzioneranno anche per AMO e per il provider OLE DB per Analysis Services. Per altre informazioni, vedere [Proprietà delle stringhe di connessione &#40;Analysis Services&#41;](connection-string-properties-analysis-services.md).  
  
 Per ulteriori informazioni sulla connessione a livello di programmazione, vedere [Establishing Connections in ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-client/connections-in-adomd-net).  
  
##  <a name="amo"></a><a name="blkmk_AMO"></a> AMO  
 AMO è un provider di dati gestito utilizzato per l'amministrazione del server e la definizione dei dati. Ad esempio, in SQL Server Management Studio si utilizza AMO per connettersi ad Analysis Services.  
  
 AMO viene installato dal programma di installazione di SQL Server ed è utilizzato dalle applicazioni client SQL Server per la connessione ad Analysis Services. È anche possibile scaricarlo e installarlo manualmente quando si usa AMO nel codice personalizzato. A questo proposito, vedere [Come determinare la versione dei provider di dati di Analysis Services](#bkmk_LibUpdate) in questo argomento. AMO può essere presente nella Global Assembly Cache, come `Microsoft.AnalysisServices`.  
  
 Una connessione tramite AMO è in genere minima, composta da "Data Source = \<servername> ". Dopo che è stata stabilita una connessione, l'API consente di usare le raccolte di database e gli oggetti principali. Sia SSDT che SSMS usano AMO per connettersi a un'istanza di Analysis Services.  
  
 Per ulteriori informazioni sulla connessione a livello di programmazione, vedere [Programming AMO Fundamental Objects](https://docs.microsoft.com/bi-reference/amo/programming-amo-fundamental-objects).  
  
## <a name="see-also"></a>Vedere anche  
 [Connetti ad Analysis Services](connect-to-analysis-services.md)  
  
  
