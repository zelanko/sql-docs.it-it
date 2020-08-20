---
description: Host delle attività - contenitore
title: Contenitore Host delle attività | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.taskhostcontainer.f1
helpviewer_keywords:
- containers [Integration Services], Task Host
- Task Host container
ms.assetid: 7394a2c2-1b07-427d-b94a-9792e7783d35
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fd2ab8fe157992077618f426f68931c8c87d8ed7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495994"
---
# <a name="task-host-container"></a>Host delle attività - contenitore

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Il contenitore host delle attività incapsula una singola attività. In Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] il contenitore host delle attività non viene configurato separatamente, ma viene configurato quando si impostano le proprietà dell'attività incapsulata. Per altre informazioni sulle attività incapsulate nel contenitore Host delle attività, vedere [Attività di Integration Services](../../integration-services/control-flow/integration-services-tasks.md).  
  
 Questo contenitore estende al livello delle attività l'utilizzo di gestori di eventi e variabili. Per altre informazioni, vedere [Gestori eventi di Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-event-handlers.md) e [Variabili di Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md).  
  
## <a name="configuration-of-the-task-host"></a>Configurazione dell'Host attività  
 È possibile impostare le proprietà a livello di codice o nella finestra **Proprietà** di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] .  
  
 Per informazioni sull'impostazione di queste proprietà in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], vedere [Impostazione delle proprietà di un'attività o di un contenitore](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b).  
  
 Per informazioni sull'impostazione di queste proprietà a livello di codice, vedere <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>.  
  
## <a name="related-tasks"></a>Attività correlate  
  
-   [Impostazione delle proprietà di un'attività o di un contenitore](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="see-also"></a>Vedere anche  
 [Contenitori in Integration Services](../../integration-services/control-flow/integration-services-containers.md)  
  
  
