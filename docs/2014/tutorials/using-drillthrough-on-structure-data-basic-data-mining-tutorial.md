---
title: Utilizzo del drill-through sui dati di struttura (esercitazione di base di Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a693979c-0564-4d6d-b35d-cbbc8f350469
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 68d5d29a4aed7380bd7a53c65d140aac24912392
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62745542"
---
# <a name="using-drillthrough-on-structure-data-basic-data-mining-tutorial"></a>Utilizzo del drill-through sui dati della struttura (Esercitazione di base sul data mining)
  Come parte della propria campagna pubblicitaria, [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] sta inviando un mailer ai potenziali clienti in età 34 e 40 demografiche. Il reparto marketing ha deciso di inviare il mailer anche ai clienti che hanno acquistato biciclette da [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] più di cinque anni fa. In questa lezione verranno identificati i clienti con le biciclette meno recenti e saranno recuperate le relative informazioni di contatto. Queste informazioni non sono incluse nel modello, ma sono incluse nella struttura. Per recuperare le informazioni di contatto, prima ci si assicurerà che il drill-through sia abilitato per la struttura, quindi si utilizzerà il drill-through per ottenere i nomi e gli indirizzi dei clienti di destinazione.  
  
### <a name="to-enable-drillthrough-on-a-mining-model"></a>Per abilitare il drill-through su un modello di data mining  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]via il **modelli di Data Mining** scheda Progettazione modelli di Data Mining fare doppio clic il **TM_Decision_Tree** del modello e selezionare **proprietà**.  
  
2.  Nella finestra Proprietà fare clic su **AllowDrillthrough**e selezionare **True**.  
  
3.  Nella scheda modelli di Data Mining, il modello e scegliere **modello di processo**.  
  
 Per altre informazioni, vedere [query drill-through &#40;Data Mining&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)  
  
### <a name="to-view-drillthrough-data-from-a-mining-model"></a>Per visualizzare i dati del drill-through da un modello di data mining  
  
1.  In Progettazione modelli di data mining fare clic sulla scheda **Visualizzatore modello di data mining** .  
  
2.  Selezionare il **TM_Decision_Tree** del modello dalle **modello di Data Mining** elenco.  
  
3.  Modifica il **sfondo** valore `1`. In questo modo, verrà visualizzata solo la parte del modello correlata ai clienti che hanno acquistato biciclette.  
  
4.  Selezionare il Visualizzatore Microsoft Decision Trees dall'elenco **Visualizzatore** . In questo modo verrà eseguito l'aggiornamento del visualizzatore con le nuove condizioni di filtro. Individuare quindi la **età > = 34 e < 41** nodo e pulsante destro del mouse il nodo.  
  
5.  Scegliere **Drill-through**, quindi **Colonne struttura e modello** per aprire la finestra **Drill-through** .  
  
6.  Scorrere fino alla colonna **Structure.Date First Purchase** per visualizzare le date di acquisto delle biciclette meno recenti.  
  
7.  Per copiare i dati negli Appunti, fare clic con il pulsante destro del mouse su qualsiasi riga nella tabella e selezionare **Copia tutto**.  
  
 È stata completata l'esercitazione di base sul data mining. Dopo avere familiarizzato con l'utilizzo degli strumenti di data mining, si consiglia di completare anche l'esercitazione intermedia sul data mining, in cui viene illustrato come creare modelli per le previsioni, le analisi degli acquisti e il clustering delle sequenze.  
  
## <a name="previous-task-in-lesson"></a>Attività precedente della lezione  
 [Creazione di stime &#40;Esercitazione di base sul data mining&#41;](../../2014/tutorials/creating-predictions-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Creare una query di stima usando Generatore di query di stima](../../2014/analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)  
  
  
