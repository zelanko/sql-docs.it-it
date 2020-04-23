---
title: Tipo di connessione di Analysis Services per DMX (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- parameters [Reporting Services], DMX
- Data Mining Prediction [Reporting Services]
- query view [Reporting Services]
- DMX [Reporting Services]
- design view [Reporting Services]
- data mining [Reporting Services]
- passing parameters [Reporting Services]
ms.assetid: 2de825e9-6d8a-4128-add0-da15dc6cea3e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2c6d2c689689cde5c6c5ef4ffa8ab5c0e8737078
ms.sourcegitcommit: c37777216fb8b464e33cd6e2ffbedb6860971b0d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2020
ms.locfileid: "82086966"
---
# <a name="analysis-services-connection-type-for-dmx-ssrs"></a>Tipo di connessione di Analysis Services per DMX (SSRS)
  Quando si crea un set di dati da un'origine dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], Progettazione report visualizza la finestra di progettazione query MDX (Multidimensional Expression) se rileva un cubo valido. Se non viene rilevato alcun cubo, ma è disponibile un modello di data mining, in Progettazione report viene visualizzata la finestra Progettazione query DMX (Data Mining Extensions). Per visualizzare alternativamente le finestre di progettazione MDX e DMX, fare clic sul pulsante **Tipo di comando DMX** (![Passa alla visualizzazione linguaggio query DMX](../media/rsqdicon-commandtypedmx.gif "Passaggio alla visualizzazione linguaggio di query DMX")) sulla barra degli strumenti. La finestra di progettazione query DMX consente di compilare in modo interattivo una query DMX tramite elementi grafici. Per utilizzare Progettazione query DMX, l'origine dei dati specificata deve avere già un modello di data mining che fornisce i dati. I risultati della query vengono convertiti in un set di righe bidimensionale da utilizzare nel report.  
  
> [!NOTE]  
>  Prima di progettare il report, è necessario eseguire il training del modello. Per altre informazioni, vedere [Soluzioni di data mining](https://docs.microsoft.com/analysis-services/data-mining/data-mining-solutions).  
  
## <a name="design-mode"></a>Modalità progettazione  
 Progettazione query DMX viene aperto in modalità progettazione. Tale modalità include un'area di progettazione grafica utilizzata per la selezione di un singolo modello di data mining e di una tabella di input e una griglia utilizzata per specificare la query di stima. Sono disponibili altre due modalità di Progettazione query, ovvero query e risultati. In modalità query, la griglia della modalità progettazione è sostituita da un riquadro Query che è possibile utilizzare per digitare query DMX. In modalità risultati il set di risultati restituito dalla query viene visualizzato in una griglia di dati.  
  
 Per modificare le modalità di Progettazione query DMX, fare clic con il pulsante destro del mouse nell'area di progettazione della query e scegliere **Progettazione**, **Query**o **Risultato**. Per altre informazioni, vedere [Interfaccia utente di Progettazione query DMX in Analysis Services](analysis-services-dmx-query-designer-user-interface.md) e [Recuperare i dati da un modello di data mining &#40;DMX&#41; &#40;SSRS&#41;](retrieve-data-from-a-data-mining-model-dmx-ssrs.md).  
  
## <a name="designing-a-prediction-query"></a>Progettazione di una query di stima  
 Il riquadro Progettazione query in modalità progettazione contiene due finestre, ovvero **Modello di data mining** e **Seleziona tabella di input**. Usare la finestra **Modello di data mining** per selezionare il modello di data mining da usare nella query. Usare la finestra **Seleziona tabella/e di input** per selezionare la tabella sulla quale basare le stime. Se si vuole usare una query singleton anziché una tabella di input, fare clic con il pulsante destro del mouse nel riquadro di progettazione query e scegliere **Query singleton**. La finestra **Seleziona tabella/e di input** è sostituita da una finestra **Input query singleton** .  
  
 In modalità progettazione trascinare i campi dalle finestre **Modello di data mining** e **Seleziona tabella/e di input** nella colonna **Campo** del riquadro griglia. È inoltre possibile compilare le colonne restanti per specificare un alias, mostrare il campo nei risultati, raggruppare campi e specificare un operatore per limitare il valore del campo a uno specifico criterio o argomento. In modalità query trascinare i campi nel riquadro Query per compilare la query DMX.  
  
## <a name="using-parameters"></a>Utilizzo di parametri  
 È possibile passare parametri di report a un parametro di query DMX. A tale scopo, è necessario aggiungere un parametro alla query DMX, definire i parametri di query nella finestra di dialogo **Parametri query** e quindi modificare i parametri di report associati. Per definire un parametro di query, fare clic su **Parametri query** (![icona della finestra di dialogo Parametri query](../media/iconqueryparameter.gif "Icona della finestra di dialogo Parametri query")) nella barra degli strumenti. Per istruzioni sulla definizione dei parametri in una query DMX, vedere [Definizione dei parametri in Progettazione query MDX per Analysis Services &#40;Generatore report e SSRS&#41;](define-parameters-in-the-mdx-query-designer-for-analysis-services.md).  
  
 Per altre informazioni sulla gestione della relazione tra i parametri di query e i parametri di report, vedere [Associazione di un parametro di query a un parametro di report &#40;Generatore report e SSRS&#41;](associate-a-query-parameter-with-a-report-parameter-report-builder-and-ssrs.md). Per altre informazioni sui parametri, vedere [Parametri report &#40;Generatore report e Progettazione report&#41;](../report-design/report-parameters-report-builder-and-report-designer.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Soluzioni di data mining](https://docs.microsoft.com/analysis-services/data-mining/data-mining-solutions)   
 [Strumenti di progettazione di query in Progettazione reportSQL Server Data Tools &#40;SSRS&#41;](query-design-tools-ssrs.md)   
 [Connessioni dati, origini dati e stringhe di connessione in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)  
  
  
