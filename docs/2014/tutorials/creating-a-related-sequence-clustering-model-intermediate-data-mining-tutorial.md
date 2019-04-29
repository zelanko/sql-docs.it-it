---
title: Creazione di un modello Sequence Clustering correlato (esercitazione intermedia di Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1fb4f5bc-1756-45ca-9cd7-411a8c5992a9
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 71db7ba5246e151bbca8a52972a2ba835b80ddb6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62855874"
---
# <a name="creating-a-related-sequence-clustering-model-intermediate-data-mining-tutorial"></a>Creazione di un modello Sequence Clustering correlato (Esercitazione intermedia sul data mining)
  Tramite l'esplorazione del modello Sequence Clustering sono stati individuati altri attributi, quali Region e Income, in grado di influire in modo significativo sui modelli. Per comprendere meglio le sequenze, verrà pertanto creato un modello Sequence Clustering correlato e verranno rimossi gli attributi relativi ai dati demografici dei clienti.  
  
 In questa attività verrà creata una copia del modello Sequence Clustering regionale, quindi verranno rimosse dal modello tutte le colonne non correlate direttamente alle sequenze.  
  
 Il nuovo modello conterrà esattamente le stesse colonne del modello di data mining sul quale è basato. Non è tuttavia necessario rimuovere le colonne dalla struttura di data mining, ma è sufficiente specificare che il nuovo modello di data mining ignora tali colonne.  
  
### <a name="to-make-a-copy-of-the-sequence-clustering-model"></a>Per creare una copia del modello Sequence Clustering  
  
1.  Nelle [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], in Data Mining Designer, fare clic sui **modelli di Data Mining** scheda.  
  
2.  Fare doppio clic il modello si desidera copiare e scegliere **nuovo modello di Data Mining**.  
  
3.  Nel **nuovo modello di Data Mining** della finestra di dialogo digitare un nome di modello e selezionare Microsoft `Sequence Clustering`.  
  
     Per questa esercitazione, digitare il nome `Sequence Clustering`.  
  
4.  Fare clic su **OK**.  
  
### <a name="to-remove-columns-from-the-mining-model"></a>Per rimuovere le colonne dal modello di data mining  
  
1.  Nel **modello di Data Mining** scheda, nella colonna per il nuovo modello con nome Sequence Clustering, fare clic sulla riga per il **Income Group** attributo, quindi selezionare **ignora**.  
  
2.  Ripetere questo passaggio per l'attributo **regione**.  
  
3.  Fare clic sul segno più accanto al nome di tabella **v Assoc Seq Line Items**per espandere la tabella e visualizzare le colonne della tabella nidificata.  
  
     Il nuovo modello dovrebbe ora contenere solo le colonne seguenti:  
  
     **Ordine NumberKey**  
  
     **Chiave di numeri di riga**  
  
     **Modello di stima**  
  
### <a name="to-process-the-new-sequence-clustering-model"></a>Per elaborare il nuovo modello Sequence Clustering  
  
1.  Nel **modello di Data Mining** scheda, fare doppio clic su nuovo modello con nome `Sequence Clustering`e selezionare **Elabora modello**.  
  
     Poiché il nuovo il modello di data mining semplificato è basato su una struttura che è già stata elaborata, non è necessario rielaborare la struttura. È sufficiente elaborare il nuovo modello di data mining.  
  
2.  Fare clic su **Sì** per distribuire il progetto di data mining i dati aggiornati nel server.  
  
3.  Nel **modello di processo di Data Mining** finestra di dialogo, fare clic su **eseguire**.  
  
4.  Fare clic su **chiudere** per chiudere la **stato elaborazione** la finestra di dialogo e quindi fare clic su **chiudere** nuovamente nel **Elabora modello di Data Mining** nella finestra di dialogo.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Creazione di stime su un modello Sequence Clustering &#40;esercitazione intermedia sul Data Mining&#41;](../../2014/tutorials/create-predictions-on-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Requisiti e considerazioni sull'elaborazione &#40;data mining&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
