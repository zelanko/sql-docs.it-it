---
title: 'Attività 9: aggiunta della trasformazione Unione input multipli per combinare record corretti e con correzione | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 24ba466d-a7d3-49e7-9111-b348399c9e58
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 89e336b326550f07a5ad6fb5dfab449dbe349109
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85006250"
---
# <a name="task-9-adding-union-all-transform-to-combine-correct-and-corrected-records"></a>Attività 9: Aggiunta della trasformazione Unione input multipli a Combina record corretti e con correzione
  In questa attività viene aggiunta la trasformazione Unione input multipli al flusso di dati. La trasformazione Unione input multipli consente di combinare più input in un unico output. Nello scenario attuale i record corretti e con correzione vengono combinati in un flusso.  
  
1.  Trascinare la trasformazione **Unione** input multipli dalla sezione **comune** della **casella degli strumenti SSIS** alla scheda flusso di **dati** e posizionarla in **Seleziona record corretti e con correzione**.  
  
2.  Fare clic con il pulsante destro del mouse su **Union All** Transform nella scheda **flusso di dati** e scegliere **Rinomina**. Digitare **Combina record corretti e con correzione**e premere **invio**.  
  
     ![Combina record corretti e con correzione](../../2014/tutorials/media/et-addinguattocombinecacrecords-01.jpg "Combina record corretti e con correzione")  
  
3.  Connettersi **selezionare i record corretti e corretti** per **combinare i record corretti e con correzione** nella scheda **flusso di dati** usando il connettore blu. Verrà visualizzata la finestra di dialogo **Selezione output input** .  
  
4.  Nella finestra di dialogo **output di input** selezionare **Correggi** per l' **output** e fare clic su **OK**.  
  
     ![Finestra di dialogo Selezione input e output](../../2014/tutorials/media/et-addinguattocombinecacrecords-02.jpg "Finestra di dialogo Selezione input e output")  
  
5.  Spostare il connettore intitolato **Correct** a sinistra trascinando il punto alla fine del connettore verso sinistra.  
  
     ![Connetti Correggi a Combina corretti e con correzione](../../2014/tutorials/media/et-addinguattocombinecacrecords-03.jpg "Connetti Correggi a Combina corretti e con correzione")  
  
6.  Se si seleziona la trasformazione seleziona **record corretti e con correzione** , verrà visualizzato un altro connettore blu. Trascinare il connettore blu per **combinare i record corretti e con correzione**.  
  
     ![Connetti Con correzione a Combina corretti e con correzione](../../2014/tutorials/media/et-addinguattocombinecacrecords-04.jpg "Connetti Con correzione a Combina corretti e con correzione")  
  
7.  Il titolo del **connettore** deve essere **corretto**. Poiché sono presenti solo due condizioni **corrette** e **corrette e una**condizione è già stata utilizzata, la finestra di dialogo **Selezione output input** non viene visualizzata questa volta. Se i collegamenti si sovrappongono, spostarne uno a sinistra e l'altro a destra trascinando il collegamento a sinistra o a destra.  
  
## <a name="next-step"></a>passaggio successivo  
 [Attività 10: Aggiunta della trasformazione Raggruppamento fuzzy per l'identificazione di duplicati](../../2014/tutorials/task-10-adding-fuzzy-group-transform-to-identify-duplicates.md)  
  
  
