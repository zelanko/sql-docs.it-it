---
title: Scheda matrice di classificazione (visualizzazione Grafico accuratezza modello di data mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.accuracychart.confusionmatrix.f1
ms.assetid: 85d5a047-d656-41e0-8a31-400271c2a620
author: minewiskan
ms.author: owend
ms.openlocfilehash: d202d552b25095d0d0845ff64f9c0e289f7bba0e
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527497"
---
# <a name="classification-matrix-tab-mining-accuracy-chart-view"></a>Scheda Matrice di classificazione (visualizzazione Grafico accuratezza modello di data mining)
  Nella scheda **matrice di classificazione** viene visualizzata una matrice di classificazione per ogni modello selezionato nella griglia dei modelli nella scheda **Mapping colonne** . La matrice di classificazione è disponibile solo se la colonna stimabile selezionata nella scheda **Mapping colonne** non è continua. Per una descrizione più dettagliata della scheda **Matrice di classificazione** , vedere [Testing and Validation &#40;Data Mining&#41;](data-mining/testing-and-validation-data-mining.md).  
  
## <a name="options"></a>Opzioni  
 **Copia**  
 Consente di copiare il contenuto di ogni matrice di classificazione negli Appunti.  
  
 **Conteggi per \<model> il\< predictable column>**  
 Visualizza una matrice di classificazione per ogni modello di data mining nella struttura di data mining. La matrice contiene le colonne seguenti:  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|**Stimati**|Include una riga per ogni stato della colonna stimabile.|  
|**\<states>reale**|Una colonna per ogni stato nella colonna stimabile. Se lo stato della riga e della colonna corrispondono, la cella rappresenta il numero effettivo di volte in cui lo stato si è verificato nel database. In caso contrario, la cella rappresenta l'errore della stima.|  
  
## <a name="see-also"></a>Vedere anche  
 [Progettazione Grafico accuratezza modello di data mining &#40;&#41;di data mining](mining-accuracy-chart-designer-data-mining.md)   
 [Attività e procedure di test e convalida &#40;di data mining&#41;](data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)   
 [Test e convalida &#40;Data mining&#41;](data-mining/testing-and-validation-data-mining.md)  
  
  
