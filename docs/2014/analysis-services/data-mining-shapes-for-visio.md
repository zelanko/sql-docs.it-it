---
title: Forme di data mining per Visio | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining shapes
- templates [Visio]
- Visio shapes
- shapes, data mining
ms.assetid: 11a821d9-1c0a-442e-b735-92208ce479dc
author: minewiskan
ms.author: owend
ms.openlocfilehash: 1d30456ac3685aa3dc40af6f1c79f92796fc1404
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84525777"
---
# <a name="data-mining-shapes-for-visio"></a>Forme di data mining per Visio
  Le forme di data mining per Visio forniscono il modelli personalizzati per la visualizzazione dei modelli di data mining. Tramite questi modelli, è possibile connettersi a un modello creato in precedenza e creare presentazioni interattive per illustrare i risultati del processo di data mining.  
  
 I modelli offrono molti vantaggi rispetto ai grafici statici e alle acquisizioni di schermate, che interagiscono con i modelli data mining sottostanti, archiviati in un'istanza di Analysis Services, e consentono di personalizzare il modo in cui vengono visualizzati i modelli nel modello di data mining. È possibile comprimere ed espandere un modello di albero, applicare filtri ai nodi dati o in base agli attributi e visualizzare le statistiche del modello come probabilità e coefficienti.  
  
 ![DM](media/dm-stencil.gif "DM")  
  
 Nei modelli di Visio sono incluse le procedure guidate seguenti:  
  
-   **Diagramma della rete di dipendenze:** Utilizzare questa procedura guidata per creare grafici per gli alberi delle decisioni e le reti neurali.  
  
-   **Diagramma dell'albero delle decisioni:** Utilizzare questa procedura guidata per creare diagrammi che mostrino i punti decisionali e le formule associati ai modelli di albero delle decisioni. Questo diagramma può inoltre essere utilizzato con i modelli di regressione.  
  
-   **Diagramma cluster:** Utilizzare questa procedura guidata per creare grafici colorati per i modelli di segmentazione. È possibile spostarsi tra varie viste, ad esempio discriminante attributi, profili dei cluster e dipendenze, e personalizzare l'aspetto dei cluster.  
  
## <a name="installation"></a>Installazione  
 Quando si installano i modelli di data mining per Visio, per impostazione predefinita vengono installati i file seguenti in \<drive> \programmi\microsoft SQL Server 2012 DM Add-ins (o \<drive> \ o programmi (x86) \microsoft SQL Server 2012 DM Add-ins):  
  
-   **Microsoft Data mining. VST** Questo modello contiene la formattazione, il layout e le procedure guidate preprogettate per semplificare l'utilizzo delle forme data mining.  
  
-   **Microsoft Data mining Shape Studio. VSS** Questo file di stencil contiene forme associate al modello.  
  
## <a name="how-to-use-the-templates"></a>Come usare i modelli  
 Per aprire i modelli, è possibile fare doppio clic sul file di forma o è possibile aprire Visio e quindi aprire il modello di forma.  
  
1.  Rilasciare una delle forme di data mining di Visio dallo stencil in una nuova pagina.  
  
2.  All'avvio della procedura guidata connettersi al server che contiene il modello di data mining che si desidera visualizzare.  
  
3.  Selezionare il modello di data mining facendo corrispondere il tipo di modello al tipo di visualizzazione.  
  
4.  Impostare le opzioni relative al modo in cui i dati devono essere visualizzati e formattati.  
  
5.  Dopo aver completato la **creazione guidata forma di data mining**, è possibile modificare e migliorare l'utilizzo delle funzionalità di Visio.  
  
 Per ulteriori informazioni su come utilizzare e migliorare i diagrammi di modello di Visio, vedere [visualizzazione di modelli di data mining in visio &#40;componenti aggiuntivi Data mining&#41;](viewing-data-mining-models-in-visio-data-mining-add-ins.md)  
  
## <a name="requirements"></a>Requisiti  
  
-   Per poter utilizzare i modelli, è innanzitutto necessario creare una connessione a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
     Nella procedura guidata verrà chiesto di selezionare un server [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e di specificare il database contenente il modello di data mining.  
  
     Per informazioni su come creare una connessione, vedere [connettersi ai dati di origine &#40;client di data mining per&#41;Excel ](connect-to-source-data-data-mining-client-for-excel.md).  
  
-   Se si utilizza Strumenti di analisi tabelle, assicurarsi di salvare i modelli nel server [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e di non utilizzare modelli temporanei.  
  
-   Il modello deve essere creato utilizzando uno degli algoritmi supportati: Clustering, Decision Trees, Neural Networks, Naïve Bayes o Logistic Regression.  
  
  
