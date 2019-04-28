---
title: Scheda matrice di classificazione (vista grafico di accuratezza Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.accuracychart.confusionmatrix.f1
ms.assetid: 85d5a047-d656-41e0-8a31-400271c2a620
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1879e9ec4f2a6decf4168e7c49a5e81d3a043d29
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62681730"
---
# <a name="classification-matrix-tab-mining-accuracy-chart-view"></a>Scheda Matrice di classificazione (visualizzazione Grafico accuratezza modello di data mining)
  Nella scheda **Matrice di classificazione** viene visualizzata una matrice di classificazione per ogni modello selezionato nella griglia dei modelli nella scheda **Mapping colonne** . La matrice di classificazione è disponibile solo se la colonna stimabile selezionata nella scheda **Mapping colonne** non è continua. Per una descrizione più dettagliata della scheda **Matrice di classificazione** , vedere [Testing and Validation &#40;Data Mining&#41;](data-mining/testing-and-validation-data-mining.md).  
  
## <a name="options"></a>Opzioni  
 **Copia**  
 Consente di copiare il contenuto di ogni matrice di classificazione negli Appunti.  
  
 **Dati relativi al numero \<model > su \< colonna stimabile >**  
 Visualizza una matrice di classificazione per ogni modello di data mining nella struttura di data mining. La matrice contiene le colonne seguenti:  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**Stimato**|Include una riga per ogni stato della colonna stimabile.|  
|**\<stati > (effettivo)**|Una colonna per ogni stato nella colonna stimabile. Se lo stato della riga e della colonna corrispondono, la cella rappresenta il numero effettivo di volte in cui lo stato si è verificato nel database. In caso contrario, la cella rappresenta l'errore della stima.|  
  
## <a name="see-also"></a>Vedere anche  
 [Finestra di progettazione grafico accuratezza di data mining &#40;Data Mining&#41;](mining-accuracy-chart-designer-data-mining.md)   
 [Test e convalida le attività e procedure relative alla &#40;Data Mining&#41;](data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)   
 [Test e convalida &#40;Data mining&#41;](data-mining/testing-and-validation-data-mining.md)  
  
  
