---
title: Esercitazioni su Analysis Services Internet Sales (livello di compatibilità 1200) | Microsoft Docs
ms.date: 05/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 06b3aace2320882d209e6a7ab0f67a16a6f8a6df
ms.sourcegitcommit: e4794943ea6d2580174d42275185e58166984f8c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65503625"
---
# <a name="adventure-works-internet-sales-tutorial-1200"></a>Esercitazione di Adventure Works Internet Sales (1200)
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

Questa esercitazione è incluse lezioni sulla creazione di un modello tabulare di Analysis Services al [livello di compatibilità 1200](../tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md) utilizzando [SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)e distribuisce il modello in Analysis Services server in locale o in Azure.  
 
Se si usa Azure Analysis Services o SQL Server 2017 e si vuole creare a livello del modello di compatibilità 1400, usare il [(livello di compatibilità 1400) di modellazione tabulare](../tutorial-tabular-1400/as-adventure-works-tutorial.md). Questa versione aggiornata Usa la funzionalità Recupera dati moderna per connettersi e importare i dati di origine, Usa il linguaggio di M per configurare le partizioni e include lezioni supplementari aggiuntive.

> [!IMPORTANT]
> È consigliabile creare i modelli tabulari a livello di compatibilità più recente supportato dal server. Modelli con livello di compatibilità delle versioni successive offrono prestazioni migliori, funzionalità aggiuntive e verranno aggiornate più facilmente ai livelli di compatibilità futura.
 
  
## <a name="what-you-learn"></a>Tutto ciò che Apprendi   
  
-   Come creare un nuovo progetto di modello tabulare in SSDT.
  
-   Modalità di importazione dei dati da un database relazionale di SQL Server a un progetto di modello tabulare.  
  
-   Modalità di creazione e gestione delle relazioni tra tabelle nel modello.  
  
-   Modalità di creazione e gestione di calcoli, misure e indicatori di prestazioni chiave per l'analisi dei dati del modello.  
  
-   Come creare e gestire prospettive e gerarchie che consentono a più utenti di esplorare con facilità i dati del modello fornendo punti di vista specifici dell'applicazione e aziendali.  
  
-   Come creare le partizioni dividere i dati della tabella in parti logiche più piccole, che possono essere elaborate indipendente dalle altre partizioni.  
  
-   Modalità di protezione degli oggetti e dei dati del modello tramite la creazione di ruoli con membri utente.  
  
-   Come distribuire un modello tabulare, un server di Analysis Services in locale o in Azure.  
  
## <a name="scenario"></a>Scenario  
Questa esercitazione è basata su Adventure Works Cycles, una società fittizia. Adventure Works è una grande società multinazionale che produce biciclette, componenti e accessori per mercati commerciali di America del Nord, Europa e Asia. Con sede a Bothell, Washington, l'azienda ha un organico 500 dipendenti. Inoltre, Adventure Works ha diversi team di vendita regionali di mercato.  
  
Per offrire un supporto migliore per le esigenze di analisi dei dati di team di vendita e marketing e dei responsabili, si desidera creare un modello tabulare che consenta agli utenti di analizzare i dati relativi alle vendite Internet nel database di esempio AdventureWorksDW.  
  
Per completare l'esercitazione e il modello tabulare relativo alle vendite Internet di Adventure Works, è necessario completare diverse lezioni. In ogni lezione è un numero di attività. completare ogni attività nell'ordine è necessario per il completamento della lezione. Mentre in una lezione specifica potrebbero esserci diverse attività che portano un risultato simile, ma come si completano ogni attività è leggermente diversa. Ciò sta a indicare che è spesso più di un modo per completare una determinata attività e che l'utente usando le competenze che apprese nelle attività precedenti.  
  
Lo scopo delle lezioni è guidare è durante la creazione di un modello tabulare di base in esecuzione nella modalità In-Memory utilizzando numerose funzionalità incluse in SSDT. Poiché ogni lezione è basata su quella precedente, è necessario completare le lezioni in ordine. Dopo aver completato tutte le lezioni, aver creato e distribuito il modello tabulare di esempio Adventure Works Internet Sales in un server Analysis Services.  
  
Questa esercitazione non fornisce lezioni o informazioni sulla gestione di un database di modello tabulare distribuito tramite SQL Server Management Studio o sull'utilizzo di un'applicazione client di creazione di report per la connessione a un modello distribuito per l'esplorazione dei dati del modello.  
  
## <a name="prerequisites"></a>Prerequisiti  
Per completare questa esercitazione, sono necessari i prerequisiti seguenti:  
  
-   La versione più recente di [SSDT](../../ssdt/download-sql-server-data-tools-ssdt.md).

-   La versione più recente di SQL Server Management Studio. [Ottenere la versione più recente](../../ssms/download-sql-server-management-studio-ssms.md). 
  
-   Un'applicazione client, ad esempio [Power BI Desktop](https://powerbi.microsoft.com/desktop/) o Excel.    
  
-   Un'istanza di SQL Server con il database di esempio Adventure Works DW. Questo database di esempio include i dati necessari per completare questa esercitazione. [Ottenere la versione più recente](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks).  
  

-   Un Azure Analysis Services o SQL Server 2016 o versione successiva istanza di Analysis Services per distribuire il modello a. [Iscriversi a una versione di valutazione gratuita di Azure Analysis Services](https://azure.microsoft.com/services/analysis-services/).
  
## <a name="lessons"></a>Lezioni  
L'esercitazione include le lezioni seguenti:  
  
|Lezione|Tempo stimato per il completamento|  
|----------|------------------------------|  
|[Lezione 1: Creare un nuovo progetto di modello tabulare](lesson-1-create-a-new-tabular-model-project.md)|10 minuti|  
|[Lezione 2: Aggiungere dati](lesson-2-add-data.md)|20 minuti|  
|[Lezione 3: Contrassegna come tabella data](lesson-3-mark-as-date-table.md)|3 minuti|  
|[Lezione 4: Creare relazioni](lesson-4-create-relationships.md)|10 minuti|  
|[Lezione 5: Creare colonne calcolate](lesson-5-create-calculated-columns.md)|15 minuti|
|[Lezione 6: Creare misure](lesson-6-create-measures.md)|30 minuti|  
|[Lezione 7: Creare indicatori di prestazioni chiave](lesson-7-create-key-performance-indicators.md)|15 minuti|  
|[Lezione 8: Creare prospettive](lesson-8-create-perspectives.md)|5 minuti|  
|[Lezione 9: Creare gerarchie](lesson-9-create-hierarchies.md)|20 minuti|  
|[Lezione 10: Creare partizioni](lesson-10-create-partitions.md)|15 minuti|  
|[Lezione 11: Creare ruoli](lesson-11-create-roles.md)|15 minuti|  
|[Lezione 12: Analizza in Excel](lesson-12-analyze-in-excel.md)|20 minuti| 
|[Lezione 13: Distribuire](lesson-13-deploy.md)|5 minuti|  
  
## <a name="supplemental-lessons"></a>Lezioni supplementari  
Questa esercitazione sono incluse lezioni supplementari. Gli argomenti di questa sezione non sono necessari per completare l'esercitazione, ma possono risultare utili per comprendere meglio le funzionalità avanzate di creazione dei modelli tabulari.  
  
|Lezione|Tempo stimato per il completamento|  
|----------|------------------------------|  
|[Implementare la sicurezza dinamica mediante i filtri di riga](supplemental-lesson-implement-dynamic-security-by-using-row-filters.md)|30 minuti|  
|[Configurare le proprietà di creazione di report per i report Power View](supplemental-lesson-configure-reporting-properties-for-power-view-reports.md)|30 minuti| 

  
## <a name="next-steps"></a>Passaggi successivi  
Per iniziare l'esercitazione, passare alla prima lezione: [Lezione 1: Creare un nuovo progetto di modello tabulare](lesson-1-create-a-new-tabular-model-project.md).  
  
  
  

