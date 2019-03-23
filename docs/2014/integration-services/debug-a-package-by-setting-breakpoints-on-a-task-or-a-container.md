---
title: Debug di un pacchetto impostando punti di interruzione in un'attività o un contenitore | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], breakpoints
- breakpoints [Integration Services]
- tasks [Integration Services], breakpoints
ms.assetid: e7fa106a-2221-403a-bb74-efc9f12bb450
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3c78fb92078c604d881f18ea3472e23619771b49
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58374619"
---
# <a name="debug-a-package-by-setting-breakpoints-on-a-task-or-a-container"></a>Debug di un pacchetto impostando punti di interruzione in un'attività o in un contenitore
  In questa procedura viene descritto come impostare punti di interruzione in un pacchetto, in un'attività o in un contenitore Ciclo For, Ciclo Foreach o Sequenza.  
  
### <a name="to-set-breakpoints-in-a-package-a-task-or-a-container"></a>Per impostare punti di interruzione in un pacchetto, in un'attività o in un contenitore  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  Fare doppio clic sul pacchetto in cui si desidera impostare punti di interruzione.  
  
3.  In Progettazione SSIS eseguire una delle operazioni seguenti:  
  
    -   Per impostare punti di interruzione nell'oggetto di pacchetto, nella scheda **Flusso di controllo** posizionare il cursore in un punto qualsiasi dello sfondo dell'area di progettazione, fare clic con il pulsante destro del mouse e quindi scegliere **Modifica punti di interruzione**.  
  
    -   Per impostare punti di interruzione nel flusso di controllo di un pacchetto, nella scheda **Flusso di controllo** fare clic con il pulsante destro del mouse su un'attività o su un contenitore Ciclo For, Ciclo Foreach o Sequenza e quindi scegliere **Modifica punti di interruzione**.  
  
    -   Per impostare punti di interruzione in un gestore evento, nella scheda **Gestore evento** fare clic con il pulsante destro del mouse su un'attività o su un contenitore Ciclo For, Ciclo Foreach o Sequenza e quindi scegliere **Modifica punti di interruzione**.  
  
4.  Nella finestra di dialogo **Imposta punti di interruzione \<nome contenitore>** selezionare i punti di interruzione da attivare.  
  
5.  Facoltativamente, modificare il tipo di passaggi e il numero di passaggi per ogni punto di interruzione.  
  
6.  Per salvare il pacchetto, scegliere **Salva elementi selezionati** dal menu **File** .  
  
## <a name="see-also"></a>Vedere anche  
 [Risoluzione dei problemi relativi agli strumenti per lo sviluppo dei pacchetti](troubleshooting/troubleshooting-tools-for-package-development.md)   
 [Eseguire il debug di uno script impostando punti di interruzione in un'attività e in un componente Script](data-flow/transformations/script-component.md)   
 [Scrittura di codice e debug dell'attività Script](control-flow/script-task.md)   
 [Codifica e debug del componente script](extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
  
  
