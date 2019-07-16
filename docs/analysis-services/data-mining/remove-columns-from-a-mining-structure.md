---
title: Rimuovere colonne da una struttura di Data Mining | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bd8691d8ec0cc1546e27e8195e7d0bbc20709f59
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209680"
---
# <a name="remove-columns-from-a-mining-structure"></a>Rimuovere colonne da una struttura di data mining
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  È possibile utilizzare Progettazione modelli di data mining per rimuovere le colonne da una struttura di data mining dopo averla creata. I motivi per cui rimuovere una colonna della struttura di data mining possono includere i seguenti:  
  
-   La struttura di data mining contiene più copie di una colonna e si desidera evitare l'utilizzo di dati duplicati in un modello.  
  
-   I dati devono essere protetti, ma il drill-through è abilitato.  
  
-   I dati non vengono utilizzati nella modellazione e non devono essere elaborati.  
  
 L'eliminazione di una colonna dalla struttura di data mining non comporta la modifica della colonna nella vista origine dati o nei dati esterni. Solo i metadati vengono eliminati. Tuttavia, quando si modificano le colonne utilizzate in una struttura di data mining, è necessario rielaborare la struttura e alcuni modelli basati su di essa.  
  
### <a name="to-remove-a-column-from-the-mining-structure"></a>Per rimuovere una colonna dalla struttura di data mining  
  
1.  Selezionare la scheda **Struttura di data mining** in Progettazione modelli di data mining.  
  
2.  Espandere l'albero per visualizzare tutte le colonne della struttura di data mining.  
  
3.  Fare clic con il pulsante destro del mouse sulla colonna che si desidera eliminare, quindi scegliere **Elimina**.  
  
4.  Nella finestra di dialogo **Elimina oggetti** fare clic su **OK**.  
  
## <a name="see-also"></a>Vedere anche  
 [Attività e procedure relative alla struttura di data mining](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  
