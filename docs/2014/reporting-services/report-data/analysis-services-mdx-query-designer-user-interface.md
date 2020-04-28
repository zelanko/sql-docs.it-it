---
title: Interfaccia utente di Progettazione query MDX di Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10012"
- sql12.rtp.rptdesigner.dataview.asquerydesigner.f1
helpviewer_keywords:
- MDX [Reporting Services], creating datasets
- query designers [Reporting Services]
ms.assetid: d9c7c0b3-fce4-4a65-b679-408273e6a925
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a31c451b89ca226d207862c375943f6ffcfbb5e8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81388709"
---
# <a name="analysis-services-mdx-query-designer-user-interface"></a>Interfaccia utente di Progettazione query MDX di Analysis Services
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] sono disponibili finestre Progettazione query con interfaccia grafica per la compilazione di query MDX (Multidimensional Expression) e query DMX (Data Mining Expression) per un'origine dati di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . In questo argomento viene descritto Progettazione query MDX. Per altre informazioni sulla finestra Progettazione query DMX, vedere [Tipo di connessione di Analysis Services per DMX &#40;SSRS&#41;](analysis-services-connection-type-for-dmx-ssrs.md).

 Nella finestra Progettazione query con interfaccia grafica MDX sono disponibili due modalità: progettazione e query. In ogni modalità è disponibile un riquadro dei metadati dal quale è possibile trascinare membri dei cubi selezionati per compilare una query MDX che recupera dati quando il report viene elaborato.

> [!IMPORTANT]
>  Gli utenti accedono alle origini dati quando creano ed eseguono query. È necessario concedere autorizzazioni minime per le origini dati, ad esempio autorizzazioni di sola lettura.

## <a name="graphical-mdx-query-designer-in-design-mode"></a>Progettazione query MDX in modalità progettazione
 Quando si modifica una query MDX per un set di dati del report, la finestra Progettazione query MDX con interfaccia grafica verrà aperta in modalità progettazione.

 Nella figura seguente vengono etichettati i riquadri per la modalità progettazione.

 ![Progettazione query MDX di Analysis Services, visualizzazione progettazione](../../analysis-services/media/rsqd-dsawas-mdx-designmode.gif "Progettazione query MDX di Analysis Services, visualizzazione progettazione")

 Nella tabella seguente vengono elencati i riquadri disponibili in questa modalità:

|Riquadro|Funzione|
|----------|--------------|
|Pulsante Seleziona cubo (**...**)|Consente di visualizzare il cubo attualmente selezionato.|
|Riquadro dei metadati|Consente di visualizzare un elenco gerarchico di misure, indicatori di prestazioni chiave (KPI) e dimensioni definiti sul cubo selezionato.|
|Riquadro Membri calcolati|Consente di visualizzare i membri calcolati attualmente definiti disponibili per l'utilizzo nella query.|
|Riquadro Filtro|Consente di scegliere dimensioni e gerarchie correlate per filtrare i dati a livello di origine e limitare i dati restituiti al report.|
|Riquadro Dati|Consente di visualizzare le intestazioni di colonna per il set di risultati quando si trascinano gli elementi dal riquadro metadati e dal riquadro Membri calcolati. Consente di aggiornare automaticamente il set di risultati se viene selezionato il pulsante **Esecuzione automatica** . .|

 È possibile trascinare dimensioni, misure e indicatori di prestazioni chiave (KPI) dal riquadro metadati e membri calcolati dal riquadro Membro calcolato nel riquadro Dati. Nel riquadro Filtro è possibile selezionare dimensioni e gerarchie correlate e impostare espressioni di filtro per limitare i dati disponibili per la query. Se l'interruttore **Esecuzione automatica** (![Esecuzione automatica della query](../../analysis-services/media/rsqdicon-autoexecute.gif "Esecuzione automatica della query")) sulla barra degli strumenti è selezionato, Progettazione query esegue la query ogni volta che si rilascia un oggetto di metadati nel riquadro Dati. È possibile eseguire manualmente la query usando il pulsante **Esegui** (![Esecuzione della query](../../analysis-services/media/rsqdicon-run.gif "Eseguire la query")) sulla barra degli strumenti.

 Quando si crea una query MDX in questa modalità, le seguenti proprietà aggiuntive vengono incluse automaticamente nella query:

 **Proprietà membro** MEMBER_CAPTION, MEMBER_UNIQUE_NAME

 **Proprietà cella** VALUE, BACK_COLOR, FORE_COLOR, FORMATTED_VALUE, FORMAT_STRING, FONT_NAME, FONT_SIZE, FONT_FLAGS

 Per specificare le proprietà aggiuntive personalizzate, è necessario modificare manualmente la query MDX in modalità query.

### <a name="graphical-mdx-query-designer-toolbar-in-design-mode"></a>Barra degli strumenti di Progettazione query MDX in modalità progettazione
 I pulsanti della barra degli strumenti di Progettazione query consentono di progettare query MDX utilizzando l'interfaccia grafica. Nella tabella seguente vengono elencati i pulsanti con le relative funzioni.

|Button|Descrizione|
|------------|-----------------|
|**Modifica come testo**|Non abilitato per questo tipo di origine dati.|
|**Importa**|Consente di importare una query esistente da un file di definizione di report (con estensione rdl) nel file system. Per altre informazioni, vedere [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).|
|![Passaggio alla visualizzazione query MDX](../../analysis-services/media/rsqdicon-commandtypemdx.gif "Passaggio alla visualizzazione query MDX")|Consente di passare al tipo di comando MDX.|
|![Passaggio alla visualizzazione linguaggio di query DMX](../media/rsqdicon-commandtypedmx.gif "Passaggio alla visualizzazione linguaggio di query DMX")|Consente di passare al tipo di comando DMX.|
|![Aggiornamento dei dati dei risultati](../../analysis-services/media/rsqdicon-refresh.gif "Aggiornamento dei dati dei risultati")|Consente di aggiornare i metadati dall'origine dati.|
|![Aggiungi membro calcolato](../../analysis-services/media/rsqdicon-addcalculatedmember.gif "Aggiungi membro calcolato")|Consente di visualizzare la finestra di dialogo **Generatore membri calcolati** ,|
|![Mostrare/Nascondere le celle vuote](../../analysis-services/media/rsqdicon-showemptycells.gif "Mostrare/Nascondere le celle vuote")|Consente di visualizzare o nascondere le celle vuote nel riquadro Dati. Questa operazione equivale a utilizzare la clausola NON EMPTY in MDX.|
|![Esecuzione automatica della query](../../analysis-services/media/rsqdicon-autoexecute.gif "Esecuzione automatica della query")|Consente di eseguire automaticamente la query e di visualizzarne i risultati ogni volta che viene apportata una modifica. I risultati verranno visualizzati nel riquadro Dati.|
|![Pulsante Mostra aggregazioni](../../analysis-services/media/rsqdicon-showaggregations.gif "Pulsante Mostra aggregazioni")|Consente di visualizzare le aggregazioni nel riquadro Dati.|
|![Elimina](../../analysis-services/media/rsqdicon-delete.gif "Delete")|Consente di eliminare dalla query la colonna selezionata nel riquadro Dati.|
|![Icona della finestra di dialogo Parametri query](../../analysis-services/media/iconqueryparameter.gif "Icona della finestra di dialogo Parametri query")|Consente di visualizzare la finestra di dialogo **Parametri query** . Quando si specificano valori per un parametro di query, viene creato automaticamente un parametro di report con lo stesso nome. Il valore del parametro di query viene impostato su un'espressione che fa riferimento al parametro di report.|
|![Pulsante Prepara query](../../analysis-services/media/rsqdicon-preparequery.gif "Pulsante Prepara query")|Consente di preparare la query.|
|![Eseguire la query](../../analysis-services/media/rsqdicon-run.gif "Eseguire la query")|Consente di eseguire la query di e visualizzare i risultati nel riquadro Dati.|
|![Annullare la query](../../analysis-services/media/rsqdicon-cancel.gif "Annullare la query")|Consente di annullare la query.|
|![Passare alla modalità progettazione](../../analysis-services/media/rsqdicon-designmode.gif "Passare alla modalità progettazione")|Consente di passare dalla modalità progettazione alla modalità query e viceversa.|

## <a name="graphical-mdx-query-designer-in-query-mode"></a>Progettazione query MDX in modalità query
 Per modificare la finestra Progettazione query con interfaccia grafica attivando la modalità **Query** , fare clic sul pulsante **Modalità progettazione** sulla barra degli strumenti.

 Nella figura seguente vengono etichettati i riquadri per la modalità query.

 ![Progettazione query MDX di Analysis Services, visualizzazione query](../../analysis-services/media/rsqd-dsawas-mdx-querymode.gif "Progettazione query MDX di Analysis Services, visualizzazione query")

 Nella tabella seguente vengono elencati i riquadri disponibili in questa modalità:

|Riquadro|Funzione|
|----------|--------------|
|Pulsante Seleziona cubo (**...**)|Consente di visualizzare il cubo attualmente selezionato.|
|Riquadro Metadati/Funzioni/Modelli|Consente di visualizzare un elenco gerarchico di misure, indicatori di prestazioni chiave (KPI) e dimensioni definiti sul cubo selezionato.|
|Riquadro query|Consente di visualizzare il testo della query.|
|Riquadro Risultati|Consente di visualizzare i risultati dell'esecuzione della query.|

 Nel riquadro Metadati vengono visualizzate le schede **Metadati**, **Funzioni**e **Modelli**. Dalla scheda **Metadati** è possibile trascinare dimensioni, gerarchie, indicatori di prestazioni chiave (KPI) e misure nel riquadro Query MDX. Dalla scheda **Funzioni** è possibile trascinare funzioni nel riquadro Query MDX. Dalla scheda **Modelli** è possibile aggiungere modelli MDX al riquadro Query MDX. Quando si esegue la query, nel riquadro Risultati verranno visualizzati i risultati per la query MDX.

 È possibile estendere la query MDX predefinita generata in modalità progettazione per includere proprietà del membro e della cella aggiuntive. Quando si esegue la query, questi valori non vengono visualizzati nel set di risultati, ma vengono passati nuovamente a [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] ed è possibile usarli in un report. Per altre informazioni, vedere la sezione relativa alle proprietà di campo estese per un database di Analysis Services (SSRS).

### <a name="graphical-query-designer-toolbar-in-query-mode"></a>Barra degli strumenti della finestra Progettazione query con interfaccia grafica in modalità query
 I pulsanti della barra degli strumenti di Progettazione query consentono di progettare query MDX utilizzando l'interfaccia grafica.

 I pulsanti della barra degli strumenti sono identici in modalità progettazione e in modalità query, ma i pulsanti seguenti non sono abilitati in modalità query:

-   **Modifica come testo**

-   **Aggiungi membro calcolato** (![Aggiungi membro calcolato](../../analysis-services/media/rsqdicon-addcalculatedmember.gif "Aggiungi membro calcolato"))

-   **Mostrare/Nascondere le celle vuote** (![Mostrare/Nascondere le celle vuote](../../analysis-services/media/rsqdicon-showemptycells.gif "Mostrare/Nascondere le celle vuote"))

-   **Esecuzione automatica** (![Esecuzione automatica della query](../../analysis-services/media/rsqdicon-autoexecute.gif "Esecuzione automatica della query"))

-   **Mostra aggregazioni** (![Pulsante Mostra aggregazioni](../../analysis-services/media/rsqdicon-showaggregations.gif "Pulsante Mostra aggregazioni"))

## <a name="see-also"></a>Vedere anche
 [Definire i parametri in Progettazione query MDX per Analysis Services &#40;Generatore report e SSRS&#41;](define-parameters-in-the-mdx-query-designer-for-analysis-services.md) [creare un set di dati condiviso o un set di dati incorporato &#40;Generatore report e SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md) [Analysis Services tipo di connessione per DMX &#40;SSRS&#41;](analysis-services-connection-type-for-dmx-ssrs.md) [file di configurazione RSReportDesigner](../report-server/rsreportdesigner-configuration-file.md) [Analysis Services tipo di connessione per MDX &#40;SSRS](analysis-services-connection-type-for-mdx-ssrs.md)&#41;


