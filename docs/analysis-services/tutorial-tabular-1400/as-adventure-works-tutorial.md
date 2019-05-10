---
title: Esercitazioni su Analysis Services Adventure Works Internet Sales (1400) | Microsoft Docs
ms.date: 05/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 39d4c0e19d89438aa08ff2f7ead24184196d5412
ms.sourcegitcommit: e4794943ea6d2580174d42275185e58166984f8c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65503280"
---
# <a name="adventure-works-internet-sales-tutorial-1400"></a>Esercitazione di Adventure Works Internet Sales (1400)

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

Questa esercitazione è incluse lezioni su come creare e distribuire un modello tabulare al [livello di compatibilità 1400](../tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md). Se si ha familiarità con Analysis Services e la modellazione tabulare, completare questa esercitazione è il modo più rapido per imparare a creare e distribuire un modello tabulare di base usando Visual Studio. Dopo aver ottenuto i prerequisiti sul posto, sono necessarie due o tre ore per il completamento.  
  
## <a name="what-you-learn"></a>Tutto ciò che Apprendi   
  
-   Come creare un nuovo progetto di modello tabulare al **livello di compatibilità 1400** in Visual Studio con SSDT.
  
-   Come importare dati da un database relazionale in un database modello tabulare dell'area di lavoro di progetto.  
  
-   Modalità di creazione e gestione delle relazioni tra tabelle nel modello.  
  
-   Come creare colonne calcolate, misure e indicatori di prestazioni chiave che consentono agli utenti di analizzare le metriche aziendali critiche.  
  
-   Come creare e gestire prospettive e gerarchie che consentono a più utenti di esplorare con facilità i dati del modello fornendo punti di vista specifici dell'applicazione e aziendali.  
  
-   Modalità di creazione di partizioni che consentono di dividere i dati della tabella in parti logiche più piccole che possono essere elaborate indipendentemente dalle altre partizioni.  
  
-   Modalità di protezione degli oggetti e dei dati del modello tramite la creazione di ruoli con membri utente.  
  
-   Come distribuire un modello tabulare da un **Azure Analysis Services** server oppure **SQL Server 2017 Analysis Services** server mediante SSDT.  
  
## <a name="prerequisites"></a>Prerequisiti  

Per completare questa esercitazione, è necessario:  
  
-   Un server Azure Analysis Services o un server di SQL Server 2017 Analysis Services in modalità tabulare. Iscriversi per ottenere una [versione di valutazione di Azure Analysis Services](https://azure.microsoft.com/services/analysis-services/) e [creare un server](https://docs.microsoft.com/azure/analysis-services/analysis-services-create-server) o il download gratuito [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).

-   Un' [Azure SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/create-data-warehouse-portal) con il **database AdventureWorksDW di esempio**, o un Data Warehouse di on-premise SQL Server con un [database di esempio AdventureWorksDW](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks). Durante l'installazione di un database AdventureWorksDW in un'istanza locale SQL Server Data Warehouse, usare la versione del database di esempio corrispondente con la versione di server. 

    **Importante:** Se si installa il database di esempio in locale SQL Server Data Warehouse e distribuire il modello a un server Azure Analysis Services, un' [gateway dati locale](https://docs.microsoft.com/azure/analysis-services/analysis-services-gateway) è obbligatorio.

-   La versione più recente di [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx). Oppure, se si dispone già di Visual Studio 2017, è possibile scaricare e installare [progetti di Microsoft Analysis Services](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects) pacchetto (VSIX). Per questa esercitazione, i riferimenti a Visual Studio e SSDT sono sinonimi. 

-   La versione più recente di [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).    

-   Un'applicazione client, ad esempio [Power BI Desktop](https://powerbi.microsoft.com/desktop/) o Excel. 

## <a name="scenario"></a>Scenario  

Questa esercitazione è basata su Adventure Works Cycles, una società fittizia. Adventure Works è una grande società multinazionale che produce e commercializza biciclette, componenti e accessori per mercati commerciali di America del Nord, Europa e Asia. L'azienda ha un organico 500 dipendenti. Inoltre, Adventure Works ha diversi team di vendita regionali di mercato. Il progetto consiste nel creare un modello tabulare agli utenti di vendite e marketing di analizzare i dati di vendite Internet nel database AdventureWorksDW.  
  
Per completare l'esercitazione, è necessario completare diverse lezioni. In ogni lezione, esistono attività. Completare ogni attività nell'ordine è necessario per il completamento della lezione. Mentre in una lezione specifica potrebbero esserci diverse attività che portano un risultato simile, ma come si completano ogni attività è leggermente diversa. Questa metodologia è spesso più di un modo per completare un'attività e che l'utente usando le competenze che apprese nelle lezioni precedenti e nelle attività.  
  
Lo scopo delle lezioni è guidare è durante la creazione di un modello tabulare di base usando alcune delle funzionalità incluse in SSDT. Poiché ogni lezione è basata su quella precedente, è necessario completare le lezioni in ordine.
  
Questa esercitazione non fornisce lezioni sulla gestione di un server nel portale di Azure, la gestione di un server o un database usando SQL Server Management Studio, o un'applicazione client di esplorare i dati del modello. 


## <a name="lessons"></a>Lezioni  

L'esercitazione include le lezioni seguenti:  
  
|Lezione|Tempo stimato per il completamento|  
|----------|------------------------------|  
|[1 - creare un nuovo progetto di modello tabulare](../tutorial-tabular-1400/as-lesson-1-create-a-new-tabular-model-project.md)|10 minuti|  
|[2 - Recuperare i dati](../tutorial-tabular-1400/as-lesson-2-get-data.md)|10 minuti|  
|[3 - Contrassegnare come tabella data](../tutorial-tabular-1400/as-lesson-3-mark-as-date-table.md)|3 minuti|  
|[4 - Creare relazioni](../tutorial-tabular-1400/as-lesson-4-create-relationships.md)|10 minuti|  
|[5 - Creare colonne calcolate](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md)|15 minuti|
|[6 - Creare misure](../tutorial-tabular-1400/as-lesson-6-create-measures.md)|30 minuti|  
|[7: creare indicatori di prestazioni chiave (KPI)](../tutorial-tabular-1400/as-lesson-7-create-key-performance-indicators.md)|15 minuti|  
|[8 - Creare prospettive](../tutorial-tabular-1400/as-lesson-8-create-perspectives.md)|5 minuti|  
|[9 - Creare gerarchie](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md)|20 minuti|  
|[10 - Creare partizioni](../tutorial-tabular-1400/as-lesson-10-create-partitions.md)|15 minuti|  
|[11 - Creare ruoli](../tutorial-tabular-1400/as-lesson-11-create-roles.md)|15 minuti|  
|[12 - Analizzare in Excel](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md)|5 minuti| 
|[13 - Distribuire](../tutorial-tabular-1400/as-lesson-13-deploy.md)|5 minuti|  
  
## <a name="supplemental-lessons"></a>Lezioni supplementari  

Queste lezioni non sono necessarie per completare l'esercitazione, ma possono essere utile per una migliore comprensione avanzate dei modelli tabulari le funzioni di modifica.  
  
|Lezione|Tempo stimato per il completamento|  
|----------|------------------------------|  
|[Righe di dettaglio](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)|10 minuti|
|[Sicurezza dinamica](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)|30 minuti|
|[Gerarchie incomplete](../tutorial-tabular-1400/as-supplemental-lesson-ragged-hierarchies.md)|20 minuti| 

  
## <a name="next-steps"></a>Passaggi successivi  

Per iniziare, vedere [lezione 1: Creare un nuovo progetto di modello tabulare](../tutorial-tabular-1400/as-lesson-1-create-a-new-tabular-model-project.md).  
  
  
  

