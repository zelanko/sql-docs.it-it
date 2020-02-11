---
title: Modificare o eliminare partizioni (Analyisis Services-Multidimensional) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- modifying partitions
- partitions [Analysis Services], modifying
ms.assetid: fb7a64ca-d021-4926-b92d-83476fbc40a3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7d7f51b24c487175d13153b9e5627e101175740b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66075144"
---
# <a name="edit-or-delete-partitions-analyisis-services---multidimensional"></a>Modificare o eliminare partizioni (Analyisis Services - Multidimensionale)
  Le partizioni dei cubi vengono modificate tramite la scheda **Partizioni** di Progettazione cubi in [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)]. Nella scheda **Partizioni** sono elencate le partizioni di tutti i gruppi di misure di un cubo. Sono inoltre elencate le partizioni writeback per le quali è abilitata la funzionalità di writeback.  
  
 Per modificare le partizioni per qualsiasi gruppo di misure, espandere il gruppo di misure nella scheda **partizioni** . le partizioni per un gruppo di misure sono elencate in base al numero ordinale in un formato di tabella con le colonne elencate nella tabella seguente.  
  
 Le impostazioni per un gruppo di misure collegato devono essere modificate nel cubo di origine.  
  
 L'eliminazione di partizioni si verifica automaticamente quando una partizione di origine viene unita in una partizione di destinazione. La partizione specificata come origine viene eliminata dopo l'unione. È inoltre possibile eliminare partizioni manualmente in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o nella scheda Partizioni in [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)]. Fare clic con il pulsante destro del mouse e scegliere **Elimina**. Tenere presente che se si elimina una partizione vengono eliminati anche i dati e le aggregazioni. Come precauzione, assicurarsi di disporre di un backup recente del database qualora sia necessario annullare questo passaggio.  
  
> [!NOTE]  
>  In alternativa, è possibile utilizzare script XMLA per automatizzare le attività per la compilazione, l'unione e l'eliminazione di partizioni. Uno script XMLA può essere creato ed eseguito in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]o in pacchetti SSIS personalizzati eseguibili come attività pianificate. Per altre informazioni, vedere [Automatizzare le attività amministrative di Analysis Services con SSIS](../instances/automate-analysis-services-administrative-tasks-with-ssis.md).  
  
## <a name="partition-source"></a>Origine partizione  
 Specifica la query denominata o la tabella di origine per la partizione. Per modificare la tabella di origine, fare clic sulla cella e quindi sul pulsante Sfoglia (**...**).  
  
 ![Colonna di origine nel riquadro Partizione](../media/ssas-partitionsource.png "Colonna di origine nel riquadro Partizione")  
  
 Se la partizione è basata su una query, fare clic sul pulsante Sfoglia (**...**) per modificare la query. In questo modo, verrà modificata la proprietà **Source** della partizione. Per altre informazioni, vedere [Modificare l'origine di una partizione in modo da usare una tabella dei fatti diversa](change-a-partition-source-to-use-a-different-fact-table.md).  
  
 È possibile specificare una tabella nella vista origine dati con la stessa struttura della tabella di origine originale (nell'origine dati esterna da cui vengono recuperati i dati). L'origine può trovarsi in qualsiasi origine dati o vista origine dati del database del cubo.  
  
## <a name="storage-settings"></a>Impostazioni di archiviazione  
 Nella scheda Partizioni di Progettazione cubi è possibile fare clic su **Impostazioni di archiviazione** per selezionare una delle impostazioni standard per l'archiviazione MOLAP, ROLAP o HOLAP o per configurare impostazioni personalizzate per la modalità di archiviazione e la memorizzazione nella cache attiva. L'impostazione predefinita è MOLAP perché offre le migliori prestazioni per le query. Per altre informazioni su ogni impostazione, vedere [Impostare l'archiviazione delle partizioni &#40;Analysis Services - Multidimensionale&#41;](set-partition-storage-analysis-services-multidimensional.md).  
  
 È possibile configurare separatamente l'archiviazione per ogni partizione di ogni gruppo di misure in un cubo. È inoltre possibile configurare le impostazioni di archiviazione predefinite per un cubo o un gruppo di misure. L'archiviazione viene configurata nella scheda **Partizioni** della Creazione guidata cubo.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare e gestire una partizione locale &#40;Analysis Services&#41;](create-and-manage-a-local-partition-analysis-services.md)   
 [Progettazione di aggregazioni &#40;Analysis Services-&#41;multidimensionali](designing-aggregations-analysis-services-multidimensional.md)   
 [Unire partizioni in Analysis Services &#40;SSAS-&#41;multidimensionali](merge-partitions-in-analysis-services-ssas-multidimensional.md)  
  
  
