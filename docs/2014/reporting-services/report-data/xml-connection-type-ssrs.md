---
title: Tipo di connessione XML (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 5b55fff2-1b15-4156-83ef-15ad9cf9f509
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6d9f5c70e0457009f71c3b9087ecf9f1354a8835
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66106930"
---
# <a name="xml-connection-type-ssrs"></a>Tipo di connessione XML (SSRS)
  Per includere dati nel report da un'origine dati XML, è necessario disporre di un set di dati basato su un'origine dati del report di tipo XML. Questo tipo di origine dati incorporato è basato sull'estensione per i dati XML. Utilizzare questo tipo di origine dati per connettersi e recuperare dati da documenti XML, servizi Web o valori XML incorporati nella query.  
  
 Questa estensione per i dati supporta parametri e credenziali gestiti separatamente dalla stringa di connessione.  
  
 Usare le informazioni presenti in questo argomento per compilare un'origine dati. Per istruzioni dettagliate, vedere [aggiungere e verificare una connessione dati o un'origine dati &#40;Generatore report e SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="connection-string"></a><a name="Connection"></a> Stringa di connessione  
 La stringa di connessione deve essere un URL che punta al servizio Web, all'applicazione Web o al documento XML disponibile tramite HTTP. I documenti XML devono avere estensione xml. È inoltre possibile utilizzare una stringa di connessione vuota per i dati XML incorporati nella query del set di dati.  
  
 Nell'esempio seguente viene illustrata la sintassi della stringa di connessione, rispettivamente per un servizio Web e per un documento XML. Il protocollo `file://` non è supportato.  
  
|Tipo di documento XML|Esempio di stringa di connessione|  
|-----------------------|-------------------------------|  
|Servizio Web|`http://adventure-works.com/results.aspx`|  
|Documento XML|`http://localhost/XML/Customers.xml`|  
|Documento XML incorporato|*Vuoto*|  
  
 Per altri esempi di stringhe di connessione, vedere [Connessioni dati, origini dati e stringhe di connessione in Generatore report](../data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
##  <a name="credentials"></a><a name="Credentials"></a> Credenziali  
 Le credenziali sono necessarie per eseguire query, nonché per visualizzare l'anteprima del report in locale e dal server di report.  
  
 Dopo aver pubblicato il report, potrebbe essere necessario modificare le credenziali per l'origine dati affinché quando il report viene eseguito nel server di report, le autorizzazioni per il recupero dei dati risultino valide.  
  
 Da un client di creazione di report sono disponibili le opzioni seguenti per la specifica delle credenziali:  
  
-   Utente di Windows corrente (nota anche come sicurezza integrata).  
  
-   Non sono necessarie credenziali. Se non si specificano credenziali, viene utilizzato l'accesso anonimo. Verificare di aver definito l'account di esecuzione automatica per il server di report per eseguire la connessione a un'origine dei dati esterna. L'estensione per l'elaborazione di dati XML non passa credenziali all'URL di destinazione o al servizio Web, pertanto la connessione ha esito positivo solo se è stato definito l'account di esecuzione automatica. Per altre informazioni, vedere [Configurare l'account di esecuzione automatica &#40;Gestione configurazione SSRS&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md) nella documentazione relativa a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Documentazione online](https://go.microsoft.com/fwlink/?linkid=121312) di  su msdn.microsoft.com.  
  
 Credenziali archiviate e credenziali fornite dall'utente non sono supportate. Se la sicurezza integrata di Windows è disabilitata, non è possibile utilizzarla per recuperare dati. Se si specificano credenziali archiviate o fornite dall'utente, si verificherà un errore in fase di esecuzione.  
  
 Per ulteriori informazioni, vedere [connessioni dati, origini dati e stringhe di connessione in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) o [specificare le credenziali in Generatore report](../specify-credentials-in-report-builder.md).  
  
##  <a name="queries"></a><a name="Query"></a> Query  
 Una query consente di specificare quali dati recuperare per un set di dati del report. Le colonne nel set di risultati per una query popolano la raccolta dei campi per un set di dati. In un report viene elaborato solo il primo set di risultati recuperato da una query.  
  
 Per creare la query, è necessario utilizzare la finestra Progettazione query basata su testo. La query deve restituire dati XML.  
  
 Per altre informazioni sulla finestra Progettazione query basata su testo, vedere [Interfaccia utente di Progettazione query basata su testo &#40;Generatore report &#41;](text-based-query-designer-user-interface-report-builder.md).  
  
 I valori possibili di una query del set di dati per un'origine dati di tipo XML sono illustrati di seguito.  
  
-   *Empty*: consente di utilizzare una query vuota per creare un set di risultati predefinito. La query predefinita viene creata leggendo l'origine dei dati e attraversando la gerarchia del nodo XML fino alla prima raccolta foglia. Il set di risultati include tutti i nodi con valori di testo e tutti gli attributi dei nodi nel percorso. Sulle colonne del set di risultati viene eseguito il mapping ai campi del set di dati.  
  
-   Un percorso di elemento: specifica la sequenza di nodi da utilizzare durante il recupero di dati XML dall'origine dati.  
  
-   Elemento XML Query: specifica di query XML con gli elementi facoltativi seguenti:  
  
    -   **Per un servizio Web:**  
  
         Elementi XML obbligatori:  
  
         `<Method Namespace=`*"Namespace"*  `Name="MethodName" />`  
  
         `-- or --`  
  
         `<SoapAction>` *soap action* `</SoapAction>`  
  
         Elementi XML facoltativi:  
  
         `<ElementPath>`  *element path*  `</ElementPath>`  
  
         `<Method Namespace=`*"Namespace"*  `Name="MethodName" />`  
  
         `-- or --`  
  
         `<SoapAction>` *soap action* `</SoapAction>`  
  
    -   **Per un documento XML:**  
  
         Elementi XML facoltativi:  
  
         `<ElementPath>`  *element path*  `</ElementPath>`  
  
    -   **Per un documento XML incorporato:**  
  
         Elementi XML obbligatori:  
  
         `<XmlData>` inner XML `</XmlData>`  
  
         Elementi XML facoltativi:  
  
         `<ElementPath>`  *element path*  `</ElementPath>`  
  
         `-- or --`  
  
         `<ElementPath IgnoreNamespaces="true">`  *element path*  `</ElementPath>`  
  
 Per altre informazioni sulla sintassi di query, vedere [Sintassi di query XML per i dati del report XML &#40;SSRS&#41;](report-data-ssrs.md) nella documentazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Documentazione online](https://go.microsoft.com/fwlink/?linkid=121312) su msdn.microsoft.com.  
  
 Per consultare degli esempi, vedere [Reporting Services: Using XML and Web Service Data Sources](https://go.microsoft.com/fwlink/?LinkId=81654).  
  
### <a name="requirements-for-retrieving-xml-web-service-data"></a>Requisiti per il recupero di dati del servizio Web XML  
 Lo schema non viene rilevato automaticamente dall'estensione per l'elaborazione dati XML. È pertanto necessario essere in grado di individuare i metodi SOAP tramite i quali verranno recuperati i dati desiderati. È inoltre necessario comprendere lo spazio dei nomi o lo schema di indirizzamento che il servizio Web utilizza per i dati.  
  
 Per un servizio Web, è possibile fornire un <`Query` elemento> che specifica un metodo da chiamare o un'azione SOAP. È possibile lasciare la query vuota e utilizzare la query predefinita se l'origine dei dati XML ha una struttura gerarchica che genera i dati che si desidera utilizzare per il report. Per gli attributi e i valori del nodo elemento XML recuperati durante l'esecuzione della query viene eseguito il mapping ai campi del set di dati utilizzati nel report.  
  
### <a name="requirements-for-retrieving-xml-document-data"></a>Requisiti per il recupero di dati di documenti XML  
 Se si utilizza il protocollo HTTP, il server deve restituire dati XML oppure i dati XML devono essere incorporati nell'elemento `Query` XML. Se si fa riferimento a un documento XML direttamente utilizzando il protocollo HTTP, l'estensione deve essere xml.  
  
 È necessario conoscere la procedura di creazione di una query XML per il recupero di tutti i dati che si desidera utilizzare. Se non viene specificato un percorso di elemento, il comportamento predefinito previsto per l'analisi di un documento XML consiste nel selezionare il primo percorso disponibile di una raccolta di nodi foglia nel documento XML. Se nel documento XML sono inclusi percorsi aggiuntivi di altre raccolte di nodi foglia di pari livello, tali nodi verranno ignorati a meno che non venga specificato un percorso nella query.  
  
 È possibile specificare un percorso di elemento utilizzando una sintassi XML simile a XQuery.  
  
 Per altre informazioni sulla sintassi di query, vedere [Sintassi del percorso di elemento per i dati del report XML &#40;SSRS&#41;](element-path-syntax-for-xml-report-data-ssrs.md) nella documentazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Documentazione online](https://go.microsoft.com/fwlink/?linkid=121312) su msdn.microsoft.com.  
  
##  <a name="parameters"></a><a name="Parameters"></a> Parametri  
 La query non viene analizzata per identificare parametri.  
  
 Per aggiungere i parametri, è necessario crearli manualmente usando la pagina **Parametri** nella finestra di dialogo [Proprietà set di dati](../dataset-properties-dialog-box-parameters-report-builder.md) .  
  
##  <a name="remarks"></a>Osservazioni su <a name="Remarks"></a>  
 L'estensione per i dati XML supporta report di dati XML tabulari e non gerarchici. Per altre informazioni, vedere [Aggiungere dati da origini dati esterne &#40;SSRS&#41;](add-data-from-external-data-sources-ssrs.md).  
  
 Non è disponibile alcun supporto predefinito per il recupero di documenti XML da un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
##  <a name="how-to-topics"></a><a name="HowTo"></a>Procedure  
 In questa sezione sono contenute istruzioni dettagliate per l'utilizzo di connessioni dati, origini dati e set di dati.  
  
 [Aggiungere e verificare una connessione dati o un'origine dati &#40;Generatore report e SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [Creare un set di dati condiviso o un set di dati incorporato &#40;Generatore report e SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [Aggiungere un filtro a un set di dati &#40;Generatore report e SSRS&#41;](add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
##  <a name="related-sections"></a><a name="Related"></a>Sezioni correlate  
 In queste sezioni della documentazione sono incluse informazioni concettuali approfondite sui dati dei report, nonché le informazioni necessarie sulle procedure per definire, personalizzare e usare parti di un report correlate ai dati.  
  
 [Aggiungere dati a un report &#40;Generatore report e SSRS&#41;](report-datasets-ssrs.md)  
 Viene fornita una panoramica sull'accesso ai dati del report.  
  
 [Connessioni dati, origini dati e stringhe di connessione in Generatore report](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
 Vengono fornite informazioni sulle connessioni dati e sulle origini dati.  
  
 [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Vengono fornite informazioni sui set di dati incorporati e condivisi.  
  
 [Raccolta di campi del set di dati &#40;Generatore report e SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)  
 Vengono fornite informazioni sulla raccolta di campi di set di dati generata dalla query.  
  
 [Origini dati supportate da Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) nella documentazione relativa a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] inclusa nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [documentazione online](https://go.microsoft.com/fwlink/?linkid=121312) di .  
 Vengono fornite informazioni dettagliate sul supporto delle piattaforme e delle versioni per ogni estensione per i dati.  
  
## <a name="see-also"></a>Vedi anche  
 [Parametri del report &#40;Generatore report e Progettazione report&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtrare, raggruppare e ordinare i dati &#40;Generatore report e SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Espressioni &#40;Generatore report e SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
  
  
