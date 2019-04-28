---
title: Forme di Data Mining per Visio | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining shapes
- templates [Visio]
- Visio shapes
- shapes, data mining
ms.assetid: 11a821d9-1c0a-442e-b735-92208ce479dc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 92630f90d7b18ad668dcffc02feeb65990cf3c84
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62690007"
---
# <a name="data-mining-shapes-for-visio"></a>Forme di data mining per Visio
  Le forme di data mining per Visio forniscono il modelli personalizzati per la visualizzazione dei modelli di data mining. Tramite questi modelli, è possibile connettersi a un modello creato in precedenza e creare presentazioni interattive per illustrare i risultati del processo di data mining.  
  
 I modelli offrono numerosi vantaggi rispetto ai grafici statici e le acquisizioni di schermata - interagiscono con i modelli di data mining dei dati sottostante, che vengono archiviati in un'istanza di Analysis Services, e consentono di personalizzare il modo in cui gli schemi nel modello di data mining vengono visualizzati. È possibile comprimere ed espandere un modello di albero, applicare filtri ai nodi dati o in base agli attributi e visualizzare le statistiche del modello come probabilità e coefficienti.  
  
 ![DM](media/dm-stencil.gif "DM")  
  
 Nei modelli di Visio sono incluse le procedure guidate seguenti:  
  
-   **Diagramma della rete di dipendenze:** Utilizzare questa procedura guidata per creare grafici per le reti neurali e alberi delle decisioni.  
  
-   **Diagramma di albero delle decisioni:** Utilizzare questa procedura guidata per creare i diagrammi che mostrano i punti decisionali e le formule associate ai modelli di albero delle decisioni. Questo diagramma può inoltre essere utilizzato con i modelli di regressione.  
  
-   **Diagramma dei cluster:** Utilizzare questa procedura guidata per creare grafici colorati per i modelli di segmentazione. È possibile spostarsi tra varie viste, ad esempio discriminante attributi, profili dei cluster e dipendenze, e personalizzare l'aspetto dei cluster.  
  
## <a name="installation"></a>Installazione  
 Quando si installa i modelli di Data Mining per Visio, per impostazione predefinita i file seguenti vengono installati in \<unità > \Programmi\Microsoft SQL Server 2012 DM Add-Ins (o \<unità > \ o file di programma (x86) \Microsoft SQL Server 2012 DM Add-Ins):  
  
-   **Microsoft Data VST** questo modello contiene preimpostato di formattazione, layout e le procedure guidate che consentono di lavorare con le forme di data mining.  
  
-   **Microsoft Data Mining Shape Studio.vss** questo file di stencil sono contenute le forme associate al modello.  
  
## <a name="how-to-use-the-templates"></a>Come usare i modelli  
 Per aprire i modelli, è possibile fare doppio clic sul file di forma o è possibile aprire Visio e quindi aprire il modello di forma.  
  
1.  Rilasciare una delle forme di data mining di Visio dallo stencil in una nuova pagina.  
  
2.  All'avvio della procedura guidata connettersi al server che contiene il modello di data mining che si desidera visualizzare.  
  
3.  Selezionare il modello di data mining facendo corrispondere il tipo di modello al tipo di visualizzazione.  
  
4.  Impostare le opzioni relative al modo in cui i dati devono essere visualizzati e formattati.  
  
5.  Dopo aver completato la **procedura guidata forma di Data Mining**, si dispone di un diagramma che è possibile modificare e migliorare l'utilizzo delle funzionalità di Visio.  
  
 Per altre informazioni su come utilizzare e migliorare i diagrammi di modello di Visio, vedere [visualizzazione di modelli di Data Mining di Visio &#40;componenti aggiuntivi Data Mining&#41;](viewing-data-mining-models-in-visio-data-mining-add-ins.md)  
  
## <a name="requirements"></a>Requisiti  
  
-   Per poter utilizzare i modelli, è innanzitutto necessario creare una connessione a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
     Nella procedura guidata verrà chiesto di selezionare un server [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e di specificare il database contenente il modello di data mining.  
  
     Per informazioni su come creare una connessione, vedere [Connetti ai dati di origine &#40;Client di Data Mining per Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md).  
  
-   Se si utilizza Strumenti di analisi tabelle, assicurarsi di salvare i modelli nel server [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e di non utilizzare modelli temporanei.  
  
-   Il modello deve essere creato utilizzando uno degli algoritmi supportati: Clustering, Decision Trees, Neural Networks, Naïve Bayes o Logistic Regression.  
  
  
