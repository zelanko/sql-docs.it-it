---
title: Scegliere un tipo di grafico di accuratezza e impostare le opzioni del grafico | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Mining Accuracy Chart [Analysis Services]
- mining models [Analysis Services], validating
- classification accuracy [data mining]
- accuracy testing [data mining]
ms.assetid: bd24dd4a-624f-478a-9c94-b1361e857680
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6d9f375eb2d55c396000b7c2d7a14614153861e6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66085819"
---
# <a name="choose-an-accuracy-chart-type-and-set-chart-options"></a>Scegliere un tipo di grafico di accuratezza e impostare le opzioni del grafico
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in sono disponibili più metodi per determinare la validità dei modelli di data mining. Il tipo di grafico di accuratezza che è possibile creare per ogni modello o struttura dipende dai fattori seguenti:  
  
-   Tipo di algoritmo utilizzato per creare il modello  
  
-   Tipo di dati dell'attributo stimabile  
  
-   Numero di attributi stimabili per le misurazioni  
  
 In questo argomento viene fornita una panoramica dei diversi grafici di accuratezza.  
  
 **Nota** I grafici e le relative definizioni non vengono salvati. Se si chiude la finestra che contiene un grafico, questo dovrà essere creato di nuovo.  
  
## <a name="accuracy-chart-types"></a>Tipi di grafici di accuratezza  
 A seconda del tipo di grafico scelto, è possibile configurare opzioni, esplorare il grafico o copiare quest'ultimo negli Appunti e utilizzare i dati in Excel.  
  
#### <a name="lift-chart"></a>Grafico di accuratezza  
 Dopo avere configurato le opzioni per i modelli e i dati di testing, fare clic sulla scheda **Grafico di accuratezza** per visualizzare i risultati. È inoltre possibile copiare il grafico negli Appunti o visualizzare i dettagli di singole linee di tendenza o punti dati in Legenda data mining.  
  
#### <a name="profit-chart"></a>Grafico profitti  
 Dopo avere configurato le opzioni per i modelli e i dati di testing, fare clic sulla scheda **Grafico di accuratezza** , selezionare **Grafico profitti** nell'elenco **Tipo di grafico** per impostare le opzioni del grafico dei profitti, quindi scegliere **OK** per visualizzare i risultati.  
  
 È possibile utilizzare la finestra di dialogo **Impostazioni grafico profitti** tutte le volte che lo si desidera per provare diverse opzioni relative ai costi, quindi visualizzare di nuovo il grafico. Legenda data mining contiene informazioni dettagliate sui profitti stimati per ciascun modello. È inoltre possibile copiare il grafico e il contenuto di Legenda data mining negli Appunti per utilizzarli in Excel.  
  
#### <a name="scatter-plot"></a>Grafico a dispersione  
 Se è stato selezionato il tipo di modello appropriato, quando si fa clic sulla scheda **Grafico di accuratezza** il tipo di grafico viene automaticamente impostato su **Grafico a dispersione** e viene visualizzato un grafico a dispersione. Non è possibile effettuare altre operazioni di configurazione. È inoltre possibile copiare il grafico negli Appunti e incollarlo come elemento grafico in Excel o in un'altra applicazione.  
  
#### <a name="classification-matrix"></a>Matrice di classificazione  
 Per una matrice di classificazione, usare la scheda **Selezione input** per scegliere i modelli e i dati di testing, quindi fare clic sulla scheda **Matrice di classificazione** per visualizzare i risultati.  
  
 Il contenuto di una matrice di classificazione è lo stesso per tutti i tipi di modello e non può essere configurato. È inoltre possibile copiare i dati del grafico negli Appunti e quindi utilizzarli in Excel.  
  
#### <a name="cross-validation-report"></a>Report Convalida incrociata  
 Per un report di convalida incrociata, dopo aver selezionato una struttura di data mining o un modello di data mining in Esplora soluzioni, fare clic sulla scheda **Convalida incrociata** , configurare tutte le opzioni pertinenti, quindi fare clic su **Ottieni risultati** per generare il report. Non è possibile effettuare altre operazioni di configurazione.  
  
 Il formato del report di convalida incrociata è lo stesso per tutti i tipi di modello e non può essere configurato. Il contenuto del report varia tuttavia in base al tipo di modello analizzato e al tipo di dati dell'attributo stimabile. È inoltre possibile copiare i risultati del report negli Appunti e utilizzare i dati in Excel.  
  
  
