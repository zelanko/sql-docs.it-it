---
title: Le partizioni remote | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3f7729fc1ddeb95c4ab9c780dfc6c48c253666f0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209298"
---
# <a name="partitions---remote-partitions"></a>Partizioni: partizioni remote
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  I dati di una partizione remota vengono archiviati in un'istanza diversa di Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] rispetto all'istanza che contiene le definizioni (metadati) della partizione e il cubo padre. Una partizione remota viene amministrata nella stessa istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in cui sono definiti la partizione e il cubo padre.  
  
> [!NOTE]
>  Per archiviare una partizione remota, il computer deve avere un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] installata ed essere in esecuzione allo stesso livello di service pack dell'istanza in cui è stata definita la partizione. Non sono supportate partizioni remote in istanze di una versione precedente di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Quando le partizioni remote sono incluse in un gruppo di misure, l'utilizzo della memoria e della CPU del cubo viene distribuito fra tutte le partizioni del gruppo di misure. Quando ad esempio viene elaborata una partizione remota, autonomamente o nell'ambito dell'elaborazione del cubo padre, l'utilizzo di memoria e CPU per la partizione si verifica per la maggior parte nell'istanza remota di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
> [!NOTE]  
>  Un cubo contenente partizioni remote può contenere dimensioni abilitate per la scrittura. Ciò può tuttavia influire sulle prestazioni relative al cubo. Per altre informazioni sulle dimensioni abilitate per la scrittura, vedere [dimensioni abilitate per la scrittura](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md).  
  
## <a name="storage-modes-for-remote-partitions"></a>Modalità di archiviazione per le partizioni remote  
 Per le partizioni remote può essere utilizzato qualsiasi tipo di archiviazione utilizzato per le partizioni locali, ovvero OLAP multidimensionale (MOLAP), OLAP ibrido (HOLAP) oppure OLAP relazionale (ROLAP). Le partizioni remote supportano inoltre la memorizzazione nella cache attiva. In base alla modalità di archiviazione di una partizione remota, nell'istanza remota di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] vengono archiviati i dati seguenti.  
  
|||  
|-|-|  
|Tipo di archiviazione|Data|  
|MOLAP|Aggregazioni della partizione e una copia dei dati di origine della partizione|  
|HOLAP|Aggregazioni delle partizioni|  
|ROLAP|Nessun dato della partizione|  
  
 Se un gruppo di misure contiene più partizioni MOLAP o HOLAP archiviate in più istanze di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], i dati nei dati del gruppo di misure vengono distribuiti dal cubo tra tali istanze di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
## <a name="merging-remote-partitions"></a>Unione di partizioni remote  
 Le partizioni remote possono essere unite solo ad altre partizioni remote archiviate nella stessa istanza remota di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Per altre informazioni sull'unione di partizioni, vedere [unire partizioni in Analysis Services &#40;SSAS - multidimensionale&#41;](../../analysis-services/multidimensional-models/merge-partitions-in-analysis-services-ssas-multidimensional.md).  
  
## <a name="archiving-and-restoring-remote-partitions"></a>Archiviazione e ripristino di partizioni remote  
 È possibile archiviare o ripristinare i dati delle partizioni remote quando il database in cui è memorizzata la partizione remota viene archiviato o ripristinato. Se si ripristina un database senza ripristinare una partizione remota, è necessario elaborare la partizione remota per poter utilizzare i dati della partizione. Per altre informazioni sull'archiviazione e il ripristino dei database, vedere [Backup e ripristino di database di Analysis Services](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Creare e gestire una partizione remota &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/create-and-manage-a-remote-partition-analysis-services.md)   
 [Elaborazione di Analysis Services gli oggetti](../../analysis-services/multidimensional-models/processing-analysis-services-objects.md)  
  
  
