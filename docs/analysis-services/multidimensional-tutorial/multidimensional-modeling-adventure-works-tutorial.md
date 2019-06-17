---
title: Modellazione multidimensionale (esercitazione Adventure) | Microsoft Docs
ms.date: 05/06/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 98e995a89f9993a54736c4966639fd583e2391b6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65403723"
---
# <a name="multidimensional-modeling-adventure-works-tutorial"></a>Modellazione multidimensionale (esercitazione di AdventureWorks)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

Introduzione all'esercitazione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Tutorial. In questa esercitazione viene descritto come utilizzare [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] per sviluppare e distribuire un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilizzando la società fittizia [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] per tutti gli esempi.  
  
## <a name="what-you-learn"></a>Tutto ciò che Apprendi  
In questa esercitazione verranno illustrate le operazioni seguenti:  
  
-   Come definire origini dati, viste origine dati, dimensioni, attributi, relazioni tra attributi, gerarchie e cubi in un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] all'interno di [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
-   Come visualizzare dati di dimensioni e cubi distribuendo il progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]e come elaborare gli oggetti distribuiti per popolarli con i dati dell'origine dati sottostante.  
  
-   Come modificare le misure, le dimensioni, le gerarchie, gli attributi e i gruppi di misure nel progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e come distribuire le modifiche incrementali al cubo distribuito nel server di sviluppo.  
  
-   Come definire calcoli, indicatori di prestazioni chiave (KPI), azioni, prospettive, traduzioni e ruoli di sicurezza in un cubo.  
  
Con questa esercitazione viene fornita una descrizione dello scenario in modo da comprendere meglio il contesto di queste lezioni. Per ulteriori informazioni, vedere [Scenario di Analysis Services Tutorial](analysis-services-tutorial-scenario.md).  
  
## <a name="prerequisites"></a>Prerequisiti  
Per completare tutte le lezioni di questa esercitazione sono necessari dati di esempio, file di progetto di esempio e software specifici. Per istruzioni su come trovare e installare i prerequisiti per questa esercitazione, vedere [Installare dati di esempio e progetti per l'esercitazione di modellazione multidimensionale di Analysis Services](install-sample-data-and-projects.md).  
  
Per completare questa esercitazione sono inoltre necessarie le autorizzazioni seguenti:  
  
-   È necessario essere membro del gruppo Administrators nel computer locale di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o membro del ruolo di amministrazione del server nell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
-   È necessario avere autorizzazioni di lettura il **AdventureWorksDW** database di esempio. Questo database di esempio è valido per la versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
## <a name="lessons"></a>Lezioni  
L'esercitazione include le lezioni seguenti.  
  
|Lezione|Tempo stimato per il completamento|  
|----------|------------------------------|  
|[Lezione 1: Definizione di una vista origine dati all'interno di un'analisi di progetto di servizi](lesson-1-defining-a-data-source-view-within-an-analysis-services-project.md)|15 minuti|  
|[Lezione 2: Definizione e distribuzione di un cubo](lesson-2-defining-and-deploying-a-cube.md)|30 minuti|  
|[Lezione 3: Modifica le misure, attributi e gerarchie](lesson-3-modifying-measures-attributes-and-hierarchies.md)|45 minuti|  
|[Lezione 4: La definizione di attributo avanzato e proprietà dimensione](lesson-4-defining-advanced-attribute-and-dimension-properties.md)|120 minuti|  
|[Lezione 5: Definizione delle relazioni tra dimensioni e gruppi di misure](lesson-5-defining-relationships-between-dimensions-and-measure-groups.md)|45 minuti|  
|[Lezione 6: Definizione di calcoli](lesson-6-defining-calculations.md)|45 minuti|  
|[Lezione 7: Definizione degli indicatori di prestazioni chiave &#40;indicatori KPI&#41;](lesson-7-defining-key-performance-indicators-kpis.md)|30 minuti|  
|[Lezione 8: Definizione delle azioni](lesson-8-defining-actions.md)|30 minuti|  
|[Lezione 9: Definizione di prospettive e traduzioni](lesson-9-defining-perspectives-and-translations.md)|30 minuti|  
|[Lezione 10: Definizione dei ruoli amministrativi](lesson-10-defining-administrative-roles.md)|15 minuti|  
  
> [!NOTE]  
> Il database del cubo che verrà creato in questa esercitazione è una versione semplificata del [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] progetto di modello multidimensionale che fa parte dei database di esempio Adventure Works disponibili per il download in GitHub. La versione per l'esercitazione del database multidimensionale Adventure Works è semplificata per focalizzare maggiormente l'attenzione sulle specifiche competenze con cui si desidera subito familiarizzare. Dopo avere completato l'esercitazione, esplorare il progetto di modello multidimensionale per proprio conto per accrescere la comprensione della modellazione multidimensionale in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
## <a name="next-step"></a>Passaggio successivo  
Per iniziare l'esercitazione, passare alla prima lezione: [Lezione 1: Definizione di una vista origine dati all'interno di un'analisi progetto Services](lesson-1-defining-a-data-source-view-within-an-analysis-services-project.md).  
  
  
  
