---
title: Escludere una colonna da un modello di Data Mining | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5643f9795d702aeab95ed92d796c93df3ffcd133
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68183290"
---
# <a name="exclude-a-column-from-a-mining-model"></a>Escludere una colonna da un modello di data mining
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Quando si crea un nuovo modello di data mining, potrebbe non essere necessario utilizzare tutte le colonne presenti nella struttura di data mining su cui il modello è basato. Ad esempio, si potrebbe avere aggiunto una colonna nome cliente per il drill-through, ma non si vuole usarlo per la modellazione. In alternativa, è possibile decidere di creare più copie di una colonna con discretizzazioni diverse e utilizzare solo una delle copie in ogni modello e ignorare il resto. È anche possibile aggiungere in modo selettivo le colonne di input in molti modelli diversi per capire come la variabile aggiunta influisce sulla colonna di output.  
  
 Non è necessario creare una nuova struttura di data mining per ogni combinazione di colonne; è semplicemente possibile contrassegnare una colonna come non utilizzata in un determinato modello.  
  
### <a name="to-exclude-a-column-from-a-mining-model"></a>Per escludere una colonna da un modello di data mining  
  
1.  Nella scheda **Modelli di data mining** di Progettazione modelli di data mining in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]selezionare la cella corrispondente alla colonna che si desidera escludere, nel modello di data mining appropriato.  
  
2.  Selezionare **Ignora** nell'elenco a discesa.  
  
## <a name="see-also"></a>Vedere anche  
 [Attività e procedure relative al modello di data mining](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
