---
title: Creare una query DMX in SQL Server Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- templates [Analysis Services], queries
- SQL Server Management Studio [Analysis Services], DMX queries
- predictions [Analysis Services], DMX prediction queries
- predictions [DMX]
- prediction queries [DMX]
- queries [DMX], prediction queries
- mining models [Analysis Services], DMX
ms.assetid: 568ce40a-1f53-47eb-8c79-14347cdfde83
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ef1595ff322979a150c8854a73db5088cd8e0139
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66085465"
---
# <a name="create-a-dmx-query-in-sql-server-management-studio"></a>Creare una query DMX in SQL Server Management Studio
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] offre un set di funzionalità che consentono di creare query di stima, query sul contenuto e query di definizione dei dati su modelli e strutture di data mining.  
  
-   Un generatore di query di stima grafico è disponibile sia in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] che in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]per semplificare il processo di scrittura delle query di stima e il mapping dei set di dati a un modello.  
  
-   I modelli di query forniti in Esplora modelli avviano rapidamente la creazione di molti tipi di query DMX, tra cui molti tipi di query di stima. Vengono forniti modelli per query contenuto, query che utilizzano set di dati nidificati, query che restituiscono case dalla struttura di data mining e anche query di definizione dei dati.  
  
-   In Visualizzatore metadati nei riquadri delle query MDX e DMX è presente un elenco di modelli e strutture disponibili che è possibile trascinare nel generatore di query, nonché un elenco di funzioni DMX. Questa funzionalità consente di ottenere con facilità i nomi degli oggetti corretti, senza doverli digitare.  
  
 In questo argomento viene illustrato come compilare una query DMX tramite Visualizzatore metadati e l'editor di query DMX.  
  
##  <a name="dmx-query-templates"></a><a name="BKMK_Templates"></a>Modelli di query DMX  
 I modelli per la creazione delle query DMX di base sono disponibili in Esplora modelli. La cartella **DMX** contiene modelli di data mining, divisi nelle categorie seguenti:  
  
-   **Contenuto del modello**  
  
-   **Gestione modelli**  
  
-   **Query di stima**  
  
-   **Contenuto della struttura**  
  
 È inoltre possibile creare modelli personalizzati, per query o comandi eseguiti frequentemente.  
  
## <a name="xmla-query-templates"></a>Modelli di query XMLA  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] include anche modelli per le query XMLA.  
  
 I tipi di query che è possibile eseguire tramite XMLA e DMX sono parzialmente sovrapposti. Ad esempio, è possibile creare alcune query contenuto del modello tramite DMX o i set di righe dello schema di data mining, ma i set di righe dello schema talvolta contengono informazioni non esposte nelle query contenuto DMX.  
  
 Sono inoltre presenti alcune differenze fondamentali nella modalità di gestione delle operazioni in DMX e in XMLA. Ad esempio, è possibile usare XMLA per eseguire operazioni amministrative, come il backup di un intero database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], ma per eseguire il backup di un solo modello di data mining in DMX è disponibile un comando semplice, [EXPORT &#40;DMX&#41;](/sql/dmx/export-dmx), più indicato allo scopo.  
  
##  <a name="build-and-run-a-dmx-query"></a><a name="BKMK_Building_Queries"></a>Compilare ed eseguire una query DMX  
  
#### <a name="open-a-new-dmx-query-window"></a>Aprire una nuova finestra Query DMX  
  
1.  Fare clic su **Nuova query** in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e quindi selezionare **Nuova query DMX di Analysis Server**.  
  
2.  Quando viene visualizzata la finestra di dialogo **Connetti al server** , selezionare l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] contenente i modelli di data mining da usare.  
  
#### <a name="open-template-explorer"></a>Aprire Esplora modelli  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]scegliere **Esplora modelli** dal menu **Visualizza**.  
  
2.  Fare clic su **Analysis Server** per ottenere una visualizzazione albero dei modelli applicabili a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
#### <a name="apply-a-template-to-build-a-query"></a>Applicare un modello per compilare una query  
  
-   Fare clic con il pulsante destro del mouse sul tipo di query adatto e scegliere **Apri**.  
  
-   In alternativa, trascinare il modello nell'editor di query.  
  
-   È anche possibile compilare i parametri per la query scegliendo l'opzione **Specifica valori per parametri**dal menu **Query** .  
  
 Per esempi relativi alla creazione di tipi specifici di query dai modelli, vedere gli argomenti seguenti:  
  
 [Creare una query di stima singleton da un modello](create-a-singleton-prediction-query-from-a-template.md)  
  
 [Creare una query sul contenuto di un modello di data mining](create-a-content-query-on-a-mining-model.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Interfacce di query di data mining](data-mining-query-tools.md)   
 [Guida di riferimento a DMX &#40;Data Mining Extensions&#41;](/sql/dmx/data-mining-extensions-dmx-reference)  
  
  
