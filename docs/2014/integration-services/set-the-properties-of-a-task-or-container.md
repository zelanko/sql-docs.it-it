---
title: Impostare le proprietà di un'attività o contenitore | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- tasks [Integration Services], properties
ms.assetid: 52d47ca4-fb8c-493d-8b2b-48bb269f859b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 05e98e0a735cc54e129b82c65841c6db688953de
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66055664"
---
# <a name="set-the-properties-of-a-task-or-container"></a>Impostazione delle proprietà di un'attività o di un contenitore
  È possibile impostare la maggior parte delle proprietà delle attività e dei contenitori usando la finestra **Proprietà**. Fanno eccezione le proprietà delle raccolte di attività e quelle troppo complesse per essere impostate nella finestra **Proprietà**. L'enumeratore usato dal contenitore Ciclo Foreach, ad esempio, non può essere configurato nella finestra **Proprietà**. Per impostare tali proprietà complesse, è necessario utilizzare un editor attività o contenitori. La maggior parte degli editor attività e contenitori include più nodi, ognuno dei quali contiene proprietà correlate. Il nome del nodo indica l'oggetto delle proprietà contenute.  
  
 Le procedure seguenti descrivono come impostare le proprietà di un'attività o di un contenitore usando la finestra **Proprietà** o l'editor attività o contenitori corrispondente.  
  
### <a name="to-set-the-properties-of-a-task-or-container-by-using-the-properties-window"></a>Per impostare le proprietà di un'attività o di un contenitore utilizzando la finestra Proprietà  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di controllo** .  
  
4.  Nell'area di progettazione della scheda **Flusso di controllo** fare clic con il pulsante destro del mouse sull'attività o sul contenitore, quindi scegliere **Proprietà**.  
  
5.  Nella finestra **Proprietà** aggiornare i valori delle proprietà.  
  
    > [!NOTE]  
    >  È possibile impostare la maggior parte delle proprietà digitando un valore direttamente nella casella di testo o selezionandone uno in un elenco. Alcune proprietà sono tuttavia più complesse e dispongono di un editor proprietà personalizzato. Per impostare la proprietà, fare clic nella casella di testo, quindi sul pulsante di compilazione **(...)** per aprire l'editor personalizzato.  
  
6.  Facoltativamente, creare espressioni di proprietà per aggiornare dinamicamente le proprietà dell'attività o del contenitore. Per altre informazioni, vedere [Aggiunta o modifica di un'espressione di proprietà](expressions/add-or-change-a-property-expression.md).  
  
7.  Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
### <a name="to-set-the-properties-of-a-task-or-container-by-using-a-task-or-container-editor"></a>Per impostare le proprietà di un'attività o di un contenitore utilizzando un editor attività o contenitori  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di controllo** .  
  
4.  Nell'area di progettazione della scheda **Flusso di controllo** fare clic con il pulsante destro del mouse sull'attività o sul contenitore, quindi scegliere **Modifica** per aprire l'editor attività o contenitori corrispondente.  
  
     Per informazioni sulla configurazione di un contenitore Ciclo For, vedere [Configurazione di un contenitore Ciclo For](control-flow/for-loop-container.md).  
  
     Per informazioni sulla configurazione di un contenitore Ciclo Foreach, vedere [Configurazione di un contenitore Ciclo Foreach](control-flow/foreach-loop-container.md).  
  
    > [!NOTE]  
    >  Il contenitore Sequenza non dispone di un editor personalizzato.  
  
5.  Se l'editor attività o contenitori include più nodi, fare clic su quello che contiene la proprietà da impostare.  
  
6.  Facoltativamente, fare clic su **Espressioni** e, nella pagina **Espressioni** , creare espressioni di proprietà per aggiornare in modo dinamico le proprietà dell'attività o del contenitore. Per altre informazioni, vedere [Aggiunta o modifica di un'espressione di proprietà](expressions/add-or-change-a-property-expression.md).  
  
7.  Aggiornare il valore delle proprietà.  
  
8.  Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
## <a name="see-also"></a>Vedere anche  
 [Attività di Integration Services](control-flow/integration-services-tasks.md)   
 [Contenitori in Integration Services](control-flow/integration-services-containers.md)  
  
  
