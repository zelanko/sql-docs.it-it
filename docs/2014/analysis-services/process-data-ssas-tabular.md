---
title: Elaborare dati (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d88f2dc9-2933-4be5-9bf3-48ffbc2d0a1a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0a0ca45681866e0ba96edaa81c21445a89f94275
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66070695"
---
# <a name="process-data-ssas-tabular"></a>Elaborare dati (SSAS tabulare)
  Quando si importano dati in un modello tabulare, nella modalità cache si acquisisce uno snapshot di tali dati al momento dell'importazione. In alcuni casi, tali dati potrebbero non cambiare mai, pertanto non devono essere aggiornati nel modello. Tuttavia, è più probabile che i dati che si importano cambino regolarmente, pertanto affinché il modello rifletta i dati più recenti delle origini dati, è necessario elaborarli (aggiornarli) e calcolare nuovamente i dati calcolati. Per aggiornare i dati nel modello, è necessario eseguire un'azione di elaborazione in tutte le tabelle, in una singola tabella, in base a una partizione o a una connessione all'origine dati.  
  
 Durante la creazione del progetto di modello, tutte le azioni di elaborazione devono essere avviate manualmente in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Dopo la distribuzione di un modello, le operazioni di elaborazione possono essere eseguite tramite [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] oppure pianificate utilizzando uno script. Tutte le attività descritte di seguito riguardano le azioni di elaborazione che è possibile eseguire durante la creazione di modelli in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Per altre informazioni sulle azioni di elaborazione per un modello distribuito, vedere [elaborare Database, tabella o partizione](tabular-models/process-database-table-or-partition-analysis-services.md).  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Elaborare manualmente i dati &#40;SSAS tabulare&#41;](manually-process-data-ssas-tabular.md)|Viene descritto come elaborare manualmente i dati dell'area di lavoro modello.|  
|[Risolvere i problemi relativi all'elaborazione dei dati &#40;SSAS tabulare&#41;](troubleshoot-process-data-ssas-tabular.md)|Viene descritto come risolvere i problemi relativi alle operazioni di elaborazione.|  
  
  
