---
title: Aggiungere o eliminare un'attività o un contenitore in un flusso di controllo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], adding
- adding tasks
- adding containers
- tasks [Integration Services], adding
ms.assetid: 653084c6-87a3-45d5-b458-914ecf24d56a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f13db8a1e22c88c4433cd8928479a6ed1af540f6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62833136"
---
# <a name="add-or-delete-a-task-or-a-container-in-a-control-flow"></a>Aggiunta o eliminazione di un'attività o un contenitore in un flusso di controllo
  Quando si usa la progettazione dei flussi di controllo, nella casella degli strumenti di Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] sono elencate le attività disponibili in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per la compilazione del flusso di controllo in un pacchetto. Per altre informazioni sulla casella degli strumenti, vedere [Casella degli strumenti SSIS](../ssis-toolbox.md).  
  
 Un pacchetto può includere più istanze della stessa attività. Ogni istanza di un'attività è univocamente identificata nel pacchetto e può avere una propria configurazione.  
  
 Se si elimina un'attività, verranno eliminati anche i vincoli di precedenza che la connettono ad altre attività e contenitori nel flusso di controllo.  
  
 Nelle procedure seguenti viene descritto come aggiungere o eliminare un'attività o un contenitore nel flusso di controllo di un pacchetto.  
  
### <a name="to-add-a-task-or-a-container-to-a-control-flow"></a>Per aggiungere un'attività o un contenitore a un flusso di controllo  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di controllo** .  
  
4.  Per aprire la **casella degli strumenti**, scegliere **Casella degli strumenti** dal menu **Visualizza** .  
  
5.  Espandere **Elementi flusso di controllo** e **Attività di manutenzione**.  
  
6.  Trascinare attività e contenitori dalla **casella degli strumenti** all'area di progettazione della scheda **Flusso di controllo** .  
  
7.  Connettere un'attività o un contenitore nel flusso di controllo del pacchetto trascinandone il connettore fino a un altro componente nel flusso di controllo.  
  
8.  Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
### <a name="to-delete-a-task-or-a-container-from-a-control-flow"></a>Per eliminare un'attività o un contenitore da un flusso di controllo  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo. Eseguire una delle operazioni seguenti:  
  
    -   Fare clic sulla scheda **Flusso di controllo** , fare clic con il pulsante destro del mouse sull'attività o il contenitore da rimuovere e quindi scegliere **Elimina**.  
  
    -   Aprire **Esplora pacchetti**. Nella cartella **File eseguibili** fare clic con il pulsante destro del mouse sull'attività o il contenitore da rimuovere e quindi scegliere **Elimina**.  
  
3.  Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
## <a name="see-also"></a>Vedere anche  
 [Attività di Integration Services](integration-services-tasks.md)   
 [Contenitori in Integration Services](integration-services-containers.md)   
 [Flusso di controllo](control-flow.md)  
  
  
