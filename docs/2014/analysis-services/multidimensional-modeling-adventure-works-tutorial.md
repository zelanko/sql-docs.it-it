---
title: Modellazione multidimensionale (esercitazione di Adventure Works) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- tutorials [Analysis Services]
- Analysis Services, tutorials
ms.assetid: db55e226-601a-4026-8651-573195555a59
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 174d4ab61cf56f4916babb1639e110162d20e6fd
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66077576"
---
# <a name="multidimensional-modeling-adventure-works-tutorial"></a>Modellazione multidimensionale (esercitazione di AdventureWorks)
  Introduzione all'esercitazione [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial. In questa esercitazione viene descritto come utilizzare [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] per sviluppare e distribuire un progetto di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] utilizzando la società fittizia [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] per tutti gli esempi.  
  
## <a name="what-you-will-learn"></a>Lezioni dell'esercitazione  
 In questa esercitazione verranno illustrate le operazioni seguenti:  
  
-   Come definire origini dati, viste origine dati, dimensioni, attributi, relazioni tra attributi, gerarchie e cubi in un progetto di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] all'interno di [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
  
-   Come visualizzare dati di dimensioni e cubi distribuendo il progetto di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] in un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]e come elaborare gli oggetti distribuiti per popolarli con i dati dell'origine dati sottostante.  
  
-   Come modificare le misure, le dimensioni, le gerarchie, gli attributi e i gruppi di misure nel progetto di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e come distribuire le modifiche incrementali al cubo distribuito nel server di sviluppo.  
  
-   Come definire calcoli, indicatori di prestazioni chiave (KPI), azioni, prospettive, traduzioni e ruoli di sicurezza in un cubo.  
  
 Con questa esercitazione viene fornita una descrizione dello scenario in modo da comprendere meglio il contesto di queste lezioni. Per ulteriori informazioni, vedere [Analysis Services Tutorial Scenario](analysis-services-tutorial-scenario.md).  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per completare tutte le lezioni di questa esercitazione sono necessari dati di esempio, file di progetto di esempio e software specifici. Per istruzioni su come trovare e installare i prerequisiti per questa esercitazione, vedere [Install Sample Data and Projects for the Analysis Services Multidimensional Modeling Tutorial](install-sample-data-and-projects.md).  
  
 Per completare questa esercitazione sono inoltre necessarie le autorizzazioni seguenti:  
  
-   È necessario essere membro del gruppo Administrators nel computer locale di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o membro del ruolo di amministrazione del server nell'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
-   È necessario disporre di autorizzazioni di lettura per il database di esempio **AdventureWorksDW2012** . Questo database di esempio è valido per la versione [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] .  
  
## <a name="lessons"></a>Lezioni  
 L'esercitazione include le lezioni seguenti.  
  
|Lezione|Tempo previsto per il completamento|  
|------------|--------------------------------|  
|[Lezione 1: Definizione di una vista origine dati in un progetto di Analysis Services](lesson-1-defining-a-data-source-view-within-an-analysis-services-project.md)|15 minuti|  
|[Lezione 2: Definizione e distribuzione di un cubo](lesson-2-defining-and-deploying-a-cube.md)|30 minuti|  
|[Lezione 3: Modifica di misure, attributi e gerarchie](lesson-3-modifying-measures-attributes-and-hierarchies.md)|45 minuti|  
|[Lezione 4: Definizione delle proprietà avanzate di attributi e dimensioni](lesson-4-defining-advanced-attribute-and-dimension-properties.md)|120 minuti|  
|[Lezione 5: Definizione delle relazioni tra dimensioni e gruppi di misure](lesson-5-defining-relationships-between-dimensions-and-measure-groups.md)|45 minuti|  
|[Lezione 6: Definizione di calcoli](lesson-6-defining-calculations.md)|45 minuti|  
|[Lezione 7: Definizione degli indicatori di prestazioni chiave &#40;KPI&#41;](lesson-7-defining-key-performance-indicators-kpis.md)|30 minuti|  
|[Lezione 8: Definizione di azioni](lesson-8-defining-actions.md)|30 minuti|  
|[Lezione 9: Definizione di prospettive e traduzioni](lesson-9-defining-perspectives-and-translations.md)|30 minuti|  
|[Lezione 10: Definizione dei ruoli amministrativi](lesson-10-defining-administrative-roles.md)|15 minuti|  
  
> [!NOTE]  
>  Il database del cubo che verrà creato in questa esercitazione è una versione semplificata del progetto di modello multidimensionale di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] che fa parte dei database di esempio di Adventure Works disponibile per il download sul sito codeplex. La versione per l'esercitazione del database multidimensionale Adventure Works è semplificata per focalizzare maggiormente l'attenzione sulle specifiche competenze con cui si desidera subito familiarizzare. Dopo avere completato l'esercitazione, esplorare il progetto di modello multidimensionale per proprio conto per accrescere la comprensione della modellazione multidimensionale in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
## <a name="next-step"></a>passaggio successivo  
 Per iniziare questa esercitazione, passare alla prima lezione: [Lesson 1: Defining a Data Source View within an Analysis Services Project](lesson-1-defining-a-data-source-view-within-an-analysis-services-project.md).  
  
  
