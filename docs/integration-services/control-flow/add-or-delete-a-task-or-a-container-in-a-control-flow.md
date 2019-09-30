---
title: Aggiungere o eliminare un'attività o un contenitore in un flusso di controllo | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], adding
- adding tasks
- adding containers
- tasks [Integration Services], adding
ms.assetid: 653084c6-87a3-45d5-b458-914ecf24d56a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 76e7db001469b141df5633228927135c6d01af53
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298437"
---
# <a name="add-or-delete-a-task-or-a-container-in-a-control-flow"></a>Aggiunta o eliminazione di un'attività o un contenitore in un flusso di controllo

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Quando si usa la progettazione dei flussi di controllo, nella casella degli strumenti di Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] sono elencate le attività disponibili in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per la compilazione del flusso di controllo in un pacchetto. Per altre informazioni sulla casella degli strumenti, vedere [Casella degli strumenti SSIS](../../integration-services/ssis-toolbox.md).  
  
 Un pacchetto può includere più istanze della stessa attività. Ogni istanza di un'attività è univocamente identificata nel pacchetto e può avere una propria configurazione.  
  
 Se si elimina un'attività, verranno eliminati anche i vincoli di precedenza che la connettono ad altre attività e contenitori nel flusso di controllo.  
  
 Nelle procedure seguenti viene descritto come aggiungere o eliminare un'attività o un contenitore nel flusso di controllo di un pacchetto.  
  
## <a name="add-a-task-or-a-container-to-a-control-flow"></a>Aggiungere un'attività o un contenitore a un flusso di controllo  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di controllo** .  
  
4.  Per aprire la **casella degli strumenti**, scegliere **Casella degli strumenti** dal menu **Visualizza** .  
  
5.  Espandere **Elementi flusso di controllo** e **Attività di manutenzione**.  
  
6.  Trascinare attività e contenitori dalla **casella degli strumenti** all'area di progettazione della scheda **Flusso di controllo** .  
  
7.  Connettere un'attività o un contenitore nel flusso di controllo del pacchetto trascinandone il connettore fino a un altro componente nel flusso di controllo.  
  
8.  Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
## <a name="delete-a-task-or-a-container-from-a-control-flow"></a>Eliminare un'attività o un contenitore da un flusso di controllo  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo. Eseguire una delle operazioni seguenti:  
  
    -   Fare clic sulla scheda **Flusso di controllo** , fare clic con il pulsante destro del mouse sull'attività o il contenitore da rimuovere e quindi scegliere **Elimina**.  
  
    -   Aprire **Esplora pacchetti**. Nella cartella **File eseguibili** fare clic con il pulsante destro del mouse sull'attività o il contenitore da rimuovere e quindi scegliere **Elimina**.  
  
3.  Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  

## <a name="set-the-properties-of-a-task-or-container"></a>Impostare le proprietà di un'attività o di un contenitore
È possibile impostare la maggior parte delle proprietà delle attività e dei contenitori usando la finestra **Proprietà**. Fanno eccezione le proprietà delle raccolte di attività e quelle troppo complesse per essere impostate nella finestra **Proprietà**. L'enumeratore usato dal contenitore Ciclo Foreach, ad esempio, non può essere configurato nella finestra **Proprietà**. Per impostare tali proprietà complesse, è necessario utilizzare un editor attività o contenitori. La maggior parte degli editor attività e contenitori include più nodi, ognuno dei quali contiene proprietà correlate. Il nome del nodo indica l'oggetto delle proprietà contenute.  
  
 Le procedure seguenti descrivono come impostare le proprietà di un'attività o di un contenitore usando la finestra **Proprietà** o l'editor attività o contenitori corrispondente.  
  
### <a name="set-the-properties-of-a-task-or-container-with-the-properties-window"></a>Impostare le proprietà di un'attività o di un contenitore con la finestra Proprietà  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di controllo** .  
  
4.  Nell'area di progettazione della scheda **Flusso di controllo** fare clic con il pulsante destro del mouse sull'attività o sul contenitore, quindi scegliere **Proprietà**.  
  
5.  Nella finestra **Proprietà** aggiornare i valori delle proprietà.  
  
    > [!NOTE]  
    >  È possibile impostare la maggior parte delle proprietà digitando un valore direttamente nella casella di testo o selezionandone uno in un elenco. Alcune proprietà sono tuttavia più complesse e dispongono di un editor proprietà personalizzato. Per impostare la proprietà, fare clic nella casella di testo, quindi sul pulsante di compilazione **(...)** per aprire l'editor personalizzato.  
  
6.  Facoltativamente, creare espressioni di proprietà per aggiornare dinamicamente le proprietà dell'attività o del contenitore. Per altre informazioni, vedere [Aggiunta o modifica di un'espressione di proprietà](../../integration-services/expressions/add-or-change-a-property-expression.md).  
  
7.  Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
### <a name="set-the-properties-of-a-task-or-container-with-the-task-or-container-editor"></a>Impostare le proprietà di un'attività o di un contenitore con l'editor attività o contenitori  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di controllo** .  
  
4.  Nell'area di progettazione della scheda **Flusso di controllo** fare clic con il pulsante destro del mouse sull'attività o sul contenitore, quindi scegliere **Modifica** per aprire l'editor attività o contenitori corrispondente.  
  
     Per informazioni sulla configurazione di un contenitore Ciclo For, vedere [Configurazione di un contenitore Ciclo For](https://msdn.microsoft.com/library/b9cd7ea7-b198-4a35-8b16-6acf09611ca5).  
  
     Per informazioni sulla configurazione di un contenitore Ciclo Foreach, vedere [Configurazione di un contenitore Ciclo Foreach](https://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25).  
  
    > [!NOTE]  
    >  Il contenitore Sequenza non dispone di un editor personalizzato.  
  
5.  Se l'editor attività o contenitori include più nodi, fare clic su quello che contiene la proprietà da impostare.  
  
6.  Facoltativamente, fare clic su **Espressioni** e, nella pagina **Espressioni** , creare espressioni di proprietà per aggiornare in modo dinamico le proprietà dell'attività o del contenitore. Per altre informazioni, vedere [Aggiunta o modifica di un'espressione di proprietà](../../integration-services/expressions/add-or-change-a-property-expression.md).  
  
7.  Aggiornare il valore delle proprietà.  
  
8.  Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
## <a name="see-also"></a>Vedere anche  
 [Attività di Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Contenitori in Integration Services](../../integration-services/control-flow/integration-services-containers.md)   
 [Flusso di controllo](../../integration-services/control-flow/control-flow.md)  
  
  
