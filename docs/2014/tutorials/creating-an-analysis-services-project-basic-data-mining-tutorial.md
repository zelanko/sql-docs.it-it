---
title: Creazione di un'analisi di progetto (esercitazione di base di Data Mining) di servizi | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 784c0401-0358-4117-9c85-4e8220ce71d9
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ee6c1a8b765843304d25f1e2ad485ede2badcba4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62855188"
---
# <a name="creating-an-analysis-services-project-basic-data-mining-tutorial"></a>Creazione di un progetto di Analysis Services (Esercitazione di base sul data mining)
  In ogni progetto di [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] vengono definiti gli oggetti in un singolo database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Un database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] può contenere molti tipi diversi di oggetti  
  
-   Modelli multidimensionali (cubi)  
  
-   Strutture e modelli di data mining  
  
-   Supporto di oggetti quali origini dati, viste origine dati e assembly personalizzati  
  
 Si noti che il processo di data mining **non** richiede l'uso di un cubo. Se è necessario eseguire il data mining in un cubo esistente, occorre aggiungere i modelli di data mining nello stesso progetto usato per compilare il cubo. Per la maggior parte delle operazioni è tuttavia possibile compilare i modelli in origini dati relazionali, ad esempio un data warehouse, evitando così l'uso di un cubo che comporta una riduzione delle prestazioni.  
  
 In questa esercitazione verrà usato un data warehouse relazionale, [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)], come origine dati. Tutti gli oggetti di data mining verranno distribuiti in un database [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] denominato `BasicDataMining`, usato esclusivamente per il data mining.  
  
 Per impostazione predefinita, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usa l'istanza **localhost** per i nuovi progetti. Se si usa un'istanza denominata o un server diverso, è necessario creare e aprire il progetto prima di modificare il nome dell'istanza.  
  
 Per altre informazioni sui progetti di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , vedere [Creating an Analysis Services Project](../analysis-services/lesson-1-1-creating-an-analysis-services-project.md).  
  
### <a name="to-create-an-analysis-services-project"></a>Per creare un progetto di Analysis Services  
  
1.  Aprire [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
2.  Scegliere **Nuovo** dal menu **File**e quindi selezionare **Progetto**.  
  
3.  Verificare che **Progetti Business Intelligence** sia selezionato nel riquadro **Tipi progetto** .  
  
4.  Nel riquadro **Modelli** selezionare **Progetto multidimensionale e di data mining di Analysis Services**.  
  
5.  Nel **Name** casella, denominare il nuovo progetto `BasicDataMining`.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-change-the-instance-where-data-mining-objects-are-stored"></a>Per modificare l'istanza in cui vengono archiviati gli oggetti di data mining  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]scegliere **Proprietà** dal menu **Progetto**.  
  
2.  Sul lato sinistro del riquadro **Pagine delle proprietà** fare clic su **Distribuzione**in **Proprietà di configurazione**.  
  
3.  Sul lato destro del riquadro **Pagine delle proprietà** , verificare in **Destinazione**che il nome del **Server** sia **localhost**. Se si usa un'altra istanza, digitarne il nome. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Creazione di un'origine dati &#40;esercitazione di base di Data Mining&#41;](../../2014/tutorials/creating-a-data-source-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Compilare progetti di Analysis Services &#40;SSDT&#41;](../analysis-services/multidimensional-models/build-analysis-services-projects-ssdt.md)   
 [Creare un progetto di Analysis Services &#40;SSDT&#41;](../analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt.md)  
  
  
