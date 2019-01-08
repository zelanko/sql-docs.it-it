---
title: Tipo di connessione dell'elenco SharePoint (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 2c4adf2f-e9c4-4fae-bd3c-97fe64436caf
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: d218103d5a8de6b10ad5b1981f13ac4526f59aee
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53358243"
---
# <a name="sharepoint-list-connection-type-ssrs"></a>Tipo di connessione dell'elenco SharePoint (SSRS)
  Per includere dati da un elenco Microsoft SharePoint nel report, è necessario aggiungere o creare un set di dati basato su un'origine dati del report di tipo Elenco Microsoft SharePoint. Si tratta di un tipo di origine dati predefinito basato sull'estensione per i dati dell'Elenco SharePoint di Microsoft SQL Server Reporting Services. Utilizzare questo tipo di origine dati per connettersi e recuperare i dati dell'elenco dai siti [!INCLUDE[SPF2010](../../includes/spf2010-md.md)], [!INCLUDE[SPS2010](../../includes/sps2010-md.md)], [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 3.0 e [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007.  
  
 Usare le informazioni presenti in questo argomento per compilare un'origine dati. Per istruzioni dettagliate, vedere [aggiungere e verificare una connessione dati o un'origine dati &#40;Generatore Report e SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a> Stringa di connessione  
 La stringa di connessione a un elenco SharePoint è l'URL al sito principale o secondario di SharePoint, ad esempio `http://MySharePointWeb/MySharePointSite` o `http://MySharePointWeb/MySharePointSite/Subsite`.  
  
 In Progettazione query vengono visualizzati automaticamente gli elenchi SharePoint a cui è possibile accedere perché si dispone delle autorizzazioni sufficienti.  
  
 Per altri esempi di stringhe di connessione, vedere [Connessioni dati, origini dati e stringhe di connessione in Generatore report](../data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
##  <a name="Credentials"></a> Credenziali  
 Le credenziali sono necessarie per eseguire query, nonché per visualizzare l'anteprima del report in locale e dal server di report. Dopo aver pubblicato il report, potrebbe essere necessario modificare le credenziali per l'origine dati affinché quando il report viene eseguito nel server di report, le autorizzazioni per il recupero dei dati risultino valide. I tipi di credenziali che è possibile usare con questa estensione per i dati dipendono dalla configurazione della tecnologia SharePoint per l'elenco SharePoint usato come origine dati.  
  
 Nelle tabelle seguenti viene illustrato il comportamento di recupero delle credenziali per l'estensione dell'elenco SharePoint, quando ci si connette a un elenco SharePoint di una farm locale e a un elenco SharePoint remoto.  
  
 La**Tabella 1** è indicata per i report distribuiti in un sito Windows SharePoint legacy. Un sito Windows legacy supporta solo Kerberos, NTLM e l'autenticazione basata su moduli (FBA, Forms Based Authentication). La**tabella 2** è indicata per i report distribuiti in un sito di SharePoint basato sulle attestazioni.  
  
 **Tabella 1**  
  
||Credenziali supportate|Autenticazione di Windows in modalità classica|<sup>3</sup> autenticazione delle attestazioni|  
|-|---------------------------|-----------------------------------------|----------------------------------------|  
|Elenco SharePoint di una farm locale|Autenticazione di Windows (integrata) o token utente di SharePoint|Yes|Yes|  
||Archiviate, su richiesta, nessuna (con le credenziali di Windows<sup>1</sup>)|Yes|No|  
|Elenco SharePoint remoto|Autenticazione di Windows (integrata) o token utente di SharePoint|Yes|Non<sup>2</sup>|  
||Archiviate, su richiesta, nessuna (con le credenziali di Windows<sup>1</sup>)|Yes|Non<sup>2</sup>|  
  
 **tabella 2**  
  
||Credenziali supportate|Autenticazione di Windows in modalità classica|<sup>3</sup> autenticazione delle attestazioni|  
|-|---------------------------|-----------------------------------------|----------------------------------------|  
|Elenco SharePoint di una farm locale|Autenticazione di Windows (integrata) o token utente di SharePoint|Yes|Yes|  
||Archiviate, su richiesta, nessuna (con le credenziali di Windows<sup>1</sup>)|No|No|  
|Elenco SharePoint remoto|Autenticazione di Windows (integrata) o token utente di SharePoint|Yes|Non<sup>2</sup>|  
||Archiviate, su richiesta, nessuna (con le credenziali di Windows<sup>1</sup>)|No|Non<sup>2</sup>|  
  
 <sup>1</sup> credenziali archiviate e credenziali su richiesta con credenziali non Windows non è supportato.  
  
 <sup>2</sup> l'autenticazione basata su form e l'autenticazione delle attestazioni non sono supportate per gli elenchi SharePoint remoti.  
  
 <sup>3</sup> l'autenticazione di Windows, autenticazione basata su form (FBA), i token Secure Application Markup Language (SAML), altri provider di identità o una combinazione di più di quanto sopra accennato provider di autenticazione.  
  
 **Autenticazione di Windows**  
 Per una tecnologia SharePoint configurata per essere usata con un server di report in modalità Account attendibile, questa opzione non è supportata. Si applica solo alle versioni precedenti di SQL Server 2012 Reporting Services.  
  
 Per una tecnologia SharePoint configurata per essere usata con un server di report nella modalità integrata di Windows, questa opzione si applica sia all'utente corrente di Windows sia all'utente corrente di SharePoint.  
  
 Per una tecnologia SharePoint configurata per essere usata senza un server di report (modalità locale), questa opzione non è supportata. Per altre informazioni sulla modalità locale, vedere [Report in modalità locale e con connessione nel visualizzatore di report &#40;Reporting Services in modalità SharePoint&#41;](../local-vs-connected-mode-report-viewer-reporting-services-sharepoint-mode.md).  
  
 **Credenziali non richieste (Non usare credenziali):**  
 Per usare questa opzione, è necessario configurare l'account di esecuzione automatica sul server di report. Per altre informazioni, vedere [Configurare l'account di esecuzione automatica &#40;Gestione configurazione SSRS&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
 Per informazioni sul supporto dell'autenticazione delle attestazioni nello stack di Microsoft Business Intelligence, vedere la pagina relativa all' [utilizzo dell'autenticazione delle attestazioni nello stack di Microsoft Business Intelligence](https://social.technet.microsoft.com/wiki/contents/articles/15274.using-claims-authentication-across-the-microsoft-bi-stack.aspx).  
  
 Per altre informazioni, vedere [connessioni dati, origini dati e stringhe di connessione in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md), [specificare le credenziali in Generatore Report](../specify-credentials-in-report-builder.md), e [origini dati supportate da Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md).  
  
##  <a name="Query"></a> Query  
 Per progettare una query, creare un nuovo set di dati basato sull'origine dati, quindi aprire la finestra Progettazione query associata. Per altre informazioni, vedere [Creare un set di dati condiviso o un set di dati incorporato &#40;Generatore report e SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md).  
  
 Nella finestra Progettazione query con interfaccia grafica dell'elenco SharePoint vengono visualizzati quattro riquadri:  
  
 **Elenchi SharePoint**  Viene visualizzato un elenco di tutti gli elenchi SharePoint nel sito per questa origine dati. Selezionare un elenco, quindi selezionare i campi desiderati per la query. I nomi di campi in questo riquadro sono i nomi descrittivi di SharePoint, noti anche come nomi visualizzati. Posizionarsi su un elemento per visualizzare le proprietà seguenti nella descrizione comando:  
  
-   **Nome** Il nome univoco del campo.  
  
-   **Identificatore** L'identificatore univoco del campo.  
  
-   **Tipo campo** Il tipo di dati del campo.  
  
-   **Nascosto** Se il campo viene visualizzato nella visualizzazione elenco SharePoint.  
  
 La selezione di campi da più elenchi non è supportata. È possibile creare un set di dati per ogni elenco e selezionare campi da ogni set di dati. Se gli elenchi includono un campo comune, sarà possibile usare la funzione Lookup in un'area di dati tablix associata a un set di dati per recuperare un valore dall'altro set di dati non associato all'area di dati. Per altre informazioni, vedere [Funzione Lookup &#40;Generatore report e SSRS&#41;](../report-design/report-builder-functions-lookup-function.md).  
  
-   **Campi selezionati**  Vengono visualizzati i campi selezionati. I nomi di campi in questo riquadro sono i nomi descrittivi specificati da un utente di SharePoint. Quando si chiude Progettazione query, questi nomi vengono visualizzati nella raccolta campi del set di dati nel riquadro Dati report. La relazione tra nomi univoci e nomi descrittivi è disponibile nella pagina [Finestra di dialogo Proprietà set di dati, Campi &#40;Generatore report&#41;](../dataset-properties-dialog-box-fields-report-builder.md).  
  
-   **Filtri applicati**  Consente di limitare i dati restituiti dall'elenco SharePoint, prima di essere restituiti al report. Selezionare il nome campo, l'operatore e il valore da usare per limitare i dati recuperati nell'elenco. Gli operatori variano a seconda del tipo di dati del valore selezionato.  
  
     Non è possibile modificare il tipo di ordinamento o specificare gruppi nella finestra Progettazione query con interfaccia grafica. Per eseguire tale operazione, impostare le espressioni di ordinamento nel set di dati del report e le espressioni di raggruppamento nelle aree dati del report. I parametri di query non sono supportati. Per filtrare i dati nel report, usare i filtri del report o i parametri del report creati. Per altre informazioni, vedere [Filtrare, raggruppare e ordinare i dati &#40;Generatore report e SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md) e [Parametri report &#40;Generatore report e Progettazione report&#41;](../report-design/report-parameters-report-builder-and-report-designer.md).  
  
-   **Risultati query**  Vengono visualizzate le righe di esempio restituite quando viene eseguita la query. Se i valori dell'elenco SharePoint vengono frequentemente modificati sul sito di SharePoint, i valori visualizzati nel riquadro dei risultati della query potrebbero differire da quelli visualizzati nel report.  
  
-   **Campi selezionati**  Vengono visualizzati i campi selezionati. I nomi di campi in questo riquadro sono i nomi descrittivi specificati da un utente di SharePoint. Quando si chiude Progettazione query, questi nomi vengono visualizzati nella raccolta campi del set di dati nel riquadro Dati report. La relazione tra nomi univoci e nomi descrittivi è disponibile nella pagina [Finestra di dialogo Proprietà set di dati, Campi &#40;Generatore report&#41;](../dataset-properties-dialog-box-fields-report-builder.md).  
  
-   **Filtri applicati**  Consente di limitare i dati restituiti dall'elenco SharePoint, prima di essere restituiti al report. Selezionare il nome campo, l'operatore e il valore da usare per limitare i dati recuperati nell'elenco. Gli operatori variano a seconda del tipo di dati del valore selezionato.  
  
     Non è possibile modificare il tipo di ordinamento o specificare gruppi nella finestra Progettazione query con interfaccia grafica. Per eseguire tale operazione, impostare le espressioni di ordinamento nel set di dati del report e le espressioni di raggruppamento nelle aree dati del report. I parametri di query non sono supportati. Per filtrare i dati nel report, usare i filtri del report o i parametri del report creati. Per altre informazioni, vedere [Filtrare, raggruppare e ordinare i dati &#40;Generatore report e SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md) e [Parametri report &#40;Generatore report e Progettazione report&#41;](../report-design/report-parameters-report-builder-and-report-designer.md).  
  
-   **Risultati query**  Vengono visualizzate le righe di esempio restituite quando viene eseguita la query. Se i valori dell'elenco SharePoint vengono frequentemente modificati sul sito di SharePoint, i valori visualizzati nel riquadro dei risultati della query potrebbero differire da quelli visualizzati nel report.  
  
 Per altre informazioni, vedere [Progettazione query di elenco di SharePoint &#40;Generatore report&#41;](sharepoint-list-query-designer-report-builder.md).  
  
### <a name="query-text"></a>Testo della query  
 Per visualizzare la query generata dalla finestra Progettazione query con interfaccia grafica., passare a Progettazione query basata su testo. In questa visualizzazione è possibile vedere l'XML creato dalla finestra Progettazione query con interfaccia grafica. Nell'XML sono inclusi gli elementi per il nome dell'elenco, la raccolta campi e il filtro.  
  
#### <a name="example-1-specified-fields-for-a-list"></a>Esempio 1. Campi specificati per un elenco  
 Nell'esempio seguente viene mostrata una query di SharePoint valida:  
  
```  
<RSSharePointList>  
<listName>MyList</listName>  
<viewFields>  
  <FieldRef Name="Field1"/>  
  <FieldRef Name="Field4"/>  
</viewFields>  
<Query>  
  <Where>  
    <And>  
      <Gt>  
        <FieldRef Name="Field1"/>  
        <Value Type="Integer">1</Value>  
      </Gt>  
      <IsNotNull>  
        <FieldRef Name="Field2"/>  
        <Value Type="string"/>  
      </IsNotNull>   
    </And>  
  </Where>  
</Query>  
</RSSharePointList>  
```  
  
 È possibile modificare questa vista della query finché rimane il testo XML valido.  
  
#### <a name="example-2-all-fields-for-a-list"></a>Esempio 2. Tutti i campi per un elenco  
 È possibile specificare anche solo il nome di un elenco, e tutti i campi, inclusi i campi nascosti, restituiti. Nell'esempio seguente vengono recuperati tutti i campi da un elenco denominato Attività:  
  
```  
<RSSharePointList>  
<listName>Tasks</listName>  
</RSSharePointList>  
```  
  
 Tutti i campi per l'elenco Attività vengono restituiti nei risultati della query.  
  
##  <a name="Parameters"></a> Parametri  
 I parametri non sono supportati da questa estensione per i dati.  
  
  
##  <a name="HowTo"></a> Procedure  
 In questa sezione sono contenute istruzioni dettagliate per l'utilizzo di connessioni dati, origini dati e set di dati.  
  
 [Aggiungere e verificare una connessione dati o un'origine dati &#40;Report e SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [Creare un set di dati condiviso o un set di dati incorporato &#40;Generatore report e SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [Aggiungere un filtro a un set di dati &#40;Generatore report e SSRS&#41;](add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="Related"></a> Sezioni correlate  
 In queste sezioni della documentazione sono incluse informazioni concettuali approfondite sui dati dei report, nonché le informazioni necessarie sulle procedure per definire, personalizzare e usare parti di un report correlate ai dati.  
  
 [Aggiungere dati a un Report &#40;Report e SSRS&#41;](report-datasets-ssrs.md)  
 Viene fornita una panoramica sull'accesso ai dati del report.  
  
 [Connessioni dati, origini dati e stringhe di connessione in Generatore report](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
 Vengono fornite informazioni sulle connessioni dati e sulle origini dati.  
  
 [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Vengono fornite informazioni sui set di dati incorporati e condivisi.  
  
 [Raccolta di campi del set di dati &#40;Generatore report e SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)  
 Vengono fornite informazioni sulla raccolta di campi di set di dati generata dalla query.  
  
 [Origini dati supportate da Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) nella documentazione relativa a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] inclusa nella [documentazione online](https://go.microsoft.com/fwlink/?linkid=121312) di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
 Vengono fornite informazioni dettagliate sul supporto delle piattaforme e delle versioni per ogni estensione per i dati.  
  
  
## <a name="see-also"></a>Vedere anche  
 [Parametri report &#40;Generatore report e Progettazione report&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtro, raggruppamento e ordinamento di dati &#40;Generatore report e SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Espressioni &#40;Generatore report e SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
  
  
