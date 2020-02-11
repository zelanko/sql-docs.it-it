---
title: Utilizzo del drill-through sui dati della struttura (esercitazione di base sul data mining) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62745542"
---
# <a name="using-drillthrough-on-structure-data-basic-data-mining-tutorial"></a>Utilizzo del drill-through sui dati della struttura (Esercitazione di base sul data mining)
  Nell'ambito della campagna pubblicitaria, [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] sta inviando un mailer a potenziali clienti nella 34-40 età demografica. Il reparto marketing ha deciso di inviare il mailer anche ai clienti che hanno acquistato biciclette da [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] più di cinque anni fa. In questa lezione verranno identificati i clienti con le biciclette meno recenti e saranno recuperate le relative informazioni di contatto. Queste informazioni non sono incluse nel modello, ma sono incluse nella struttura. Per recuperare le informazioni di contatto, prima ci si assicurerà che il drill-through sia abilitato per la struttura, quindi si utilizzerà il drill-through per ottenere i nomi e gli indirizzi dei clienti di destinazione.  
  
### <a name="to-enable-drillthrough-on-a-mining-model"></a>Per abilitare il drill-through su un modello di data mining  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], nella scheda **modelli** di data mining di progettazione modelli di data mining, fare clic con il pulsante destro del mouse sul modello di **TM_Decision_Tree** e scegliere **Proprietà**.  
  
2.  Nella finestra Proprietà fare clic su **AllowDrillthrough**e selezionare **True**.  
  
3.  Nella scheda Modelli di data mining fare clic con il pulsante destro del mouse sul modello e scegliere **Elabora modello**.  
  
 Per ulteriori informazioni, vedere [query drill-through &#40;Data Mining&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)  
  
### <a name="to-view-drillthrough-data-from-a-mining-model"></a>Per visualizzare i dati del drill-through da un modello di data mining  
  
1.  In Progettazione modelli di data mining fare clic sulla scheda **Visualizzatore modello di data mining** .  
  
2.  Selezionare il modello di **TM_Decision_Tree** nell'elenco **modello di data mining** .  
  
3.  Modificare il **** valore di sfondo `1`in. In questo modo, verrà visualizzata solo la parte del modello correlata ai clienti che hanno acquistato biciclette.  
  
4.  Selezionare il Visualizzatore Microsoft Decision Trees dall'elenco **Visualizzatore** . In questo modo verrà eseguito l'aggiornamento del visualizzatore con le nuove condizioni di filtro. Individuare quindi il nodo **Age >= 34 e <41** , quindi fare clic con il pulsante destro del mouse sul nodo.  
  
5.  Scegliere **Drill-through**, quindi **Colonne struttura e modello** per aprire la finestra **Drill-through** .  
  
6.  Scorrere fino alla colonna **Structure.Date First Purchase** per visualizzare le date di acquisto delle biciclette meno recenti.  
  
7.  Per copiare i dati negli Appunti, fare clic con il pulsante destro del mouse su qualsiasi riga nella tabella e selezionare **Copia tutto**.  
  
 È stata completata l'esercitazione di base sul data mining. Dopo avere familiarizzato con l'utilizzo degli strumenti di data mining, si consiglia di completare anche l'esercitazione intermedia sul data mining, in cui viene illustrato come creare modelli per le previsioni, le analisi degli acquisti e il clustering delle sequenze.  
  
## <a name="previous-task-in-lesson"></a>Attività precedente della lezione  
 [Creazione di stime &#40;esercitazione di base sul data mining&#41;](../../2014/tutorials/creating-predictions-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Creare una query di stima utilizzando Generatore query di stima](../../2014/analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)  
  
  
