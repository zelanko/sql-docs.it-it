---
title: Tipo di connessione Analysis Services per MDX (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: bd2e7148-3124-4e07-9734-22333127c3be
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: dbd62eff94b1a885198c62a9a36cb8eef7ba57c7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68892118"
---
# <a name="analysis-services-connection-type-for-mdx-ssrs"></a>Tipo di connessione Analysis Services per MDX (SSRS)
  Per includere dati da un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cubo nel report, è necessario disporre di un set di dati basato su un'origine dati del report di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]tipo. Questo tipo di origine dati predefinito è basato sull'estensione per [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] i dati. È possibile recuperare i metadati relativi a dimensioni, gerarchie, livelli, indicatori di prestazioni chiave (KPI), misure e attributi [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] da un cubo per utilizzarli come dati del report.  
  
 Questa estensione per l'elaborazione dati supporta parametri multivalore, aggregazioni server e credenziali gestiti separatamente dalla stringa di connessione.  
  
 Usare le informazioni presenti in questo argomento per compilare un'origine dati. Per istruzioni dettagliate, vedere [aggiungere e verificare una connessione dati o un'origine dati &#40;Generatore report e SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a>Stringa di connessione  
 Quando ci si connette a un cubo di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , si esegue la connessione all'oggetto di database in un'istanza di Analysis Services in un server. Il database potrebbe disporre di più cubi. Il cubo viene specificato nella finestra Progettazione query quando si compila la query. L'esempio seguente mostra una stringa di connessione:  
  
```  
data source=<server name>;initial catalog=<database name>  
```  
  
 Per altri esempi di stringhe di connessione, vedere [Connessioni dati, origini dati e stringhe di connessione in Generatore report](../data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
  
  
##  <a name="Credentials"></a>Credenziali  
 Le credenziali sono necessarie per eseguire query, nonché per visualizzare l'anteprima del report in locale e dal server di report.  
  
 Dopo aver pubblicato il report, potrebbe essere necessario modificare le credenziali per l'origine dati affinché quando il report viene eseguito nel server di report, le autorizzazioni per il recupero dei dati risultino valide.  
  
 Da un client di creazione di report sono disponibili le opzioni seguenti per la specifica delle credenziali:  
  
-   Utente di Windows corrente (nota anche come sicurezza integrata).  
  
-   Utilizzare un nome utente e una password archiviati.  
  
-   Richiedere all'utente le credenziali. Questa opzione supporta solo la sicurezza integrata di Windows.  
  
-   Non sono necessarie credenziali. Per utilizzare questa opzione, è necessario aver configurato l'account di esecuzione automatica sul server di report. Per altre informazioni, vedere [Configurare l'account di esecuzione automatica &#40;Gestione configurazione SSRS&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md) nella [documentazione relativa a Reporting Services](https://go.microsoft.com/fwlink/?linkid=121312) nel sito msdn.microsoft.com.  
  
 Per ulteriori informazioni, vedere [connessioni dati, origini dati e stringhe di connessione in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) o [specificare le credenziali in Generatore report](../specify-credentials-in-report-builder.md).  
  
  
  
##  <a name="Query"></a>Query  
 Una volta creata una connessione dati a un'origine dati di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , si crea un set di dati e si definisce una query MDX (Multidimensional Expression) che consente di specificare quali dati recuperare dal cubo. Utilizzare la finestra Progettazione query con interfaccia grafica MDX per visualizzare e selezionare le strutture di dati sottostanti nell'origine dati.  
  
 È possibile specificare una query nei modi seguenti:  
  
-   Compilare una query in modo interattivo. La finestra Progettazione query MDX per Analysis Services supporta le visualizzazioni seguenti:  
  
    -   **Visualizzazione progettazione** Trascinare dimensioni, membri, proprietà dei membri, misure e indicatori KPI dal browser metadati al riquadro **dati** per compilare una query MDX. Trascinare i membri calcolati dal riquadro Membri calcolati al riquadro Dati per definire altri campi del set di dati.  
  
    -   **Visualizzazione query** Trascinare dimensioni, membri, proprietà dei membri, misure e indicatori KPI dal Visualizzatore metadati al riquadro query per compilare una query MDX. È possibile modificare il testo MDX direttamente nel riquadro Query. Trascinare i membri calcolati dal riquadro Membri calcolati al riquadro Query per definire altri campi del set di dati.  
  
     Per altre informazioni, vedere [Interfaccia utente di Progettazione query MDX di Analysis Services &#40;Generatore report &#41;](../analysis-services-mdx-query-designer-user-interface-report-builder.md).  
  
-   Importare una query MDX esistente da un report. Usare il pulsante di query **Importa** per cercare un file con estensione rdl e importare una query. È possibile importare una query da un report che contiene un set di dati incorporato basato sull'origine dati [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . L'importazione di una query MDX direttamente da un file con estensione mdx non è supportata.  
  
 In fase di progettazione eseguire la query per visualizzare un set di risultati. I risultati della query vengono recuperati automaticamente come un set di righe bidimensionale. Le colonne nel set di risultati per una query popolano la raccolta dei campi per un set di dati. Dopo aver compilato la query, visualizzare la raccolta dei campi del set di dati generata dai metadati nel riquadro dei dati del report. Quando viene eseguito il report, vengono restituiti i dati effettivi dall'origine dati esterna.  
  
 L'estensione per l'elaborazione dati di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] supporta proprietà estese dei campi del set di dati. Si tratta di valori che sono disponibili nell'origine dati esterna e non nel riquadro dei dati del report. È possibile utilizzare le proprietà di campo estese supportate dall'estensione per l'elaborazione dati di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] nel report tramite la raccolta predefinita `Fields`. Per le proprietà che dispongono di valori nell'origine dati, è possibile accedere ai valori predefiniti, ad esempio `FormattedValue`, `Color` o `UniqueName`. Per ulteriori informazioni, vedere [proprietà di campo estese per un Database Analysis Services &#40;SSRS&#41;](extended-field-properties-for-an-analysis-services-database-ssrs.md)).  
  
  
  
##  <a name="Parameters"></a> Parametri  
 Per includere parametri di query, creare un filtro nell'area del filtro in Progettazione query e contrassegnarlo come parametro. Viene creato automaticamente un set di dati per fornire i valori disponibili di ogni filtro. Per impostazione predefinita, tali set di dati non vengono visualizzati nel riquadro dei dati del report. Per altre informazioni, vedere [Definire parametri in Progettazione query MDX per Analysis Services &#40;Generatore report e SSRS&#41;](define-parameters-in-the-mdx-query-designer-for-analysis-services.md) e [Visualizzare set di dati nascosti per i valori dei parametri di dati multidimensionali &#40;Generatore report e SSRS&#41;](show-hidden-datasets-for-parameter-values-multidimensional-data.md).  
  
 Per impostazione predefinita, i dati di ogni parametro di report sono di tipo **Text**. Dopo aver creato i parametri di report, potrebbe essere necessario modificare i valori predefiniti. Per ulteriori informazioni, vedere la pagina relativa al [Parametri report &#40;Generatore report e Progettazione report&#41;](../report-design/report-parameters-report-builder-and-report-designer.md).  
  
  
  
##  Osservazioni su <a name="Remarks"></a>  
 L'estensione per i dati di Analysis Services è basata sul protocollo XMLA (XML for Analysis). I set di risultati provenienti dai cubi vengono recuperati tramite il protocollo XMLA come un set di righe bidimensionale. Le gerarchie incomplete non sono supportate. Per altre informazioni, vedere [Gerarchie incomplete](https://docs.microsoft.com/analysis-services/multidimensional-models/user-defined-hierarchies-ragged-hierarchies).  
  
 È possibile recuperare dati anche da un cubo di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dal tipo di origine dati OLE DB. Per altre informazioni, vedere [Tipo di connessione OLE DB &#40;SSRS&#41;](ole-db-connection-type-ssrs.md).  
  
 Per altre informazioni sul supporto della versione, vedere [Origini dei dati supportate da Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) nella documentazione relativa a [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] inclusa nella documentazione online[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [ di ](https://go.microsoft.com/fwlink/?linkid=121312).  
  
  
  
##  <a name="Related"></a>Sezioni correlate  
 In queste sezioni della documentazione sono incluse informazioni concettuali approfondite sui dati dei report, nonché le informazioni necessarie sulle procedure per definire, personalizzare e usare parti di un report correlate ai dati.  
  
 [Aggiungere dati a un report &#40;Generatore report e SSRS&#41;](report-datasets-ssrs.md)  
 Viene fornita una panoramica sull'accesso ai dati del report.  
  
 [Connessioni dati, origini dati e stringhe di connessione in Generatore report](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
 Vengono fornite informazioni sulle connessioni dati e sulle origini dati.  
  
 [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Vengono fornite informazioni sui set di dati incorporati e condivisi.  
  
 [Raccolta di campi del set di dati &#40;Generatore report e SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)  
 Vengono fornite informazioni sulla raccolta di campi di set di dati generata dalla query.  
  
 [Proprietà di campo estese per un database Analysis Services &#40;SSRS&#41;](extended-field-properties-for-an-analysis-services-database-ssrs.md)  
 Vengono fornite informazioni su campi aggiuntivi che sono disponibili tramite il provider di dati XMLA.  
  
 Le [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] [origini dati supportate da Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) nella documentazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nella documentazione [online](https://go.microsoft.com/fwlink/?linkid=121312)di.  
 Vengono fornite informazioni dettagliate sul supporto delle piattaforme e delle versioni per ogni estensione per i dati.  
  
  
  
## <a name="see-also"></a>Vedere anche  
 [Parametri report &#40;Generatore report e Progettazione report&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtro, raggruppamento e ordinamento di dati &#40;Generatore report e SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Espressioni &#40;Generatore report e SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
  
  
