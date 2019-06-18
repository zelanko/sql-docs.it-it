---
title: Interfaccia utente di Progettazione query MDX di Analysis Services | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
f1_keywords:
- "10012"
- sql13.rtp.rptdesigner.dataview.asquerydesigner.f1
helpviewer_keywords:
- MDX [Reporting Services], creating datasets
- query designers [Reporting Services]
ms.assetid: d9c7c0b3-fce4-4a65-b679-408273e6a925
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 41d02ba0cd1dc9067bd6425895e53d9a949fd0d3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65573271"
---
# <a name="analysis-services-mdx-query-designer-user-interface"></a>Interfaccia utente di Progettazione query MDX di Analysis Services
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sono disponibili finestre Progettazione query con interfaccia grafica per la compilazione di query MDX (Multidimensional Expression) e query DMX (Data Mining Expression) per un'origine dati di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . In questo argomento viene descritto Progettazione query MDX. Per altre informazioni sulla finestra Progettazione query DMX, vedere [Tipo di connessione di Analysis Services per DMX &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-dmx-ssrs.md).  
  
 Nella finestra Progettazione query con interfaccia grafica MDX sono disponibili due modalità: progettazione e query. In ogni modalità è disponibile un riquadro dei metadati dal quale è possibile trascinare membri dei cubi selezionati per compilare una query MDX che recupera dati quando il report viene elaborato.  
  
> [!IMPORTANT]  
>  Gli utenti accedono alle origini dati quando creano ed eseguono query. È necessario concedere autorizzazioni minime per le origini dati, ad esempio autorizzazioni di sola lettura.  
  
> [!NOTE]  
>  L'importazione di una query con estensione mdx da un file non è supportata.  
  
## <a name="graphical-mdx-query-designer-in-design-mode"></a>Progettazione query MDX in modalità progettazione  
 Quando si modifica una query MDX per un set di dati del report, la finestra Progettazione query MDX con interfaccia grafica verrà aperta in modalità progettazione.  
  
 Nella figura seguente vengono etichettati i riquadri per la modalità progettazione.  
  
 ![Progettazione query MDX di Analysis Services in visualizzazione Progettazione](../../reporting-services/report-data/media/rsqd-dsawas-mdx-designmode.gif "Progettazione query MDX di Analysis Services in visualizzazione Progettazione")  
  
 Nella tabella seguente vengono elencati i riquadri disponibili in questa modalità:  
  
|Riquadro|Funzione|  
|----------|--------------|  
|Pulsante Seleziona cubo ( **...** )|Consente di visualizzare il cubo attualmente selezionato.|  
|Riquadro dei metadati|Consente di visualizzare un elenco gerarchico di misure, indicatori di prestazioni chiave (KPI) e dimensioni definiti sul cubo selezionato.|  
|Riquadro Membri calcolati|Consente di visualizzare i membri calcolati attualmente definiti disponibili per l'utilizzo nella query.|  
|Riquadro Filtro|Consente di scegliere dimensioni e gerarchie correlate per filtrare i dati a livello di origine e limitare i dati restituiti al report.|  
|Riquadro Dati|Consente di visualizzare le intestazioni di colonna per il set di risultati quando si trascinano gli elementi dal riquadro metadati e dal riquadro Membri calcolati. Consente di aggiornare automaticamente il set di risultati se viene selezionato il pulsante **Esecuzione automatica** . .|  
  
 È possibile trascinare dimensioni, misure e indicatori di prestazioni chiave (KPI) dal riquadro metadati e membri calcolati dal riquadro Membro calcolato nel riquadro Dati. Nel riquadro Filtro è possibile selezionare dimensioni e gerarchie correlate e impostare espressioni di filtro per limitare i dati disponibili per la query. Se l'interruttore **Esecuzione automatica** (![Esecuzione automatica della query](../../reporting-services/report-data/media/rsqdicon-autoexecute.gif "Esecuzione automatica della query")) sulla barra degli strumenti è selezionato, Progettazione query esegue la query ogni volta che si rilascia un oggetto di metadati nel riquadro Dati. È possibile eseguire manualmente la query usando il pulsante **Esegui** (![Esecuzione della query](../../reporting-services/report-data/media/rsqdicon-run.gif "Esecuzione della query")) sulla barra degli strumenti.  
  
 Quando si crea una query MDX in questa modalità, le seguenti proprietà aggiuntive vengono incluse automaticamente nella query:  
  
 **Proprietà membro** MEMBER_CAPTION, MEMBER_UNIQUE_NAME  
  
 **Proprietà cella** VALUE, BACK_COLOR, FORE_COLOR, FORMATTED_VALUE, FORMAT_STRING, FONT_NAME, FONT_SIZE, FONT_FLAGS  
  
 Per specificare le proprietà aggiuntive personalizzate, è necessario modificare manualmente la query MDX in modalità query.  
  
### <a name="graphical-mdx-query-designer-toolbar-in-design-mode"></a>Barra degli strumenti di Progettazione query MDX in modalità progettazione  
 I pulsanti della barra degli strumenti di Progettazione query consentono di progettare query MDX utilizzando l'interfaccia grafica. Nella tabella seguente vengono elencati i pulsanti con le relative funzioni.  
  
|Pulsante|Descrizione|  
|------------|-----------------|  
|**Modifica come testo**|Non abilitato per questo tipo di origine dati.|  
|**Importa**|Consente di importare una query esistente da un file di definizione di report (con estensione rdl) nel file system. Per altre informazioni, vedere [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).|  
|![Passa alla visualizzazione query MDX](../../reporting-services/report-data/media/rsqdicon-commandtypemdx.gif "Passa alla visualizzazione query MDX")|Consente di passare al tipo di comando MDX.|  
|![Passa alla visualizzazione linguaggio query DMX](../../reporting-services/report-data/media/rsqdicon-commandtypedmx.gif "Passa alla visualizzazione linguaggio query DMX")|Consente di passare al tipo di comando DMX.|  
|![Aggiorna i dati dei risultati](../../reporting-services/report-data/media/rsqdicon-refresh.gif "Aggiorna i dati dei risultati")|Consente di aggiornare i metadati dall'origine dati.|  
|![Add calculated member](../../reporting-services/report-data/media/rsqdicon-addcalculatedmember.gif "Add calculated member")|Consente di visualizzare la finestra di dialogo **Generatore membri calcolati** ,|  
|![Visualizza/nascondi celle vuote](../../reporting-services/report-data/media/rsqdicon-showemptycells.gif "Visualizza/nascondi celle vuote")|Consente di visualizzare o nascondere le celle vuote nel riquadro Dati. Questa operazione equivale a utilizzare la clausola NON EMPTY in MDX.|  
|![Esecuzione automatica della query](../../reporting-services/report-data/media/rsqdicon-autoexecute.gif "Esecuzione automatica della query")|Consente di eseguire automaticamente la query e di visualizzarne i risultati ogni volta che viene apportata una modifica. I risultati verranno visualizzati nel riquadro Dati.|  
|![Pulsante Mostra aggregazioni](../../reporting-services/report-data/media/rsqdicon-showaggregations.gif "Pulsante Mostra aggregazioni")|Consente di visualizzare le aggregazioni nel riquadro Dati.|  
|![Elimina](../../reporting-services/report-data/media/rsqdicon-delete.gif "Elimina")|Consente di eliminare dalla query la colonna selezionata nel riquadro Dati.|  
|![Icona della finestra di dialogo Parametri query](../../reporting-services/report-data/media/iconqueryparameter.gif "Icona della finestra di dialogo Parametri query")|Consente di visualizzare la finestra di dialogo **Parametri query** . Quando si specificano valori per un parametro di query, viene creato automaticamente un parametro di report con lo stesso nome. Il valore del parametro di query viene impostato su un'espressione che fa riferimento al parametro di report.|  
|![Pulsante Prepara query](../../reporting-services/report-data/media/rsqdicon-preparequery.gif "Pulsante Prepara query")|Consente di preparare la query.|  
|![Esecuzione della query](../../reporting-services/report-data/media/rsqdicon-run.gif "Esecuzione della query")|Consente di eseguire la query di e visualizzare i risultati nel riquadro Dati.|  
|![Annullamento della query](../../reporting-services/report-data/media/rsqdicon-cancel.gif "Annullamento della query")|Consente di annullare la query.|  
|![Passa alla modalità progettazione](../../reporting-services/media/rsqdicon-designmode.gif "Passa alla modalità progettazione")|Consente di passare dalla modalità progettazione alla modalità query e viceversa.|  
  
## <a name="graphical-mdx-query-designer-in-query-mode"></a>Progettazione query MDX in modalità query  
 Per modificare la finestra Progettazione query con interfaccia grafica attivando la modalità **Query** , fare clic sul pulsante **Modalità progettazione** sulla barra degli strumenti.  
  
 Nella figura seguente vengono etichettati i riquadri per la modalità query.  
  
 ![Progettazione query MDX di Analysis Services in visualizzazione Query](../../reporting-services/report-data/media/rsqd-dsawas-mdx-querymode.gif "Progettazione query MDX di Analysis Services in visualizzazione Query")  
  
 Nella tabella seguente vengono elencati i riquadri disponibili in questa modalità:  
  
|Riquadro|Funzione|  
|----------|--------------|  
|Pulsante Seleziona cubo ( **...** )|Consente di visualizzare il cubo attualmente selezionato.|  
|Riquadro Metadati/Funzioni/Modelli|Consente di visualizzare un elenco gerarchico di misure, indicatori di prestazioni chiave (KPI) e dimensioni definiti sul cubo selezionato.|  
|Riquadro query|Consente di visualizzare il testo della query.|  
|Riquadro Risultati|Consente di visualizzare i risultati dell'esecuzione della query.|  
  
 Nel riquadro Metadati vengono visualizzate le schede **Metadati**, **Funzioni**e **Modelli**. Dalla scheda **Metadati** è possibile trascinare dimensioni, gerarchie, indicatori di prestazioni chiave (KPI) e misure nel riquadro Query MDX. Dalla scheda **Funzioni** è possibile trascinare funzioni nel riquadro Query MDX. Dalla scheda **Modelli** è possibile aggiungere modelli MDX al riquadro Query MDX. Quando si esegue la query, nel riquadro Risultati verranno visualizzati i risultati per la query MDX.  
  
 È possibile estendere la query MDX predefinita generata in modalità progettazione per includere proprietà del membro e della cella aggiuntive. Quando si esegue la query, questi valori non vengono visualizzati nel set di risultati, ma vengono passati nuovamente a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ed è possibile usarli in un report. Per altre informazioni, vedere [Proprietà di campo estese per un database di Analysis Services &#40;SSRS&#41;](../../reporting-services/report-data/extended-field-properties-for-an-analysis-services-database-ssrs.md).  
  
### <a name="graphical-query-designer-toolbar-in-query-mode"></a>Barra degli strumenti della finestra Progettazione query con interfaccia grafica in modalità query  
 I pulsanti della barra degli strumenti di Progettazione query consentono di progettare query MDX utilizzando l'interfaccia grafica.  
  
 I pulsanti della barra degli strumenti sono identici in modalità progettazione e in modalità query, ma i pulsanti seguenti non sono abilitati in modalità query:  
  
-   **Modifica come testo**  
  
-   **Aggiungi membro calcolato** (![Add calculated member](../../reporting-services/report-data/media/rsqdicon-addcalculatedmember.gif "Add calculated member"))  
  
-   **Mostra celle vuote** (![Visualizza/nascondi celle vuote](../../reporting-services/report-data/media/rsqdicon-showemptycells.gif "Visualizza/nascondi celle vuote"))  
  
-   **Esecuzione automatica** (![Esecuzione automatica della query](../../reporting-services/report-data/media/rsqdicon-autoexecute.gif "Esecuzione automatica della query"))  
  
-   **Mostra aggregazioni** (![Pulsante Mostra aggregazioni](../../reporting-services/report-data/media/rsqdicon-showaggregations.gif "Pulsante Mostra aggregazioni"))  
  
## <a name="see-also"></a>Vedere anche  
 [Definizione dei parametri in Progettazione query MDX per Analysis Services &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/define-parameters-in-the-mdx-query-designer-for-analysis-services.md)   
 [Creare un set di dati condiviso o un set di dati incorporato &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)   
 [Tipo di connessione di Analysis Services per DMX &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-dmx-ssrs.md)   
 [RSReportDesigner - file di configurazione](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)   
 [Tipo di connessione di Analysis Services per MDX &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md)  
  
  
