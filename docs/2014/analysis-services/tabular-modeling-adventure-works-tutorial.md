---
title: Modellazione tabulare (esercitazione di Adventure Works) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 140d0b43-9455-4907-9827-16564a904268
author: minewiskan
ms.author: owend
ms.openlocfilehash: d914595c5c62016efca26dece908ee28b7010706
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940012"
---
# <a name="tabular-modeling-adventure-works-tutorial"></a>Modellazione tabulare (esercitazione di AdventureWorks)
  In questa esercitazione sono incluse lezioni sulla creazione di un [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] modello tabulare di Analysis Services tramite [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
## <a name="what-you-will-learn"></a>Lezioni dell'esercitazione  
 Durante questa esercitazione verranno appresi i concetti seguenti:  
  
-   Modalità di creazione di un nuovo progetto di modello tabulare in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
  
-   Modalità di importazione dei dati da un database relazionale di SQL Server a un progetto di modello tabulare.  
  
-   Modalità di creazione e gestione delle relazioni tra tabelle nel modello.  
  
-   Modalità di creazione e gestione di calcoli, misure e indicatori di prestazioni chiave per l'analisi dei dati del modello.  
  
-   Modalità di creazione e gestione di prospettive e gerarchie che semplificano l'esplorazione dei dati del modello fornendo punti di vista specifici dell'applicazione e dell'azienda.  
  
-   Modalità di creazione di partizioni che consentono di dividere i dati della tabella in parti logiche più piccole che possono essere elaborate indipendentemente dalle altre partizioni.  
  
-   Modalità di protezione degli oggetti e dei dati del modello tramite la creazione di ruoli con membri utente.  
  
-   Modalità di distribuzione di un modello tabulare in un'istanza di produzione o sandbox di Analysis Services in esecuzione in modalità tabulare.  
  
## <a name="tutorial-scenario"></a>Scenario dell'esercitazione  
 Questa esercitazione si riferisce alla società fittizia [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]. [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] è una multinazionale che produce e commercializza biciclette in acciaio e in materiali compositi sui mercati dell'America del Nord, dell'Europa e dell'Asia. La sede centrale di [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] si trova a Bothell, nello stato di Washington, e vi lavorano 500 dipendenti. [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] dispone inoltre di numerosi team di vendita dislocati nelle diverse aree di mercato.  
  
 Per offrire un supporto migliore per le esigenze di analisi dei dati di team di vendita e marketing e dei responsabili, si desidera creare un modello tabulare che consenta agli utenti di analizzare i dati relativi alle vendite Internet nel database di esempio AdventureWorksDW.  
  
 Per completare l'esercitazione e il modello tabulare relativo alle vendite Internet di Adventure Works, è necessario completare diverse lezioni. Ogni lezione include specifiche attività; il completamento di ogni attività nell'ordine previsto è necessario per portare a termine la lezione. Sebbene in una lezione specifica potrebbero essere presenti diverse attività che portano a un risultato simile, la modalità di completamento di ogni attività è leggermente diversa. L'obiettivo è quello di mostrare come spesso vi sia più di un modo per completare una determinata attività e di incentivare l'utilizzo di nozioni apprese nelle attività precedenti.  
  
 Lo scopo delle lezioni è quello di assistere l'utente nella creazione di un modello tabulare di base in esecuzione nella modalità In-Memory utilizzando numerose funzionalità incluse in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Poiché ogni lezione è basata su quella precedente, è necessario completare le lezioni in ordine. Dopo aver completato tutte le lezioni, sarà stato creato e distribuito il modello tabulare di esempio di Adventure Works relativo alle vendite Internet in un server Analysis Services.  
  
> [!NOTE]  
>  Questa esercitazione non fornisce lezioni o informazioni sulla gestione di un database di modello tabulare distribuito tramite SQL Server Management Studio o sull'utilizzo di un'applicazione client di creazione di report per la connessione a un modello distribuito per l'esplorazione dei dati del modello.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per completare l'esercitazione, è necessario che siano installati i prerequisiti seguenti:  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Istanza di Analysis Services in esecuzione nella modalità tabulare.  
  
-   [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
-   Database di esempio AdventureWorksDW. Questo database di esempio include i dati necessari per completare questa esercitazione. Per scaricare il database di esempio, vedere [https://github.com/microsoft/sql-server-samples/releases/tag/adventureworks](https://github.com/microsoft/sql-server-samples/releases/tag/adventureworks) .  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel 2003 o versione successiva (per l'utilizzo con la funzionalità Analizza in Excel nella lezione 11)  
  
## <a name="lessons"></a>Lezioni  
 L'esercitazione include le lezioni seguenti:  
  
|Lezione|Tempo previsto per il completamento|  
|------------|--------------------------------|  
|[Lezione 1: Creare un nuovo modello di progetto tabulare](lesson-1-create-a-new-tabular-model-project.md)|10 minuti|  
|[Lezione 2: Aggiungere dati](lesson-2-add-data.md)|20 minuti|  
|[Lezione 3: Rinominare colonne](rename-columns.md)|20 minuti|  
|[Lezione 4: Contrassegna come tabella data](lesson-3-mark-as-date-table.md)|3 minuti|  
|[Lezione 5: Crea relazioni](lesson-4-create-relationships.md)|10 minuti|  
|[Lezione 6: Creare colonne calcolate](lesson-5-create-calculated-columns.md)|15 minuti|  
|[Lezione 7: Creare misure](lesson-6-create-measures.md)|30 minuti|  
|[Lezione 8: Creare indicatori di prestazioni chiave](lesson-7-create-key-performance-indicators.md)|15 minuti|  
|[Lezione 9: Creare prospettive](lesson-8-create-perspectives.md)|5 minuti|  
|[Lezione 10: Creare gerarchie](lesson-9-create-hierarchies.md)|20 minuti|  
|[Lezione 11: Creare partizioni](lesson-10-create-partitions.md)|15 minuti|  
|[Lezione 12: Creazione di ruoli](lesson-11-create-roles.md)|15 minuti|  
|[Lezione 13: Analizza in Excel](lesson-12-analyze-in-excel.md)|20 minuti|  
|[Lezione 14: Distribuire](lesson-13-deploy.md)|5 minuti|  
  
## <a name="supplemental-lessons"></a>Lezioni supplementari  
 In questa esercitazione sono incluse [Lezioni supplementari](../tutorials/supplemental-lessons.md). Gli argomenti di questa sezione non sono necessari per completare l'esercitazione, ma possono risultare utili per comprendere meglio le funzionalità avanzate di creazione dei modelli tabulari.  
  
 L'esercitazione include le lezioni supplementari seguenti:  
  
|Lezione|Tempo previsto per il completamento|  
|------------|--------------------------------|  
|[Implementare la sicurezza dinamica mediante i filtri di riga](../tutorials/implement-dynamic-security-by-using-row-filters.md)|30 minuti|  
|[Configurare le proprietà dei report per Power View report](supplemental-lesson-configure-reporting-properties-for-power-view-reports.md) Configurare le proprietà dei report per Power View report|30 minuti|  
  
## <a name="next-step"></a>passaggio successivo  
 Per iniziare l'esercitazione, passare alla prima lezione: [Lezione 1: Creare un nuovo modello di progetto tabulare](lesson-1-create-a-new-tabular-model-project.md).  
  
  
