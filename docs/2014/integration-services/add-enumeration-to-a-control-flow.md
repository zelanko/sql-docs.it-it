---
title: Aggiungere l'enumerazione a un flusso di controllo | Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- adding enumerations
- Foreach Loop containers
- control flow [Integration Services], enumerations
- repeating workflows
- enumerations [Integration Services]
ms.assetid: f212b5fb-3cc4-422e-9b7c-89eb769a812a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: cad9c6a3537fb523a13f0206eed6c8eee837ed06
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66061906"
---
# <a name="add-enumeration-to-a-control-flow"></a>Aggiunta di un'enumerazione a un flusso di controllo
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] include il contenitore Ciclo Foreach, un elemento del flusso di controllo che semplifica l'integrazione di un costrutto di ciclo per l'enumerazione di file e oggetti nel flusso di controllo di un pacchetto. Per altre informazioni, vedere [Contenitore Ciclo Foreach](control-flow/foreach-loop-container.md).  
  
 Il contenitore Ciclo Foreach non offre funzionalità, ma solo una struttura in cui è possibile compilare un flusso di controllo ripetibile, nonché specificare e configurare un tipo di enumeratore. Per aggiungere funzionalità al contenitore Ciclo Foreach è necessario includervi almeno un'attività. Per altre informazioni, vedere [Attività di Integration Services](control-flow/integration-services-tasks.md).  
  
 Il contenitore Ciclo Foreach può includere un flusso di controllo con più attività e può includere altri contenitori. L'aggiunta di attività e contenitori a un contenitore Ciclo Foreach è analoga all'aggiunta di tali elementi a un pacchetto, con la differenza che è necessario trascinare attività e contenitori nel contenitore Ciclo Foreach anziché nel pacchetto. Se il contenitore Ciclo Foreach include più di un contenitore o attività, sarà possibile connettere tali elementi utilizzando vincoli di precedenza, come avviene nei pacchetti. Per altre informazioni, vedere [Vincoli di precedenza](control-flow/precedence-constraints.md).  
  
### <a name="to-implement-a-foreach-loop-container-in-a-control-flow"></a>Per implementare un contenitore Ciclo Foreach in un flusso di controllo  
  
1.  Aggiungere il contenitore Ciclo Foreach al pacchetto. Per altre informazioni, vedere [aggiunta o eliminazione di un'attività o un contenitore in un flusso di controllo](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  .  
  
2.  Aggiungere attività e contenitori al contenitore Ciclo Foreach. Per altre informazioni, vedere [aggiunta o eliminazione di un'attività o un contenitore in un flusso di controllo](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  .  
  
3.  Connettere le attività e i contenitori inclusi nel contenitore Ciclo Foreach tramite vincoli di precedenza. Per altre informazioni, vedere [Connessione di attività e contenitori tramite un vincolo di precedenza predefinito](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md).  
  
4.  Configurare il contenitore Ciclo Foreach. Per altre informazioni, vedere [Configurazione di un contenitore Ciclo Foreach](../../2014/integration-services/configure-a-foreach-loop-container.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiunta o eliminazione di un'attività o un contenitore in un flusso di controllo](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)   
 [Raggruppare o separare componenti](group-or-ungroup-components.md)   
 [Vincoli di precedenza](control-flow/precedence-constraints.md)   
 [Aggiungere un'iterazione a un flusso di controllo](add-iteration-to-a-control-flow.md)   
 [Flusso di controllo](control-flow/control-flow.md)  
  
  
