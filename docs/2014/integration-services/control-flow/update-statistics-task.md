---
title: Attività Aggiorna statistiche | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.updatestatisticstask.f1
helpviewer_keywords:
- updating statistics
- Update Statistics task [Integration Services]
ms.assetid: 0247483b-f092-4511-8fa8-3610108bd1bc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: be80af34bc2dc8b5d069406bc13a8f8f9b25c42c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62829450"
---
# <a name="update-statistics-task"></a>Attività Aggiorna statistiche
  L'attività Aggiorna statistiche consente di aggiornare le informazioni sulla distribuzione dei valori di chiave per uno o più gruppi o raccolte di statistiche nella tabella o vista indicizzata specificata. Per altre informazioni, vedere [Statistics](../../relational-databases/statistics/statistics.md).  
  
 Tramite l'attività Aggiorna statistiche un pacchetto può aggiornare le statistiche per uno o più database. Se si utilizza l'attività per aggiornare le statistiche in un singolo database, sarà possibile scegliere le viste e le tabelle di cui aggiornare le statistiche. È possibile configurare l'attività in modo da aggiornare tutte le statistiche, solo le statistiche delle colonne oppure solo le statistiche degli indici.  
  
 L'attività incapsula un'istruzione UPDATE STATISTICS che include le clausole e gli argomenti seguenti:  
  
-   Argomento *table_name* o *view_name* .  
  
-   Se l'aggiornamento interessa tutte le statistiche, è implicita la clausola WITH ALL.  
  
-   Se l'aggiornamento interessa solo le colonne, viene inclusa la clausola WITH COLUMN.  
  
-   Se l'aggiornamento interessa solo gli indici, viene inclusa la clausola WITH INDEX.  
  
 Se l'attività Aggiorna statistiche viene utilizzata per aggiornare statistiche in più database, eseguirà più istruzioni UPDATE STATISTICS, una per ogni tabella o vista. Tutte le istanze dell'istruzione UPDATE STATISTICS usano la stessa clausola ma valori di *table_name* o *view_name* diversi. Per altre informazioni, vedere [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql) e [UPDATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/update-statistics-transact-sql).  
  
> [!IMPORTANT]  
>  Il tempo richiesto dall'attività per creare l'istruzione Transact-SQL da eseguire è proporzionale al numero delle statistiche da aggiornare. Se l'attività è configurata per l'aggiornamento delle statistiche in tutte le tabelle e le viste di un database con un numero elevato di indici oppure per l'aggiornamento delle statistiche in più database, la generazione dell'istruzione Transact-SQL potrebbe richiedere una quantità di tempo considerevole.  
  
## <a name="configuration-of-the-update-statistics-task"></a>Configurazione dell'attività Aggiorna statistiche  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] . Questa attività è disponibile nella sezione **Attività di manutenzione** della **casella degli strumenti** di Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] .  
  
 Per informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Attività Aggiorna statistiche &#40;Piano di manutenzione&#41;](../../relational-databases/maintenance-plans/update-statistics-task-maintenance-plan.md)  
  
## <a name="related-tasks"></a>Attività correlate  
 Per altre informazioni sull'impostazione di queste proprietà in Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Impostazione delle proprietà di un'attività o di un contenitore](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Attività di Integration Services](integration-services-tasks.md)   
 [Flusso di controllo](control-flow.md)  
  
  
