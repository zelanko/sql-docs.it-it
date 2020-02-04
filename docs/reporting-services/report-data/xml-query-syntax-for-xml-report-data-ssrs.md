---
title: Sintassi di query XML per i dati del report XML (SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- namespaces [Reporting Services]
- data processing extensions [Reporting Services], data sources
- xmldp [Reporting Services]
- XML [Reporting Services], data retrieval
ms.assetid: d203886f-faa1-4a02-88f5-dd4c217181ef
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3fc3cddc10dd53225867b910b8a3b3cb9c73d6ca
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "65574852"
---
# <a name="xml-query-syntax-for-xml-report-data-ssrs"></a>Sintassi di query XML per i dati del report XML (SSRS)
  In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]è possibile creare set di dati per origini dati XML. Dopo aver definito un'origine dati, è possibile creare una query per il set di dati. In base al tipo di dati XML a cui punta l'origine dati, è possibile creare la query del set di dati includendo un elemento **Query** XML o un percorso di elemento. Un elemento **Query** XML inizia con un tag **\<Query>** e include spazi dei nomi ed elementi XML che variano in base all'origine dati. Un percorso di elemento è indipendente dallo spazio dei nomi e specifica i nodi e gli attributi dei nodi dei dati XML sottostanti da utilizzare tramite una sintassi di tipo XPath. Per altre informazioni sui percorsi di elementi, vedere [Sintassi del percorso di elemento per i dati del report XML &#40;SSRS&#41;](../../reporting-services/report-data/element-path-syntax-for-xml-report-data-ssrs.md).  
  
 È possibile creare un'origine dei dati XML per i tipi di dati XML seguenti:  
  
-   Documenti XML a cui punta un URL tramite il protocollo HTTP  
  
-   Endpoint del servizio Web che restituiscono dati XML  
  
-   Dati XML incorporati  
  
 La modalità usata per specificare un elemento **Query** XML o un percorso di elemento dipende dal tipo di dati XML.  
  
 Per un documento XML, l'elemento **Query** XML è facoltativo. Se viene incluso, può contenere un elemento **ElementPath**XML facoltativo. Per il valore dell'elemento **ElementPath** XML viene usata la sintassi del percorso di elemento. Gli elementi **Query** XML ed **ElementPath** XML vengono inclusi per consentire l'elaborazione corretta degli spazi dei nomi quando richiesto dai dati XML dell'origine dati.  
  
 Per un endpoint servizio Web a cui punta un URL della stringa di connessione, l'elemento **Query** XML definisce l'azione SOAP o il metodo del servizio Web oppure entrambi. Tramite il provider di dati XML viene creata una richiesta del servizio Web per recuperare i dati XML da utilizzare per il report.  
  
> [!NOTE]  
>  Quando uno spazio dei nomi del servizio Web contiene una barra ( **/)** , includere sia il metodo del servizio Web che l'azione SOAP, per consentire all'estensione per l'elaborazione dati XML di derivare lo spazio dei nomi in modo corretto.  
  
 Per un documento XML incorporato, l'elemento **Query** XML definisce i dati XML incorporati da usare, include gli spazi dei nomi facoltativi e contiene un elemento **ElementPath**XML facoltativo.  
  
## <a name="specifying-query-parameters-for-xml-data"></a>Impostazione di parametri di query per dati XML  
 È possibile specificare parametri di query per documenti XML.  
  
-   Per le richieste di URL, i parametri di query vengono inclusi come parametri URL standard.  
  
-   Per le richieste del servizio Web, i parametri di query vengono passati al metodo del servizio Web. Per definire un parametro di query, usare la pagina **Parametri** della finestra di dialogo **Proprietà set di dati** . 
  
### <a name="example"></a>Esempio  
 Negli esempi della tabella seguente viene illustrato come recuperare i dati dal servizio Web ReportServer, da un documento XML e dai dati XML incorporati.  
  
|Origine dei dati XML|Esempio di query|  
|---------------------|-------------------|  
|Dati XML del servizio Web dal metodo <xref:ReportService2010.ReportingService2010.ListChildren%2A> .|`<Query>`<br /><br /> `<Method Name="ListChildren" Namespace="https://schemas.microsoft.com/sqlserver/2005/06/30/reporting/reportingservices" />`<br /><br /> `</Query>`|  
|Dati XML del servizio Web tramite SoapAction.|`<Query xmlns=namespace>`<br /><br /> `<SoapAction>https://schemas/microsoft.com/sqlserver/2005/03/23/reporting/reportingservices/ListChildren</SoapAction>`<br /><br /> `</Query>`|  
|Documento XML o dati XML incorporati che utilizzano spazi dei nomi.<br /><br /> Elemento Query specificando gli spazi dei nomi per un percorso di elemento.|`<Query xmlns:es="https://schemas.microsoft.com/StandardSchemas/ExtendedSales">`<br /><br /> `<ElementPath>/Customers/Customer/Orders/Order/es:LineItems/es:LineItem</ElementPath>`<br /><br /> `</Query>`|  
|Documento XML incorporato.|`<Query>`<br /><br /> `<XmlData>`<br /><br /> `<Customers>`<br /><br /> `<Customer ID="1">Bobby</Customer>`<br /><br /> `</Customers>`<br /><br /> `</XmlData>`<br /><br /> `<ElementPath>Customer {@}</ElementPath>`<br /><br /> `</Query>`|  
|Documento XML che utilizza valori predefiniti.|*Nessuna query*.<br /><br /> Il percorso viene derivato dal documento XML stesso ed è indipendente dallo spazio dei nomi.|  
  
> [!NOTE]  
>  Nel primo esempio di servizio Web è riportato il contenuto del server di report che usa il metodo <xref:ReportService2006.ReportingService2006.ListChildren%2A> . Per eseguire questa query, è necessario creare una nuova origine dati e impostare la stringa di connessione su `https://localhost/reportserver/reportservice2006.asmx`. Il metodo <xref:ReportService2006.ReportingService2006.ListChildren%2A> accetta due parametri: **Elemento** e **Ricorsivo**. Impostare il valore predefinito per **Elemento** su **/** e **Ricorsivo** su **1**.  
  
## <a name="specifying-namespaces"></a>Definizione degli spazi dei nomi  
 Usare l'elemento **Query** XML per specificare gli spazi dei nomi usati nei dati XML dell'origine dati. Nella query XML seguente viene usato lo spazio dei nomi **sales**. Nei nodi **ElementPath** XML per `sales:LineItems` e `sales:LineItem` viene usato lo spazio dei nomi **sales**.  
  
```  
<Query xmlns:sales=  
"https://schemas.microsoft.com/StandardSchemas/ExtendedSales">  
   <SoapAction>  
      https://schemas.microsoft.com/SalesWebService/ListOrders   
   </SoapAction>  
   <ElementPath>  
      Customers/Customer/Orders/Order/sales:LineItems/sales:LineItem  
   </ElementPath>  
</Query>  
```  
  
 Per specificare lo spazio dei nomi del provider di dati, affinché lo spazio dei nomi predefinito rimanga vuoto, usare **xmldp**, come illustrato nell'esempio seguente.  
  
### <a name="example"></a>Esempio  
 Negli esempi seguenti viene utilizzato il documento XML DPNamespace.xml, illustrato dopo la tabella. Nella tabella sono illustrati due esempi di sintassi ElementPath XML che include i prefissi degli spazi dei nomi.  
  
|Elemento Query XML|Campi risultanti nel set di dati|  
|-----------------------|-------------------------------------|  
|\<Query/>|Value A: `https://schemas.microsoft.com/...`<br /><br /> Value B: `https://schemas.microsoft.com/...`<br /><br /> Value C: `https://schemas.microsoft.com/...`|  
|`<xmldp:Query xmlns:xmldp="https://schemas.microsoft.com/sqlserver/2005/02/reporting/XmlDPQuery" xmlns:ns="https://schemas.microsoft.com/...">`<br /><br /> `<xmldp:ElementPath>Root {}/ns:Element2/Node</xmldp:ElementPath>`<br /><br /> `</xmldp:Query>`|Value D<br /><br /> Value E<br /><br /> Value F|  
  
#### <a name="xml-document-dpnamespacexml"></a>Documento XML: DPNamespace.xml  
 È possibile copiare il codice XML seguente e salvarlo in un URL disponibile per Progettazione report, per l'uso come origine dati XML, ad esempio, https://localhost/DPNamespace.xml.  
  
```  
<Root xmlns:ns="https://schemas.microsoft.com/...">  
   <ns:Element1>  
      <Node>Value A</Node>  
      <Node>Value B</Node>  
      <Node>Value C</Node>  
   </ns:Element1>  
   <ns:Element2>  
      <Node>Value D</Node>  
      <Node>Value E</Node>  
      <Node>Value F</Node>  
   </ns:Element2>  
</Root>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Tipo di connessione XML &#40;SSRS&#41;](../../reporting-services/report-data/xml-connection-type-ssrs.md)   
 [Esercitazioni su Reporting Services &#40;SSRS&#41;](../../reporting-services/reporting-services-tutorials-ssrs.md)  
  
  
