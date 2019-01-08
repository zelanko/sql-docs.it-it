---
title: Attività Esegui istruzione T-SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executetsqlstatementtask.f1
helpviewer_keywords:
- Transact-SQL statements, SSIS
- statements [Integration Services]
- Execute T-SQL Statement task [Integration Services]
ms.assetid: 7e9086ca-d27e-46c0-bfad-d61333ebd55e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c578c07c1e20331d2b2b302619cfc95b9463a639
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52767313"
---
# <a name="execute-t-sql-statement-task"></a>Attività Esegui istruzione T-SQL
  L'attività Esegui istruzione T-SQL consente di eseguire istruzioni Transact-SQL. Per altre informazioni, vedere [Guida di riferimento a Transact-SQL &#40;Motore di database&#41;](/sql/t-sql/language-reference) e [Query di Integration Services &#40;SSIS&#41;](../integration-services-ssis-queries.md).  
  
 Questa attività è simile all'attività Esegui SQL, ma supporta solo la versione Transact-SQL del linguaggio SQL e non può essere utilizzata per eseguire istruzioni su server che utilizzano altri sottolinguaggi del linguaggio SQL. Se è necessario eseguire query con parametri, salvare i risultati delle query nelle variabili oppure utilizzare espressioni di proprietà, è necessario utilizzare l'attività Esegui SQL anziché l'attività Esegui istruzione T-SQL. Per altre informazioni, vedere [Attività Esegui SQL](execute-sql-task.md).  
  
## <a name="configuration-of-the-execute-t-sql-task"></a>Configurazione dell'attività Esegui istruzione T-SQL  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] . Questa attività è disponibile nella sezione **Attività di manutenzione** della **casella degli strumenti** di Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] .  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Attività Esegui istruzione T-SQL &#40;Piano di manutenzione&#41;](../../relational-databases/maintenance-plans/execute-t-sql-statement-task-maintenance-plan.md)  
  
 Per altre informazioni sull'impostazione di queste proprietà in Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Impostazione delle proprietà di un'attività o di un contenitore](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Attività di Integration Services](integration-services-tasks.md)   
 [Flusso di controllo](control-flow.md)   
 [MERGE in Integration Services Packages](merge-in-integration-services-packages.md)  
  
  
