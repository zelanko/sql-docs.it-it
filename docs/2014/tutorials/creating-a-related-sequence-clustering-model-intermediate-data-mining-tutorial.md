---
title: Creazione di un modello Sequence Clustering correlato (Esercitazione intermedia sul data mining) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62855874"
---
# <a name="creating-a-related-sequence-clustering-model-intermediate-data-mining-tutorial"></a>Creazione di un modello Sequence Clustering correlato (Esercitazione intermedia sul data mining)
  Tramite l'esplorazione del modello Sequence Clustering sono stati individuati altri attributi, quali Region e Income, in grado di influire in modo significativo sui modelli. Per comprendere meglio le sequenze, verrà pertanto creato un modello Sequence Clustering correlato e verranno rimossi gli attributi relativi ai dati demografici dei clienti.  
  
 In questa attività verrà creata una copia del modello Sequence Clustering regionale, quindi verranno rimosse dal modello tutte le colonne non correlate direttamente alle sequenze.  
  
 Il nuovo modello conterrà esattamente le stesse colonne del modello di data mining sul quale è basato. Non è tuttavia necessario rimuovere le colonne dalla struttura di data mining, ma è sufficiente specificare che il nuovo modello di data mining ignora tali colonne.  
  
### <a name="to-make-a-copy-of-the-sequence-clustering-model"></a>Per creare una copia del modello Sequence Clustering  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]Progettazione modelli di data mining di fare clic sulla scheda **modelli di data mining** .  
  
2.  Fare clic con il pulsante destro del mouse sul modello che si desidera copiare e scegliere **nuovo modello di data mining**.  
  
3.  Nella finestra di dialogo **nuovo modello di data mining** Digitare un nome di modello e selezionare `Sequence Clustering`Microsoft.  
  
     Per questa esercitazione, digitare il nome `Sequence Clustering`.  
  
4.  Fare clic su **OK**.  
  
### <a name="to-remove-columns-from-the-mining-model"></a>Per rimuovere le colonne dal modello di data mining  
  
1.  Nella scheda **modello di data mining** , nella colonna relativa al nuovo modello denominato Sequence Clustering, fare clic sulla riga dell'attributo **Income Group** e selezionare **Ignora**.  
  
2.  Ripetere questo passaggio per l' **area**dell'attributo.  
  
3.  Fare clic sul segno più accanto al nome della tabella, **v Assoc Seq Line Items**, per espandere la tabella e visualizzare le colonne della tabella nidificata.  
  
     Il nuovo modello dovrebbe ora contenere solo le colonne seguenti:  
  
     **NumberKey ordine**  
  
     **Chiave numero di riga**  
  
     **Stima modello**  
  
### <a name="to-process-the-new-sequence-clustering-model"></a>Per elaborare il nuovo modello Sequence Clustering  
  
1.  Nella scheda **modello di data mining** fare clic con il pulsante destro del `Sequence Clustering`mouse sul nuovo modello denominato e scegliere **Elabora modello**.  
  
     Poiché il nuovo il modello di data mining semplificato è basato su una struttura che è già stata elaborata, non è necessario rielaborare la struttura. È sufficiente elaborare il nuovo modello di data mining.  
  
2.  Fare clic su **Sì** per distribuire il progetto data mining aggiornato al server.  
  
3.  Nella finestra di dialogo **Elabora modello di data mining** fare clic su **Esegui**.  
  
4.  Fare clic su **Chiudi** per chiudere la finestra di dialogo **Stato elaborazione** , quindi fare di nuovo clic su **Chiudi** nella finestra di dialogo **Elabora modello di data mining** .  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Creazione di stime in un modello Sequence Clustering &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/create-predictions-on-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Requisiti e considerazioni sull'elaborazione &#40;&#41;di data mining](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
