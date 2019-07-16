---
title: I database modello multidimensionale (SSAS) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1ec839c9638b3baf79cba0148cc932ead7820f7b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208677"
---
# <a name="multidimensional-model-databases-ssas"></a>Database modelli multidimensionali (SSAS)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è una raccolta di origini dati, viste origine dati, cubi, dimensioni e ruoli. Facoltativamente, in un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] possono essere incluse strutture per data mining e assembly personalizzati che consentono di aggiungere funzioni definite dall'utente al database.  
  
 I cubi sono gli oggetti query fondamentali in Analysis Services. Quando si esegue una connessione a un database di Analysis Services tramite un'applicazione client, si esegue in pratica la connessione a un cubo all'interno di tale database. È possibile che in un database siano contenuti più cubi se si riutilizzano dimensioni, assembly, ruoli o strutture di data mining in più contesti.  
  
 È possibile creare e modificare a livello di codice un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o tramite uno di questi metodi interattivi:  
  
-   Distribuire un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] da [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] in un'istanza designata di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Con questo processo viene creato un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , se nell'istanza non esiste già un database con lo stesso nome, e viene creata un'istanza degli oggetti designati nel nuovo database creato. Quando si utilizza un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], le modifiche apportate agli oggetti nel progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] diventano effettive solo al momento della distribuzione del progetto in un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
-   Creare un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] vuoto all'interno di un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], quindi connettersi direttamente a tale database mediante [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e creare oggetti all'interno di esso anziché di un progetto. Quando si utilizza un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in questo modo, le modifiche apportate agli oggetti diventano effettive nel database con cui viene stabilita la connessione al momento del salvataggio dell'oggetto modificato.  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] viene utilizzata l'integrazione con software per il controllo del codice sorgente per supportare più sviluppatori che utilizzano contemporaneamente oggetti diversi all'interno di un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Uno sviluppatore può inoltre interagire direttamente con un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , anziché tramite un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . In questo caso, tuttavia, gli oggetti di un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] potrebbero risultare non sincronizzati con il progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilizzato per la distribuzione. Dopo la distribuzione, un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene amministrato mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Mediante [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è inoltre possibile apportare determinate modifiche a un database di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], ad esempio a partizioni e ruoli, a causa delle quali gli oggetti di un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] potrebbero risultare non sincronizzati con il progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilizzato per la distribuzione.  
  
## <a name="related-tasks"></a>Attività correlate  
 [Collegamento e scollegamento di database di Analysis Services](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)  
  
 [Backup e ripristino di database di Analysis Services](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
 [Documentazione e script per un database di Analysis Services](../../analysis-services/multidimensional-models/document-and-script-an-analysis-services-database.md)  
  
 [Modificare o eliminare un database di Analysis Services](../../analysis-services/multidimensional-models/modify-or-delete-an-analysis-services-database.md)  
  
 [Spostare un database di Analysis Services](../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)  
  
 [Rinominare un database multidimensionale &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/rename-a-multidimensional-database-analysis-services.md)  
  
 [Livello di compatibilità di un database multidimensionale &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)  
  
 [Impostare le proprietà dei database multidimensionali &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/set-multidimensional-database-properties-analysis-services.md)  
  
 [Sincronizzare database di Analysis Services](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)  
  
 [Passare un database di Analysis Services tra le modalità ReadOnly e ReadWrite](../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Connettersi in modalità online a un database di Analysis Services](../../analysis-services/multidimensional-models/connect-in-online-mode-to-an-analysis-services-database.md)   
 [Creare un progetto di Analysis Services &#40;SSDT&#41;](../../analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt.md)   
 [Query su dati multidimensionali con MDX](../../analysis-services/multidimensional-models/mdx/querying-multidimensional-data-with-mdx.md)  
  
  
