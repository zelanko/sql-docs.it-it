---
title: Interfaccia utente della finestra Progettazione query del modello di report | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.dataview.smqlquerydesigner.f1
- "10015"
helpviewer_keywords:
- report models [Reporting Services], queries
- datasets [Reporting Services], creating
- query designers [Reporting Services]
ms.assetid: db86c208-ff1e-4297-aa0c-c250f053f83e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9b5b63ddc613135015027eb549212a8cafb35f7c
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59963167"
---
# <a name="report-model-query-designer-user-interface"></a>Interfaccia utente della finestra Progettazione query del modello di report
  In Progettazione report sono disponibili due finestre Progettazione query che consentono di specificare i dati di un'origine dati di tipo Modello Server report da utilizzare in un report. Utilizzare la finestra Progettazione query con interfaccia grafica per esaminare e scegliere le entità modello e i campi delle entità. Utilizzare la finestra Progettazione query basata su testo per utilizzare direttamente una specifica del linguaggio SMDL in formato XML.  
  
> [!IMPORTANT]  
>  Gli utenti accedono alle origini dati quando creano ed eseguono query. È necessario concedere autorizzazioni minime per le origini dati, ad esempio autorizzazioni di sola lettura.  
  
## <a name="graphical-query-designer"></a>Finestra Progettazione query con interfaccia grafica  
 In Progettazione report è disponibile una finestra Progettazione query con interfaccia grafica che consente di creare ed eseguire query SMDL per popolare la raccolta di campi per un set di dati del report durante l'elaborazione del report stesso. Questa finestra è suddivisa in tre aree o riquadri.  
  
 Nella figura seguente vengono etichettati tutti i riquadri.  
  
 ![Interfaccia utente della finestra Progettazione query del modello semantico](../media/rsqd-dsawmodel-smql.gif "Interfaccia utente della finestra Progettazione query del modello semantico")  
  
 Nella tabella seguente viene descritta la funzione di ogni riquadro.  
  
|Riquadro|Funzione|  
|----------|--------------|  
|Riquadro di esplorazione|Consente di visualizzare rappresentazioni grafiche delle entità e dei campi delle entità nel modello. Utilizzare questo riquadro per esaminare entità, entità relative correlate e campi.|  
|Area di progettazione|Consente di visualizzare un elenco dei campi dal modello. Utilizzare questo riquadro per definire il layout dei campi selezionati.|  
|Results pane|Consente di visualizzare i risultati della query. Per eseguire la query, fare clic con il pulsante destro del mouse su un riquadro qualsiasi e scegliere **Esegui** o fare clic sul pulsante **Esegui** (![Esecuzione della query](../../analysis-services/media/rsqdicon-run.gif "Esecuzione della query")) sulla barra degli strumenti.|  
  
 La modifica delle informazioni nel riquadro di esplorazione o nel riquadro Area di progettazione influenzerà il contenuto del riquadro Risultati quando viene selezionato **Esegui**.  
  
 Per eseguire azioni all'interno di un determinato riquadro, ad esempio per eliminare una colonna dall'area di progettazione, fare clic con il pulsante destro del mouse sulla colonna, quindi scegliere il comando desiderato dal menu.  
  
### <a name="graphical-query-designer-toolbar"></a>Barra degli strumenti della finestra Progettazione query con interfaccia grafica  
 Nel progettare la query, è anche possibile utilizzare i pulsanti della barra degli strumenti. Nella tabella seguente sono elencati i pulsanti sulla barra degli strumenti e le relative funzioni.  
  
|Button|Descrizione|  
|------------|-----------------|  
|**Modifica come testo**|Consente di passare dalla finestra Progettazione query basata su testo alla finestra Progettazione query con interfaccia grafica e viceversa. La query per un'origine dati di tipo Modello Server report è costituita da una specifica del linguaggio SMQL in formato XML.|  
|**Importa**|Consente di importare una query esistente da un file di definizione di report (con estensione rdl) nel file system. Per altre informazioni, vedere [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).|  
|![Azione Annulla](../media/rsqdicon-undo.gif "Azione Annulla")|Consente di annullare l'ultima azione.|  
|![Azione Ripristina](../media/rsqdicon-redo.gif "Azione Ripristina")|Consente di ripetere l'ultima azione.|  
|![Esecuzione della query](../../analysis-services/media/rsqdicon-run.gif "Esecuzione della query")|Consente di eseguire la query e di visualizzare le righe risultanti nel riquadro Risultati.|  
|![Icona del filtro accanto alla colonna di filtro selezionata](../media/rsqdicon-filter.gif "Icona del filtro accanto alla colonna di filtro selezionata")|Consente di aprire la finestra di dialogo **Filtra dati** , nella quale è possibile specificare i dati in base ai quali applicare il filtro. È possibile specificare i filtri indipendentemente dai dati attualmente presenti nell'area di progettazione.|  
  
## <a name="text-based-query-designer"></a>Finestra Progettazione query basata su testo  
 Quando si crea una query del set di dati di Modello Server report, per impostazione predefinita viene visualizzata la finestra Progettazione query con interfaccia grafica. Per passare alla finestra Progettazione query basata su testo, fare clic sul pulsante **Modifica come testo** sulla barra degli strumenti.  
  
 Nella finestra Progettazione query basata su testo sono inclusi due riquadri, ovvero un riquadro query SMQL e un riquadro Risultati. Questa visualizzazione di Progettazione query è utile essenzialmente quando si dispone già di una specifica di query SMQL da un'altra origine e si desidera incollarla nel riquadro query. Diversamente dalla finestra Progettazione query con interfaccia grafica, nella finestra Progettazione query basata su testo la sintassi della query non viene controllata né la query viene ristrutturata. Quando si fa clic su **Esegui** sulla barra degli strumenti, la query viene eseguita sull'origine dati e i risultati vengono visualizzati nel riquadro Risultati.  
  
 Nella figura seguente vengono etichettati tutti i riquadri.  
  
 ![Progettazione query SMQL standard](../media/rsqd-dsawmodel-smql-generic.gif "Progettazione query SMQL standard")  
  
 Nella tabella seguente viene descritta la funzione di ogni riquadro.  
  
|Riquadro|Funzione|  
|----------|--------------|  
|Riquadro query|Consente di visualizzare il testo della specifica SMQL.|  
|Riquadro Risultati|Consente di visualizzare i risultati della query. Per eseguire la query, fare clic con il pulsante destro del mouse su un riquadro qualsiasi e scegliere **Esegui**oppure fare clic sul pulsante **Esegui** sulla barra degli strumenti.|  
  
### <a name="text-based-query-designer-toolbar"></a>Barra degli strumenti di Progettazione query basata su testo  
 Nel progettare la query, è anche possibile utilizzare i pulsanti della barra degli strumenti. Nella tabella seguente sono elencati i pulsanti sulla barra degli strumenti e le relative funzioni.  
  
|Button|Descrizione|  
|------------|-----------------|  
|**Modifica come testo**|Consente di passare dalla finestra Progettazione query basata su testo alla finestra Progettazione query con interfaccia grafica e viceversa.|  
|**Importa**|Consente di importare una query da un report esistente.|  
|![Esecuzione della query](../../analysis-services/media/rsqdicon-run.gif "Esecuzione della query")|Consente di eseguire il testo della query e di visualizzare il set di righe risultanti nel riquadro Risultati.|  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire query di strumenti di progettazione di Report della finestra di progettazione di SQL Server Data Tools &#40;SSRS&#41;](query-design-tools-ssrs.md)   
 [Aggiungere dati da origini dati esterne &#40;SSRS&#41;](add-data-from-external-data-sources-ssrs.md)   
 [Connessione a un modello di report &#40;SSRS&#41;](report-model-connection-ssrs.md)   
 [File di configurazione RSReportDesigner](../report-server/rsreportdesigner-configuration-file.md)  
  
  
