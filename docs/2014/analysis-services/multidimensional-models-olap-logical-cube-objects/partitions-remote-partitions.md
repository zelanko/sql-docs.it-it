---
title: Partizioni remote | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- storage [Analysis Services], partitions
- archiving remote partitions [Analysis Services]
- partitions [Analysis Services], remote
- restoring remote partitions [Analysis Services]
- backing up remote partitions [Analysis Services]
- partitions [Analysis Services], storage
- storing data [Analysis Services], partitions
- MasterDataSourceID property
- remote partitions [Analysis Services]
ms.assetid: 63f5d9f5-c6b6-4ceb-94fe-7b6c396d10bb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d092c33c8c350dc19b749fd3b31ccf1b8c73eac6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62727346"
---
# <a name="remote-partitions"></a>Partizioni remote
  I dati di una partizione remota vengono archiviati in un'istanza di Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] diversa da quella dell'istanza di che contiene le definizioni (metadati) della partizione e del relativo cubo padre. Una partizione remota viene amministrata nella stessa istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in cui sono definiti la partizione e il cubo padre.  
  
> [!NOTE]  
>  Per archiviare una partizione remota, è necessario che nel computer sia installata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] un'istanza di e che sia in esecuzione lo stesso livello di Service Pack dell'istanza di in cui è stata definita la partizione. Non sono supportate partizioni remote in istanze di una versione precedente di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Quando le partizioni remote sono incluse in un gruppo di misure, l'utilizzo della memoria e della CPU del cubo viene distribuito fra tutte le partizioni del gruppo di misure. Quando ad esempio viene elaborata una partizione remota, autonomamente o nell'ambito dell'elaborazione del cubo padre, l'utilizzo di memoria e CPU per la partizione si verifica per la maggior parte nell'istanza remota di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
> [!NOTE]  
>  Un cubo contenente partizioni remote può contenere dimensioni abilitate per la scrittura. Ciò può tuttavia influire sulle prestazioni relative al cubo. Per altre informazioni sulle dimensioni abilitate per la scrittura, vedere [dimensioni abilitate](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)per la scrittura.  
  
## <a name="storage-modes-for-remote-partitions"></a>Modalità di archiviazione per le partizioni remote  
 Per le partizioni remote può essere utilizzato qualsiasi tipo di archiviazione utilizzato per le partizioni locali, ovvero OLAP multidimensionale (MOLAP), OLAP ibrido (HOLAP) oppure OLAP relazionale (ROLAP). Le partizioni remote supportano inoltre la memorizzazione nella cache attiva. In base alla modalità di archiviazione di una partizione remota, nell'istanza remota di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] vengono archiviati i dati seguenti.  
  
|||  
|-|-|  
|Tipo di archiviazione|data|  
|MOLAP|Aggregazioni della partizione e una copia dei dati di origine della partizione|  
|HOLAP|Aggregazioni delle partizioni|  
|ROLAP|Nessun dato della partizione|  
  
 Se un gruppo di misure contiene più partizioni MOLAP o HOLAP archiviate in più istanze di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], i dati nei dati del gruppo di misure vengono distribuiti dal cubo tra tali istanze di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
## <a name="merging-remote-partitions"></a>Unione di partizioni remote  
 Le partizioni remote possono essere unite solo ad altre partizioni remote archiviate nella stessa istanza remota di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Per altre informazioni sull'Unione di partizioni, vedere [unire partizioni in Analysis Services &#40;SSAS-&#41;multidimensionali ](../multidimensional-models/merge-partitions-in-analysis-services-ssas-multidimensional.md).  
  
## <a name="archiving-and-restoring-remote-partitions"></a>Archiviazione e ripristino di partizioni remote  
 È possibile archiviare o ripristinare i dati delle partizioni remote quando il database in cui è memorizzata la partizione remota viene archiviato o ripristinato. Se si ripristina un database senza ripristinare una partizione remota, è necessario elaborare la partizione remota per poter utilizzare i dati della partizione. Per ulteriori informazioni sull'archiviazione e il ripristino di database, vedere [backup e ripristino di database Analysis Services](../multidimensional-models/backup-and-restore-of-analysis-services-databases.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Creare e gestire una partizione remota &#40;Analysis Services&#41;](../multidimensional-models/create-and-manage-a-remote-partition-analysis-services.md)   
 [Elaborazione di oggetti Analysis Services](../multidimensional-models/processing-analysis-services-objects.md)  
  
  
