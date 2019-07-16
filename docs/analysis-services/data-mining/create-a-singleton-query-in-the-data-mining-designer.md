---
title: Creare una Query Singleton in Progettazione modelli di Data Mining | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d30fee91882ecd2f76fde1e0c61d0e5bc3d302bc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68183935"
---
# <a name="create-a-singleton-query-in-the-data-mining-designer"></a>Creare una query singleton in Progettazione modelli di data mining
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Una query singleton è utile quando si desidera creare una stima per un singolo case. Per altre informazioni sulle query singleton, vedere [Query di data mining](../../analysis-services/data-mining/data-mining-queries.md).  
  
 Nella scheda **Stima modello di data mining** della Progettazione modelli di data mining è possibile creare diversi tipi di query. È possibile creare una query utilizzando la finestra di progettazione oppure digitando istruzioni Data Mining Extensions (DMX). È anche possibile iniziare con la finestra di progettazione e modificare la query creata cambiando le istruzioni DMX o aggiungendo una clausola WHERE o ORDER BY.  
  
 Per passare dalla visualizzazione della progettazione della query alla visualizzazione del testo della query e viceversa, fare clic sul primo pulsante nella barra degli strumenti. Tramite la visualizzazione del testo della query è possibile visualizzare il codice DMX creato dal generatore delle query di stima. È inoltre possibile eseguire la query, modificarla ed eseguire la query modificata. La query modificata, tuttavia, non viene mantenuta se si torna alla visualizzazione della progettazione della query  
  
 Nel codice seguente viene illustrato un esempio di query singleton confrontato al modello di invio mirato di messaggi di posta elettronica, TM_Decision_Tree.  
  
```  
SELECT [Bike Buyer], PredictProbability([Bike Buyer]) as ProbableBuyer  
FROM [TM_Decision_Tree]  
NATURAL PREDICTION JOIN  
(SELECT '2' AS [Number Children At Home], '45' as [Age])  
AS [t]  
```  
  
 Nei passaggi seguenti viene descritta la creazione della query di stima.  
  
### <a name="to-create-a-singleton-query-by-using-the-data-mining-designer"></a>Per creare una query singleton utilizzando la Progettazione modelli di data mining  
  
1.  Fare clic sulla scheda **Stima modello di data mining** in Progettazione modelli di data mining.  
  
2.  Fare clic su **Seleziona modello** nella tabella **Modello di data mining** .  
  
     Verrà visualizzata la finestra di dialogo **Seleziona modello di data mining** , in cui sono indicate tutte le strutture di data mining presenti nel progetto.  
  
     Selezionare il modello che si desidera utilizzare per creare la stima.  
  
     Ad esempio, per creare il codice di esempio mostrato all'inizio di questo argomento, selezionare TM_Decision_Tree, quindi fare clic su **OK**.  
  
3.  Fare clic su **Query singleton** sulla barra degli strumenti della scheda **Stima modello di data mining** .  
  
     Nella scheda verrà visualizzata la tabella **Input query singleton** sulle cui colonne viene eseguito il mapping automaticamente alle colonne della tabella **Modello di data mining** .  
  
4.  Nella tabella **Input query singleton** selezionare nella colonna **Valore** i valori adatti a descrivere il caso per creare una stima.  
  
     Ad esempio, selezionare **2** per **Number Children At Home**, quindi digitare **45** per **Age**.  
  
5.  Trascinare una colonna stimabile dalla tabella **Modello di data mining** alla colonna **Origine** nella parte inferiore della scheda. Facoltativamente, è possibile digitare un alias per la colonna.  
  
     Ad esempio, trascinare **Bike Buyer** nella colonna **Origine** .  
  
6.  Aggiungere eventuali funzionalità aggiuntive alla query selezionando **Funzione di stima** o **Espressione personalizzata** nell'elenco a discesa nella colonna **Origine** .  
  
     Ad esempio, fare clic su **Funzione di stima**e selezionare **PredictProbability**.  
  
7.  Fare clic su **Criteri/Argomento** nella riga **PredictProbability** e digitare il nome della colonna da stimare e facoltativamente un valore specifico da stimare.  
  
     Ad esempio, digitare **[Bike Buyer], 1**.  
  
8.  Fare clic sulla casella **Alias** nella riga **PredictProbability** e digitare un nome per fare riferimento alla nuova colonna.  
  
     Ad esempio, digitare **ProbableBuyer**.  
  
9. Fare clic su **Passa alla visualizzazione dei risultati della query** sulla barra degli strumenti della scheda **Stima modello di data mining** .  
  
     Verrà visualizzata una nuova schermata con il risultato della query. Per visualizzare l'istruzione DMX appena creata, fare clic su **SQL**.  
  
## <a name="see-also"></a>Vedere anche  
 [Query di stima &#40;Data Mining&#41;](../../analysis-services/data-mining/prediction-queries-data-mining.md)  
  
  
