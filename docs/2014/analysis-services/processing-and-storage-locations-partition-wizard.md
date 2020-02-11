---
title: Posizioni di elaborazione e archiviazione (creazione guidata partizione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitionwizard.specifyprocessingandstorage.f1
ms.assetid: dda2dc57-923d-4db9-93a7-38e95770f3df
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 73340613b14c8f0e90340b589c8b97bad7cd5599
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66070644"
---
# <a name="processing-and-storage-locations-partition-wizard"></a>Posizioni di elaborazione e archiviazione (Creazione guidata partizione)
  La pagina **Posizioni di elaborazione e archiviazione** consente di specificare l'istanza di [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] del cubo proprietario della partizione e l'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] in cui sono archiviati i dati per la partizione. La partizione può essere definita come partizione remota specificando un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] remota o una posizione di archiviazione diversa da quella predefinita. Per altre informazioni sulle partizioni remote, vedere [Partizioni remote](multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md).  
  
## <a name="processing-location-options"></a>Opzioni Posizione di elaborazione  
 **Istanza server corrente**  
 Specifica l'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] corrente come responsabile dell'elaborazione della partizione.  
  
 **Origine dati remota di Analysis Services**  
 Specifica l'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] remota come responsabile dell'elaborazione della partizione.  
  
 Selezionare nell'elenco a discesa l'origine dei dati che rappresenta l'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] remota che sarà responsabile per l'elaborazione della partizione.  
  
> [!NOTE]  
>  Se si seleziona un'origine dei dati in cui la proprietà della stringa di connessione `Initial Catalog` non è impostata su un database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] valido oppure se il database specificato nella proprietà della stringa di connessione `Initial Catalog` non supporta le partizioni remote (ovvero la proprietà `MasterDatasourceID` del database specificato non è impostata su un valore valido), si verifica un errore.  
  
 **Nuovo**  
 Consente di creare una nuova origine dei dati che rappresenta l'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] remota responsabile dell'elaborazione della partizione.  
  
## <a name="storage-location-options"></a>Opzioni Percorso di archiviazione  
 **Percorso server predefinito**  
 Specifica la cartella dati dell'istanza corrente di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] come percorso di archiviazione dei dati di aggregazione e indicizzazione per la partizione.  
  
 **Cartella specificata**  
 Specifica il percorso di archiviazione dei dati di aggregazione e indicizzazione per la partizione.  
  
 **...**  
 Consente di visualizzare la finestra di dialogo **Cerca cartella remota** in cui è possibile selezionare una cartella per **Cartella specificata**.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida sensibile al contesto della creazione guidata partizione &#40;Analysis Services-Dati multidimensionali&#41;](partition-wizard-f1-help-analysis-services-multidimensional-data.md)   
 [Partizioni &#40;Analysis Services Dati multidimensionali&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [Finestra di dialogo Cerca cartella remota &#40;Analysis Services-Dati multidimensionali&#41;](browse-for-remote-folder-dialog-box-analysis-services-multidimensional-data.md)  
  
  
