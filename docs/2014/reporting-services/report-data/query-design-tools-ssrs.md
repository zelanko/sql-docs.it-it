---
title: Strumenti di progettazione di query in Progettazione report SQL Server Data Tools (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- graphical query designer [Reporting Services]
- MDX query designer [Reporting Services]
- text-based query designer [Reporting Services]
- DMX [Reporting Services]
- query designers [Reporting Services]
- generic query designer See text-based query designer
- Reporting Services, query designers
- semantic queries [Reporting Services]
- Report Model Query Designer
ms.assetid: a8139a9d-4aeb-4e64-96f3-564edf60479f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1179f4e5a6c8be90b5bc52b814ae49c96a3a39aa
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81388627"
---
# <a name="query-design-tools-in-report-designer-sql-server-data-tools-ssrs"></a>Strumenti per la progettazione di query in Progettazione report in SQL Server Data Tools (SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] include svariati strumenti per la progettazione di query che è possibile usare per creare query sui set di dati in Progettazione report. La disponibilità di un particolare strumento di progettazione query dipende dal tipo di origine dei dati utilizzato. Inoltre, in alcuni strumenti di progettazione query sono disponibili modalità alternative, così che sia possibile scegliere se lavorare in modalità visiva o direttamente nel linguaggio query. In questo argomento si illustrano tutti gli strumenti disponibili e si descrivono i tipi di origine dei dati supportati da ognuno di essi. Vengono quindi descritti gli strumenti seguenti:

-   [Finestra Progettazione query basata su testo](#Textbased)

-   [Finestra Progettazione query con interfaccia grafica](#Graphical)

-   [Progettazione query modelli di report](#Model)

-   [Progettazione query MDX](#MDX)

-   [Progettazione query DMX](#DMX)

-   [Progettazione query SapNetWeaver BI](#SAPBW)

-   [Progettazione query Hyperion Essbase [Reporting Services]](#Hyperion)

 Quando si usa un modello di progetto Server report o una procedura guidata Server report, tutti gli strumenti di progettazione query vengono eseguiti nell'ambiente di progettazione dati di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] . Per altre informazioni sugli strumenti di progettazione query, vedere [Strumenti di progettazione query in Reporting Services](../reporting-services-query-designers.md).

##  <a name="text-based-query-designer"></a><a name="Textbased"></a>Progettazione query basata su testo
 La finestra Progettazione query basata su testo è lo strumento di compilazione di query predefinito per la maggior parte delle origini [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]dati relazionali supportate, tra cui Oracle, Teradata, OLE DB, XML e ODBC. A differenza della finestra Progettazione query con interfaccia grafica, questo strumento non consente di convalidare la sintassi delle query durante la fase di progettazione. Nella figura seguente viene illustrato lo strumento Progettazione query basata su testo.

 ![Finestra Progettazione query standard per query di dati relazionali](../../analysis-services/media/rsqd-dsaw-sql-generic.gif "Finestra Progettazione query standard per query di dati relazionali")

 È consigliabile utilizzare la finestra Progettazione query basata su testo per creare query complesse, impiegare stored procedure, eseguire query sui dati XML e scrivere query dinamiche. A seconda dell'origine dei dati, è possibile attivare/disattivare il pulsante **Modifica come testo** sulla barra degli strumenti per passare dalla finestra Progettazione query con interfaccia grafica alla finestra Progettazione query basata su testo e viceversa. Per altre informazioni, vedere [Interfaccia utente di Progettazione query basata su testo](../text-based-query-designer-user-interface.md).

##  <a name="graphical-query-designer"></a><a name="Graphical"></a>Finestra Progettazione query con interfaccia grafica
 La finestra Progettazione query con interfaccia grafica viene usata per creare o modificare query [!INCLUDE[tsql](../../includes/tsql-md.md)] eseguite su un database relazionale. Questo strumento di progettazione delle query viene utilizzato in diversi prodotti di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] e in altri componenti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . A seconda del tipo di origine dei dati, esso supporta le modalità Text, StoredProcedure e TableDirect. Nella figura seguente viene illustrata la finestra Progettazione query con interfaccia grafica.

 ![Finestra Progettazione query con interfaccia grafica per query SQL](../media/rsqd-dsaw-sql.gif "Finestra Progettazione query con interfaccia grafica per query SQL")

 È possibile fare clic sul pulsante **Modifica come testo** sulla barra degli strumenti per passare dalla finestra Progettazione query con interfaccia grafica alla finestra Progettazione query basata su testo e viceversa. Per altre informazioni, vedere [Interfaccia utente della finestra Progettazione query con interfaccia grafica](graphical-query-designer-user-interface.md).

##  <a name="report-model-query-designer"></a><a name="Model"></a>Progettazione query modelli di report
 Lo strumento Progettazione query modelli di report viene utilizzato per creare o modificare query eseguite su un modello di report SMDL pubblicato in un server di report. I report eseguiti sulla base di modelli supportano l'esplorazione dei dati click-through. La query determina il percorso di questa esplorazione in fase di esecuzione. Nella figura seguente viene illustrato lo strumento Progettazione query modelli di report.

 ![Interfaccia di progettazione query modelli semantici](../media/rsqd-dsawmodel-smql.gif "Interfaccia di progettazione query modelli semantici")

 Per utilizzare Progettazione query modelli di report, è necessario definire un'origine dei dati che punti a un modello pubblicato. Quando si definisce un set di dati per l'origine dei dati, è possibile aprire la query del set di dati nella finestra Progettazione query modelli di report. La finestra Progettazione query modelli di report può essere utilizzata in modalità grafica o basata su testo. È possibile fare clic sul pulsante **Modifica come testo** sulla barra degli strumenti per passare dalla finestra Progettazione query con interfaccia grafica alla finestra Progettazione query basata su testo e viceversa. Per altre informazioni, vedere [Interfaccia utente della finestra Progettazione query del modello di report](report-model-query-designer-user-interface.md).

##  <a name="mdx-query-designer"></a><a name="MDX"></a>Progettazione query MDX
 La finestra Progettazione query MDX (Multidimensional Expression) consente di creare o modificare query eseguite su un'origine dati di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] con cubi multidimensionali. Nella figura seguente viene illustrato lo strumento Progettazione query MDX dopo che la query e il filtro sono stati definiti.

 ![Progettazione query MDX di Analysis Services, visualizzazione progettazione](../../analysis-services/media/rsqd-dsawas-mdx-designmode.gif "Progettazione query MDX di Analysis Services, visualizzazione progettazione")

 Per utilizzare questa finestra, è necessario definire un'origine dei dati che contenga un cubo di Analysis Services valido ed elaborato. Quando si definisce un set di dati per l'origine dei dati, è possibile aprire la query nella finestra Progettazione query MDX. Se necessario, utilizzare i pulsanti MDX e DMX sulla barra degli strumenti per passare dalla modalità MDX a DMX e viceversa. Per altre informazioni, vedere [Interfaccia utente di Progettazione query MDX di Analysis Services](analysis-services-mdx-query-designer-user-interface.md).

##  <a name="dmx-query-designer"></a><a name="DMX"></a>Progettazione query DMX
 La finestra Progettazione query DMX (Data Mining Prediction Expression) consente di creare o modificare query in esecuzione su un'origine dati di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] con modelli di data mining. Nella figura seguente viene illustrato lo strumento Progettazione query DMX dopo che il modello e le tabelle di input sono state selezionate.

 ![Progettazione query DMX di Analysis Services, visualizzazione progettazione](../media/rsqd-dsawas-dmx-designmode.gif "Progettazione query DMX di Analysis Services, visualizzazione progettazione")

 Per utilizzare la Progettazione query DMX, è necessario definire un'origine dei dati che includa un modello di data mining valido e disponibile. Quando si definisce un set di dati per l'origine dei dati, è possibile aprire la query nella finestra Progettazione query DMX. Se necessario, utilizzare i pulsanti MDX e DMX sulla barra degli strumenti per passare dalla modalità MDX a DMX e viceversa. Dopo aver selezionato il modello, è possibile creare query di stima di data mining che forniscano dati a un report. Per altre informazioni, vedere [Interfaccia utente di Progettazione query DMX di Analysis Services](analysis-services-dmx-query-designer-user-interface.md).

##  <a name="sap-netweaver-bi-query-designer"></a><a name="SAPBW"></a>Progettazione query SAP NetWeaver BI
 La finestra Progettazione query [!INCLUDE[SAP_DPE_BW_1](../../../includes/sap-dpe-bw-1-md.md)] consente di recuperare dati da un database di [!INCLUDE[SAP_DPE_BW_1](../../../includes/sap-dpe-bw-1-md.md)] . Per usarla, è necessario disporre di un'origine dei dati di [!INCLUDE[SAP_DPE_BW_1](../../../includes/sap-dpe-bw-1-md.md)] che includa almeno una query InfoCube, MultiProvider o Web definita. Nella figura seguente viene illustrato lo strumento Progettazione query [!INCLUDE[SAP_DPE_BW_1](../../../includes/sap-dpe-bw-1-md.md)] .

 ![Progettazione query mediante MDX in modalità progettazione](../media/rsqd-dssapbw-mdx-designmode.gif "Progettazione query mediante MDX in modalità progettazione")

##  <a name="hyperion-essbase-query-designer"></a><a name="Hyperion"></a>Progettazione query Hyperion Essbase
 Progettazione query [!INCLUDE[extEssbase](../../../includes/extessbase-md.md)] consente di recuperare dati da un database e applicazioni di [!INCLUDE[extEssbase](../../../includes/extessbase-md.md)] . Nella figura seguente viene illustrato lo strumento Progettazione query [!INCLUDE[extEssbase](../../../includes/extessbase-md.md)] .

 ![Progettazione query per origini dati Hyperion Essbase](../media/rsqd-dshyperionessbase-mdx-designmode.gif "Progettazione query per origini dati Hyperion Essbase")

 Per utilizzarla, è necessario disporre di un'origine dei dati di [!INCLUDE[extEssbase](../../../includes/extessbase-md.md)] che disponga di almeno un database. Per altre informazioni, vedere [Interfaccia utente di Progettazione query SAP NetWeaver BI](sap-netweaver-bi-query-designer-user-interface.md).

## <a name="see-also"></a>Vedere anche
 [Gli strumenti di Reporting Services](../tools/reporting-services-tools.md) [aggiungono dati a un report &#40;Generatore report e SSRS&#41;](report-datasets-ssrs.md) [connessioni dati, origini dati e stringhe di connessione in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) [esercitazioni](../reporting-services-tutorials-ssrs.md) Reporting Services &#40;SSRS&#41;[origini dati supportate da Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) [creare un'origine dati incorporata o condivisa &#40;SSRS](../create-an-embedded-or-shared-data-source-ssrs.md)&#41;


