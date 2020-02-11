---
title: Escludere una colonna da un modello di data mining | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- excluding mining model columns
- mining models [Analysis Services], columns
- columns [data mining], excluding
ms.assetid: 404fe5fe-3ba2-4b9b-8780-0d02343d467f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 70049092909b625a1f304f16f153bf4287d5bcdf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66084562"
---
# <a name="exclude-a-column-from-a-mining-model"></a>Escludere una colonna da un modello di data mining
  Quando si crea un nuovo modello di data mining, potrebbe non essere necessario utilizzare tutte le colonne presenti nella struttura di data mining su cui il modello è basato. Ad esempio, è possibile che sia stata aggiunta una colonna nome cliente per il drill-through, ma non si desidera utilizzarla per la modellazione. In alternativa, è possibile decidere di creare più copie di una colonna con discretizzazioni diverse e utilizzare solo una delle copie in ogni modello e ignorare il resto. È anche possibile aggiungere in modo selettivo le colonne di input in molti modelli diversi per capire come la variabile aggiunta influisce sulla colonna di output.  
  
 Non è necessario creare una nuova struttura di data mining per ogni combinazione di colonne; è semplicemente possibile contrassegnare una colonna come non utilizzata in un determinato modello.  
  
### <a name="to-exclude-a-column-from-a-mining-model"></a>Per escludere una colonna da un modello di data mining  
  
1.  Nella scheda **Modelli di data mining** di Progettazione modelli di data mining in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]selezionare la cella corrispondente alla colonna che si desidera escludere, nel modello di data mining appropriato.  
  
2.  Selezionare **Ignora** nell'elenco a discesa.  
  
## <a name="see-also"></a>Vedere anche  
 [Attività e procedure relative al modello di data mining](mining-model-tasks-and-how-tos.md)  
  
  
